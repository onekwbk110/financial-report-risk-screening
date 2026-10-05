# Contributing

Thanks for helping improve **financial-report-risk-screening**（财报排雷 Skill）.

This repo is a reusable agent skill: workflow instructions + reference methods. It is not a trading bot, valuation model, or legal accusation engine.

## What To Contribute

High-value contributions:

- market adapters (A-share / HK / US / A+H / ADR disclosure quirks)
- industry-specific red-flag rules and counter-examples
- issue-card playbooks
- HTML template / CSS readability fixes
- test prompts and reproducible sample outputs based on **public filings only**
- validation helpers, source-index templates, scoring edge-case notes
- docs typos, clearer trigger examples, bilingual wording fixes

Small PRs are welcome. A one-line fix or a clearer counter-example is useful.

## What Not To Contribute

Do **not** add:

- private / non-public filings, credentials, cookies, or vendor API keys
- proprietary paid-database dumps
- accusations of fraud / tunneling / misconduct as fact without official findings
- buy/sell recommendations, target prices, or “稳赚” language
- large binary PDFs of annual reports (link to exchange / cninfo / SEC instead)

## Example-Report Rules

If you contribute a sample report under `docs/examples/`:

1. Use only public official disclosures (annual report, interim report, exchange announcements).
2. Put the exact trigger prompt in `docs/examples/README.md` or the sample’s source index.
3. Include a `source_index.md` with filing titles, dates, and public URLs.
4. Keep HTML standalone and openable locally.
5. Keep the disclaimer visible near the top and bottom:

   `仅供学习研究，不构成投资建议。`

6. Prefer risk-signal language: “需要进一步验证”, “风险信号”, “当前无法由公开资料完全解决”.

## How To Propose A Change

1. Open an Issue first for rule changes or new market adapters (optional for typos).
2. Fork and create a branch.
3. Keep the PR focused: one rule cluster or one docs/example change per PR.
4. In the PR description, state:
   - what changed
   - which reference file / score domain it affects
   - how you validated it (trigger prompt, company, filing year)

## Local Layout Reminder

```text
financial-report-risk-screening/
  SKILL.md
  references/
  docs/examples/
  CONTRIBUTING.md
```

Keep `SKILL.md` concise. Put detailed methods in `references/`.

## Review Bar

Maintainers look for:

- official filings as highest authority
- clear separation of fact / calculation / interpretation / open question
- no unsupported severe conclusions
- reproducible public examples when claiming a workflow improvement

## License

By contributing, you agree your contribution is licensed under the MIT License.
