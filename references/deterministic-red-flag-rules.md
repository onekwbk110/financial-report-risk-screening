# Deterministic Red-Flag Rule Library

This reference distills the downloaded `财报排雷v2` skill into a safer rule layer. Use these as fast triggers, not final conclusions. Every triggered rule must be validated through business logic, accounting policy, cash flow, balance-sheet trace, and peer comparison.

## Use Rules

1. Run rules after basic extraction and before 15-domain scoring.
2. Record result as triggered / not triggered / unavailable / not comparable.
3. Unavailable data lowers disclosure quality but is not automatically a red flag, especially for Hong Kong filings.
4. Industry-specific balance sheets override generic thresholds. Banks, insurers, brokers, utilities, developers, SaaS, biotech, and platform companies need adapted tests.
5. If a rule triggers for 2+ consecutive years or combines with another related rule, escalate priority.

## Severity Mapping

- High -> usually P1; P0 if it touches cash authenticity, audit opinion, official fraud, going concern, or controller fund occupation.
- Medium -> usually P2; escalate to P1 if persistent, large, or combined with cash-flow weakness.
- Info -> context adjustment, not a deduction by itself.

## 38 Fast Rules

| ID | Domain | Trigger | Severity | Map To |
|---|---|---|---|---|
| T001 | Receivables | Receivable growth exceeds revenue growth by >10pp for 2 consecutive years | High | Revenue authenticity |
| T002 | Receivables | Ending receivables / revenue >30%; use industry-specific threshold | Medium | Revenue authenticity |
| T003 | Receivables | Ending receivables / revenue >100% | High | Revenue authenticity, hard-gate candidate |
| T004 | Receivables | Receivables over 1 year >20% or rises >5pp YoY | High | Revenue authenticity |
| T005 | Inventory | Inventory growth exceeds revenue growth by >15pp | Medium | Inventory/cost |
| T006 | Inventory | Inventory write-down ratio materially below peers or suddenly declines | Medium | Inventory/cost |
| T007 | Inventory | Inventory days rise >30 days YoY or >2x peer average | Medium | Inventory/cost |
| T008 | Goodwill | Goodwill / equity >30% | Medium | Goodwill/M&A |
| T009 | Goodwill | Acquired target misses expectations but goodwill is not impaired | High | Goodwill/M&A |
| T010 | Cash | High cash and high interest-bearing debt coexist | High | Cash quality, hard-gate candidate |
| T011 | Cash | Interest income / average cash and financial assets is abnormally low | High | Cash quality |
| T012 | Cash | Restricted cash / monetary funds >30% | High | Cash quality |
| T013 | OCF | OCF / net profit <1 for 3+ years | High | Cash-flow quality |
| T014 | Sales Cash | A-share sales cash received / revenue persistently below VAT-adjusted benchmark | Medium | Cash-flow quality |
| T015 | Sales Cash | HK/US sales cash received / revenue persistently below 1.0 without business reason | Medium | Cash-flow quality |
| T016 | Profit Quality | Nonrecurring gains / net profit >30% | Medium | Profit structure |
| T017 | Gross Margin | Gross margin moves >10pp without business explanation | High | Gross margin |
| T018 | Expenses | Revenue grows while expense ratio drops >5pp without explanation | Medium | Earnings management |
| T019 | Audit | Audit opinion is not clean/unmodified, or emphasis affects core risks | High | Credibility, hard-gate candidate |
| T020 | Audit | Auditor changed more than once in 3 years, or changed after problematic opinion | High | Credibility |
| T021 | Controller | Controlling shareholder pledge ratio >50% | High | Governance |
| T022 | Related Party | Related sales / revenue >30% or related transaction is economically central | High | Governance |
| T023 | Revenue Timing | Q4 revenue >35% of full-year revenue without seasonality | Medium | Revenue authenticity |
| T024 | CIP | Construction in progress materially overdue or over budget and not transferred | High | Long-term assets |
| T025 | Fixed Assets | Fixed assets / assets >40% and turnover below peers | Medium | Long-term assets |
| T026 | Consolidation | Large intragroup transactions and asymmetric parent/subsidiary profit/cash | High | Parent-consolidated |
| T027 | Financing CF | Financing inflows and outflows both >2x operating cash flow | Medium | Debt/liquidity |
| T028 | Tax | Effective tax unusually low and tax benefits explain material profit | Medium | Profit quality |
| T029 | Overseas | Overseas revenue >50% and margin far above domestic/peers | High | Revenue authenticity |
| T030 | Controller | Controller shares frozen or pledge/forced-sale risk disclosed | High | Governance |
| T031 | Audit/Governance | Overseas revenue dominates but auditor capability/disclosure is weak | Medium | Credibility |
| T032 | Revenue/Fraud | Gross margin far above peers without moat evidence | High | Gross margin |
| T033 | Revenue/Fraud | Contracts and fund flows form a circular chain without real business | High | Fraud-pattern |
| T034 | Asset Inflation | CIP payments or counterparties suggest related-party circular funding | High | Long-term assets |
| T035 | OCF | Operating cash flow negative for 3 consecutive years | High | Cash-flow quality |
| T036 | Inventory | Inventory write-down / inventory <1% while inventory days rise | Medium | Inventory/cost |
| T037 | Receivables | Bad-debt expense/provision falls >30% while receivable risk rises | High | Revenue authenticity |
| T038 | Impairment | Reversal of impairment/provisions >10% of net profit | High | Earnings management |

## Rule Clusters

Escalate when these combinations appear:

1. **Paper-profit cluster**: T001/T003/T004 + T013/T014/T015.
2. **Cash authenticity cluster**: T010 + T011 + T012.
3. **Inventory-cost cluster**: T005/T007 + T017/T036.
4. **Acquisition-risk cluster**: T008/T009 + nonrecurring profit + weak OCF.
5. **Controller-risk cluster**: T021/T030 + related receivables/prepayments/guarantees.
6. **Cross-border opacity cluster**: T029 + T031 + weak cash collection.
7. **Big-bath/smoothing cluster**: T018 + T028 + T038 + deferred tax anomalies.

## Known Fixes To Downloaded Skill

The downloaded skill is useful, but correct these issues when using its rules:

1. CAS/A-share inventory accounting does not generally allow LIFO under current PRC standards; do not treat A-share LIFO as normal.
2. Long-term asset impairment under CAS is generally not reversible once recognized; short-term assets such as inventory and receivables have different treatment.
3. The sales-cash/revenue benchmark around 1.13 is only a rough A-share VAT heuristic. It varies with tax rate, export rebates, business model, collection cycle, and revenue classification.
4. “Non-standard audit opinion” should not always be automatic P0. Emphasis matters differ in severity; use hard gate only when core assets, revenue, cash, or going concern are affected.
5. Thresholds like 30% receivables/revenue or goodwill/equity must be industry-adjusted.
