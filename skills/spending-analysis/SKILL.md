---

name: spending-analysis
description: Analyze Wallet transactions to understand spending by category, merchant, account, period, and trend.
compatibility: opencode
-----------------------

# Spending Analysis

Analyze actual Wallet spending for the requested period.

## Core Metrics

Calculate when supported:

* Total spending
* Average monthly spending
* Average transaction amount
* Spending by category
* Spending by merchant/counterparty
* Spending by account
* Spending by month
* Spending by currency
* Recurring spending
* Largest transactions

## Categories

Identify:

* Highest-spending categories
* Category percentage of total spending
* Category changes over time
* Categories with significant increases
* Categories with significant decreases

Do not assume a category is good or bad.

## Merchants

When merchant/counterparty information is available, identify:

* Top merchants
* Largest merchant increases
* Recurring merchants
* High-value merchants

Group clearly related transactions when the data supports it.

Do not incorrectly merge unrelated merchants.

## Time Trends

Analyze spending across the requested period.

Useful comparisons include:

* Month over month
* Quarter over quarter
* Year over year
* First vs last month
* Period averages

Prefer sustained patterns over isolated changes.

## Large Transactions

Identify unusually large transactions relative to the user's historical spending.

Do not call a transaction suspicious merely because it is large.

Use language such as:

> "This transaction is significantly larger than the user's typical transaction size."

## Recurring Spending

Identify recurring expenses when supported by:

* Similar merchant
* Similar amount
* Regular timing
* Repeated occurrence

Do not claim that an expense is a subscription unless the available data supports that interpretation.

## Exclusions

Exclude from spending calculations:

* Internal transfers
* Credit-card payments representing already-counted purchases
* Other non-spending records when clearly identifiable

## Reconciliation

Where possible:

`category totals = total spending`

and:

`monthly totals = period spending`

Investigate discrepancies before reporting totals.

## Currency

Keep different currencies separate unless a reliable conversion method is available.

Never present a combined spending total without clearly identifying the currency basis.
