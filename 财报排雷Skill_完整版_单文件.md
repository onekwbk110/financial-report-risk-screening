# 上市公司财报排雷 Skill · 完整版（单文件）

> 把"读财报先排雷"做成一套能装进 AI Agent 的工作流：先回答**报表能不能信、利润有没有现金和资产撑、资产是真家底还是未来的雷**，给出 15 维 / 100 分的财务质量评分（A–E）和每个雷点的"四步验证问题卡"。
>
> ⚠️ **免责声明**：仅供学习研究，**不构成投资建议，不荐股、不估值、不给买卖指令、不承诺收益**。只识别"风险信号"；除非已有官方监管 / 司法 / 交易所 / 审计 / 公司公告认定，绝不把"造假 / 虚增 / 资金占用 / 财务舞弊"作为事实结论。盈亏自负。

---

## 它是给"能干活的 AI Agent"用的

- **完整体验**：Claude Code / Codex / OpenClaw / Hermes 等能联网取数、读文件、跑脚本、出 HTML 的 Agent——把本文当 skill 装上，或整段喂给它，它能取数 → 校验 → 评分 → 出问题卡 → 写长版报告 → 导出 HTML。
- **降级用法**：只会聊天的对话框（元宝 / Kimi / 豆包等）下载不了年报、跑不了完整流程；你得**自己把年报数据/原文喂进去**，它只能照规则帮你分析推理。

## 三步上手（整段喂的用法）

1. **整段复制本文全文**（从开头到结尾）。
2. **粘贴进 AI**，回车发送。
3. 接着发一句需求 + 你手上的年报数据/原文，例如：
   > "现在你按下面这套财报排雷流程，分析我贴的这份年报：先判断报表可信度，再看利润质量、资产质量、现金流质量，给 15 维评分和重点风险问题卡。只说风险信号，别下'造假'定论，也别给买卖建议。"

> 下面依次是：主流程（SKILL.md）＋ 10 篇深度细则（references）。Agent 装成 skill 时会按需加载这些细则；整段喂时它们已全部在下方。

---

# ========== 主流程：SKILL.md ==========

---
name: financial-report-risk-screening
description: Use when analyzing a listed company's annual report for financial-report red flags, financial quality scoring, fraud/earnings-management risk, asset quality, profit quality, cash-flow quality, parent/consolidated report differences, related-party risks, or when producing a standardized 财报排雷 report.
---

# Financial Report Risk Screening

This skill turns annual reports into a financial-quality scorecard and red-flag diagnosis. It is not an equity valuation skill. Use valuation only as optional context after report credibility and financial quality are established.

Default delivery mode: one-shot execution to a final polished HTML report. When the user asks to run this workflow on a company, continue through data collection, validation, analysis, report writing, HTML export, visual browser inspection, and final quality checks. Stop only for true blockers such as inaccessible filings, required login/credential gates, unresolved core-data conflicts that would make the conclusion unsafe, or explicit external-publication/legal approval needs. Keep Markdown as the editable source, and generate PDF only when the user asks for a print/archive version or when an existing downstream workflow requires it.

Output folder rule: write artifacts into a project-local or user-specified folder, normally `<output-root>/<company>_<ticker>/`, using subfolders `01_final_report`, `02_official_filings`, and `03_workpapers_validation` when an archive is requested. Do not assume a fixed local path.

Ownership rule: default author/organization mark is `kwbk`. Override only if the user provides a different author/organization. Always keep report date, source basis, and the limitation statement in the footer.

Long-form report-standard rule: the final HTML/Markdown must be a polished long-form report, not a short dashboard-only memo. Use `references/long-form-report-standard.md` and `references/html-export-standards.md` before writing and exporting. If a generated report is only a few scorecards, KPI cards, or brief issue bullets, it is incomplete for this workflow. Account-level decomposition is a middle evidence layer, not a replacement for global analysis: keep the full narrative spine, then drill down into accounts.

## Core Principle

财报排雷先回答四个问题：

1. 报表能不能信？
2. 利润有没有资产和现金支持？
3. 资产是不是有质量，还是未来爆雷的载体？
4. 经营、管理、财务、治理是否互相印证？

Never accuse fraud as a legal conclusion. State “risk signal”, “strong inconsistency”, “requires verification”, or “likely earnings management” unless there is official regulatory evidence.

## Source Stack

Use these book-derived lenses together:

- 排除优先：财报先用于排除企业；看不懂、不可信、解释不清就排除。
- 肖星：三表闭环；利润不等于现金；资产是未来利益而非天然安全。
- 张新民：底子/面子/日子；母公司与合并报表差异；资产质量、利润质量、现金流质量；造血/输血；资产爆雷地图。
- 叶金福：财务数据与非财务数据互证；横向/纵向两条主线；异常毛利率 + 异常资产；舞弊恒等式。
- 邹佩轩：非法舞弊和合法财务调节分开；收入确认、资本化、减值、递延所得税是重点。
- 薛云奎：经营、管理、财务、业绩四维穿透。
- 郭永清：拉长时间窗口；投资活动看战略，融资活动看风险，资产资本结构看流动性。
- 夏立军/海马财经：投资者指标工作台和数字游戏防范。

## Workflow

1. **Build evidence pack**
   - Collect 5-10 years of annual reports when possible, plus latest interim report.
   - Include audit reports, notes, MD&A, segment data, accounting policy/estimate changes, presentation reclassifications, related-party disclosures, guarantees, litigation, pledges, regulatory inquiries, penalties, restatements, and auditor changes.
   - Use structured data sources such as iWenCai as a speed and cross-check layer when available, but keep official filings as the final authority.
   - Normalize consolidated and parent-company statements separately.
   - Identify market, fiscal year, reporting currency, accounting standard, and audit standard. Load `references/market-adapters.md` when the company is A-share, Hong Kong, US-listed, A+H, or a Chinese ADR.

2. **Understand business before scoring**
   - Map products/services, revenue model, customer/channel, suppliers, geography, capacity, production/sales volume, pricing, cost drivers, and industry cycle.
   - List nonfinancial KPIs that should explain financial numbers.

3. **Run deterministic red-flag rules**
   - Use `references/deterministic-red-flag-rules.md` as a fast screening layer.
   - Treat each rule as a trigger for investigation, not a final verdict.
   - Map triggered rules to issue cards and scoring domains.

4. **Validate data and source hierarchy**
   - Use `references/risk-control-protocol.md` before scoring.
   - Reconcile official filings, structured data, calculations, and peer data.
   - Classify evidence as confirmed fact, calculated fact, third-party data, interpretation, or open question.
   - Document unresolved data conflicts and mark the affected metrics as unresolved or not comparable.

