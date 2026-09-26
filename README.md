# OpenCode Wallet Financial Report

A specialized **OpenCode Agent + Skills** package for generating polished financial reports from **Wallet by BudgetBakers** through MCP.

> **Important:** Wallet by BudgetBakers MCP must be configured and working in OpenCode **before using this Agent**.

This repository provides the Agent and Skills only. It does not install or configure the Wallet MCP server for you.

---

## Agent

### Wallet Financial Report

A read-only financial reporting Agent for OpenCode that uses Wallet by BudgetBakers MCP to analyze all eligible accounts and produce a polished financial PDF.

It handles:

* Complete account retrieval
* Financial analysis
* Charts and visual summaries
* PDF report design
* Data and visual quality checks

The Agent must never modify Wallet data.

---

## Skills

### 1. Wallet Read-Only

Ensures Wallet MCP is used strictly for reading data.

Handles:

* Complete account retrieval
* Pagination
* Deduplication
* Account completeness
* Transfer handling
* Currency awareness

---

### 2. Financial Analysis

Turns Wallet data into meaningful financial metrics and observations.

Covers:

* Net worth
* Assets and liabilities
* Income and expenses
* Cash flow
* Savings
* Debt
* Investments
* Financial trends

---

### 3. Financial Data Visualization

Defines how financial information should be presented visually.

Covers:

* KPI cards
* Charts
* Account visualizations
* Trends
* Financial summaries
* Large account sets

The goal is clear, attractive, at-a-glance communication.

---

### 4. PDF Report Design

Defines the visual structure and design of the final PDF.

Uses a clean, premium financial-report style with:

* Strong typography
* Consistent spacing
* Cards
* Charts
* Visual hierarchy
* Material UI-inspired styling

---

### 5. Report Quality Check

Performs the final validation before the report is finished.

Checks:

* Wallet read-only compliance
* Account completeness
* Data accuracy
* Financial reconciliation
* Transfer handling
* Currency handling
* PDF readability
* Visual integrity

---

# Wallet by BudgetBakers MCP

Wallet MCP must be configured and working in OpenCode before using the Agent.

The official Wallet MCP uses a remote Streamable HTTP endpoint:

```text
https://mcp.wallet.budgetbakers.com
```

Wallet MCP supports read and write permissions. For this Agent, **only read permissions should be enabled** in Wallet's MCP settings. Wallet's documentation states that permissions can be controlled at the Wallet level, with read access separated from create, update, and delete permissions.

## 1. Add Wallet MCP to OpenCode

Run:

```bash
opencode mcp add wallet --global --url https://mcp.wallet.budgetbakers.com
```

The `--global` option makes the MCP server available across your OpenCode projects. OpenCode's `mcp add` command supports adding remote MCP servers with `--url`.

## 2. Authenticate Wallet MCP

Wallet MCP uses OAuth 2.0 with PKCE for supported clients. OpenCode provides an MCP authentication command for OAuth-enabled servers.

Run:

```bash
opencode mcp auth wallet
```

Follow the authentication prompts.

If your OpenCode version instead prompts you to authenticate through the OpenCode interface, complete the displayed authentication flow.

## 3. Verify the connection

Run:

```bash
opencode mcp list
```

You should see the Wallet MCP server and its connection status.

You can also check the configured server with:

```bash
opencode mcp ls
```

OpenCode documents `mcp list` / `mcp ls` for viewing configured MCP servers and their connection status.

## 4. Enable read-only permissions in Wallet

Open the Wallet web application and go to the MCP permissions settings.

Enable:

```text
Read / Browse
```

Keep these disabled:

```text
Create
Update
Delete
```

The Wallet MCP permission system separates read access from write permissions. With write permissions disabled, the MCP server will not expose those write capabilities to the AI client.

This is strongly recommended for this project because the Agent is intended to perform **financial analysis only**.

### Required permission model

```text
Wallet MCP
│
├── Read       ✅
├── Create     ❌
├── Update     ❌
└── Delete     ❌
```

The Agent itself also follows a strict read-only policy.

> **Do not enable Wallet write permissions for this Agent.**

---

# Manual Agent Installation

After Wallet MCP is configured, install the Agent and Skills into OpenCode's global configuration.

No installation or uninstallation scripts are included.

