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

The HTML must use the **v1.0 蓝白仪表盘** chrome in `references/html-v1.0-layout.md`, matching `docs/preview-v1.0.png`. After that chrome, keep a long-form research report (risk map, three-statement synthesis, account cards, appendix). Do not ship cream/serif magazine pages.

Required front matter / first viewport:

- Cover title and company code in the top bar.
- Author/organization when provided by the user.
- Report status: `内部研究草稿`, `internal research draft`, or user-specified status.
- Four cards: 综合评分, 评级含义, 硬闸门触发, 结论建议.
- Yellow 关键风险摘要 banner.
- 15-domain score table with blue header and A–E pills.

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

- Add subtle visible author/organization mark only when provided.
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
