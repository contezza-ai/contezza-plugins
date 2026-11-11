---
name: setup
description: Verify and troubleshoot the Contezza AI for Financial Services connection bundled with this plugin. Use right after adding the plugin, when the Contezza financial services tools are not appearing, or when a call fails.
---

# Setup: Contezza AI for Financial Services

This plugin bundles a remote MCP server. No credentials and no account:

```
https://mcp.contezza.ai/finserv/mcp   (streamable HTTP, read-only, no auth)
```

## Connect it (the step most people miss)

- **Chat in claude.ai or the desktop app:** adding the plugin does not connect the
  server. Open **Customize > Plugins > Contezza AI for Financial Services > Connectors**.
  The row `contezza-financial-services` shows **Not added**: select **Add**, then
  **Connect**. Then, in the chat, select **+ > Connectors** and make sure Contezza is
  switched on. On a Team or Enterprise plan, an Owner adds the connector for the
  organization first.
- **Cowork:** connect it from the same Connectors tab, then start a new session. If the
  session reports that `mcp.contezza.ai` is blocked, an admin must allow that domain in
  the organization's network settings.
- **Claude Code:** the server connects on its own when the plugin is enabled. Run
  `/mcp` to confirm `contezza-financial-services` is connected.

## Verify

When connected, the server lists nine tools: `analyze_rent_roll`,
`benchmark_mortgage_application`, `check_lending_policy_consistency`,
`compute_commercial_worksheet`, `compute_prequal_worksheet`, `extract_lending_facts`,
`get_model_risk_checklist`, `lookup_regulatory_facts`, `screen_policy_against_regulation`.

Ask: "Is the QM debt-to-income limit still 43 percent?" The answer should come from
`lookup_regulatory_facts`, report the 43 percent test as superseded history (the 2013
rule, effective January 10, 2014, replaced by the price-based General QM definition
effective March 1, 2021), cite the public source for each fact, and say that it is not
legal or compliance advice.

## Troubleshooting

- **Tools not listed:** check the plugin is enabled (Customize > Plugins, or `/plugin`
  in Claude Code), check the Connectors tab shows **Connected**, then start a new session.
- **Connection errors:** confirm the service is up by fetching
  `https://mcp.contezza.ai/health` in a browser or with WebFetch; it returns `ok`. If a
  proxy or sandbox restricts outbound HTTPS, allow `mcp.contezza.ai`.
- **A call is refused as too frequent:** the service allows 60 calls a minute per
  session and 600 a minute per address. Wait a minute and retry.
- **A call is refused as too large:** requests over 1.2 MB are rejected. Split the
  document and use `extract_lending_facts`, which takes up to five documents of
  200,000 characters each.
- **A worksheet refuses the input:** it accepts numbers only. Remove names, identifiers
  and protected characteristics.
- **A benchmark cell is not served:** fewer than 30 decisioned applications fall in that
  band. Widen the state or the loan type.

Support: hello@contezza.ai · Docs: https://contezza.ai/financial-services.html
