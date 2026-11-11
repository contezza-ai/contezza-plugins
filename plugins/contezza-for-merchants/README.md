# Contezza AI for Merchants

Trusted merchant knowledge for AI agents: policy checks, brand knowledge graphs
with citations to each brand's own published pages, and audit-grounded category
norms, plus tools to author and lint Verified Answers feeds. Built by Contezza AI,
a product of TechMatrix AI Systems LLC.

## Connect it first (chat and Cowork)

Adding the plugin does not connect its server. In claude.ai or the Claude desktop app:

1. Open **Customize > Plugins**, select **Contezza AI for Merchants**, then the **Connectors** tab.
2. Select **Add**, then **Connect**. No sign-in and no account are needed.
3. In a chat, select **+**, then **Connectors**, and make sure Contezza is switched on.

On a Team or Enterprise plan, an Owner adds the connector for the organization first.
In Cowork, if a session reports that `mcp.contezza.ai` is blocked, an admin must allow
that domain in the organization's network settings. Claude Code connects the server on
its own when the plugin is enabled.

## What you can ask

The connector (`contezza-merchants`, `https://mcp.contezza.ai/ecommerce/mcp`,
read-only, no authentication) serves five tools:

- `check_policy_consistency`: paste two policy texts, such as an FAQ and a returns
  page, and get a verdict on conflicting fees, return windows, warranty and shipping
  terms, with the mismatched excerpts. It processes only the pasted text and stores nothing.
- `get_brand_graph`: a brand's products, policies and claims, each with a citation to
  the brand's own published pages and a verification status. Where a brand's pages
  disagree, both sources are returned instead of one being picked.
- `get_category_norms`: anonymized observed ranges from audited merchant cohorts, with
  the sample size stated.
- `get_agent_readiness_checklist`: concrete actions across the five dimensions
  Contezza audits.
- `list_verified_brands`: the brands whose graphs are served. Demonstration data is labeled.

Try: "Which brands have verified knowledge graphs on Contezza?" or "Check these two
policy texts for conflicting fees", followed by the two texts.

## Skills and command

- `verified-feed-authoring`: author a Verified Answers feed for a brand, with citation
  anchors, explicit contradiction handling and review dates.
- `adapter-quickstart`: wire the open `contezza-for-commerce-agents` adapter into
  Anthropic's commerce-agents blueprint.
- `/feed-lint`: lint a feed file. In Cowork and Claude Code run it by name; in chat it
  loads as a skill.
- `setup`: verify and troubleshoot the connection.

## Data

The skills and the command run where Claude runs and send nothing. The connector
sends only your tool inputs to `mcp.contezza.ai`: the two texts you paste for a
consistency check, a brand name, or a category. Contezza stores none of it. See the
[privacy policy](https://contezza.ai/privacy.html) for what the service logs to operate.
Brand graphs are built from each brand's own published pages; demonstration brands are
labeled as such. The example feeds in the skills are fictional.

**Demonstration notice.** These tools demonstrate what Contezza does. Demonstration
brands such as Acme Outdoors are fictional sample data and must not be taken as actual
merchant data or as guidance. Category norms are observed ranges from a small audited
sample, stated with their sample size, not market statistics. Audited brand graphs cite
the brand's own published pages as of their verification date; check the citation before
relying on a fact. Nothing here is guidance for your own policies or business decisions.

Part of the [contezza-plugins](https://github.com/contezza-ai/contezza-plugins)
marketplace · [contezza.ai](https://contezza.ai) · Support: hello@contezza.ai · Apache-2.0
