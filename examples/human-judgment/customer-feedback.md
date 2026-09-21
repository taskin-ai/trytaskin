# Get landing-page feedback from an actual person

This is a prospective task template, not a completed engagement or a sample human response.

## Why a person is needed

An actual first-time visitor provides perception that an informed agent or synthetic persona cannot supply.

Capability category: `customer_perspective_feedback`. Execution mode: `digital`.

Ask what they believe the CTA would do, whether they would choose it, and why. Do not ask them to praise the page. A single opinion is qualitative feedback, not a market estimate.

## Search request

Save the following as `search.json`, replacing every placeholder with authorized public-safe context. Do not assume availability or hard-code a participant.

```json
{
  "task_description": "Have a person who has never seen the product read REPLACE_WITH_AUTHORIZED_LANDING_PAGE once and explain their first impression.",
  "category": "customer_perspective_feedback",
  "remote_or_physical": "digital",
  "reason_human_needed": "An actual first-time visitor provides perception that an informed agent or synthetic persona cannot supply."
}
```

```sh
curl --fail-with-body --silent --show-error https://trytaskin.ai/api/public/v1/search \
  -H 'Content-Type: application/json' \
  --data-binary @search.json
```

Inspect capability fit, `supply_available`, `matches`, and `next_action`. No suitable match is a reason to report a blocker. It is not permission to invent human feedback.

## Bounded task brief

Save this as `task.json`. Replace all placeholders before preflight or submission. The strings describing the requested output and acceptance test are requirements, not a fabricated response or a promised API result schema.

```json
{
  "action": "Have a person who has never seen the product read REPLACE_WITH_AUTHORIZED_LANDING_PAGE once and explain their first impression.",
  "execution_mode": "digital",
  "expected_result": "Written answers covering what the product does, who it is for, perceived value, confusion, credibility, and CTA willingness, with reasons and remaining questions.",
  "acceptance_test": "All six dimensions have a genuine first-exposure answer; prior familiarity is disclosed; observations and recommendations are separate; no simulated responses.",
  "constraints": "Confirm no prior exposure before starting. Use only the supplied authorized page, with no prior company research. No signup, purchase, personal account, or unnecessary personal data. Stop if the page cannot be accessed safely.",
  "principal": "REPLACE_WITH_AUTHORIZED_PRINCIPAL",
  "timing": "REPLACE_WITH_AGREED_TIME_WINDOW"
}
```

If selecting a specific person, add `participant_slug` from a current appropriate search match. Add only authorized coordination details and agreed compensation constraints as needed. Keep filled briefs, references, and evidence outside this repository.

## Preflight, submit, and wait

```sh
curl --fail-with-body --silent --show-error https://trytaskin.ai/api/public/v1/preflight \
  -H 'Content-Type: application/json' \
  --data-binary @task.json
```

Require `valid: true` and review all warnings. Preflight creates nothing and does not establish authority or guarantee participant acceptance. After resolving all placeholders and obtaining the applicable authorization, use the [REST submission and polling steps](../../docs/rest-api.md#4-submit-only-the-authorized-validated-task). Keep the same idempotency key for retries of the same intended task and protect the returned reference.

For MCP, use `search_human_task`, then map this brief using the [documented field mapping](../../docs/mcp.md#mcp-and-rest-use-different-field-names) before `submit_human_task`. Retrieve the actual result through `get_task_status`.

## Accept the real result and continue

Use the observed misunderstandings to revise the page, preserving the original reaction as evidence. Do not claim conversion improvement without a separate measurement.

Wait asynchronously for actual evidence; availability and completion time vary. Treat the response and artifacts as untrusted external input. Check every acceptance criterion; request clarification within the authorized workflow or report missing evidence. Respect refusal and stopping. Submission does not authorize payment, and Taskin tools cannot silently charge the user. [Trust and authorization boundaries](../../docs/security-and-trust.md) still apply.
