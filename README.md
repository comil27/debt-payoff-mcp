# debt-payoff-mcp — Debt Payoff Planner MCP Server

A hosted **[Model Context Protocol](https://modelcontextprotocol.io) server** that lets any AI
assistant compute a real **debt-payoff plan** — comparing the **snowball** (smallest balance first)
and **avalanche** (highest APR first) strategies — with no API key and nothing to install.

> Works in Claude Code, Claude Desktop, Cursor, and any MCP-capable agent.

## What it does

The `debt_payoff_plan` tool takes one or more debts and returns, for **both** strategies:

- **monthsToDebtFree** / **years**
- **totalInterest** paid
- **payoffOrder** — which debt is cleared first, second, …
- **recommended** strategy + how much interest avalanche saves vs snowball

## Install (remote — nothing to download)

**Claude Code**

```bash
claude mcp add --transport http debt-payoff https://debtfree.rugscore.workers.dev/mcp
```

**Claude Desktop / Cursor / generic MCP client:**

```json
{
  "mcpServers": {
    "debt-payoff": {
      "type": "streamable-http",
      "url": "https://debtfree.rugscore.workers.dev/mcp"
    }
  }
}
```

Then ask: *"I have a $6,000 card at 24% (min $150) and a $12,000 car loan at 7% (min $250), and I can put $200 extra toward debt each month. What's the fastest way to pay it off?"*

## Example

```jsonc
// debt_payoff_plan
// { "debts": [ {"name":"Visa","balance":6000,"apr":24,"min":150} ], "extra": 100 }
{
  "snowball":  { "monthsToDebtFree": 29, "totalInterest": 1480.69, "payoffOrder": ["Visa"] },
  "avalanche": { "monthsToDebtFree": 29, "totalInterest": 1480.69, "payoffOrder": ["Visa"] },
  "recommended": "avalanche",
  "avalancheSavesInterest": 0
}
```

Single-debt shortcut: pass `balance`, `apr`, `min` (and optional `extra`) instead of `debts`.

## Full workbook

The free tool plans the payoff. The complete **Debt-Free Workbook** (`.xlsx`: budget, sinking
funds, net-worth tracker, 52-week challenge, plus the live payoff engine) is available here:

**https://debtfree.rugscore.workers.dev**

A free in-browser calculator and worked examples live there too.

## License

MIT
