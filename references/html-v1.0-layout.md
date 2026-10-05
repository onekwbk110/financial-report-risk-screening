# HTML v1.0 Layout Contract

Canonical visual system for every 财报排雷 HTML report. Agents must follow this file and clone the live example, not invent a new look.

## Canonical references

| Artifact | Path | Role |
|---|---|---|
| Screenshot | `docs/preview-v1.0.png` | First-viewport look: 核心结论四宫格 + 黄条摘要 + 15 维蓝表头 |
| Live example | `docs/examples/北方导航_600435_财报排雷报告.html` | Copy CSS, section titles, cards, table, badges |
| Bundled clone | `references/html-v1.0-example.html` | Same file, for skill folders that do not ship `docs/` |
| This spec | `references/html-v1.0-layout.md` | Tokens and required blocks |

Do **not** use: warm paper, e-ink, electronic-magazine serif covers, dark ink-on-cream pages, Source Serif / Songti display headings, or stock-trading green/red dashboards.

## First viewport (must match preview-v1.0.png)

1. Slim top bar: company name · ticker · market · period.
2. Disclaimer: `仅供学习研究，不构成投资建议。`
3. `一、核心结论` with a 5px blue left bar on the title.
4. Four equal white cards:
   - 综合评分（大号分数 + 字母级 + 一句话质量含义）
   - 评级含义（A–E 及解释）
   - 硬闸门触发（项数；0 项用绿色，≥1 项用红色）
   - 结论建议（可继续研究 / 需重大折价审查 / 原则排除）
5. Yellow `关键风险摘要` banner under the four cards.
6. `二、15维度评分卡`: table columns `维度 | 满分 | 得分 | 评级 | 核心问题`. Blue header row. Per-row letter grade pills.

Then continue as long-form (not a one-page memo): 风险地图、趋势/三表、科目证据卡、硬闸门表、跟踪清单、来源附录.

## Tokens

```text
background:    #f3f6fb
card:          #ffffff
ink:           #1f2937
muted:         #6b7280
line:          #e5eaf2
blue header:   #3d7ee8
navy title:    #1e3a5f
alert bg:      #fff7e6
alert text:    #92400e
shadow:        0 8px 24px rgba(31, 58, 99, 0.06)
radius:        14px cards, 12px alert
font:          "PingFang SC", "Microsoft YaHei", "Noto Sans SC", sans-serif
max-width:     1180px
```

Grade pills (white text, 4px radius):

| Grade | Background |
|---|---|
| A | `#22c55e` |
| B | `#3b82f6` |
| C | `#f59e0b` |
| D | `#f97316` |
| E | `#ef4444` |

Map domain score / max:

- ≥ 0.85 → A
- ≥ 0.70 → B
- ≥ 0.55 → C
- ≥ 0.40 → D
- else → E

Risk tags: P0/P1 rose, P2 amber, 通过/未触发 green, 观察 indigo.

## Required CSS skeleton

Copy structure from the 600435 example. Minimum CSS:

```css
body { font-family: "PingFang SC", "Microsoft YaHei", "Noto Sans SC", sans-serif; background: #f3f6fb; color: #1f2937; }
.section-title { display: flex; align-items: center; gap: 10px; color: #1e3a5f; font-size: 20px; font-weight: 700; }
.section-title::before { content: ""; width: 5px; height: 22px; border-radius: 3px; background: #3d7ee8; }
.cards-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; }
.kpi { background: #fff; border-radius: 14px; box-shadow: 0 8px 24px rgba(31,58,99,.06); padding: 18px; }
.score-table thead th { background: #3d7ee8; color: #fff; }
.alert { background: #fff7e6; border: 1px solid #fde68a; border-radius: 12px; color: #92400e; }
```

On narrow screens, collapse `.cards-4` to 1–2 columns. Tables must scroll horizontally.

## QA against the template

Before delivery, open the HTML in a browser and confirm:

- First screen looks like `docs/preview-v1.0.png` (blue bar titles, four cards, yellow banner, blue table header).
- Not the cream/serif magazine layout.
- Score, rating, hard-gate count, and conclusion in the four cards match the Markdown source.
- Disclaimer at top and bottom.
