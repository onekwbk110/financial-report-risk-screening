# 财报排雷 100 分评分体系

## 1. Rating

Score recent 5 years by default. Use 10 years when data is available or when the company is cyclical, heavily acquisitive, or suspected of long-cycle manipulation.

| Score | Rating | Meaning |
|---:|---|---|
| 85-100 | A | 财务质量优秀，重大红旗少，利润、资产、现金流高度互证 |
| 70-84 | B | 财务质量良好，有可解释瑕疵 |
| 55-69 | C | 财务质量一般，多项问题需验证 |
| 40-54 | D | 财务质量较差，核心资产/利润/现金流至少一项明显弱 |
| 0-39 | E | 高风险，原则排除或进入深度尽调 |

Source basis:

- Official-disclosure basis: conclusions are based on annual reports, interim reports, audit reports, exchange announcements, or regulator filings.
- Supplemented basis: conclusions use official disclosures plus structured data or external context, with conflicts resolved in favor of official filings.
- Unresolved basis: key official disclosures are missing, not comparable, or materially conflicted; affected conclusions must be marked unresolved.

Risk-control rule:

- A severe conclusion cannot rely only on a ratio or third-party structured data. For P1/P0 issues, reconcile to official filings and apply `risk-control-protocol.md`.
- If the report has unresolved data conflicts in revenue, profit, OCF, cash, debt, receivables, inventory, or goodwill, mark the affected conclusion as unresolved and do not escalate severity until resolved.
- If the unresolved conflict affects a hard gate, do not issue a hard-gate conclusion until resolved or clearly label the report as information-insufficient.
- If a margin, expense, asset-quality, or cash-flow anomaly overlaps with a disclosed accounting policy change, estimate change, or presentation reclassification, apply `accounting-policy-change-protocol.md` before deducting points.

## 2. Hard Gates

If one hard gate triggers, rating cap is D unless fully resolved with evidence. If two or more trigger, rate E by default.

1. Audit opinion is disclaimer/adverse, or qualified/emphasis matter affects core assets, revenue, cash, or going concern.
2. Official finding of major financial fraud, false disclosure, occupied funds, or major accounting error in recent 5 years.
3. Cash authenticity concern: high cash + high interest-bearing debt + low interest income + restricted/pledged cash opacity.
4. Operating cash flow is materially below core profit for 3+ years, explained mainly by receivables, inventory, contract assets, or other working-capital build-up.
5. Major unexplained growth or impairment risk in receivables, inventory, goodwill, construction in progress, intangible assets, biological assets, or long-term equity investments.
6. Related-party funds, guarantees, advances, prepayments, or other receivables indicate possible tunneling or funding support.
7. Frequent auditor/CFO changes combined with multiple financial anomalies.
8. The business model or key asset cannot be verified from public evidence and is central to revenue/profit.

## 3. The 15 Domains

| Domain | Points |
|---|---:|
| 1. Audit, disclosure, and reporting credibility | 8 |
| 2. Accounting policy and estimate quality | 6 |
| 3. Business-financial consistency | 7 |
| 4. Parent vs consolidated report and group structure | 6 |
| 5. Cash and financial assets quality | 7 |
| 6. Revenue authenticity and receivables/contract assets | 9 |
| 7. Inventory, cost, and gross margin quality | 8 |
| 8. Long-term operating assets and capex effectiveness | 7 |
| 9. Goodwill, M&A, and long-term investments | 6 |
| 10. Profit structure and recurring earnings quality | 8 |
| 11. Cash-flow quality and free-cash-flow resilience | 9 |
| 12. Debt, liquidity, and financing dependence | 7 |
| 13. Working-capital and operating efficiency | 6 |
| 14. Governance, related parties, pledges, guarantees, litigation | 6 |
| 15. Earnings-management and fraud-pattern risk | 7 |
| **Total** | **100** |

## 4. Fast Rule Overlay

Before final scoring, run `deterministic-red-flag-rules.md`. Use triggered rules to:

1. Create issue cards.
2. Allocate deductions to the relevant scoring domains.
3. Escalate multi-rule clusters.
4. Mark affected metrics unresolved/not comparable when required data is unavailable.

Do not double-count the same root cause. Example: receivables growth, weak OCF, and low sales-cash ratio may all describe one revenue-collection problem; score it once but cite all evidence.

For each triggered rule, record whether the evidence is from official filing, calculated fact, structured-data query, secondary source, or open question.

## 5. Domain Checks

### 1. Audit, Disclosure, And Reporting Credibility, 8

Full-score signals:

- Standard unqualified audit opinion for many years.
- Key audit matters are clear and consistent with business.
- Notes disclose aging, impairment, restricted cash, related parties, segment data, top customers/suppliers where required.
- No frequent restatements, auditor changes, CFO changes, or late reports.

Deduct:

- Non-standard audit opinion: -4 to -8.
- Key audit matters repeatedly focus on revenue, inventory, impairment, goodwill, going concern, or cash: -1 to -4.
- Auditor changes, especially after non-standard opinion: -2 to -5.
- Weak notes for key accounts: -1 to -4.
- Accounting restatement or correction: -2 to -6.

### 2. Accounting Policy And Estimate Quality, 6

Check revenue recognition, inventory costing, depreciation/amortization lives, bad-debt provisioning, impairment tests, R&D capitalization, borrowing-cost capitalization, fair-value assets, lease accounting, deferred tax.

Also check disclosed changes in accounting policies, accounting estimates, new standard adoption, prior-period error corrections, and presentation reclassifications. Build a bridge when expenses or assets move between accounts.

Deduct:

- Policy/estimate change increases profit without strong business reason: -2 to -6.
- Presentation/reclassification change makes key ratios look better but is not quantified or clearly explained: -1 to -4.
- Affected line items are compared across years without adjustment despite disclosed reclassification: -1 to -3 and mark as not comparable.
- Depreciation/amortization lives materially more aggressive than peers: -1 to -3.
- R&D or interest capitalization ratio rises sharply: -1 to -4.
- Bad-debt, inventory, impairment assumptions looser than risk profile: -1 to -4.
- Deferred tax assets/liabilities change sharply without clear source: -1 to -3.

### 3. Business-Financial Consistency, 7

Use 薛云奎四维 and 叶金福互证.

Check:

- Revenue growth vs volume, price, capacity, store/user/order data, geography, and channel.
- Cost changes vs raw materials, labor, energy, utilization, logistics.
- Asset growth vs business expansion.
- Margin vs competitive position and industry cycle.

Deduct:

- Financial growth lacks nonfinancial support: -2 to -7.
- KPI trend contradicts revenue/profit trend: -2 to -6.
- Business explanation depends only on management narrative: -1 to -4.
- Industry downturn but company sharply outperforms without evidence: -2 to -6.

### 4. Parent Vs Consolidated Report And Group Structure, 6

Use 张新民 framework.

Check:

- Parent company operating assets vs investment assets after excluding cash.
- Parent revenue/profit/cash vs consolidated.
- Other receivables/payables between parent and subsidiaries.
- Minority interests, minority profit share, subsidiaries contributing assets/profit/cash.
- Whether parent is operating-led, investment-led, or mixed.

Deduct:

- Parent has little operation but large unexplained receivables/prepayments: -1 to -4.
- Consolidated profit depends on subsidiaries while parent cash/controls are weak: -1 to -4.
- Minority interests or profit share inconsistent with consolidation story: -1 to -3.
- Group structure too complex for public verification: -1 to -4.

### 5. Cash And Financial Assets Quality, 7

Check monetary funds, restricted cash, pledged deposits, wealth-management products, financial assets, interest income, interest-bearing debt.

Deduct:

- High cash plus high debt: -2 to -7.
- Interest income too low for reported cash/financial assets: -2 to -6.
- Restricted/pledged cash material or unclear: -2 to -6.
- Large wealth-management products while raising debt/equity: -1 to -4.
- Cash concentrated in subsidiaries with limited parent access: -1 to -3.

### 6. Revenue Authenticity And Receivables/Contract Assets, 9

Check revenue by product, region, customer, channel, contract type, receivables, notes receivable, contract assets, long-term receivables, other receivables, bad debt, aging, top customers, return/refund terms.

Deduct:

- Receivables/contract assets grow faster than revenue: -2 to -6.
- Aging deteriorates or long-aged balances rise: -2 to -6.
- Bad-debt provision ratio declines while credit risk rises: -2 to -5.
- Revenue surge near period end or seasonal pattern abnormal: -1 to -4.
- New/overseas/related/dealer customers drive growth without cash: -2 to -7.
- Sales cash received lags revenue: -2 to -6.

### 7. Inventory, Cost, And Gross Margin Quality, 8

Use 叶金福毛利率分解.

Check:

- Inventory by raw materials, WIP, finished goods, goods shipped, development cost.
- Inventory turnover, aging if available, impairment, write-down reversals.
- Gross margin by product/region/channel.
- Unit price, unit cost, raw material cost, labor, manufacturing overhead, utilization.

Deduct:

- Inventory grows faster than revenue/cost for 2+ years: -2 to -6.
- Finished goods or slow-moving inventory rises: -2 to -5.
- Inventory write-down insufficient vs turnover/price decline: -2 to -5.
- Gross margin materially above peers or rises against industry trend: -2 to -6.
- Unit cost or yield assumptions inconsistent with production data: -2 to -6.
- Cost capitalization into inventory suspected: -2 to -5.

### 8. Long-Term Operating Assets And Capex Effectiveness, 7

Check fixed assets, construction in progress, intangible assets, development expenditure, right-of-use assets, long-term deferred expenses, biological assets, oil/gas assets, productive capacity.

Deduct:

- Capex remains high but revenue/core profit does not follow: -2 to -6.
- Construction in progress long overdue or repeated budget increases: -2 to -5.
- Fixed asset turnover deteriorates without strategic explanation: -1 to -4.
- Major intangible/development capitalization with weak products/revenue: -2 to -6.
- Large impairment or delayed impairment risk: -2 to -6.
- Specialized assets tied to one customer/product: -1 to -4.

### 9. Goodwill, M&A, And Long-Term Investments, 6

Check goodwill, acquired intangible assets, performance commitments, long-term equity investments, investment income, fair-value changes, disposal gains.

Deduct:

- Goodwill high vs equity/assets: -2 to -5.
- Acquired business underperforms or commitments pressure accounting: -2 to -6.
- M&A creates large goodwill/intangible assets but little cash/profit: -2 to -6.
- Investment income contributes material profit but cash dividends weak: -1 to -4.
- Long-term equity investment impairment delayed or sudden: -2 to -5.
- Frequent cross-industry acquisitions: -1 to -4.

### 10. Profit Structure And Recurring Earnings Quality, 8

Check core profit, operating profit, nonrecurring items, investment income, fair-value gains, asset disposal, government grants, other income, credit/asset impairment, tax effects.

Deduct:

- Net profit relies on nonrecurring gains: -2 to -6.
- Core operating profit weak while net profit strong: -2 to -6.
- Government subsidies or other income material and unstable: -1 to -4.
- Expenses unusually low vs peers/history: -1 to -4.
- Large impairment creates “big bath” then rebound: -1 to -5.
- Tax rate abnormal or tax expense inconsistent with profit: -1 to -4.

### 11. Cash-Flow Quality And Free-Cash-Flow Resilience, 9

Check operating cash flow, sales cash received, purchase cash paid, indirect-method adjustments, capex, dividends, borrowing, free cash flow.

Deduct:

- CFO/net profit below 0.8 for multiple years without good reason: -2 to -6.
- CFO negative while profit/revenue grows: -3 to -8.
- OCF boosted mainly by supplier/customer funding that may reverse: -1 to -5.
- Investment cash outflow unsupported by future operating results: -2 to -6.
- Frequent financing needed to maintain operations: -2 to -6.
- Dividends exceed sustainable free cash flow: -1 to -4.

### 12. Debt, Liquidity, And Financing Dependence, 7

Check short-term debt, long-term debt, bonds, leases, notes payable, interest expense, maturity, covenants, restricted assets, debt cost.

Deduct:

- Short debt pressure and insufficient available cash: -2 to -6.
- Interest-bearing debt grows faster than operating assets/cash flow: -1 to -5.
- Interest coverage deteriorates: -1 to -4.
- Debt used for low-yield financial assets or idle funds: -1 to -4.
- Significant off-balance guarantees or pledged assets: -2 to -6.
- Refinancing dependence in weak market: -2 to -5.

### 13. Working-Capital And Operating Efficiency, 6

Check receivable days, inventory days, payable days, cash conversion cycle, operating working capital, prepayments, advances from customers/contract liabilities.

Deduct:

- Cash conversion cycle deteriorates: -1 to -5.
- Receivable days and inventory days rise together: -2 to -6.
- Payable days expansion masks weak cash flow: -1 to -4.
- Negative working capital is not supported by bargaining power: -1 to -4.
- Growth requires rising working capital intensity: -1 to -4.

### 14. Governance, Related Parties, Pledges, Guarantees, Litigation, 6

Check related sales/purchases, funds, guarantees, pledges, controller financial pressure, board/governance, management pay incentives, lawsuits, penalties.

Deduct:

- Related transactions material or opaque: -2 to -6.
- Other receivables/prepayments/guarantees point to controller or related parties: -2 to -6.
- High controller pledge ratio or forced-sale risk: -1 to -4.
- Major litigation/contingent liabilities: -1 to -4.
- Management incentives create earnings pressure: -1 to -3.
- Regulatory inquiries or penalties: -1 to -6.

### 15. Earnings-Management And Fraud-Pattern Risk, 7

Use 邹佩轩 illegal-vs-legal distinction and 叶金福舞弊恒等式.

Check:

- Fraud triangle: pressure, opportunity, rationalization.
- Revenue/cost/cash/goodwill/investment-income/related-party patterns.
- Legal smoothing: revenue timing, expense accruals, capitalization, impairment timing, deferred tax.

Deduct:

- Strong pressure to meet listing, refinancing, ST avoidance, performance commitment, or market expectation: -1 to -4.
- Abnormal gross margin plus abnormal asset: -3 to -7.
- Accruals expand materially while cash weak: -2 to -6.
- Deferred tax, provisions, impairment, or capitalization signals profit shifting: -1 to -5.
- Multiple small red flags across unrelated accounts: -2 to -7.

## 5. Scorecard Output Format

For each domain output:

- score/max
- evidence
- deductions
- evidence status when a key data point is unresolved or not comparable
- linked issue cards

Then output:

- total score and rating
- hard gates triggered
- top 10 red flags
- whether public evidence is sufficient
- next verification steps
