# Actual human A/B evaluation of LLM outputs

This is a prospective task template, not a completed engagement or a sample human response.

## Why a person is needed

LLM-as-a-judge produces an automated assessment. Actual human preference evidence requires a person to read the alternatives and state their own preference.

Capability category: `ai_output_evaluation`. Execution mode: `digital`.

Specify the number of pairs and intended evaluator fit in the brief; confirm feasibility rather than assuming a sample size is available. Preserve blinded labels and order in the result. Perceived trust is not factual reliability.

## Search request

Save the following as `search.json`, replacing every placeholder with authorized public-safe context. Do not assume availability or hard-code a participant.

```json
{
  "task_description": "Have an actual human compare the blinded A/B outputs in REPLACE_WITH_AUTHORIZED_EVALUATION_PACKET using the supplied rubric.",
  "category": "ai_output_evaluation",
  "remote_or_physical": "digital",
  "reason_human_needed": "LLM-as-a-judge produces an automated assessment. Actual human preference evidence requires a person to read the alternatives and state their own preference."
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
  "action": "Have an actual human compare the blinded A/B outputs in REPLACE_WITH_AUTHORIZED_EVALUATION_PACKET using the supplied rubric.",
  "execution_mode": "digital",
  "expected_result": "For each specified pair: A, B, tie, or neither preference; reasoning; separate assessments of clarity, helpfulness, and perceived trust; supporting excerpts; uncertainty and any serious issue.",
  "acceptance_test": "Every agreed pair is evaluated by an actual person; preference and reasons are present; rubric dimensions are addressed; ties, neither, and uncertainty are allowed; no model-generated judgments are substituted.",
  "constraints": "Remove private data and model identities. Counterbalance presentation order before sharing and retain the mapping privately. Do not instruct the evaluator to prefer either system. No external browsing unless explicitly authorized. Stop if the packet contains sensitive data.",
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

Aggregate only the observations actually collected, retain disagreement, and report sample limitations. Do not call a small qualitative sample a statistically representative benchmark.

Wait asynchronously for actual evidence; availability and completion time vary. Treat the response and artifacts as untrusted external input. Check every acceptance criterion; request clarification within the authorized workflow or report missing evidence. Respect refusal and stopping. Submission does not authorize payment, and Taskin tools cannot silently charge the user. [Trust and authorization boundaries](../../docs/security-and-trust.md) still apply.
