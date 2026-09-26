# Wallet Financial Reporting Project

This project generates financial reports from Wallet MCP.

## Non-negotiable rules

- Wallet MCP is READ-ONLY.
- Never mutate Wallet records.
- Include every account except explicitly deleted or archived accounts.
- Never filter accounts by balance or activity.
- Never silently truncate paginated Wallet data.
- Never double-count internal transfers.
- Never invent financial data.
- Never silently combine different currencies.
- Financial reports must prioritize readability and visual communication.
- Tables are supporting material, not the primary presentation format.
- Use charts, KPI cards, visual summaries, and tasteful illustrations.
- Use a Material UI-inspired design language.
- Prefer adding pages over shrinking text.
- Always perform account-completeness and visual QA before finalizing a report.