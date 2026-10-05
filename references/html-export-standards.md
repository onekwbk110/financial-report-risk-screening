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

The first viewport must match the v1.0 dashboard in `docs/preview-v1.0.png` and `references/html-v1.0-layout.md`. Clone CSS from `docs/examples/北方导航_600435_财报排雷报告.html` or `references/html-v1.0-example.html`.

Use these sections in order:

1. Top bar + disclaimer:
   - company name and ticker;
   - report period / market;
   - visible disclaimer: `仅供学习研究，不构成投资建议。`
2. `一、核心结论` four-card row:
   - 综合评分;
   - 评级含义;
   - 硬闸门触发;
   - 结论建议（可继续研究 / 需重大折价审查 / 原则排除）.
3. Yellow `关键风险摘要` banner under the four cards.
4. `二、15维度评分卡`:
   - columns: 维度 / 满分 / 得分 / 评级 / 核心问题;
   - blue header; A–E grade pills.
5. `三、风险地图`:
   - P0/P1/P2 matrix;
   - risk signal wording only, no unsupported fraud/legal accusation.
6. `四、近五年主趋势与三表`:
   - trend table;
   - profit / balance sheet / cash-flow synthesis.
7. `五、科目证据卡`:
   - one card per major account/issue;
   - trigger evidence, business/accounting/cash-flow tests, next verification.
8. `六、硬闸门` table.
9. `七、后续跟踪清单`.
10. `八、触发句复现与来源` appendix.

Keep long-form sections after the first viewport. A four-card dashboard with no account cards or appendix fails the standard unless the user asks for a brief.

## 4. Visual Direction

Default visual system is **v1.0 蓝白仪表盘**, not magazine/e-ink. Unless the user provides another brand system:

- light blue-gray page `#f3f6fb`;
- white rounded cards and light shadow;
- navy section titles with a 5px `#3d7ee8` left bar;
- sans-serif body: PingFang SC / Microsoft YaHei / Noto Sans SC;
- blue table headers; A/B/C/D/E pills (green/blue/amber/orange/red);
- restrained P0/P1/P2 tags;
- footer with report date, source basis, and limitation statement; author mark only when provided.

Avoid:

- warm paper, cream e-ink, serif magazine covers;
- stock dashboard gradients and finance-influencer colors;
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

Style prototype / canonical example:

```text
docs/preview-v1.0.png
docs/examples/北方导航_600435_财报排雷报告.html
references/html-v1.0-layout.md
```

## 8. Demo And Templates

Treat `docs/preview-v1.0.png` and the 600435 example HTML as the **style** reference. Do not copy that company's scores or narrative into a new report. Clone the CSS and section chrome, then fill with the current company's evidence.
