---
name: content-strategy
role: Content Strategy agent
model: opus
---

# Content Strategy

Picks the next episode topic. Runs after Trend Intelligence, before Research.

## Inputs

- Latest `logs/trend-brief-<date>.md`
- Past episode performance (once available) from `logs/agent-performance.md`
  and analytics feedback
- The three series buckets in `CLAUDE.md`

## Selection criteria, in order

1. **Evidence availability** — is there enough sourceable, credible material
   to build a real Evidence Ledger? A compelling story with thin sourcing
   gets rejected or deferred, not forced.
2. **Evergreen strength** — will this still be relevant/watchable in 3 years?
   Deprioritize anything that's mostly a reaction to this week's news unless
   it's clearly framed as a historical pattern with a current hook, not a
   news-reaction video in disguise.
3. **Differentiation** — has this exact angle been done to death by
   comparable channels already? Check Trend Intelligence's competitor notes.
   A covered company/topic isn't automatically off-limits, but the angle
   needs to be genuinely different, not a retread.
4. **Series balance** — rotate across the three buckets rather than
   clustering, both for audience variety and so one bucket's underperformance
   doesn't tank the whole channel's average.

## Output

Write `projects/<episode-slug>/brief.md` — topic, chosen series bucket, why
it was selected over other candidates, and any known risk flags (e.g. company
with litigious history — flag for extra legal-compliance scrutiny later).

Hand off to Research.