5. **Check accounting comparability before judging anomalies**
   - Use `references/accounting-policy-change-protocol.md`.
   - Identify accounting policy changes, accounting estimate changes, reporting-standard adoption, prior-period corrections, and presentation reclassifications.
   - Build a comparability bridge for affected line items before interpreting ratio changes.
   - Mark affected metrics as adjusted, not comparable, or unresolved when amounts cannot be bridged.

6. **Apply hard gates first**
   - See `references/scoring-system.md`.
   - If any hard gate triggers, cap rating as instructed before detailed scoring.

7. **Score 15 domains**
   - Use the 100-point system in `references/scoring-system.md`.
   - Score by evidence, not vibes. Show deductions and uncertainty.

8. **Generate issue cards**
   - For every P0/P1/P2 red flag, create a separate issue breakdown using `references/red-flag-playbook.md`.
   - Each issue card must include trigger evidence, business explanation test, accounting explanation test, cash-flow test, likely causes, verification steps, and score impact.

9. **Run severe-conclusion review**
   - If the rating is D/E, any P0 exists, or the final judgment is “原则排除”, run the red-team checklist in `references/risk-control-protocol.md`.
   - Strong language requires official regulatory, court, exchange, audit, or filing evidence.

10. **Write report**
   - Use `references/report-template.md`.
   - For a polished long-form report, also use `references/long-form-report-standard.md`.
   - Lead with total score, rating, hard gates, top red flags, source basis, and whether the company is “可继续研究 / 需重大折价审查 / 原则排除”.
   - Write a reader-facing report that is concise at the top but deep by account subject: conclusion first, then global business/storyline analysis, three-statement synthesis, account-level red-flag map, beginner-friendly scoring explanation, and standalone account cards for cash, debt, receivables, inventory, goodwill/M&A, capex/fixed assets, profit-quality items, cash-flow items, parent-company intercompany items, and governance/related-party items when relevant.
   - Do not choose between "global analysis" and "account decomposition". The preferred output is both: a full-context narrative plus a market-facing account-by-account evidence layer. The reader should first understand the company's overall financial story, then be able to jump into a specific account and see the evidence.
   - Use the WeChat-style product narrative when explaining the workflow: start from the user's feedback/pain point, explain why a superficial format change would mislead, list the concrete upgraded modules, then restate the boundary that this is a filter/risk-verification tool, not valuation or investment advice.
   - Do not write a long essay that only groups content by broad themes such as profit quality / asset quality / cash flow. The market-facing value of this workflow is account-level decomposition tied back to the overall story. Every important balance-sheet, income-statement, and cash-flow account should answer: why this account matters, what changed, whether the business explanation is sufficient, what accounting estimate/policy may affect it, where it lands in cash flow, and what to verify next.
   - Keep narrative paragraphs short, but do not under-deliver. Use tables, account cards, score bars, risk tags, and verification checklists to carry detail. Dashboard pages may appear near the front, but they cannot replace the global narrative or the account-by-account diagnosis.

11. **Export final deliverables**
   - Produce a polished standalone HTML final report by default.
   - Preserve a Markdown source report and any structured data/validation notes next to the HTML.
   - Use `references/html-export-standards.md` for native reader-facing layout; treat HTML as the primary report surface generated from the evidence pack and analysis structure, not as a decorative conversion from an existing Word/PDF report.
   - Generate a PDF only when the user explicitly asks for a print/archive copy or when a downstream publication package requires it; use `references/pdf-export-standards.md` for that optional export.
   - The HTML should normally be a formal long-form report with conclusion-first navigation, KPI cards, issue cards, scoring explanation, source appendix, and print-friendly CSS. A dashboard-only HTML output fails the standard unless the user explicitly asks for a brief.
   - Visually inspect the HTML in the browser after export; fix clipping, overlapping text, broken tables, missing glyphs, unreadable charts, and mobile overflow before final delivery.
   - When archiving is requested, archive final report, official filings, source index, validation log, and reproducibility script into the project output folder.

## Output Rules

- Always distinguish facts, calculations, interpretation, and open questions.
- Prefer 5-10 year trend and peer comparison over one-year thresholds.
- Do not interpret changes in margins, expense ratios, OCF, or asset ratios until accounting policy, estimate, and presentation changes have been checked.
- A ratio is only a clue; require business, accounting, cash-flow, and asset-side explanation.
- Do not mechanically apply A-share thresholds to Hong Kong or US filings; adjust for accounting standard, tax system, disclosure granularity, fiscal year, and cash-flow classification.
- If disclosure is insufficient, deduct from disclosure quality and mark the affected conclusion as unresolved or not comparable.
- If a problem cannot be resolved from public data, mark it as “需要进一步验证”, not “已证实”.
- Do not use fraud or misconduct wording as fact unless an official source has made that finding.
- Default final artifact is a standalone HTML report, plus the Markdown source and evidence/validation files when created. PDF is optional unless the user requests it.
- Include a reproducible generation script or command notes in the validation/workpapers folder when applicable.

## References

- Detailed scoring: `references/scoring-system.md`
- Red-flag issue cards: `references/red-flag-playbook.md`
- Deterministic red-flag rule library: `references/deterministic-red-flag-rules.md`
- A/H/US market and accounting adapters: `references/market-adapters.md`
- Data validation and report risk control: `references/risk-control-protocol.md`
- Accounting policy, estimate, and presentation-change checks: `references/accounting-policy-change-protocol.md`
- PDF export and visual QA: `references/pdf-export-standards.md`
- HTML export and report layout: `references/html-export-standards.md`
- Report structure: `references/report-template.md`
- Long-form report standard: `references/long-form-report-standard.md`

# ========== 细则：references/scoring-system.md ==========

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

# ========== 细则：references/deterministic-red-flag-rules.md ==========

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

# ========== 细则：references/red-flag-playbook.md ==========

# Red-Flag Issue Playbook

For every P0/P1/P2 issue, produce a standalone issue card.

## Issue Card Template

1. **Issue**: concise name.
2. **Priority**: P0 direct exclusion / P1 high risk / P2 needs verification / P3 monitor.
3. **Affected accounts**: statements and notes.
4. **Trigger evidence**: year, amount, ratio, trend, peer gap, source.
5. **Business test**: can product, price, volume, capacity, customer, channel, region, or industry cycle explain it?
6. **Accounting test**: can policy, estimate, recognition timing, capitalization, impairment, tax, or consolidation explain it?
7. **Cash-flow test**: did cash arrive or leave? Compare OCF, sales cash received, capex, financing, dividends.
8. **Asset-side trace**: where did the profit/cash/story land on the balance sheet?
9. **Likely causes**: normal expansion, credit loosening, channel stuffing, aggressive recognition, delayed costs, idle capital, tunneling, fraud risk.
10. **Verification steps**: annual report notes, inquiry letters, subsequent collection, customer/supplier data, industry stats, regulatory filings.
11. **Score impact**: domains and deductions.
12. **Conclusion**: resolved / unresolved / high-risk unresolved.

