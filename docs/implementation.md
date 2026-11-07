# Metric Compass: implementation guide

This repository documents a proposed build. No application is installed by cloning it.

## Prerequisites

- Access to a Foundry environment and an appropriate development project.
- Permissions to define datasets, object/link types, functions, actions and application modules.
- AIP/model access only for the optional AI features being enabled.
- Agreed source contracts, business owners and review roles.

## Suggested build sequence

1. **Confirm scope:** agree on object grains, required fields, workflow states, roles and success measures.
2. **Create data inputs:** start with the fictional examples, then replace them only with approved data sources.
3. **Build pipelines:** standardize inputs with Pipeline Builder; implement complex validation in PySpark; expose quality flags.
4. **Configure ontology:** create stable IDs, links and property ownership rules; validate access from each role.
5. **Implement functions and actions:** centralize rules and enforce valid transitions and approval criteria.
6. **Build Workshop:** deliver the primary operational workflow before adding portal customization or AI.
7. **Add views:** configure Gantt, Quiver and Notepad; use Slate for the entry portal where it adds value.
8. **Configure orchestration:** schedule data builds and then business automations with scoped identities and deduplication.
9. **Add AIP:** connect authorized context, validate output contracts, evaluate representative cases and retain human review.
10. **Promote deliberately:** review changes in an isolated environment, test with the intended roles and document recovery.

## Importing the diagram

Use the Solution Designer import capability in your environment with [solution-design.json](diagrams/solution-design.json). The file is a diagram, not an infrastructure deployment manifest. Native resource RIDs are unset. Replace generic cards with native types if needed and link actual resources only in your private environment.

## Acceptance checks for a future implementation

- Scoring: verify weights, missing mandatory evidence, zero total weight and rubric revisions.
- Approval: freeze the reviewed revision and require a new revision after changed evidence.
- Reporting: compare the report score with the approved snapshot.
- Data ownership: refresh source data and confirm operational edits remain correct.
- Access: verify unauthorized reads and edits fail for objects, properties and actions.
- Automation: retry a failed effect without duplicating successful work.
- AI: reject invalid structured output and evidence references; require the intended human review.
- Documentation: ensure diagram, object definitions and action names remain consistent.

These are planned acceptance checks, not claims of tests run against a live Foundry deployment.

## Operational signals

| Area | Observe |
| --- | --- |
| Pipeline | Build outcome, freshness, validation failures and quarantine volume |
| Ontology | Sync/indexing health and availability of expected records |
| Actions/functions | Success rate, validation failures, latency and unexpected transitions |
| Automate | Evaluation outcome, effect failures, retries and duplicate prevention |
| AIP | Grounding failures, invalid output, latency, token use and review outcomes |

For a failed release, stop the affected automation, retain failure evidence, restore an approved function/application version and reconcile any already-written objects through a controlled action. Do not assume a code rollback undoes operational edits.
