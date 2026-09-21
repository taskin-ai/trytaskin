# Taskin MCP

Endpoint: **https://trytaskin.ai/mcp**. Production advertises JSON-RPC 2.0 over Streamable HTTP, protocol revision `2025-06-18`. Configure this as a remote HTTP server using your client's supported syntax. MCP installation is optional: [REST](rest-api.md) is available to any agent that can make HTTPS requests.

Production documentation states that all four public tools need no authentication. Account-scoped access is separate; see [security and trust](security-and-trust.md).

## Discover the current tool schemas

```sh
curl --fail-with-body --silent --show-error https://trytaskin.ai/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  --data '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

This direct discovery request was checked against production. Full MCP clients should manage protocol initialization and transport negotiation themselves.

Read capabilities without searching for or contacting a participant:

```sh
curl --fail-with-body --silent --show-error https://trytaskin.ai/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  --data '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"get_taskin_capabilities","arguments":{}}}'
```

## Tool contract

| Tool | Required schema arguments | Behavior |
|---|---|---|
| `get_taskin_capabilities` | None (`{}`) | Read groups, categories, requirements, and limitations. |
| `search_human_task` | `task_description` | Read capability assessment and relevant matches; creates nothing. Optional filters include `category`, `skills`, `location`, and `remote_or_physical`. |
| `submit_human_task` | `task_description`, `deliverable`, `verification_requirements` | Create a real bounded task. Supply a named `principal`, explicit execution mode, constraints, and relevant location/timing too. |
| `get_task_status` | `task_id` | Read the actual identifier returned by submission; inspect state and any available result/evidence. |

Live schema checked 2026-09-21. Schema-required arguments are a minimum, not a complete authorization or operational brief. The production guide requires attribution to a principal even though the MCP schema describes it as strongly recommended. Always name the authorized principal. Physical/hybrid work also requires a location.

## Workflow

1. Call `get_taskin_capabilities` to identify the right group and category.
2. Call `search_human_task` with the smallest bounded human step. Inspect capability fit, supply, and the returned next action. A match is not acceptance.
3. Prepare the brief and confirm the principal's authority. Include the requested deliverable, objective acceptance test, constraints, location where relevant, and permitted timing. Do not put credentials or private evidence into the brief.
4. Use REST preflight if validating a draft before submission; there is no separate MCP preflight tool in the current four-tool list.
5. Call `submit_human_task` only after the task is authorized and the search indicates Taskin can help. Use a unique `idempotency_key` for that intended task; retain it for retries.
6. Save the returned task identifier privately. The tool documentation calls it `task_id`; REST calls its returned identifier `reference`. Read the actual response rather than inventing an identifier.
7. Wait asynchronously and call `get_task_status`. Inspect errors, required user actions, and returned next actions. Do not infer success from a transport-level response alone.
8. Check the human result and evidence against the acceptance test, then continue the original workflow. Never manufacture a response while waiting or replace a refusal with repeated submissions.

## MCP and REST use different field names

| Brief meaning | MCP submission | REST TaskDraft |
|---|---|---|
| Action | `task_description` | `action` |
| Execution mode | `remote_or_physical` | `execution_mode` |
| Constraints | `requirements` | `constraints` |
| Timing | `deadline` | `timing` |
| Expected result | `deliverable` | `expected_result` |
| Acceptance test | `verification_requirements` | `acceptance_test` |
| Location | `location` | `location` |
| Responsible principal | `principal` | `principal` |
| Optional participant | `participant_slug` | `participant_slug` |
| Repeat-safe key | `idempotency_key` | `idempotency-key` HTTP header or `idempotency_key` body field |

Use `digital`, `physical`, or `hybrid` for the mode. Currency is an optional MCP field; REST TaskDraft instead defines a string `budget`. Do not pass an MCP argument object directly to REST.

Submission creates work, not payment authorization. Taskin tools cannot silently charge a user. Human consent, credentials where needed, privacy, spending authority, and scope limits remain applicable.

Sources: [production agent guide](https://trytaskin.ai/agents.md), [interface manifest](https://trytaskin.ai/.well-known/taskin.json), and live `tools/list` at the [MCP endpoint](https://trytaskin.ai/mcp).