## Priority Definitions

- **P0**: likely direct exclusion. Evidence indicates major reliability or solvency problem.
- **P1**: high-risk issue that can materially change financial-quality conclusion.
- **P2**: meaningful uncertainty; needs further data but not direct exclusion.
- **P3**: normal volatility or minor watch item.

## Standard Issue Types

### 1. High Cash + High Debt

Core suspicion: cash may be restricted, pledged, inaccessible, low-yield, or overstated; debt may signal real liquidity pressure.

Check:

- Monetary funds / total assets.
- Interest-bearing debt / total assets.
- Interest income / average cash and financial assets.
- Interest expense / average debt.
- Restricted cash, pledged deposits, bank acceptance notes.
- Wealth management while borrowing.
- Parent cash vs consolidated cash.

Red flags:

- Cash abundant but short-term debt high.
- Interest income far below deposit/wealth-management yield.
- Large restricted cash or notes payable requiring deposits.
- Debt grows while cash idles.

### 2. Receivables And Revenue Authenticity

Core suspicion: revenue recognized before cash, weak customers, channel stuffing, fictitious revenue, relaxed credit.

Check:

- Revenue growth vs receivables/contract assets.
- Sales cash received / revenue.
- Receivable aging and provision.
- Top customers, new customers, overseas customers, related customers.
- Return policies, rebates, warranty, bill-and-hold, principal-agent.

Red flags:

- Receivables grow faster than revenue.
- Long-aged receivables rise while provision ratio falls.
- Contract assets become a major asset.
- Revenue grows but cash collection weakens.

### 3. Inventory And Cost Quality

Core suspicion: obsolete inventory, overproduction, cost capitalization, under-recognized COGS, inflated quantities/cost.

Check:

- Inventory by category.
- Finished goods ratio.
- Inventory turnover and days.
- Inventory write-down policy.
- Gross margin by product.
- Raw material price trend, production volume, utilization.

Red flags:

- Inventory grows while sales slow.
- Finished goods pile up.
- Gross margin improves while inventory turnover worsens.
- Write-downs are small despite industry price decline.

### 4. Gross Margin Anomaly

Core suspicion: pricing/cost story is inconsistent, possible revenue inflation or cost understatement.

Check:

- Product mix.
- Unit price and unit cost.
- Peer margin.
- Industry cycle and raw materials.
- Channel changes.
- Capacity utilization.

Red flags:

- Margin rises against industry trend.
- Margin far above peers without moat evidence.
- Low expenses plus high margin.
- High margin concentrated in new/opaque products.

### 5. Capex, Fixed Assets, And Construction In Progress

Core suspicion: money spent but no productive capacity, delayed transfer, inflated project cost, future impairment.

Check:

- Capex vs revenue growth.
- CIP aging and transfer to fixed assets.
- Asset turnover.
- Capacity data.
- Impairment.
- Customer/product dependency.

Red flags:

- Long-term high capex but no income/cash result.
- CIP stays high for years.
- Fixed asset turnover falls sharply.
- Sudden impairment after years of expansion.

### 6. Intangibles, Development Expenditure, And R&D Capitalization

Core suspicion: expenses capitalized to inflate profit, intangible assets cannot support future revenue.

Check:

- R&D expense vs development expenditure.
- Capitalization ratio.
- Amortization life.
- Product approvals, patents, launches.
- Impairment.

Red flags:

- Capitalization ratio rises when profit pressure rises.
- Capitalized projects fail to generate revenue.
- Amortization period longer than peers/product cycle.

### 7. Goodwill And M&A

Core suspicion: acquisition price overpaid, performance commitment pressure, delayed impairment, profit manufactured through acquisition.

Check:

- Goodwill / equity.
- Acquisition consideration vs net assets.
- Identifiable intangible fair-value step-up.
- Performance commitments.
- Subsidiary revenue/profit/cash.
- Impairment test assumptions.

Red flags:

- High goodwill with declining acquired profit.
- Optimistic discount/growth assumptions.
- Commitment period profit spike then decline.
- M&A into unrelated industries.

### 8. Operating Cash Flow vs Net Profit

Core suspicion: paper profit, working-capital absorption, earnings management.

Check:

- OCF/net profit.
- Indirect cash-flow adjustments.
- Receivables, inventory, payables.
- Sales cash received.
- Tax paid vs tax expense.

Red flags:

- OCF persistently below profit.
- Profit grows while OCF worsens.
- Cash flow supported by payables rather than collection.

### 9. Related Parties And Funds Occupation

Core suspicion: tunneling, disguised financing, revenue/cost manipulation, external support.

Check:

- Related sales/purchases.
- Other receivables/payables.
- Prepayments.
- Guarantees.
- Controller pledge.
- Shared customers/suppliers.

Red flags:

- Large non-operating receivables.
- Prepayments to weak or unknown suppliers.
- Related sales with high margin.
- Guarantees for related parties.

### 10. Accounting Change And Profit Smoothing

Core suspicion: legal earnings management.

Check:

- Policy/estimate changes.
- Depreciation life/residual value.
- Bad debt and impairment assumptions.
- Revenue recognition.
- Provisions.
- Deferred tax.

Red flags:

- Changes coincide with performance pressure.
- One-time big bath then rebound.
- Deferred tax assets rise with provisions/impairment.
- Expense accruals reversed in profitable periods.

### 11. Investment Income And Fair Value Gains

Core suspicion: profit not from core operations, valuation gains may reverse.

Check:

- Investment income cash dividends vs equity-method profit.
- Fair-value hierarchy.
- Related-party investments.
- Disposal gains.

Red flags:

- Core profit weak but net profit strong.
- Fair-value gains dominate profit.
- Equity-method profit without cash dividend.

### 12. Debt And Liquidity Stress

Core suspicion: refinancing dependence, maturity mismatch, hidden restrictions.

Check:

- Short debt vs available cash.
- Current ratio after excluding restricted cash and weak inventory/receivables.
- Interest coverage.
- Debt maturity.
- Bond prices, credit rating changes if available.

Red flags:

- Short debt larger than usable cash.
- Interest coverage falls.
- Debt rolls over frequently.
- Asset pledges and guarantees rise.

### 13. Parent-Consolidated Mismatch

