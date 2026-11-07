# Synthetic example: a KPI review

[scenario.json](scenario.json) contains fictional records for an on-time-delivery KPI and its audit assessment. Dates, IDs and numbers are illustrative.

1. The business observation is **92%**, against a **95%** target.
2. The audit ratings are 90, 80, 70 and 100, weighted 0.3, 0.3, 0.2 and 0.2.
3. The proposed deterministic calculation is `90×0.3 + 80×0.3 + 70×0.2 + 100×0.2 = 85`.
4. The assessment is still **Review**. There is no approval record, so 85 is a calculated preview rather than an approved result.
5. A reviewer checks evidence and approves through an action, which freezes the score inputs and rubric version.
6. An accepted freshness finding can become an owned improvement task shown in the roadmap.

The business result of 92% and the audit score of 85/100 are intentionally different. A missing mandatory evidence item would make the assessment incomplete, even if the arithmetic could still be performed. This JSON illustrates a logical contract; it is not an automatic Foundry import bundle.
