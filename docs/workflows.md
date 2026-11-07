# Metric Compass: workflows and business rules

## Scoring, actions and approval


An illustrative audit rubric could cover definition clarity, evidence completeness, freshness, ownership and actionability. These criteria and weights must be agreed with the business; they are illustrative rather than verified implementation details.

For normalized criterion ratings from 0 to 100, a candidate calculation is:

`audit_score = sum(weight_i * rating_i) / sum(applicable_weight_i)`

Require positive total applicable weight and valid ratings. Missing mandatory evidence produces an incomplete assessment, not a fabricated rating. Excluded criteria must have an explicit applicability decision. Version the rubric so historic scores can be reproduced.

Use one TypeScript rule implementation for score preview and approved results. Approval writes the input snapshot, calculated score, rubric version, reviewer and timestamp to a revision record. Changes after approval create a new revision. Quiver and Notepad use the approved revision for official reporting.

| Action | Control / resulting behavior |
| --- | --- |
| CreateAssessment | Create a draft for a defined KPI, scope, period and rubric version |
| SubmitEvidence | Link accessible evidence and preserve its source/version |
| RecordCriterionResult | Validate rating, applicability and rationale |
| SubmitForReview | Require mandatory fields and evidence before moving to review |
| ApproveAssessment | Authorized reviewer freezes score inputs and approval metadata |
| PlanImprovement | Create dated, owned improvement work linked to an accepted finding |

The AI can suggest missing evidence and improvements. A human verifies those suggestions. Official scoring and approval use deterministic rules and authorized actions.
