---
description: Lint a Contezza Verified Answers feed YAML — structure, statuses, citations, reconciliation rules, review dates
argument-hint: <path/to/feed.yaml>
---

Lint the Verified Answers feed at: $ARGUMENTS

Use the `verified-feed-authoring` skill's rules. Run its lint pass (the
embedded Python) against the file, then go beyond it:

1. Report every lint error with the entry id and the fix.
2. Check `facts` values appear verbatim in the answer text (no rounding or
   paraphrase drift between the machine fields and the prose).
3. For each `needs_reconciliation` entry, confirm the answer text names BOTH
   conflicting figures and that each has its own citation.
4. Flag entries whose `review_by` date is in the past as due for re-verification.
5. Finish with a one-line verdict: entry count, clean/error counts, and
   whether the feed is ready for brand approval.
