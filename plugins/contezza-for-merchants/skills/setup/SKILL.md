---
name: setup
description: Verify and troubleshoot the Contezza AI for Merchants connection bundled with this plugin. Use right after adding the plugin, when Contezza tools are not appearing, or when a call fails.
---

# Setup: Contezza AI for Merchants

This plugin bundles a remote MCP server. No credentials and no account:

```
https://mcp.contezza.ai/ecommerce/mcp   (streamable HTTP, read-only, no auth)
```

## Connect it (the step most people miss)

- **Chat in claude.ai or the desktop app:** adding the plugin does not connect the
  server. Open **Customize > Plugins > Contezza AI for Merchants > Connectors**. The
  row `contezza-merchants` shows **Not added**: select **Add**, then **Connect**. Then,
  in the chat, select **+ > Connectors** and make sure Contezza is switched on. On a
  Team or Enterprise plan, an Owner adds the connector for the organization first.
- **Cowork:** connect it from the same Connectors tab, then start a new session. If the
  session reports that `mcp.contezza.ai` is blocked, an admin must allow that domain in
  the organization's network settings.
- **Claude Code:** the server connects on its own when the plugin is enabled. Run
  `/mcp` to confirm `contezza-merchants` is connected.

## Verify

When connected, the server lists five tools: `check_policy_consistency`,
`get_agent_readiness_checklist`, `get_brand_graph`, `get_category_norms`,
`list_verified_brands`.

Ask: "Which brands have verified knowledge graphs on Contezza?" The answer should come
from `list_verified_brands`, name at least one audited pilot brand whose facts cite its
own published pages, and mark any demonstration brand as fictional sample data that must
not be taken as actual merchant data or as guidance.

## Troubleshooting

- **Tools not listed:** check the plugin is enabled (Customize > Plugins, or `/plugin`
  in Claude Code), check the Connectors tab shows **Connected**, then start a new session.
- **Connection errors:** confirm the service is up by fetching
  `https://mcp.contezza.ai/health` in a browser or with WebFetch; it returns `ok`. If a
  proxy or sandbox restricts outbound HTTPS, allow `mcp.contezza.ai`.
- **A brand is not served:** `get_brand_graph` covers only the brands returned by
  `list_verified_brands`. A brand can request an audit or claim its graph at
  https://contezza.ai.
- **A consistency check reports no conflict:** the two texts agree on the money facts
  it checks (fees, return windows, warranty and shipping terms). It processes only the
  pasted text and stores nothing.

The two skills (`verified-feed-authoring`, `adapter-quickstart`) and the `/feed-lint`
command work without the connection.
Support: hello@contezza.ai · Docs: https://contezza.ai/agents.html