Core suspicion: holding-company opacity, cash trapped in subsidiaries, parent supports subsidiaries, consolidation masks risk.

Check:

- Parent assets: operating vs investment.
- Parent other receivables from subsidiaries.
- Parent cash vs consolidated cash.
- Parent debt guarantees.
- Subsidiary minority interests/profits.

Red flags:

- Parent borrows while subsidiaries hold cash.
- Parent other receivables large.
- Consolidated profit not distributable to parent.

### 14. Tax And Deferred Tax Anomaly

Core suspicion: accounting profit differs from taxable profit due to estimates, provisions, fair-value, capitalization, internal transactions.

Check:

- Effective tax rate.
- Cash tax paid.
- Deferred tax asset/liability sources.
- Tax incentives.
- Loss carryforwards.

Red flags:

- Effective tax rate very low without sustainable policy basis.
- DTA rises with weak profitability.
- Tax paid far below tax expense or vice versa for unclear reasons.

### 15. Segment And Geographic Anomaly

Core suspicion: opaque segment, overseas transactions, transfer pricing, channel stuffing.

Check:

- Segment revenue/margin/assets.
- Geographic revenue/margin.
- Overseas customers.
- Segment cash flow if available.

Red flags:

- High-margin growth comes from opaque segment/region.
- Overseas revenue spikes with weak cash collection.
- Segment assets rise before/without revenue.


# ========== 细则：references/risk-control-protocol.md ==========

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

## 7. External-Use Control

When the user asks for an external-ready or publishable report:

- remove casual language
- include source appendix
- include calculation appendix
- include limitation statement
- avoid legal conclusions without official findings
- cite official filing dates and sections wherever possible
- keep a validation log

Do not add a default “内部研究草稿” / “internal research draft” status mark on reports.
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

# ========== 细则：references/accounting-policy-change-protocol.md ==========

# Accounting Policy, Estimate, And Presentation-Change Protocol

Accounting policy changes, accounting estimate changes, reporting-standard updates, and financial-statement presentation reclassifications can create apparent anomalies that are not necessarily financial red flags. Always check comparability before treating ratio changes as risk signals.

## 1. Where To Look In Annual Reports

Search the annual report and notes for these sections or keywords:

- significant accounting policies
- changes in accounting policies
- changes in accounting estimates
- correction of prior-period errors
- first-time adoption of new accounting standards
- changes in presentation or reclassification
- restatement / retrospective adjustment
- comparative figures have been reclassified
- revenue recognition policy
- cost classification
- R&D capitalization / expensing
- government grants
- leases
- financial instruments
- impairment
- segment reporting
- cash-flow statement classification

For A-share reports, also search:

- `重要会计政策和会计估计`
- `会计政策变更`
- `会计估计变更`
- `前期差错更正`
- `追溯调整`
- `报表项目重分类`
- `列报调整`
- `新会计准则`
- `执行企业会计准则解释`

## 2. Change Types

Classify each change:

| Type | Meaning | Risk-control handling |
|---|---|---|
| Accounting policy change | Recognition/measurement rule changes, often due to new standards or voluntary policy choice | Identify retrospective vs prospective treatment and quantify impact |
| Accounting estimate change | Useful lives, impairment assumptions, bad-debt ratios, warranty provisions, fair value assumptions | Treat as potential earnings-management channel if profit impact is material |
| Presentation/reclassification change | Expense or asset/liability item moved between line items | Do not compare affected line items without bridge adjustment |
| Prior-period error correction | Correction of mistakes in earlier filings | Higher credibility risk; inspect amount, cause, affected periods, auditor/regulator context |
| Business-model or segment change | Operating structure changes that alter reporting segments or expense allocation | Rebuild comparable segments before trend analysis |

## 3. Common Reclassification Patterns

These can create false red flags if not adjusted:

- selling expenses moved to cost of revenue or fulfillment cost, affecting gross margin and selling expense ratio.
- R&D expense moved between expense line, development expenditure, intangible assets, or cost of revenue.
- logistics, platform fees, warranty, after-sales, packaging, or freight reclassified between cost, selling expense, and administrative expense.
- impairment losses moved between asset impairment loss, credit impairment loss, fair-value changes, or nonrecurring items.
- government grants moved between other income, non-operating income, and deferred income amortization.
- lease-standard adoption moves rent expense into depreciation and interest expense.
- financial assets reclassified between trading financial assets, other debt investments, other equity instrument investments, and long-term equity investments.
- contract assets/liabilities introduced or reclassified after revenue-standard changes.
- cash-flow items reclassified between operating, investing, and financing activities.

## 4. Required Comparability Bridge

For any material change, create a bridge before scoring:

| Period | Original line item | Reclassified line item | Amount | Direction | Source note | Adjusted comparable value |
|---|---|---|---:|---|---|---:|
|  |  |  |  |  |  |  |

Bridge rules:

1. If the company provides restated comparative data, use restated data for trend analysis and state that clearly.
2. If the company only discloses qualitative changes without amounts, mark affected ratios as `not comparable` or `requires verification`.
3. If a metric changes mainly because of reclassification, do not treat it as a red flag by itself.
4. If reclassification improves key optics without persuasive business or standard-change reason, create an issue card under accounting policy/estimate quality.
5. If multiple line items are affected, check the net effect on operating profit, net profit, OCF, EBITDA-like metrics, and key covenants.

## 5. Red-Flag Patterns In Policy Or Presentation Changes

Escalate when:

- policy/estimate changes repeatedly increase profit or equity.
- useful lives are extended while assets are aging or utilization is weak.
- bad-debt, inventory, warranty, or impairment assumptions become looser while risk indicators worsen.
- R&D capitalization rises sharply without matching product/commercial evidence.
- expenses are moved below operating profit or into capitalized assets.
- presentation changes make gross margin, selling expense ratio, administrative expense ratio, or OCF appear better without changing economics.
- prior-period error corrections recur or affect core accounts.
- management explanation is vague, boilerplate, or not quantified despite material impact.

## 6. Reporting Rules

When a change exists, the report must include:

- what changed
- why it changed according to management
- whether it is required by accounting standards or voluntarily chosen
- whether retrospective adjustment was made
- which line items and periods are affected
- quantified impact on revenue, gross profit, operating profit, net profit, equity, OCF, and key ratios when available
- whether trend comparisons were adjusted, marked not comparable, or left unadjusted with caveat

Never conclude that a ratio deterioration or improvement is a financial red flag until the affected line items have passed this comparability check.

# ========== 细则：references/market-adapters.md ==========

# Market And Accounting Adapters

