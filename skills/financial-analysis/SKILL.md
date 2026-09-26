---
name: financial-analysis
description: Analyzes complete Wallet financial records, reconciles balances, and derives accurate financial metrics
compatibility: opencode
---

# Financial Analysis

Analyze the complete eligible Wallet dataset.

## Core metrics

Calculate when supported:

- total assets
- total liabilities
- net worth
- cash
- investments
- income
- expenses
- net cash flow
- savings rate

## Account analysis

For every eligible account calculate, where possible:

- latest balance
- beginning balance
- ending balance
- absolute change
- percentage change
- account type
- currency
- asset/liability classification

Never remove small accounts from calculations simply because they are small.

## Time analysis

Use monthly data where sufficient history exists.

Analyze:

- net worth trend
- income trend
- expense trend
- cash-flow trend
- debt trend
- investment trend

## Spending

Analyze:

- category totals
- category shares
- monthly spending
- recurring expenses
- major categories

## Reconciliation

Check that:

assets - liabilities = net worth

where the underlying data makes this relationship applicable.

Check that:

income - expenses = net cash flow

after appropriately excluding internal transfers and other non-income/non-expense movements.

## Multi-currency

Never silently combine currencies.

Keep currencies distinct unless a trustworthy conversion mechanism is available.

## Data limitations

Explicitly identify metrics that cannot be reliably calculated.

Never invent data.