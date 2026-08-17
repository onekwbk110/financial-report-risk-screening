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
