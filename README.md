# OpenCode Wallet Financial Agents

Custom OpenCode agents and skills for analyzing **Wallet by BudgetBakers** data through the Wallet MCP.

All agents are **READ-ONLY** and never modify Wallet records.

## Requirements

* [OpenCode](https://opencode.ai)
* Wallet by BudgetBakers MCP

## Setup

### 1. Configure Wallet MCP

```bash
opencode mcp add wallet --global --url https://mcp.wallet.budgetbakers.com
opencode mcp auth wallet
opencode mcp list
```

Use read-only permissions for the Wallet MCP connection.

### 2. Install Agents & Skills

Copy the desired agent and skill files into your OpenCode global configuration directory:

```text
~/.config/opencode/
├── agents/
└── skills/
```

After copying the files, restart OpenCode if necessary. The agents should then appear in the OpenCode Agent dropdown.

## Agents

### 1. Financial Health

Analyzes your overall financial position, including:

* Net worth
* Assets and liabilities
* Income and expenses
* Cash flow
* Savings
* Debt
* Investments
* Financial trends

**Skills:**

* `wallet-readonly`
* `financial-health-analysis`
* `financial-health-insights`

### 2. Spending Analyst

Analyzes where your money is going and how spending changes over time.

**Skills:**

* `wallet-readonly`
* `spending-analysis`
* `spending-insights`

### 3. Financial Report

Creates polished, visually rich financial reports from Wallet data.

**Skills:**

* `wallet-readonly`
* `financial-analysis`
* `financial-data-viz`
* `pdf-report-design`
* `report-quality-check`

## Data Rules

All agents follow these principles:

* **READ-ONLY:** Never modify Wallet data.
* **Complete accounts:** Include every account except explicitly deleted or archived accounts.
* **No arbitrary filtering:** Never exclude accounts based on balance, activity, type, currency, age, or transaction count.
* **Complete retrieval:** Handle pagination and deduplicate records.
* **No double counting:** Avoid double-counting internal transfers and credit-card payments.
* **Multiple currencies:** Never silently combine incompatible currencies.
* **Evidence-based:** Never invent financial data.
* **Completeness check:** Verify that all eligible accounts retrieved are represented in the analysis.

## Repository Structure

```text
opencode-wallet-financial-agents/
├── README.md
├── agent/
│   ├── wallet-financial-health.md
│   ├── wallet-spending-analyst.md
│   └── wallet-financial-report.md
└── skills/
    ├── wallet-readonly/
    ├── financial-health-analysis/
    ├── financial-health-insights/
    ├── spending-analysis/
    ├── spending-insights/
    ├── financial-analysis/
    ├── financial-data-viz/
    ├── pdf-report-design/
    └── report-quality-check/
```
