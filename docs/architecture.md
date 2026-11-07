# Metric Compass: architecture

The design organizes the solution into five cooperating layers. Diagram arrows represent different relationships—data movement, function invocation, navigation, embedding or governance—as indicated by their labels.

| Layer | Responsibility |
| --- | --- |
| Data and build orchestration | Ingest, standardize and validate source-derived data; manage dependencies and freshness |
| Ontology and controlled changes | Represent operational entities and relationships; enforce writes through actions |
| Applications and reporting | Give each role an appropriate workspace, timeline and reporting view |
| AIP and human review | Ground language tasks in authorized context and review generated suggestions |
| Workflow and operations | Trigger business effects, monitor failures and support controlled delivery |

## Component responsibilities

| Capability | Role in Metric Compass |
| --- | --- |
| Ontology / Ontology Manager | KPI, observation, assessment, evidence, criterion results and improvement tasks |
| Workshop | Audit workbench: portfolio, evidence, scoring, review and roadmap |
| AIP Chatbot | Explain definitions and approved score breakdowns with evidence links |
| AIP Analyst | Investigate low scores and changes across the KPI portfolio |
| AIP Logic | Draft evidence gaps, summaries and improvement suggestions |
| Automate | Due-review alerts, improvement reminders, AI draft generation and review digests |
| Action Types | Evidence submission, criterion entry, approval and roadmap planning |
| Slate | Executive entry portal and navigation to the audit workbench |
| Notepad | Version-referenced audit report and improvement review |
| Quiver | Criterion breakdowns, approved score trends and improvement progress |
| Code Repository | PySpark data validation; TypeScript scoring and approval functions |
| Pipeline Builder | Standardize source identifiers, units, periods and reference mappings |
| Scheduler | Refresh source-derived KPI/evidence datasets in dependency order |
| Gantt Chart | Improvement tasks and reassessment roadmap inside Workshop |
| LLM | Language reasoning for summaries, evidence review and conversational analysis |

## Key engineering decisions

1. **Current object state is operational truth.** Dataset refreshes supply source-derived fields. Actions own workflow edits. Configure property ownership/edit resolution explicitly so a build cannot silently reset status or approvals. If batch analytics needs edited object state, configure an explicit supported materialization/export; it is not an automatic writeback to the backing dataset.
2. **Scheduler and Automate have different jobs.** Build schedules refresh datasets. Automate watches business conditions or timing rules and invokes actions, functions, AIP Logic or notifications. Use pipeline health checks for failed builds and stale sources. Specify the execution identity and permissions of each automation.
3. **The three AI experiences are distinct.** Chatbot offers curated interaction, Analyst supports ad-hoc investigation, and Logic performs bounded repeatable tasks with validated output. They may use the same model family, but each has separately configured context, tools and permissions.
4. **Access applies throughout.** Restrict data, ontology objects and properties as required; enforce action submission rules. Review access to generated drafts, reports and notifications too. Read-time filtering alone is not a complete downstream data-protection policy.
5. **Use a plain Gantt widget by default.** Date changes happen through action forms. If drag-and-drop resource allocation is required, adopt the Scheduling Gantt widget and configure its additional scheduling ontology and actions.
6. **Keep reports reproducible.** Include the cycle or assessment revision and an as-of timestamp. A live embedded chart may later change; create a dated report snapshot when an immutable review record is required.
7. **Avoid automation loops.** Use request/assessment ID + input version + automation purpose as an idempotency key. Do not regenerate the same draft every time its output object changes. Log invocation status and failures for controlled retry.

## Data path and write path

Source inputs pass through Pipeline Builder and PySpark validation into curated backing datasets. The ontology exposes those records and their relationships. Workshop, Quiver and AI tools consume authorized object state.

Operational changes originate in application actions or explicitly scoped automation. Function-backed actions validate business rules before making object edits. A scheduled dataset refresh must not reset action-managed status, approvals or ownership. Any batch analytics that requires edited object state needs an explicitly configured export/materialization path.

## Design tradeoffs

- **Workshop plus Slate:** Workshop owns the operational workflow; Slate supplies a custom portal where needed. Avoid maintaining two independent rule engines.
- **Pipeline Builder plus Code Repositories:** use visual transformations for simple staging and code for complex validation or reusable business logic.
- **Chatbot plus Analyst plus Logic:** these serve curated conversation, exploratory analysis and repeatable bounded tasks respectively. Their permissions and evaluation criteria differ.
- **Live objects plus snapshots:** live views support operations; versioned snapshots support reproducible approvals and reports.

See [the diagram](diagrams/solution-design.png), [ontology](ontology.md) and [workflow rules](workflows.md).
