---
name: financial-services
description: Answer US lending, mortgage, commercial credit, regulatory and model-risk questions with Contezza AI for Financial Services' cited tools. Use when the user asks about QM, ATR, Regulation B, Regulation Z or TRID, HMDA, capital rules, SR 26-2 model risk guidance, pastes a credit policy or lending document to check, gives numbers for a mortgage or commercial loan, or shares a rent roll.
---

# Financial services tools (connector `contezza-financial-services`)

Nine deterministic, read-only tools over anchor-verified public sources. Every answer
carries citations, effective dates and a note that it is not legal, compliance or credit
advice. The service processes only the text and numbers sent in the call and stores
nothing. Never send names, Social Security or account numbers, or protected
characteristics: the worksheet tools refuse them, and the rest do not need them.

## Pick the tool from the question

| The user wants | Call | Notes |
|---|---|---|
| A regulatory fact or threshold, or the coverage index | `lookup_regulatory_facts` | No arguments returns the coverage index. Superseded rules come back as dated history: say so. |
| Facts pulled out of a pasted document | `extract_lending_facts` | One text, or up to five labeled documents of 200,000 characters each. Returns a fact packet the other tools accept. |
| Two lending texts or packets compared | `check_lending_policy_consistency` | Returns the mismatched figures with excerpts. |
| A policy screened against a regulation | `screen_policy_against_regulation` | Takes a packet or a policy text plus the regulation. Flags retired thresholds still in the policy. |
| Model risk management actions | `get_model_risk_checklist` | SR 26-2, which supersedes SR 11-7; an area filter is optional. The AI and LLM area is labeled derived guidance. |
| How an application compares to public outcomes | `benchmark_mortgage_application` | HMDA public data, aggregates only, historical. Never a prediction or a decision. |
| A mortgage pre-submission worksheet | `compute_prequal_worksheet` | Numbers-only profile. Not a credit decision or a substitute for DU, LPA or TOTAL. |
| A commercial loan spread and screens | `compute_commercial_worksheet` | Numbers-only financials and loan terms. Analysis with stated assumptions. |
| A rent roll turned into NOI, occupancy and rollover | `analyze_rent_roll` | Tenants anonymized as T1..Tn. |

## How to present results

1. Lead with the answer, then the citation and effective date for each fact.
2. Keep the tool's honesty notes in your reply: superseded, derived, historical, not a
   decision. Do not soften them.
3. When a user attaches a document, pass its text to `extract_lending_facts` and reuse
   the returned packet for later calls instead of re-sending the document.
4. If the question is about the user's own organization's policies or loan book, say
   that this connector answers from public sources only. Checks over an organization's
   own documents are a separate Contezza service described at
   contezza.ai/financial-services.html.
5. If the connector is not available, follow the `setup` skill.
6. State the demonstration notice whenever it applies: any demonstration or sample
   content is labeled as such and is sample data, not actual data or guidance, never to
   be read as real records, outcomes or advice. Regulatory facts are verified against
   the cited public sources when published and can change, so the citation is the
   thing to rely on, not the summary. Benchmarks are historical public aggregates,
   never a decision about an application.
