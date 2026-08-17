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
