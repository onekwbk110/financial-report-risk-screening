# Data Validation And Report Risk-Control Protocol

Financial red-flag reports can affect a listed company's reputation and investment decisions. Treat the report as a high-stakes analytical document. The goal is to identify risk signals and evidence gaps, not to make legal accusations.

## 1. Source Hierarchy

Use this source order when evidence conflicts:

1. Official filings and exchange disclosures: annual reports, interim reports, audit reports, prospectuses, restatements, inquiry replies, regulatory decisions.
2. Company investor-relations materials: earnings calls, presentations, investor activity records, official website.
3. Structured data vendors or query tools: iWenCai, Wind, Eastmoney, Tushare, Bloomberg, FactSet, etc.
4. Public secondary sources: news, research reports, industry reports, expert commentary.

Rules:

- Never let structured data silently override official filings.
- Use iWenCai-style data as a speed layer and cross-check layer, not the final authority.
- If vendor data conflicts with filings, disclose the conflict and use the filing unless a later official correction exists.
- If a conclusion depends on one weak source, mark its source limitation and classify it as requiring verification.

## 2. Evidence Classes

Tag every important claim:

- `Confirmed fact`: directly from official filing, official announcement, audit report, or regulator document.
- `Calculated fact`: computed from disclosed numbers; include formula, unit, currency, reporting period, and source line/table.
- `Third-party data`: from structured data tools or external databases; must be reconciled to filings for key metrics.
- `Interpretation`: analytical judgment based on facts and calculations.
- `Open question`: unresolved issue that public data cannot settle.

Do not mix these classes in one sentence when the distinction matters.

## 3. Data Validation Checklist

Before scoring or writing conclusions:

1. Confirm company identity: legal name, ticker, exchange, reporting currency, fiscal year, and accounting standard.
2. Confirm report version: original, revised, restated, or corrected.
3. Check accounting comparability:
   - accounting policy changes
   - accounting estimate changes
   - new accounting-standard adoption
   - prior-period error corrections
   - presentation changes and reclassifications
   - restated comparative figures
4. Separate consolidated and parent-company statements.
5. Check unit consistency: yuan/thousand yuan/million yuan, RMB/HKD/USD, shares vs lots.
6. Reconcile core statements:
   - balance sheet total assets = total liabilities + equity
   - income statement net profit ties to profit attribution
   - cash-flow statement ending cash ties to balance-sheet cash where possible
7. Reconcile key metrics from structured data to official filings:
   - revenue
   - net profit attributable to parent
   -扣非净利润 where applicable
   - operating cash flow
   - monetary funds
   - total debt / interest-bearing debt
   - receivables / contract assets
   - inventory
   - goodwill
8. Validate signs and definitions:
   - cash outflow vs inflow
   - net vs gross debt
   - average vs period-end balances
   - TTM vs annual data
   - reported vs adjusted/non-GAAP metrics
9. Document any unresolved mismatch or comparability limitation in the report's validation log.

## 4. Conclusion Controls

Use stricter evidence thresholds for stronger conclusions:

| Conclusion Type | Minimum Evidence Standard |
|---|---|
| P3/P2 watch item | One reliable source plus transparent calculation or filing evidence |
| P1 high-risk issue | Official filing evidence plus at least one corroborating calculation, trend, peer comparison, or event source |
| P0 critical issue | Official filing/regulatory/audit evidence, or a multi-year pattern supported by multiple independent data points |
| `原则排除` | At least one hard gate or multiple P1 issues that cannot be reasonably resolved by public data |
| Fraud/false-disclosure wording | Only when an official regulator, court, exchange, or audit document has made that finding |

If the evidence threshold is not met, downgrade the wording:

- use `risk signal`, `inconsistency`, `requires verification`, `cannot be resolved from public data`
- do not use `fraud`, `false`, `fake`, `fabricated`, `tunneling`, or `money occupation` as established facts unless officially confirmed

## 5. Language Controls

Allowed wording:

- `存在风险信号`
- `与经营逻辑不完全匹配`
- `需要进一步核验`
- `公开资料无法解释`
- `构成高优先级尽调问题`
- `可能存在盈余管理动机或空间`
- `若管理层解释不能成立，则需显著下调财务质量评分`

Avoid unsupported wording:

- `造假`
- `虚构收入`
- `资金被占用`
- `掏空上市公司`
- `财务舞弊`
- `恶意隐瞒`
- `实控人侵占`

Exception: these terms may be used only when clearly attributed to official regulatory, court, exchange, or audit findings.

## 6. Red-Team Review For Severe Reports

Run a red-team review before finalizing when any of these appear:

- total rating is D or E
- final judgment is `原则排除`
- any P0 issue exists
- any claim could materially affect reputation
- report may be shared outside the user's private workspace

Red-team questions:

1. Which conclusion would be most damaging if wrong?
2. Is the exact evidence strong enough for that wording?
3. Did we check restatements, corrected reports, and latest announcements?
4. Did we separate parent and consolidated statements?
5. Did we check market/accounting-standard differences?
6. Did we check accounting policy, estimate, presentation, and reclassification changes before treating ratios as abnormal?
7. Is there a benign business explanation that still fits the facts?
8. Are we double-counting one root cause across multiple deductions?
9. Are all charts and tables traceable to sources?
10. Are all unresolved issues labeled as unresolved?
11. Should the final judgment be softened due to evidence limitations?

## 7. External-Use Control

Unless the user explicitly asks for an external-ready report, mark the output as `内部研究草稿` or `internal research draft`.

For external-ready reports:

- remove casual language
- include source appendix
- include calculation appendix
- include limitation statement
- avoid legal conclusions without official findings
- cite official filing dates and sections wherever possible
- keep a validation log

## 8. Validation Log Format

Use this table in the report:

| Item | Official filing value | Structured-data value | Difference | Resolution | Evidence status |
|---|---:|---:|---:|---|---|
| Revenue |  |  |  |  |  |

For accounting comparability:

| Change | Affected line items | Periods | Quantified impact | Adjustment made | Evidence status |
|---|---|---|---:|---|---|
|  |  |  |  |  |  |

For qualitative evidence:

| Claim | Evidence class | Primary source | Corroboration | Limitation | Evidence status |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