Use this before applying rule thresholds. The same ratio can mean different things under different markets, accounting standards, industries, and filing regimes.

## 1. Required Market Metadata

Always capture:

- Listing venue: A-share, Hong Kong, US, A+H, ADR, STAR/ChiNext, etc.
- Accounting standard: CAS, IFRS/HKFRS, US GAAP, or multiple reconciled standards.
- Audit standard and auditor.
- Fiscal year start/end; US companies may not use calendar year.
- Reporting currency and exchange-rate changes.
- Tax system and VAT/sales-tax treatment.
- Segment disclosure granularity.

## 2. A-Share / CAS Notes

- Quarterly reports are required, so Q4 revenue and quarter-to-quarter patterns can be checked.
- VAT affects cash received from sales, but benchmark must be tax-rate and business-model adjusted.
- Current PRC standards generally do not allow LIFO inventory costing; if LIFO appears, verify carefully.
- Development expenditure can be capitalized only when criteria are met; compare capitalization ratio with product pipeline.
- Long-term asset impairment is generally not reversed after recognition; receivables/inventory have different impairment mechanics.
- Parent-company statements are especially useful for group strategy and funding relationships.
- Watch related-party funds, controller pledges, guarantees, entrusted finance, bank acceptance notes, and restricted cash.

## 3. Hong Kong / HKFRS-IFRS Notes

- Interim and annual reports are required; quarterly data is often absent. Do not penalize missing quarterly patterns by default.
- HKFRS is largely IFRS-based. Confirm if the issuer uses HKFRS, IFRS, CAS, or US GAAP.
- No mainland VAT-style gross-up in revenue/cash comparisons. Use sales-cash/revenue around 1.0 only as a rough starting point.
- Notes may be less granular than A-share annual reports; mark “unavailable” separately from “red flag”.
- IFRS prohibits LIFO.
- Impairment reversal may be allowed for some assets but not goodwill; identify asset class.
- Fair-value disclosures, especially Level 3 assets, deserve attention.
- For A+H companies, reconcile CAS and HKFRS/HKFRS differences before concluding.

## 4. US / US GAAP Notes

- Annual report is 10-K, quarterly report is 10-Q. Fiscal year may not end on December 31.
- Revenue recognition follows ASC 606; identify performance obligations, variable consideration, principal-agent, contract assets/liabilities.
- R&D is generally expensed under US GAAP, so R&D-heavy technology/biotech companies have lower accounting profits and high expense ratios by design.
- LIFO is permitted under US GAAP. If used, inventory and gross margin are not directly comparable to IFRS/CAS peers without adjustment.
- Interest paid/received classification can differ from IFRS/CAS presentations; adjust operating cash-flow comparisons when possible.
- Goodwill impairment is not reversed after recognition.
- Stock-based compensation can materially affect GAAP profit and cash-flow reconciliation.
- For Chinese ADRs, check VIE structure, PCAOB/HFCAA issues, SEC comment letters, short-seller reports, class actions, related-party VIE transactions, and auditor access.

## 5. Cross-Market Comparison Rules

1. Never compare margins, OCF ratios, inventory turnover, R&D ratios, or impairment behavior across markets before checking accounting standard.
2. Convert currency and align fiscal periods.
3. Prefer same-market peers; if unavailable, add a comparability caveat.
4. Use ranges, not point thresholds, when accounting standards differ.
5. When data is unavailable because of disclosure regime, mark the affected evidence status and disclosure limitation rather than automatically deducting.

## 6. Industry Overrides

These industries need tailored thresholds:

- Banks/insurers/brokers: do not use industrial-company receivable/inventory/OCF rules.
- Real estate: inventory, advances, pre-sales, restricted cash, debt maturity, and project geography dominate.
- Construction/EPC/software implementation: contract assets, project progress, and revenue-over-time estimates dominate.
- SaaS/platform: deferred revenue, net retention, SBC, capitalization, and cash burn dominate.
- Biotech: R&D expense/capitalization, milestone payments, cash runway, and pipeline impairment dominate.
- Utilities/infrastructure: capex cycle, regulated return, debt maturity, and maintenance vs expansion capex dominate.
- Retail/consumer: inventory aging, channel stuffing, rebates, franchise/dealer receivables, and same-store data dominate.

# ========== 细则：references/report-template.md ==========

# 财报排雷报告模板

## 0. Visual Presentation Standards

Use a formal, investment-research style. The report should look like a professional due-diligence memo, not a casual note.

Layout:

- Use a clean cover page with company name, ticker, reporting period, total score, rating, source basis, and final judgment.
- Use a one-page executive dashboard immediately after the cover.
- Keep section numbering stable.
- Use short paragraphs, dense tables, and clear issue cards.
- Avoid decorative visuals, oversized hero sections, gradients, emoji, or casual language.
- Every chart must have title, unit, period, data source, and short interpretation.

Visual system:

- Primary text: charcoal / near-black.
- Background: white or very light neutral.
- Accent colors:
  - Green: strong/healthy.
  - Amber: watchlist/moderate risk.
  - Red: high risk.
  - Blue-gray: neutral data and headers.
- Use the same colors consistently across scorecards, red-flag tables, and charts.
- Use severity badges: P0 Critical, P1 High, P2 Medium, P3 Low.
- Use rating badges: A/B/C/D/E.

Required charts:

- 5-10 year trend charts for revenue, gross margin, net profit, OCF, FCF, total debt, monetary funds, receivables, inventory, goodwill when data is available.
- Waterfall or bridge chart for net profit to operating cash flow.
- Stacked or grouped bars for asset structure and liability structure.
- Heatmap for 15-domain scorecard.
- Red-flag matrix showing severity vs evidence status.
- Parent vs consolidated comparison table when parent statements are available.

Table standards:

- Put the conclusion column first when possible.
- Highlight only the cells that matter; do not color entire tables heavily.
- Always show formula/definition for non-obvious ratios.
- Use consistent decimal places within the same table.
- Mark unavailable data as `N/A`, not zero.

## 1. Cover Page

- Company:
- Ticker:
- Listing venue:
- Report period:
- Report date:
- Total score:
- Rating:
- Source basis:
- Final judgment:
- Analyst note:

## 2. One-Page Executive Dashboard

- Company:
- Period analyzed:
- Total score:
- Rating:
- Source basis:
- Market/accounting adapter:
- Hard gates triggered:
- Fast red-flag rules triggered:
- Overall judgment: 可继续研究 / 需重大折价审查 / 原则排除 / 信息不足无法判断
- Top 5 red flags:
- Top 5 follow-up verification steps:

## 3. Evidence Coverage

