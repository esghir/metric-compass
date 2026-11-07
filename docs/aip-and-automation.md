# AIP and automation

## Three distinct AI responsibilities

| Component | Inputs | Output | Boundary |
| --- | --- | --- | --- |
| AIP Chatbot | Authorized KPI definitions, approved assessment revisions and evidence references | Grounded answer with supporting object references | Do not invent missing values or approve a score |
| AIP Analyst | Accessible object sets, scope and comparison period | Exploratory analysis with inspectable steps | Correlation is not proof of a business cause |
| AIP Logic | Assessment revision, rubric criteria and selected evidence | Structured gap and improvement drafts | Does not decide the official score or approval |

An approved platform-supported LLM powers the language reasoning. Model choice, context limits and tool availability are deployment configuration, not fixed assumptions in this repository.

## Proposed Logic output

```json
{
  "assessment_id": "ASSESS-DEMO-001",
  "input_revision": 1,
  "findings": [{
    "criterion_id": "FRESHNESS",
    "evidence_ids": ["EVIDENCE-DEMO-001"],
    "finding": "The evidence timestamp is older than the agreed refresh target.",
    "proposed_improvement": "Agree an owner and schedule for refreshing the evidence.",
    "review_status": "draft"
  }]
}
```

This is an illustrative output contract. Validate types and references, reject unsupported evidence IDs, and record model/prompt versions. A reviewer accepts, edits or rejects each finding before an action turns it into official assessment input or improvement work.

## Automation rules

| Trigger | Conditions | Effect | Recovery |
| --- | --- | --- | --- |
| Assessment due for review | Owner exists; not approved or cancelled | Notify owner/reviewer | Record delivery failure and retry without duplicate notices |
| Eligible evidence revision | New input revision; no successful draft for that revision | Invoke AIP Logic and stage drafts | Preserve input version and failure reason |
| Improvement overdue | Open task with valid owner and due date | Notify responsible owner | Escalate only under configured rules |
| Periodic review digest | Approved reporting scope and recipients | Render Notepad report and notify | Record as-of time and rendering/delivery outcome |

Use an idempotency key such as `assessment_id + input_revision + automation_purpose`. Avoid retriggering a draft merely because its output object changed. Build failures and source freshness use pipeline health checks; business review rules use Automate.

## Evaluation and access

Test groundedness, evidence-link validity, missing-context behavior, structured-output validity and reviewer acceptance on synthetic or approved test data. Record latency and token consumption separately from business quality. Scope model reads and downstream draft/report visibility to the intended audience. Reviewers remain responsible for official decisions.