## macOS / Linux

The default global OpenCode configuration directory is:

```text
~/.config/opencode/
```

Create the required directories:

```bash
mkdir -p ~/.config/opencode/agents

mkdir -p ~/.config/opencode/skills/wallet-readonly
mkdir -p ~/.config/opencode/skills/financial-analysis
mkdir -p ~/.config/opencode/skills/financial-data-viz
mkdir -p ~/.config/opencode/skills/pdf-report-design
mkdir -p ~/.config/opencode/skills/report-quality-check
```

From the repository root, copy the Agent:

```bash
cp agent/wallet-financial-report.md \
  ~/.config/opencode/agents/
```

Then copy the Skills:

```bash
cp skills/wallet-readonly/SKILL.md \
  ~/.config/opencode/skills/wallet-readonly/

cp skills/financial-analysis/SKILL.md \
  ~/.config/opencode/skills/financial-analysis/

cp skills/financial-data-viz/SKILL.md \
  ~/.config/opencode/skills/financial-data-viz/

cp skills/pdf-report-design/SKILL.md \
  ~/.config/opencode/skills/pdf-report-design/

cp skills/report-quality-check/SKILL.md \
  ~/.config/opencode/skills/report-quality-check/
```

Restart or reload OpenCode.

The Agent should then appear in the OpenCode Agent selector as:

```text
Wallet Financial Report
```

---

# Windows

The equivalent global configuration directory is normally:

```text
%USERPROFILE%\.config\opencode\
```

Create the same `agents` and `skills` structure and copy the corresponding files into it.

The Wallet MCP command remains:

```powershell
opencode mcp add wallet --global --url https://mcp.wallet.budgetbakers.com
```

Then authenticate:

```powershell
opencode mcp auth wallet
```

And verify:

```powershell
opencode mcp list
```

---

# Installed Structure

After installation, your OpenCode configuration should look like:

```text
~/.config/opencode/
│
├── agents/
│   └── wallet-financial-report.md
│
└── skills/
    ├── wallet-readonly/
    │   └── SKILL.md
    │
    ├── financial-analysis/
    │   └── SKILL.md
    │
    ├── financial-data-viz/
    │   └── SKILL.md
    │
    ├── pdf-report-design/
    │   └── SKILL.md
    │
    └── report-quality-check/
        └── SKILL.md
```

The **Agent** is selected from OpenCode's Agent selector.

The **Skills** provide supporting instructions used by the Agent.

---

# Using the Agent

Once Wallet MCP is connected and the Agent has been installed, select:

```text
Wallet Financial Report
```

from the OpenCode Agent selector.

You can then ask it to generate your financial report.

For example:

```text
Generate my complete financial report from Wallet.

Use every eligible account.
Exclude only accounts that are explicitly deleted or archived.

Do not modify anything in Wallet.

Create a polished financial PDF with KPI cards,
charts, visual summaries, and clear financial insights.

Perform complete data and visual QA before finishing.
```

---

# Core Requirements

The Agent must follow these rules.

### Wallet is strictly read-only

The Agent must never:

* Create Wallet records
* Edit Wallet records
* Delete records
* Archive or unarchive accounts
* Modify transactions
* Modify balances
* Modify categories
* Create transfers
* Perform any other Wallet write operation

Only read operations are allowed.

### Every eligible account must be included

Include **every Wallet account** except accounts explicitly identified as:

* Deleted
* Archived

Do not exclude accounts because of:

* Balance
* Activity
* Transaction count
* Account type
* Currency
* Age
* Size

There is:

* No account sampling
* No minimum balance
* No maximum account count
* No activity threshold

The Agent must verify:

```text
Eligible accounts retrieved
=
Eligible accounts represented
```

### Pagination

The Agent must handle pagination completely and avoid missing accounts or transactions.

### Deduplication

Duplicate records must be detected and handled before analysis.

### Transfers

Internal transfers must not be incorrectly counted as income or expenses.

### Credit-card payments

Credit-card payments must not cause the underlying spending to be double-counted.

### Multiple currencies

Different currencies must not be silently combined.

If currency conversion is required, the methodology must be explicit.

### No invented data

The Agent must not invent missing financial information.

---

# Report Design