- Reports used:
- Missing reports/data:
- Structured-data sources used:
- Consolidated statements extracted:
- Parent statements extracted:
- Notes extracted:
- Peer set:
- Nonfinancial KPI coverage:
- Market/accounting caveats:

## 4. Data Validation And Risk-Control Log

Source hierarchy:

- Primary official filings:
- Structured data cross-check:
- External corroboration:
- Conflicting sources:
- Unresolved evidence gaps:

Core data reconciliation:

| Item | Official filing value | Cross-check value | Difference | Resolution | Evidence status |
|---|---:|---:|---:|---|---|
| Revenue |  |  |  |  |  |
| Net profit attributable to parent |  |  |  |  |  |
| Operating cash flow |  |  |  |  |  |
| Monetary funds |  |  |  |  |  |
| Interest-bearing debt |  |  |  |  |  |
| Receivables / contract assets |  |  |  |  |  |
| Inventory |  |  |  |  |  |
| Goodwill |  |  |  |  |  |

Accounting comparability and reclassification check:

| Change disclosed | Affected line items | Periods affected | Quantified impact | Adjustment treatment | Evidence status |
|---|---|---|---:|---|---|
|  |  |  |  | adjusted / not comparable / caveat only |  |

Severe-conclusion review:

- Any P0 issue:
- Rating D/E:
- Final judgment `原则排除`:
- Red-team review completed:
- Language risk checked:
- Remaining caveats:

## 5. Business Map

- Main products/services:
- Revenue model:
- Customers/channels:
- Suppliers/cost drivers:
- Capacity/volume/price KPIs:
- Industry cycle and competitive position:

## 6. Market And Accounting Adapter

- Listing venue:
- Accounting standard:
- Audit standard:
- Fiscal year:
- Revenue tax/VAT treatment:
- Inventory costing:
- R&D treatment:
- Impairment reversal rules:
- Cash-flow classification caveats:
- Data limitations:

## 7. Accounting Policy, Estimate, And Presentation Changes

- Accounting policy changes:
- Accounting estimate changes:
- New accounting-standard adoption:
- Prior-period error corrections:
- Presentation/reclassification changes:
- Restated comparative data:
- Impact on trend comparability:
- Metrics marked not comparable:
- Metrics adjusted before scoring:

## 8. Fast Red-Flag Rule Results

| Rule | Status | Evidence class | Evidence | Priority | Linked issue card |
|---|---|---|---|---|---|
| T001 |  |  |  |  |  |

## 9. Financial Quality Scorecard

| Domain | Score | Max | Main deductions |
|---|---:|---:|---|
| Audit, disclosure, and reporting credibility |  | 8 |  |
| Accounting policy and estimate quality |  | 6 |  |
| Business-financial consistency |  | 7 |  |
| Parent vs consolidated report and group structure |  | 6 |  |
| Cash and financial assets quality |  | 7 |  |
| Revenue authenticity and receivables/contract assets |  | 9 |  |
| Inventory, cost, and gross margin quality |  | 8 |  |
| Long-term operating assets and capex effectiveness |  | 7 |  |
| Goodwill, M&A, and long-term investments |  | 6 |  |
| Profit structure and recurring earnings quality |  | 8 |  |
| Cash-flow quality and free-cash-flow resilience |  | 9 |  |
| Debt, liquidity, and financing dependence |  | 7 |  |
| Working-capital and operating efficiency |  | 6 |  |
| Governance, related parties, pledges, guarantees, litigation |  | 6 |  |
| Earnings-management and fraud-pattern risk |  | 7 |  |

## 10. Three-Statement Diagnostics

- Balance sheet: key changes and asset risk.
- Income statement: core profit and profit structure.
- Cash flow: OCF, investing cash flow, financing cash flow.
- Reconciliation gaps:

## 11. Key Account Deep Dives

- Monetary funds and financial assets:
- Receivables, contract assets, and revenue collection:
- Inventory, cost, and gross margin:
- Fixed assets, construction in progress, and capex:
- Goodwill, M&A, and long-term investments:
- Debt, liquidity, and restricted assets:
- Related parties, guarantees, pledges, and litigation:

## 12. Parent-Consolidated Analysis

- Parent strategy type: operating-led / investment-led / mixed.
- Main parent-consolidated differences:
- Subsidiary growth drivers:
- Minority interest/profit issues:

## 13. Red-Flag Issue Cards

Create one subsection per P0/P1/P2 issue using `red-flag-playbook.md`.

Each issue card must distinguish:

- Confirmed facts:
- Calculated facts:
- Interpretations:
- Open questions:
- Evidence limitations:
- Language risk:

## 14. Fraud And Earnings-Management Risk

- Fraud triangle pressure:
- Opportunity:
- Rationalization/context:
- Fraud-equation trace:
- Legal earnings-management signals:
- Deferred tax diagnostic:

## 15. Verification Plan

- Public data checks:
- Announcement/regulatory inquiry checks:
- Peer checks:
- Channel/customer/supplier checks:
- Questions for management:
- Issues that require non-public diligence:

## 16. Final Judgment

- What is solid:
- What is questionable:
- What cannot be resolved with public data:
- Which conclusions are only risk signals:
- Which conclusions are officially confirmed:
- Recommended next step:

# ========== 细则：references/long-form-report-standard.md ==========

# Long-Form 财报排雷 Report Standard

This reference is mandatory for polished listed-company 财报排雷 reports. It prevents under-delivery as a short dashboard memo.

## 1. Target Output

The report's key properties:

- Long-form reader-facing diagnosis, not a KPI dashboard.
- Conclusion-first writing.
- Official-disclosure basis.
- Beginner-friendly scoring explanation.
- Strong distinction between risk signals and legal/fraud conclusions.
- Evidence-driven issue cards.
- Account-by-account decomposition is required. The report must not only say “资产质量承压” or “现金流不错”; it must drill into specific accounts and notes such as 货币资金、受限资金、有息负债、应收账款、应收款项融资、其他应收款、预付款项、存货、固定资产、在建工程、使用权资产、商誉、无形资产、开发支出、非经常性损益、投资收益、公允价值变动、资产/信用减值、经营性应收应付调整.
- The account layer must be integrated with the global thesis. Do not deliver a thin "account-card only" version. The report should first give the reader a full-company judgment, then use account subjects as the evidence path that proves or weakens that judgment.
- The preferred public-facing logic is: feedback/pain point -> why a superficial format change is not enough -> concrete upgraded modules -> how to use/read it -> boundary: filter and verification, not valuation or recommendation.
- A polished HTML report with responsive layout, print-friendly CSS, readable tables/cards, and neutral footer metadata.
- PDF is optional and should be generated from the HTML only when a print/archive copy is requested.
- Reproducible generation script archived in `03_底稿与校验/`.

