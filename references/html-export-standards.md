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
