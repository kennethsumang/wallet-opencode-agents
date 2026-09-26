---
name: wallet-readonly
description: Safely retrieve and analyze Wallet MCP data without ever mutating Wallet records
compatibility: opencode
---

# Wallet Read-Only Protocol

This skill governs ALL interaction with Wallet MCP for financial reporting.

## Absolute rule

Wallet is READ-ONLY.

Never perform any write operation.

Never:

- create records
- edit records
- delete records
- archive accounts
- unarchive accounts
- rename accounts
- modify categories
- modify transactions
- create transfers
- change balances

Use only read/query operations.

## Account enumeration

First retrieve the complete account inventory.

Do not assume the first response contains every account.

If pagination exists:

1. Retrieve every page.
2. Continue until all pages are exhausted.
3. Combine the results.
4. Deduplicate by stable account identifier.

## Eligibility

An account is eligible when it is NOT explicitly:

- deleted
- archived

Everything else is eligible.

Do not infer archival/deletion from inactivity or balance.

## Completeness invariant

Maintain:

TOTAL_RETRIEVED_ACCOUNTS
TOTAL_DELETED_ACCOUNTS
TOTAL_ARCHIVED_ACCOUNTS
TOTAL_ELIGIBLE_ACCOUNTS

Verify:

TOTAL_ELIGIBLE_ACCOUNTS =
TOTAL_RETRIEVED_ACCOUNTS -
TOTAL_DELETED_ACCOUNTS -
TOTAL_ARCHIVED_ACCOUNTS

Later verify that every eligible account appears in the report.

## Transaction retrieval

Retrieve the complete transaction dataset needed for the reporting period.

Handle pagination.

Do not silently truncate large datasets.

## Transfers

Identify internal transfers where possible.

Do not count internal transfers as external income or expenses.

## Output

Provide clean normalized data to the financial-analysis workflow.

Never modify Wallet while doing so.