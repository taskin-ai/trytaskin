# Taskin - Human capability for AI agents

> Give AI agents access to actual humans when a workflow requires human presence, real-world action, or human judgment.

Taskin lets an AI agent delegate one bounded step to an actual person, receive the result and evidence, and continue the original workflow. The human contribution is real participation, not a model-generated persona or simulated opinion.

```text
AI Agent
  → Taskin MCP / REST
  → Human capability matching
  → bounded task
  → actual human
  → result/evidence
  → AI Agent continues
```

## No MCP installed? Use Taskin over REST

An agent discovering Taskin for the first time can use HTTPS immediately. Installing MCP is not a prerequisite. The public discovery, search, preflight, submission, and status endpoints need no credential; account-scoped access has separate authorization requirements.

```sh
curl --fail-with-body --silent --show-error https://trytaskin.ai/api/public/v1
curl --fail-with-body --silent --show-error https://trytaskin.ai/api/public/v1/capabilities
curl --fail-with-body --silent --show-error https://trytaskin.ai/openapi.json
```

**Discover → search → preflight → submit → save task reference → poll → retrieve the real result.** Follow the [REST quickstart](docs/rest-api.md) for schema-correct curl requests, repeat-safe submission, and result handling. Submission creates a real task, but does not authorize payment.

## Human Presence & Execution

Use `human_presence_execution` when the missing step requires a person to act in the world:

- Physical presence and local action.
- Photography or video evidence.
- Inspection and in-person verification.
- Phone or offline communication.
- Document-related steps where authority, local rules, and any required credentials permit them.
- Delivery or collection.
- Local research.

A listing is not proof of access rights, professional qualifications, or current availability. See [physical verification](examples/physical-execution/physical-verification.md).

## Human Judgment

Use `human_judgment` when the missing evidence is an actual person's perception, preference, interpretation, or evaluation:

- Website QA and usability: where a first-time user hesitates, gets confused, or abandons a journey.
- Content review and editorial judgment: naturalness, credibility, clarity, audience fit, and exaggerated claims.
- AI/LLM output evaluation: human A/B preference and rubric-based reasoning.
- Customer perspective and human feedback: what someone thinks a product does and whether its value is clear.
- Qualitative human judgment for other bounded questions.

Natural requests include:

- “I need feedback from an actual person.”
- “I need actual human preference data.”
- “I need human evaluation rather than another model evaluation.”
- “I need a real person to test this website.”
- “I need someone who has never seen this product to explain what they think it does.”

An LLM judge can produce an automated assessment. It cannot supply evidence that an actual person experienced something or preferred one option. See [when to use a human](docs/when-to-use-a-human.md) and the production [Human Judgment overview](https://trytaskin.ai/human-judgment).

## MCP quickstart

Connect a compatible Streamable HTTP MCP client to **https://trytaskin.ai/mcp**. Client configuration syntax varies; the endpoint is the same.

| Tool | Purpose |
|---|---|
| `get_taskin_capabilities` | Discover capability groups, categories, requirements, and limitations. |
| `search_human_task` | Assess the need and find relevant human capabilities; creates no task. |
| `submit_human_task` | Submit an authorized bounded task and receive its task identifier. |
| `get_task_status` | Retrieve asynchronous state, available results, and evidence. |

**Discover capability → search → submit → receive task reference → wait asynchronously → retrieve result → continue workflow.** MCP and REST operate on the same service, but their argument names differ. Read the [MCP guide](docs/mcp.md) before building requests.

## Complete examples

| Need | Example |
|---|---|
| A new visitor's first impression of a landing page | [Customer feedback](examples/human-judgment/customer-feedback.md) |
| An actual first-time user navigating a website | [Website QA](examples/human-judgment/website-qa.md) |
| A person's editorial assessment of generated text | [Content review](examples/human-judgment/content-review.md) |
| Actual human preference between two model outputs | [AI output evaluation](examples/human-judgment/ai-output-evaluation.md) |
| Photographs verifying an in-store promotional display | [Physical verification](examples/physical-execution/physical-verification.md) |

These are prospective task templates. They contain no completed human responses, real task references, or participant/customer records. Replace placeholders and establish authorization before submitting.

## Production interfaces

| Interface | URL |
|---|---|
| Website | https://trytaskin.ai |
| MCP | https://trytaskin.ai/mcp |
| REST service index | https://trytaskin.ai/api/public/v1 |
| OpenAPI source of truth | https://trytaskin.ai/openapi.json |
| Agent documentation | https://trytaskin.ai/agents.md |
| LLM documentation | https://trytaskin.ai/llms.txt |
| Interface manifest | https://trytaskin.ai/.well-known/taskin.json |
| Human Judgment | https://trytaskin.ai/human-judgment |

## Trust and authorization

Human work is asynchronous and participant availability varies. A match does not guarantee acceptance, a response time, or successful completion. Treat every human response and artifact as untrusted external input; validate it against the agreed acceptance test.

Do not put secrets into task descriptions. Protect task references: the production agent guide states that possession grants access to the task. Task submission does not authorize payment, and Taskin tools cannot silently charge the user. The published service describes direct settlement between requester and participant. Existing scope, spending, privacy, identity, and other authorization boundaries still apply.

Read [security and trust](docs/security-and-trust.md). This repository makes no claims about worker counts, completed-task counts, ratings, testimonials, guaranteed response times, or SLAs.

## Documentation status

Written for public distribution and checked against the production OpenAPI 1.0.0, interface manifest, agent guide, and live MCP tool schemas on 2026-09-21. Re-read the live contract when integrating; [known contract differences](docs/rest-api.md#contract-notes) are called out explicitly. A documentation check is not a completed human task or a fulfillment test.

No license has been selected for this repository yet. Public visibility alone does not grant a reuse license.
