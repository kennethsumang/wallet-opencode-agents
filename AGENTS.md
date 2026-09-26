# Wallet Financial Agents

This repository contains OpenCode **agents** and **skills** that analyze **Wallet by BudgetBakers** data through the Wallet MCP, producing interactive financial analyses and polished PDF reports.

## Repository layout

```text
financial-report-agent/
├── AGENTS.md              # this file — repo conventions for coding agents
├── README.md              # end-user setup and usage instructions
├── agents/                # one OpenCode agent per .md file
│   ├── wallet-financial-health.md
│   ├── wallet-spending-analyst.md
│   └── wallet-financial-report.md
└── skills/                # one folder per skill, each with SKILL.md
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

## Agents

| Agent file | Purpose | Allowed skills |
| --- | --- | --- |
| `wallet-financial-health.md` | Overall financial position: net worth, assets/liabilities, income, expenses, cash flow, savings, debt, trends | `wallet-readonly`, `financial-health-analysis`, `financial-health-insights` |
| `wallet-spending-analyst.md` | Where money goes: categories, merchants, trends, recurring and unusual spending | `wallet-readonly`, `spending-analysis`, `spending-insights` |
| `wallet-financial-report.md` | Polished, visually rich, read-only PDF report from all eligible accounts | `wallet-readonly`, `financial-analysis`, `financial-data-viz`, `pdf-report-design`, `report-quality-check` |

## Skills

Each skill lives in `skills/<name>/SKILL.md`.

| Skill | Purpose |
| --- | --- |
| `wallet-readonly` | Read-only protocol: safe retrieval, full account enumeration, pagination, eligibility, and the completeness invariant |
| `financial-health-analysis` | Core financial-health metrics, cash-flow analysis, reconciliation, and time comparisons |
| `financial-health-insights` | Evidence-based observations, strengths, and areas to watch from health metrics |
| `spending-analysis` | Spending metrics by category, merchant, account, period, and trend |
| `spending-insights` | Evidence-based observations, trends, and unusual-spending flags from spending data |
| `financial-analysis` | Reconciles balances and derives report metrics (assets, liabilities, net worth, cash flow, savings rate) |
| `financial-data-viz` | Charts and visual summaries; tables are supporting material only |
| `pdf-report-design` | Material UI-inspired PDF layout, typography, hierarchy, and design |
| `report-quality-check` | Numerical, account-completeness, readability, and visual QA before delivery |

## File conventions

### Agent files (`agents/*.md`)

- YAML frontmatter with at least:
  - `description` — what the agent does
  - `mode` — `primary`
  - `permission.skill.<name>` — set to `allow` for every skill the agent may load
- Optional frontmatter: `color` (hex accent used by the OpenCode UI)
- Body: role statement, core rules, ordered workflow (skill loads), and output structure

### Skill files (`skills/*/SKILL.md`)

- YAML frontmatter with at least:
  - `name` — must match the folder name
  - `description` — what the skill does
  - `compatibility` — `opencode`
- Frontmatter must be delimited by `---` (three dashes)
- Body: instructions the agent follows once the skill is loaded

## Non-negotiable rules

Every agent and skill must honor these. Do not weaken them.

- Wallet MCP is READ-ONLY.
- Never mutate Wallet records (no create, edit, delete, archive, unarchive, rename, categorize, or transfer).
- Include every account except explicitly deleted or archived accounts.
- Never filter accounts by balance, activity, type, currency, age, or transaction count.
- Never silently truncate paginated Wallet data; handle pagination and deduplicate records.
- Never double-count internal transfers or credit-card payments.
- Never invent financial data.
- Never silently combine different currencies.
- Financial reports must prioritize readability and visual communication.
- Tables are supporting material, not the primary presentation format.
- Use charts, KPI cards, visual summaries, and tasteful illustrations.
- Use a Material UI-inspired design language.
- Prefer adding pages over shrinking text.
- Always perform account-completeness and visual QA before finalizing a report.