The final report should feel like a **premium financial report**, not a spreadsheet export.

Preferred elements include:

* KPI cards
* Charts
* Trend visualizations
* Financial summaries
* Account visualizations
* Short insights
* Clear typography
* Generous whitespace
* Consistent visual hierarchy

The visual style should be inspired by modern Material UI design:

* Deep blue / indigo primary
* Teal / cyan secondary
* Restrained green and red semantic colors
* Slate / gray neutrals
* Light backgrounds
* Cards
* Subtle elevation
* Restrained rounded corners

---

# Readability

Readability is a hard requirement.

The report must avoid:

* Tiny text
* Overlapping elements
* Clipped content
* Unreadable legends
* Cramped tables
* Overloaded charts
* Bad page breaks

If content does not fit:

> **Add another page instead of shrinking the content.**

Large numbers of accounts should use appropriate visualizations such as:

* Horizontal bar charts
* Account cards
* Grouped charts
* Paginated sections
* Sparklines

Avoid huge pie or donut charts containing dozens of accounts.

---

# Suggested Report Structure

The Agent may organize the report into sections such as:

1. **Cover**
2. **Executive Financial Snapshot**
3. **Net Worth / Financial Position**
4. **Cash Flow**
5. **Spending**
6. **Income**
7. **Account Overview**
8. **Debt & Investments**
9. **Trends & Observations**
10. **Detailed Account Directory**
11. **Methodology & Data Notes**

The exact structure can adapt to the available Wallet data.

---

# Quality Check

Before considering the report complete, the Agent must verify:

```text
Wallet Safety
      ↓
Account Completeness
      ↓
Data Completeness
      ↓
Financial Reconciliation
      ↓
Transfer / Payment Handling
      ↓
Currency Handling
      ↓
PDF Readability
      ↓
Visual Integrity
```

The final report should not be considered complete if:

* Eligible accounts are missing
* Pagination was incomplete
* Wallet data was modified
* Financial totals do not reconcile
* Transfers are double-counted
* Currencies are incorrectly combined
* Charts are unreadable
* PDF content is clipped or overlapping

---

# Updating

To update the Agent or Skills, pull the latest repository version:

```bash
git pull
```

Then copy the updated files into the OpenCode configuration directory again.

Restart or reload OpenCode afterward.

---

# Removing the Agent

To remove the Agent and Skills, manually delete the files copied into:

```text
~/.config/opencode/agents/
~/.config/opencode/skills/
```

Specifically:

```text
agents/wallet-financial-report.md

skills/wallet-readonly/SKILL.md
skills/financial-analysis/SKILL.md
skills/financial-data-viz/SKILL.md
skills/pdf-report-design/SKILL.md
skills/report-quality-check/SKILL.md
```

To remove the Wallet MCP server from OpenCode as well, use:

```bash
opencode mcp remove wallet
```

---

# Security

Never commit sensitive information to this repository.

Do not store:

* Wallet credentials
* MCP authentication tokens
* API keys
* Personal financial exports
* Generated financial reports containing sensitive data

For this Agent, keep Wallet MCP permissions **read-only**.

---

# Repository Structure

```text
opencode-wallet-financial-report/
│
├── README.md
│
├── agent/
│   └── wallet-financial-report.md
│
└── skills/
    ├── wallet-readonly/
    │   └── SKILL.md
    │
    ├── financial-analysis/
    │   └── SKILL.md
    │
    ├── financial-data-viz/
    │   └── SKILL.md
    │
    ├── pdf-report-design/
    │   └── SKILL.md
    │
    └── report-quality-check/
        └── SKILL.md
```

---

# In Short

```text
1. Add Wallet MCP
        ↓
opencode mcp add wallet --global \
  --url https://mcp.wallet.budgetbakers.com

        ↓
2. Authenticate
        ↓
opencode mcp auth wallet

        ↓
3. Verify
        ↓
opencode mcp list

        ↓
4. Set Wallet MCP permissions to READ-ONLY
        ↓
5. Copy Agent + Skills into ~/.config/opencode/
        ↓
6. Restart OpenCode
        ↓
7. Select "Wallet Financial Report"
        ↓
8. Generate the financial report
```

The result is a **complete, read-only Wallet analysis with professional financial visualization and PDF reporting**.
