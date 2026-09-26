---
name: report-quality-check
description: Performs numerical, account-completeness, readability, and visual QA on financial PDF reports
compatibility: opencode
---

# Financial Report QA

Do not consider the report finished until it passes all checks.

## Account completeness

Verify:

eligible Wallet accounts == accounts represented in report

Check by stable account identifier where possible.

## Wallet safety

Confirm that the workflow performed no Wallet mutations.

## Numerical checks

Verify:

- KPI values
- chart totals
- account totals
- income totals
- expense totals
- net cash flow
- net worth

Look for double-counted transfers.

## Visual checks

Inspect every PDF page.

Look for:

- clipping
- overflow
- tiny text
- unreadable charts
- broken tables
- overlapping elements
- inconsistent spacing
- inconsistent typography
- poor page breaks
- truncated account names
- misleading colors
- insufficient contrast

## Readability

Ask:

Can someone understand the financial position quickly?

Can someone find any individual account?

Can someone understand major trends without reading every table?

Can someone read the PDF comfortably on a normal screen?

If not, revise the PDF.

## Final acceptance

The report is complete only when:

- all eligible accounts are represented
- deleted/archived accounts are omitted
- Wallet remained read-only
- calculations reconcile
- charts are accurate
- PDF pages are readable
- visual design is consistent