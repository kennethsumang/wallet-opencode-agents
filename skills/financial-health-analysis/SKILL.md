---

name: financial-health-analysis
description: Calculate and interpret core financial health metrics from complete Wallet data.
compatibility: opencode
-----------------------

# Financial Health Analysis

Analyze the user's overall financial position using retrieved Wallet data.

## Core Metrics

Calculate when supported by the available data:

* Total assets
* Total liabilities
* Net worth
* Cash and liquid balances
* Investment balances
* Debt balances
* Total income
* Total expenses
* Net cash flow
* Savings
* Savings rate

Use:

`Net worth = assets - liabilities`

`Net cash flow = income - expenses`

`Savings rate = savings / income`

Only calculate a metric when the underlying data supports it.

## Time Analysis

When a date range is provided:

* Respect the requested period.
* Compare appropriate periods when useful.
* Identify meaningful increases and decreases.
* Look for sustained trends rather than isolated changes.

Useful comparisons include:

* Month over month
* Quarter over quarter
* Year over year
* Beginning vs ending position

## Financial Position

Assess:

* Asset composition
* Liability composition
* Cash position
* Debt position
* Investment position
* Changes in net worth

Do not judge the user's finances using arbitrary thresholds unless the user specifically provides them.

## Cash Flow

Analyze:

* Income
* Expenses
* Net cash flow
* Major spending areas
* Major income sources
* Changes over time

Exclude internal transfers from income and expenses.

## Reconciliation

Where possible, reconcile:

* Account balances
* Asset totals
* Liability totals
* Income
* Expenses
* Net cash flow

If values cannot be reconciled because of missing data, state the limitation.

## Multiple Currencies

Keep currencies separate unless a reliable conversion basis is available.

Never present an aggregate total across incompatible currencies without clearly stating the conversion methodology.
