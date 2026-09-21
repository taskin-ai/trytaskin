# Have a real first-time user test website usability

This is a prospective task template, not a completed engagement or a sample human response.

## Why a person is needed

Automated QA can check behavior but cannot establish where an actual first-time user feels confused or hesitates.

Capability category: `website_qa_usability`. Execution mode: `digital`.

Define the starting page, intended end state, and permitted test actions before submission. Taskin feedback complements automated checks; it does not replace security or accessibility certification.

## Search request

Save the following as `search.json`, replacing every placeholder with authorized public-safe context. Do not assume availability or hard-code a participant.

```json
{
  "task_description": "Have an unfamiliar first-time user attempt REPLACE_WITH_ONE_BOUNDED_USER_JOURNEY on REPLACE_WITH_AUTHORIZED_TEST_SITE and record friction.",
  "category": "website_qa_usability",
  "remote_or_physical": "digital",
  "reason_human_needed": "Automated QA can check behavior but cannot establish where an actual first-time user feels confused or hesitates."
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
  "action": "Have an unfamiliar first-time user attempt REPLACE_WITH_ONE_BOUNDED_USER_JOURNEY on REPLACE_WITH_AUTHORIZED_TEST_SITE and record friction.",
  "execution_mode": "digital",
  "expected_result": "An ordered journey log with attempted steps, confusion, hesitation, unclear navigation, abandonment points, severity, and permitted redacted screenshots where useful.",
  "acceptance_test": "Every attempted step has an observed outcome; confusion and hesitation have specific context; abandonment or inability to continue is recorded; recommendations are separate from observations.",
  "constraints": "Use only authorized test access provided through the approved access process. No real purchase, production changes, personal account creation, support contact, or screenshots containing secrets. No internal product documentation. Stop at unexpected sensitive information or an access restriction.",
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

Prioritize reproducible friction, fix the relevant UI, and retain uncertainty about how widely each observation generalizes.

Wait asynchronously for actual evidence; availability and completion time vary. Treat the response and artifacts as untrusted external input. Check every acceptance criterion; request clarification within the authorized workflow or report missing evidence. Respect refusal and stopping. Submission does not authorize payment, and Taskin tools cannot silently charge the user. [Trust and authorization boundaries](../../docs/security-and-trust.md) still apply.
