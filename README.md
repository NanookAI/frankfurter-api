# Frankfurter API Skill

An [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills) that
teaches AI agents (Claude Code, Claude.ai, and other skill-compatible agents) how to
use the free [Frankfurter](https://frankfurter.dev/) exchange rate API.

Frankfurter tracks daily reference rates from **84 central banks**, covering
**201 currencies** with history back to **1948** — no API key, no signup, no quotas.

## What the skill enables

Once loaded, an agent can reliably:

- Fetch the latest exchange rates (any base currency, filtered quote list)
- Convert amounts between currencies (e.g. 100 USD → TWD)
- Look up historical rates for a specific date
- Pull time series over a date range, optionally grouped by week/month
- Pin rates to a specific central bank (e.g. `providers=ECB`) for compliance use
- Request CSV or NDJSON output for data pipelines
- Avoid real-world pitfalls (blocked `Python-urllib` User-Agent, weekend/holiday
  date rollback, blended-rate drift)

All request/response examples in the skill were verified against the live API.

## Repository layout

```
skills/
└── frankfurter-api/
    ├── SKILL.md                 # Entry point: quick reference, conversion recipes, tips
    └── references/
        ├── endpoints.md         # Full v2 endpoint reference with verified examples
        └── v1-api.md            # Legacy v1 API (only for maintaining old code)
```

## Installation

### Claude Code (per-project)

Copy the skill folder into your project's `.claude/skills/` directory:

```bash
cp -r skills/frankfurter-api /path/to/your-project/.claude/skills/
```

### Claude Code (personal, all projects)

```bash
cp -r skills/frankfurter-api ~/.claude/skills/
```

### Claude.ai / other agents

Package the skill folder (respecting `.skillignore`) into a `.skill` bundle, or
upload the `skills/frankfurter-api/` folder contents wherever your agent platform
accepts skills. The skill is self-contained — no scripts, no dependencies.

## Try it

After installing, ask your agent things like:

- "What's the latest USD to TWD rate?"
- "Convert 5000 JPY to EUR"
- "Show me the EUR/USD trend for the last 3 months, grouped by week"
- "Get the official ECB reference rate for GBP on 2020-03-16"

## About the API

- Public endpoint: `https://api.frankfurter.dev` (v2)
- Free for commercial use; see each data provider's terms for the underlying data
- Open source and self-hostable via Docker — see [frankfurter.dev](https://frankfurter.dev/)

## License

The skill documentation in this repository is provided as-is. Frankfurter itself
is an independent open-source project — see [frankfurter.dev](https://frankfurter.dev/)
for its license and terms.