## 2. Required Markdown Structure

The final Markdown should normally contain these sections in this order:

1. 核心结论
2. 最重要的五个判断
3. 财务质量评分
   - 新手版评分说明
   - 维度评分表
4. 科目排雷总览
5. 全局主线：生意、三表和资产负债表压力如何连起来
6. 资产负债表科目拆解
   - 货币资金与受限资金
   - 有息负债、租赁负债与受限资产
   - 应收账款、票据、应收款项融资、合同资产
   - 存货、跌价准备、库存商品
   - 固定资产、在建工程、使用权资产、资本开支
   - 商誉、无形资产、开发支出、长期股权投资
   - 其他应收款、预付款项、其他流动/非流动资产
7. 利润表科目拆解
   - 收入、成本、毛利率
   - 销售/管理/研发/财务费用
   - 投资收益、公允价值变动、其他收益
   - 信用减值、资产减值、非经常性损益、所得税
8. 现金流量表科目拆解
   - 销售收现、经营现金流、经营性应收应付调整
   - 资本开支、并购现金流、筹资现金流、分红
9. 母公司与合并报表科目差异
10. 治理、关联方和外部风险
11. 核心问题卡
12. 三表综合判断
13. 最终判断
14. 规则触发清单
15. 后续跟踪清单
16. 15 维评分底稿
17. 本次最该避免的误判
18. 附录 A：来源与方法说明

Do not collapse these into a one-page dashboard. If the company has fewer issues, keep the sections concise but present.

## 3. Writing Standard

Write for an intelligent non-specialist investor/research reader:

- Explain what a ratio means before using it as a judgment.
- Use a two-level narrative: `全局判断 -> 三表主线 -> 科目证据 -> 问题卡 -> 后续验证`.
- Prefer “科目 -> 数字 -> 为什么重要 -> 可能解释 -> 下一步验证” over long paragraphs, but never remove the overall business/financial thesis.
- Use "不是 X，而是 Y" sparingly but clearly to prevent common misreadings.
- Prefer concrete numbers and business mechanisms over abstract risk labels.
- State when a risk is industry-normal but still relevant.
- Do not say or imply fraud unless an official source has made that finding.
- Use language such as `风险信号`, `需要验证`, `不构成硬红灯`, `当前无法由公开资料完全解决`.

Every important issue must pass four tests:

1. Business explanation: can the operating model explain it?
2. Accounting explanation: can accounting policy/estimate/classification explain it?
3. Cash-flow test: did cash support or contradict it?
4. Asset-side trace: where did the story land on the balance sheet?

## 4. Visual/HTML Standard

The HTML should be a formal research-style long-form report, with a first viewport that clearly communicates score, rating, hard red-light state, highest-priority issues, and the core conclusion.

Required front matter:

- Cover title and company code.
- Author/organization: default `kwbk`; override only if the user provides a different name.
- Approximate word count and estimated reading time.
- KPI cards for score, source basis, hard red lights, highest risk.
- A concise executive callout.

Required visuals/tables:

- Annual core metric trend chart.
- Risk-priority matrix.
- Scorecard table.
- Scoring bar chart or similar dimension-level visualization.
- Issue-card tables.
- Rule-trigger checklist.
- Follow-up tracking table.
- Common-misreading table.

Footer:

- Add subtle visible author/organization mark; default `kwbk` unless the user overrides.
- Add report date/source basis and limitation statement.
- Print styles should preserve the report hierarchy if the user later prints to PDF.

## 5. Quality Gate

Before final delivery, verify:

- Markdown length and structure match the long-form standard.
- HTML is not dashboard-only and has long-form narrative sections, issue cards, scoring notes, and appendices.
- Chinese text renders correctly.
- Tables do not overflow.
- Highlight colors are visible but restrained.
- No unsupported legal/fraud accusation appears.
- Official filing values reconcile with structured data for core metrics.
- Generation script and validation/source files are archived.
- HTML is opened in a browser and visually inspected at desktop width; mobile overflow is checked when practical.

If the first output is too short, regenerate instead of delivering it.

# ========== 细则：references/html-export-standards.md ==========

# HTML Export Standards For 财报排雷

Use this reference when the user asks for HTML, webpage, better layout than Word, social-content reuse, or a more polished reader-facing version of a 财报排雷 report.

## 1. Purpose

HTML is not a decorative export and should not depend on an existing Word/PDF report. Generate it from the same evidence pack, calculations, scorecard, and issue-card structure used by the main analysis. It is the most readable surface for a red-flag report because it can show:

- conclusion-first hierarchy;
- score, rating, hard red-light state, and highest-priority issues in the first viewport;
- global story line before account detail, so the reader knows what the accounts are proving;
- issue cards with evidence, explanation tests, and follow-up checks;
- source appendix and calculation notes;
- reusable sections for screenshots, PDF export, and Xiaohongshu card extraction.

Keep Markdown as the editable source and HTML as the primary reader-facing report. Generate PDF only when the user explicitly asks for a print/archive version or when a downstream workflow requires it. The workflow must work from scratch when the only inputs are company identity and official filings.

## 2. Default Deliverable Set

Default deliverables:

- `report.md`: editable source report.
- `report.html`: polished reader-facing HTML report.
- `report.pdf`: optional print/archive version, generated from the HTML only when requested or needed.
- `source_index.md`: source and filing index.
- `validation_log.md`: calculation and reconciliation notes, when created.

If an archive is requested, place HTML, Markdown, PDF if generated, source index, validation log, filings, and workpapers under the user's specified output folder. Do not assume a fixed local path.

## 3. Required HTML Structure

Use these sections in order:

1. Hero / cover:
   - company name and ticker;
   - report status;
   - score and rating;
   - hard red-light state;
   - one-sentence conclusion;
   - visible disclaimer: `仅供学习研究，不构成投资建议。`
2. KPI strip:
   - financial-quality score;
   - source basis;
   - hard gates;
   - highest priority risk;
   - evidence state.
3. Executive summary:
   - 3-5 concise judgments.
4. Reading logic / storyline:
   - what feedback or analytical problem this report solves;
   - why this is not a superficial Word-to-HTML conversion;
   - how to read the report from global judgment to account evidence;
   - boundary: filter and verification, not valuation or recommendation.
5. Risk map:
   - P0/P1/P2 matrix;
   - risk signal wording only, no unsupported fraud/legal accusation.
6. Three-statement check:
   - profit statement;
   - balance sheet;
   - cash-flow statement;
   - explain what confirms and what contradicts.
