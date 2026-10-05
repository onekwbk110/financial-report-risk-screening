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
- subtle author/organization mark only when the user provides one
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
