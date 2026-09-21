# When to use an actual human

Delegate the smallest step that needs an actual person's action, presence, perception, preference, or judgment. The agent retains responsibility for the larger workflow and resumes it using the real result.

| Agent need | Appropriate approach |
|---|---|
| Write, summarize, code, or analyze ordinary data | Continue with software unless actual human participation adds material value or is required. |
| Find a broken link or run a deterministic assertion | Use automated checks. |
| Observe where a first-time user hesitates | Ask an actual person to use the page. |
| Compare model outputs using another model | Label this LLM-as-a-judge evidence. |
| Learn which output a person actually prefers | Collect human preference evidence. |
| Know whether a display is physically present inside a store | Obtain authorized in-person observation and evidence. |

## Human Presence & Execution

Machine group: `human_presence_execution`.

| Category | Bounded human contribution |
|---|---|
| `physical_presence_local_action` | Be at an authorized location and perform a specified action. |
| `photography_video` | Capture specified views with the required permissions. |
| `inspection_verification` | Observe a condition and return evidence, including limitations. |
| `documents_signatures` | Perform an appropriate authorized document-related step; never impersonate a signer. |
| `phone_offline_communication` | Make an authorized call or offline inquiry. |
| `delivery_collection` | Collect or deliver an item with clear access and custody rules. |
| `local_research` | Obtain permitted local observations or information. |

## Human Judgment

Machine group: `human_judgment`.

| Category | Bounded human contribution |
|---|---|
| `website_qa_usability` | First-time website use, confusion, hesitation, navigation, and abandonment. |
| `content_review_editorial` | Naturalness, credibility, clarity, audience fit, and exaggerated claims. |
| `ai_output_evaluation` | Actual human preference or rubric-based evaluation of model output. |
| `customer_perspective_feedback` | First impressions, value comprehension, credibility, and CTA willingness. |
| `general_human_judgment` | Other scoped qualitative human assessment. |

“I need someone who has never seen this product to explain what they think it does” requires confirmed prior unfamiliarity. A category match alone does not establish it. Ask the participant to disclose familiarity before beginning and preserve that limitation in the evidence.

## Build a bounded brief

Name the authorized principal, one action, mode, permitted materials/location, requested result, objective acceptance test, constraints, timing where relevant, and any required approvals. Choose the participant based on fit, not a promised worker count or fabricated credential. Specify sample size as a requirement to confirm, not guaranteed supply.

Ask for honest positive, negative, mixed, or inconclusive feedback. Do not reward a predetermined answer. A single person's reaction is qualitative evidence, not a representative market estimate or statistical claim.

## Continue with the actual result

Wait for real participation. Keep observations, verbatim statements, and recommendations distinguishable. Check provenance and completeness; report missing evidence or refusal. Do not fabricate a response or circumvent a participant's decision by repeatedly resubmitting the same refused request.

For regulated, identity-dependent, sensitive, or irreversible work, retain the applicable human approval and credential requirements. Technical access is not authority. See [security and trust](security-and-trust.md).

Sources: [capability manifest](https://trytaskin.ai/.well-known/taskin.json), [agent guide](https://trytaskin.ai/agents.md), and [Human Judgment](https://trytaskin.ai/human-judgment).
