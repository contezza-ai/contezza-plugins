# contezza-plugins

**Contezza AI - trusted merchant knowledge for AI agents.** Claude Code plugins
from [Contezza](https://contezza.ai).

## Install

```
/plugin marketplace add contezza-ai/contezza-plugins
/plugin install contezza-for-merchants@contezza
```

## Plugins

### contezza-for-merchants

For developers making merchant content agent-ready and building on Anthropic's
[commerce-agents](https://github.com/anthropics/commerce-agents) blueprint:

- **verified-feed-authoring** (skill) — author and validate a Verified Answers
  feed: entry structure, citation anchors, contradiction handling, lint pass.
- **adapter-quickstart** (skill) — wire the
  [contezza-for-commerce-agents](https://github.com/contezza-ai/contezza-for-commerce-agents)
  adapter into a blueprint `ShoppingAgent` and smoke-test it.
- **/feed-lint** (command) — lint a feed file: structure, citation rules,
  facts-vs-prose drift, reconciliation completeness, stale review dates.
- **setup** (skill) — verify and troubleshoot the bundled MCP connection.
- **Contezza AI for Merchants** (MCP) — the four read-only tools from
  `mcp.contezza.ai/ecommerce/mcp`: verified answers, audit insights, the
  verified-brand registry, and audit requests. No auth, no account.

[contezza.ai](https://contezza.ai) · [docs](https://contezza.ai/agents.html) · hello@contezza.ai · Apache-2.0
