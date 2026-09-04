---
name: verified-feed-authoring
description: Author and validate a Contezza Verified Answers feed (YAML) for a merchant brand — entry structure, citation anchors, contradiction handling, and a lint pass. Use when creating or editing a verified-answer feed, or when asked to make merchant content agent-ready.
---

# Authoring a Verified Answers feed

A Verified Answers (VA) feed is the governed data source AI agents read instead
of crawling merchant pages. Every entry is a brand-approved answer with
citations back to the brand's own published pages. The
[contezza-for-commerce-agents](https://github.com/contezza-ai/contezza-for-commerce-agents)
adapter serves a feed like this to Anthropic's commerce-agents blueprint;
Contezza serves approved feeds to assistants over MCP.

## Feed shape

```yaml
brand: "Acme Outdoors"          # display name
tenant: acme-outdoors           # stable slug
catalog:                        # products the agent may search
  - product_id: summit-tent-4p
    title: "Summit Tent (4-person)"
    price: 499.0
    description: "Acme's flagship four-person tent. $499-$649 by fabric option."
    specs: {fabric: "ripstop canvas", price_range: "$499-$649 by fabric"}
entries:                        # the verified answers
  - id: policy.returns.window   # namespaced: policy.* / product.* / shipping.*
    topics: [returns]
    intents: ["How long do I have to return?", "return window"]
    status: verified            # verified | needs_reconciliation | draft | stale
    answer:
      text: "You have 30 days from delivery to initiate a return. Items must be unused and in original packaging."
      facts: {window_days: 30}
    citations:
      - url: "https://example.com/acme/returns"
        anchor: "within 30 days of delivery"   # exact text on the cited page
    lifecycle: {version: 1, approved_by: brand-admin, review_by: "2027-01-01"}
```

## Authoring rules (each one is load-bearing)

1. **Answers are canonical text, not summaries.** Write the answer the brand
   wants an agent to say, verbatim-servable. Numbers appear exactly as the
   brand states them; never round, never approximate.
2. **Every entry cites the page that proves it**, and `anchor` is an exact
   substring of that live page. Anchors make entries self-verifying: when the
   page changes and the anchor disappears, the entry is flagged stale before
   an agent repeats it.
3. **Contradictions are stated, never resolved silently.** When two of the
   brand's own pages disagree (an FAQ says one fee, the returns page another),
   the entry gets `status: needs_reconciliation`, an answer that names BOTH
   figures and both sources, and a citation for each. The brand resolves the
   contradiction on its pages; the feed reports the truth until then.
4. **`facts` carries the machine-readable values** the prose states — one key
   per figure. Agents and validators read these; keep them in sync with the
   text.
5. **`intents` are real shopper phrasings** (2-5 per entry) — they drive
   retrieval. Write them the way shoppers ask, not the way policies are titled.
6. **`review_by` is mandatory.** An entry without a review date is an entry
   that will silently go stale.

## Lint pass

Run this over any feed before shipping it:

```python
import sys, yaml
feed = yaml.safe_load(open(sys.argv[1]))
errs = []
ids = set()
for e in feed.get("entries", []):
    eid = e.get("id", "<missing id>")
    if eid in ids: errs.append(f"{eid}: duplicate id")
    ids.add(eid)
    if e.get("status") not in ("verified", "needs_reconciliation", "draft", "stale"):
        errs.append(f"{eid}: bad status {e.get('status')!r}")
    if not e.get("intents"): errs.append(f"{eid}: no intents")
    if not (e.get("answer") or {}).get("text"): errs.append(f"{eid}: empty answer")
    if not e.get("citations"): errs.append(f"{eid}: no citations")
    for c in e.get("citations", []):
        if not c.get("url") or not c.get("anchor"):
            errs.append(f"{eid}: citation missing url/anchor")
    if e.get("status") == "needs_reconciliation" and len(e.get("citations", [])) < 2:
        errs.append(f"{eid}: needs_reconciliation requires a citation per conflicting source")
    if not (e.get("lifecycle") or {}).get("review_by"):
        errs.append(f"{eid}: no lifecycle.review_by")
print("\n".join(errs) or f"ok — {len(ids)} entries clean")
sys.exit(1 if errs else 0)
```

Beyond the lint, verify each anchor manually or by fetching the cited page —
an anchor that is not literally on the page is a broken verification chain.

## Workflow

1. Inventory the brand's money-fact surfaces: FAQ, returns, warranty,
   shipping, product pages. These are where audits find contradictions.
2. Draft one entry per shopper question; start from the questions agents get
   wrong (fees, warranty terms, price ranges, differentiators).
3. Where surfaces disagree, write the `needs_reconciliation` entry first —
   those are the entries that save the brand from coin-flip answers.
4. Lint, verify anchors, then hand the feed to the brand for approval
   (`approved_by`); only approved entries ship as `verified`.
5. Serve it: locally via the adapter (see the adapter-quickstart skill), or
   through Contezza's hosted layer (https://contezza.ai).
