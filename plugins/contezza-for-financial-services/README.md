# Contezza AI for Financial Services

Cited lending, regulatory and model-risk checks for Claude. Nine read-only tools answer
from public US federal sources, each fact checked against the page that published it,
and from the text and numbers you paste. Every answer carries a citation and an
effective date and says that it is not legal, compliance or credit advice. Built by
Contezza AI, a product of TechMatrix AI Systems LLC.

## Connect it first (chat and Cowork)

Adding the plugin does not connect its server. In claude.ai or the Claude desktop app:

1. Open **Customize > Plugins**, select **Contezza AI for Financial Services**, then the **Connectors** tab.
2. Select **Add**, then **Connect**. No sign-in and no account are needed.
3. In a chat, select **+**, then **Connectors**, and make sure Contezza is switched on.

On a Team or Enterprise plan, an Owner adds the connector for the organization first.
In Cowork, connect it from the same Connectors tab and start a new session; if the
session reports that `mcp.contezza.ai` is blocked, an admin must allow that domain in
the organization's network settings. Claude Code connects the server on its own when
the plugin is enabled; run `/mcp` to confirm `contezza-financial-services` is connected.

## What you can ask

The connector (`contezza-financial-services`, `https://mcp.contezza.ai/finserv/mcp`,
read-only, no authentication) serves nine tools:

- `lookup_regulatory_facts`: cited facts from the CFPB ability-to-repay and qualified
  mortgage rules, Regulation B, Regulation Z and TRID, HMDA, capital rules and the
  SR 26-2 model risk guidance, each with its value, effective date and status. A rule
  that has been replaced comes back as dated history, never as current. With no
  arguments it returns the coverage index.
- `extract_lending_facts`: numeric lending facts and regulatory references pulled out
  of a pasted credit policy or loan document into a fact packet the other tools accept.
  Superseded references are flagged with their replacement.
- `check_lending_policy_consistency`: two lending texts or packets compared for
  conflicting ratios, scores, rates, fees, terms and notice windows, with excerpts.
- `screen_policy_against_regulation`: a policy's thresholds compared with the cited
  regulatory values; retired thresholds still in the policy are flagged.
- `get_model_risk_checklist`: actions grounded in SR 26-2, each citing the guidance
  sentence it comes from; the AI and LLM area is labeled derived guidance.
- `benchmark_mortgage_application`: how an application's ratios compare with outcomes
  in the CFPB's public HMDA data. Aggregates only, historical, never a decision.
- `compute_prequal_worksheet`: a mortgage pre-submission readiness worksheet from a
  numbers-only profile, with cited program screens and what-if deltas. Not a credit
  decision and not a substitute for the automated underwriting systems.
- `compute_commercial_worksheet`: a commercial loan spread with DSCR, leverage, a
  stress case, your covenant tests and cited regulatory screens.
- `analyze_rent_roll`: a rent roll turned into NOI, occupancy, lease rollover and
  tenant concentration, with tenants anonymized.

Try: "Is the QM debt-to-income limit still 43 percent?" or paste a credit policy and
ask "Screen this against the qualified mortgage thresholds."

The tools accept text and numbers only. Never send names, Social Security or account
numbers, or protected characteristics: the worksheet tools refuse them and the rest
do not need them.

## Skills

- `financial-services`: which of the nine tools to call for which question, and how
  to keep the citations, dates and honesty notes in the answer.
- `setup`: connect, verify and troubleshoot the connection.

## Data

The skills run where Claude runs and send nothing. The connector sends only your tool
inputs to `mcp.contezza.ai`: the text you paste, the numbers you give, a regulation or
topic name. The service processes them for the duration of the call and stores none of
it; see the [privacy policy](https://contezza.ai/privacy.html) for what it logs to
operate. Calls are limited to 60 a minute per session and 600 a minute per address.

**Demonstration notice.** These tools demonstrate what Contezza does. Any demonstration
or sample content they return is labeled as such and is sample data, not actual data
or guidance. Regulatory and program facts are verified against the cited public sources
when published and can change, so check the citation before relying on one. Benchmarks
are historical public aggregates and never a decision about any application. Nothing
here is legal, compliance, credit or business advice.

Part of the [contezza-plugins](https://github.com/contezza-ai/contezza-plugins)
marketplace · [contezza.ai/financial-services.html](https://contezza.ai/financial-services.html) · Support: hello@contezza.ai · Apache-2.0
