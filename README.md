# Metric Compass

Metric Compass is a proposed Palantir Foundry solution for auditable KPI assessments, evidence-based scoring and tracked improvement roadmaps.

**Architecture portfolio · Palantir Foundry · Ontology · AIP · Human-reviewed decisions**

## Why this project exists

KPI reviews become difficult to trust when definitions, evidence, ratings and improvement actions live in separate places. Metric Compass connects them in a single operational model so a reviewer can trace a score back to its evidence and follow the work needed to improve it.

**Intended outcome:** Trace a KPI from its definition and observations through an evidence-backed assessment to an approved score and an owned improvement plan.

## Solution design

**Original Solution Designer export:**

[![Open the full-size Metric Compass Solution Designer diagram](docs/diagrams/solution-design.png)](docs/diagrams/solution-design.png)

This detailed diagram is the proposed Foundry solution design. It groups the design into five areas: KPI definitions and data orchestration; ontology and controlled changes; applications and reporting; AIP and human review; workflow and operations. The linked PNG is 2048 × 1299 pixels. Its resolution is suitable for a portfolio, but the diagram is dense: small labels are hard to read in the README preview. Click the image to open it at full size and zoom in. The companion [workflow.svg](docs/diagrams/workflow.svg) presents the KPI assessment lifecycle in a simpler, more readable view.

```mermaid
flowchart TD
    U["KPI owners · auditors · reviewers · managers"] --> S["Source KPI definitions · observations · evidence"]
    S --> P["Pipeline Builder · validation · curated datasets"]
    P --> O["Ontology: KPI · Assessment · Criterion · Evidence"]
    O --> W["Workshop · Slate · Quiver · Notepad · roadmap"]
    O --> A["AIP Chatbot · Analyst · Logic · approved LLM"]
    A --> H["Human evidence review and approval"]
    W --> X["Action Types · versioned assessment states"]
    H --> X
    X --> M["Automate · Scheduler · audit history"]
    M --> O
```

The editable [Solution Designer JSON](docs/diagrams/solution-design.json) accompanies the diagram and can be imported into a compatible Solution Designer. Importing the JSON draws the design; it does not provision Foundry resources. See [the component and data flow details](docs/architecture.md).

## What the design covers

- Evidence-linked assessment and score history
- Deterministic scoring with versioned criteria and weights
- Controlled approval and reassessment workflow
- Gantt roadmap for accepted improvement tasks
- Quiver trends and Notepad review reports
- AIP evidence-gap suggestions with human review

## Who uses it

KPI owners provide evidence, auditors rate criteria, reviewers approve assessments, and managers prioritize improvement work.

## End-to-end workflow

![Metric Compass KPI audit workflow diagram](docs/diagrams/workflow.svg)

```mermaid
flowchart TD
    D["Curated KPI and evidence data"] --> O["KPI and assessment ontology"]
    O --> W["Workshop audit workbench"]
    W --> R["Record evidence and criterion ratings"]
    R --> S["Deterministic scoring function"]
    S --> A{"Reviewer approves?"}
    A -->|Return| R
    A -->|Approve| H["Versioned assessment"]
    H --> P["Improvement roadmap and Gantt"]
    O --> AI["AIP drafts evidence gaps"]
    AI --> V["Human checks suggestions"]
    V --> R
    H --> N["Quiver analysis and Notepad report"]
```

## Start here

1. Read the [architecture and tool responsibilities](docs/architecture.md).
2. Inspect the [ontology and data contracts](docs/ontology.md).
3. Follow the [workflow and business rules](docs/workflows.md).
4. Review the [AIP and automation design](docs/aip-and-automation.md).
5. Walk through the [synthetic example](examples/README.md).
6. Use the [implementation and validation guide](docs/implementation.md) to plan a Foundry build.

## Example scenario

A fictional service team reviews an on-time-delivery KPI. Its operational value is 92%, while its audit maturity score is 85/100. These measure different things: the first describes delivery performance; the second describes the quality of the KPI definition, evidence and governance.

## Repository contents

| Path | Contents |
| --- | --- |
| `docs/diagrams/solution-design.json` | Editable Solution Designer diagram |
| `docs/diagrams/solution-design.png` | Original detailed Solution Designer diagram |
| `docs/diagrams/workflow.svg` | Readable companion KPI evidence and approval workflow graphic |
| `docs/architecture.md` | Layers, component roles and engineering decisions |
| `docs/ontology.md` | Object grains, links, keys and data ownership |
| `docs/workflows.md` | States, actions, calculations and completion rules |
| `docs/aip-and-automation.md` | AI inputs/outputs, review gates and automation triggers |
| `docs/implementation.md` | Suggested build sequence, validation and operations |
| `examples/` | Fictional records and an illustrative walkthrough |
| `docs/references.md` | Official Palantir capability references |

## Status and scope

This is a **conceptual solution-design repository**, not a deployable Foundry application. It contains documentation, diagrams and synthetic records; it does not contain production code, provisioned ontology objects, live connections or configured AI agents. Detailed schemas, formulas and workflow rules are proposed implementation choices.

Importing the JSON draws the solution architecture; it does not create Foundry resources. Some tools appear as generic custom cards for compatibility with the supplied export format. The JSON has been structurally validated; import behavior depends on your Solution Designer version.

## Technology coverage

Ontology Manager, Workshop, Slate, Action Types, PySpark, TypeScript, Code Repositories, Pipeline Builder, Scheduler, Automate, Quiver, Notepad, Gantt Chart, AIP Chatbot, AIP Analyst, AIP Logic and LLMs.

## Foundry tools and their roles

These are proposed components in the conceptual design; they are not claims that a production Foundry environment has already been configured.

| Tool | Role in Metric Compass |
| --- | --- |
| Ontology Manager | Model KPI definitions, observations, assessments, criteria, evidence, reviewers and improvement tasks. |
| Pipeline Builder | Standardize KPI inputs and validate units, reporting periods, keys and evidence freshness. |
| Code Repository (PySpark / TypeScript) | Version source transformations and deterministic scoring functions. |
| Scheduler | Refresh source-derived observations and downstream score or trend datasets. |
| Action Types | Submit evidence, record criterion ratings, return or approve assessments and plan improvements. |
| Workshop | Provide the KPI audit workbench for owners, auditors and reviewers. |
| Slate | Deliver a focused portfolio landing page when a custom interface is useful. |
| Gantt chart | Plan and track approved improvement tasks, owners, dates and dependencies. |
| Quiver | Compare approved scores, evidence completeness and improvement trends across periods. |
| Notepad | Produce versioned audit and review reports with rationale and evidence references. |
| AIP Chatbot | Answer grounded questions about authorized KPI definitions and assessment records. |
| AIP Analyst | Explore portfolio patterns and evidence gaps without approving scores. |
| AIP Logic | Draft evidence-gap summaries and improvement suggestions for human review. |
| LLM | Provide the approved model runtime behind AIP features; outputs require grounding and evaluation. |
| Automate | Notify owners about overdue reviews and approved improvement tasks; log effects. |

## Contributing

Suggest changes with a clear problem statement and the affected documentation or diagram. Keep examples fictional, state assumptions explicitly, and update the ontology and workflow references when a design changes. Do not submit credentials, internal URLs or organization-specific data.
