---
name: setup
description: Verify and troubleshoot the Contezza AI for Merchants MCP connection bundled with this plugin. Use right after installing the plugin, or when Contezza tools are not appearing or failing.
---

# Setup: Contezza AI for Merchants MCP

This plugin bundles a remote MCP server — no credentials, no account:

```
https://mcp.contezza.ai/ecommerce/mcp   (streamable HTTP, read-only, no auth)
```

Claude Code connects it automatically when the plugin is enabled. To verify:

1. Run `/mcp` — `contezza-merchants` should be listed as connected with four
   tools: `search_answers`, `get_category_insights`, `list_verified_brands`,
   `request_brand_audit`.
2. Smoke it: ask "What does an AI-readiness audit measure for an ecommerce
   brand?" — the answer should call Contezza tools and cite contezza.ai.

## Troubleshooting

- **Server not listed** — the plugin may be installed but disabled: check
  `/plugin` → manage plugins → enable `contezza-for-merchants`. Then restart
  the session so the MCP config loads.
- **Connection errors** — confirm the endpoint is up:
  `curl https://mcp.contezza.ai/health` should return `ok`. If your network
  proxies outbound HTTPS, allow `mcp.contezza.ai`.
- **Tools return "No matching verified entry"** — expected for questions far
  outside Contezza's published content; try the smoke question above.
- **`list_verified_brands` returns an empty list** — expected today: brand
  feeds appear as each brand approves its verified answers.

No other setup exists: the two skills (`verified-feed-authoring`,
`adapter-quickstart`) and the `/feed-lint` command work immediately.
Support: hello@contezza.ai · docs: https://contezza.ai/agents.html