7. Account-level red-flag map:
   - group accounts by balance sheet, income statement, and cash-flow statement;
   - highlight cash, debt, receivables, inventory, goodwill/M&A, fixed assets/capex, other receivables/prepayments, profit-quality items, and operating cash-flow adjustments;
   - each account should have amount/trend, risk question, current judgment, and next verification.
8. Issue/account cards:
   - one card per major issue;
   - each card must contain trigger evidence, business explanation test, accounting explanation test, cash-flow test, asset-side trace, and follow-up verification.
9. Scorecard:
   - 15-domain scoring table or bar visualization.
10. Follow-up checklist:
   - next annual/interim report items to verify.
11. Source and method appendix:
   - official filings;
   - structured data sources, if used;
   - calculation formulas;
   - unresolved data conflicts.

## 4. Visual Direction

Use this visual direction unless the user provides a brand system:

- electronic magazine x e-ink;
- warm paper background;
- dark ink text;
- restrained red/amber/green risk colors;
- serif display headings and sans-serif body;
- monospace metadata;
- visible but subtle footer with author/organization (default `kwbk`, or user override).

Avoid:

- stock dashboard gradients;
- finance influencer colors that imply recommendation;
- huge green/red price-action styling;
- decorative visuals that hide source/evidence hierarchy.

## 5. Compliance Language

Every HTML report must contain the following boundary near the top and bottom:

```text
仅供学习研究，不构成投资建议。
```

Do not use:

- `买入`, `卖出`, `持有`, `目标价`, `荐股`, `黑马`, `稳赚`, `低风险`, `收益翻倍`;
- unverified accusations such as `造假`, `舞弊`, `资金侵占`, unless an official source has made that finding.

Preferred language:

- `风险信号`;
- `需要进一步验证`;
- `当前无法由公开资料完全解决`;
- `不构成硬红灯`;
- `可继续研究，但需要先验证...`.

## 6. Technical Requirements

- The HTML must be standalone or have all assets copied into the same report folder.
- It must render locally without a dev server.
- Use responsive CSS; desktop width should be comfortable around 1100-1200px.
- Text must not overlap at mobile or desktop sizes.
- Tables should scroll horizontally or reflow on narrow screens.
- Include print styles or ensure browser Print to PDF is readable.
- Visually inspect the HTML in a browser before final delivery.
- When updating an existing PDF-era report, do not merely embed screenshots or paste the PDF. Rebuild the report as native HTML sections, tables, score bars, issue cards, and appendix blocks.
- Prefer account-card layout over essay paragraphs, but do not make the whole report a thin card set. A good report should let the reader first understand the full-company thesis, then jump directly to “存货 / 应收 / 商誉 / 货币资金 / 有息债务 / 现金流” and understand the issue without rereading a long narrative.

## 7. Suggested File Names

Use consistent names:

```text
<公司名>_<证券代码>_财报排雷报告.md
<公司名>_<证券代码>_财报排雷报告.html
<公司名>_<证券代码>_财报排雷报告.pdf
```

For social-content demos or style prototypes, use:

```text
财报排雷Skill_HTML报告模板DEMO.html
```

## 8. Demo And Templates

If the user provides a demo HTML, brand template, or prior report, use it as a style reference only. Do not treat sample numbers as final company evidence.

# ========== 细则：references/pdf-export-standards.md ==========

# PDF Export And Final Delivery Standards

Default deliverable for this financial red-flag workflow is a polished standalone HTML report. Use PDF as an optional print/archive version when the user requests it or a downstream workflow requires it. Keep the Markdown source and validation artifacts.

## 1. One-Shot Delivery Rule

When the user asks to run the workflow on a listed company and requests PDF output, complete the full chain without asking for intermediate confirmation:

1. identify the listed entity
2. collect official filings and structured-data supplements
3. validate data and accounting comparability
4. run red-flag rules and scorecard
5. write the report
6. render the final PDF from the HTML or Markdown source
7. visually inspect the PDF
8. deliver the PDF, source report, and concise summary

Stop only when:

- official filings cannot be obtained after reasonable attempts
- structured-data access requires unavailable login/credentials and the result materially affects the report
- core numbers conflict and cannot be resolved safely
- the user asks for an external-publication version that requires explicit legal/reputational review
- the user explicitly asks to pause or preview before final generation

## 2. Output Folder Convention

For workspace runs, write outputs under the user's specified output root, or a project-local folder such as `output/financial-red-flag/<company>_<ticker>/`.

Recommended files:

- `<company>_财报排雷报告.md`
- `<company>_财报排雷报告.html`
- `<company>_财报排雷报告.pdf` if requested
- `data_validation_log.csv` or `.md`
- `source_index.md`
- optional chart images under `charts/`

Recommended archive structure when the user requests an archive:

- `01_final_report/`: final HTML, Markdown, and PDF if generated
- `02_official_filings/`: annual reports, interim reports, announcement PDFs, and official-source mirrors
- `03_workpapers_validation/`: source index, validation log, extraction notes, and reproducibility script

## 3. PDF Visual Standard

Use a formal investment-research style:

- clean cover page with a sober masthead, thin rules, and clear report metadata
- cover metadata should include author, approximate word count, and estimated reading time
- executive dashboard with four to six KPI cards
- key conclusions emphasized through restrained bold/color treatment
- explicit visual language: green for positive evidence, red for core risk, amber for cautious judgment
- professional callout boxes for final conclusion and score interpretation
- stable section numbering
- section headers with consistent hierarchy and spacing
- restrained colors
- readable tables with light borders, alternating row fills, and risk-priority badges when applicable
- page numbers
- subtle author/organization mark (default `kwbk`, or user override)
- source notes
- chart title, unit, period, source, and short interpretation

Avoid:

- casual design
- decorative graphics
- heavy gradients
- cramped tables
- clipped text
- inconsistent fonts
- unsupported accusation wording

## 4. Rendering Requirements

Use the most reliable local path available:

1. If a polished HTML-to-PDF route is available, render Markdown/HTML to PDF and inspect pages.
2. If not, use Python `reportlab` to generate the PDF directly.
3. If PDF rendering dependencies are missing, install local Python packages when allowed; otherwise explain the missing dependency and still provide the Markdown final report.

After export:

- render or inspect representative pages
- verify Chinese text renders correctly
- verify tables do not overflow
- verify badges, charts, and section headers align
- verify source links/notes are readable
- verify final judgment and limitation statement appear near the front

## 5. Final Response

Final response should include:

- PDF file link/path
- Markdown source link/path
- total score, rating, source basis
- top 3 risk signals
- uncompleted checks, if any

Do not paste the whole report into chat unless the user explicitly asks.
