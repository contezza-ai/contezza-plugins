---
name: adapter-quickstart
description: Wire the contezza-for-commerce-agents adapter into Anthropic's commerce-agents blueprint — install, point a ShoppingAgent at a Verified Answers feed, and smoke-test the governed backend. Use when setting up a shopping agent on verified merchant data.
---

# Quickstart: verified merchant data under a blueprint shopping agent

The [contezza-for-commerce-agents](https://github.com/contezza-ai/contezza-for-commerce-agents)
adapter is a drop-in `StorefrontBackend` for Anthropic's
[commerce-agents](https://github.com/anthropics/commerce-agents) blueprint. It
serves `search_policies`, `search_products`, and `get_product_details` from a
Verified Answers feed — the same agent, with governed data underneath instead
of crawled pages.

## Setup

```bash
git clone https://github.com/anthropics/commerce-agents.git
git clone https://github.com/contezza-ai/contezza-for-commerce-agents.git
cd commerce-agents && pip install -e .   # or the blueprint's documented install
pip install pyyaml
```

Make both importable (the adapter needs the blueprint's type contracts on
PYTHONPATH — `StorefrontBackend`, `Policy`, `Product`, `ProductDetails`).

## Wire it

```python
import sys
sys.path.insert(0, "path/to/contezza-for-commerce-agents")
from contezza_governed_backend import ContezzaGovernedBackend

backend = ContezzaGovernedBackend.from_feed(
    "path/to/contezza-for-commerce-agents/examples/acme-outdoors.yaml"
)
agent = ShoppingAgent(backend=backend, config=ShoppingAgentConfig(...), client=...)
```

`examples/acme-outdoors.yaml` is a fictional demonstration feed. To serve a
real brand, author a feed with the `verified-feed-authoring` skill and point
`from_feed` at it. Cart, orders, and checkout raise `NotOffered` — wire your
own systems for those or disable them in `ShoppingAgentConfig`.

## Verify

```bash
cd path/to/contezza-for-commerce-agents && python test_smoke.py   # expects: ok
```

Then ask the agent the money questions crawled backends get wrong:

- "What is the restocking fee?" — on the example feed this returns the
  `needs_reconciliation` answer: the brand's FAQ and returns page state
  DIFFERENT fees, and the agent says so explicitly instead of picking one.
  That behavior — disclosed contradiction over confident coin-flip — is the
  point of governed data.
- "How much is the Summit Tent?" — returns the full price range by variant,
  not a single flattened number.

## Behavior guarantees you inherit

- Policy answers are the brand's approved canonical text, served with citations.
- Unreconciled contradictions between the brand's own pages are stated, never
  silently resolved.
- Feed entries carry source anchors that are re-verified on schedule; an entry
  whose anchor disappears flags stale before it can mislead a shopper.

Docs: https://contezza.ai/agents.html · hello@contezza.ai
