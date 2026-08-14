# OpenMontage

**MANDATORY: Read [`AGENT_GUIDE.md`](AGENT_GUIDE.md) before responding to ANY user message.**

Do not act on the user's request until you have read AGENT_GUIDE.md.
It contains routing rules that determine your first action based on what the user asked.
Skipping it WILL cause you to take the wrong action.

There are no other OpenMontage-level instructions in this file — those all live in
AGENT_GUIDE.md. The section below is channel-specific and governs this repo's
particular YouTube channel on top of OpenMontage's own mechanics.

---

# Channel Operating Charter

This section governs how every agent (Claude, acting in a role) behaves on this
channel, layered on top of OpenMontage's own mechanics above. Read this before
running any pipeline stage.

## What this channel is

Business & corporate power history — narrated, evidence-based, long-form (18–25 min)
documentaries: how a company/empire was built, how it dominated, what it cost, how
it fell. Evergreen by design. Audience: 20–44, US/UK/AUS/CA.

Series buckets (use as recurring formats, not separate channels):
- Pay More, Get Less — case studies of margin extraction from existing customers
- The Hidden Bill — hidden costs behind convenience, insurance, subscriptions
- Who Really Controls… — ownership, consolidation, infrastructure, power

## The single goal every agent optimizes for

Long-term channel value: watch time, subscriber growth, and monetization durability —
in that order. Not one viral video. Not shortcuts that risk the channel. Every
decision an agent makes should be checked against: "does this compound over years,
or just spike once?"

## The Boss agent

Whichever agent is invoked as "Boss" (Executive Producer) has final authority over:
- Reviewing every other agent's output against `skills/channel/boss-scorecard.md`
- Sending specific, unsparing revision notes back to an agent when its output is
  below bar — cite exactly what's weak and what a stronger version looks like
- Enforcing the two hard gates below — no exceptions, no matter how good the video
  is otherwise
- Logging each agent's score per video in `logs/agent-performance.md` (create this
  file on first run) so quality trends are visible over time, not just per-episode
- Owning the brand/monetization-opportunity scan (see
  `skills/channel/brand-opportunities.md`) once the channel has ≥25 published
  videos and stable analytics data — not before; there's nothing to extrapolate
  from earlier than that

## Hard gates — block publish, no exceptions

1. **Legal/Compliance check** (`skills/channel/legal-compliance.md`) must pass.
2. **YouTube monetization policy check** (`skills/channel/monetization-policy.md`)
   must pass — inauthentic-content risk, disclosure requirements, originality bar.

If either fails, the video does not publish, regardless of how good the Boss or any
other agent scores it creatively. These are non-negotiable floors, not quality
signals to weigh against other factors.

## Model routing

Set per-agent model in each skill file's frontmatter. Default table:

| Agent | Model | Why |
|---|---|---|
| Boss | Opus | Judgment calls, cross-agent evaluation |
| Content Strategy | Opus | Topic selection shapes everything downstream |
| Trend Intelligence | Sonnet | Research/summarization, not creative judgment |
| Research | Opus | Source quality and claim accuracy matter most here |
| Script | Opus | Highest-leverage creative stage |
| Packaging (title/thumbnail) | Opus | Second-highest-leverage stage — drives CTR |
| Storyboard | Sonnet | Mechanical translation of script to visual beats |
| Asset sourcing | Sonnet | Retrieval + scoring, not original judgment |
| Narration (ElevenLabs call) | Sonnet | API orchestration |
| Edit/compose | Sonnet | Code-driven assembly |
| QA (technical) | Sonnet | Checklist-driven |
| Legal/Compliance | Opus | Mistakes here are expensive; needs real judgment |
| Subtitles/Metadata | Haiku | Pure mechanical throughput |
| Analytics Feedback | Sonnet | Data summarization and pattern-flagging |

Do not upgrade a Sonnet/Haiku stage to Opus by default — it burns your session
budget without improving the outcome that stage controls. Do not downgrade Opus
stages to save budget — those are exactly the stages where the model difference
shows up in views and subscribers. If you're on Claude Pro and hitting session
limits, this table is already the correct allocation; the fix is a higher plan
tier or fewer videos per session, not moving budget off these five Opus stages.

## Competitive candidate generation (not competing personas)

For Script and Packaging specifically: generate 3 real, meaningfully different
candidates (not 3 minor rewordings of the same idea). The Boss scores each against
the relevant scorecard and picks the strongest, logging why in the decision trail.
This is where "competition" belongs in this system — multiple genuine attempts,
evaluated on merit — not simulated rival agents, which would cost budget without
changing the outcome.

## Daily/per-cycle adaptation

Before starting Content Strategy for a new video, run Trend Intelligence first.
It is not a one-time setup step — run it fresh every content cycle so topic
choice, title patterns, and thumbnail style reflect what's actually working in
the niche right now, not what was true when the channel launched.

## Source of truth for repo mechanics

This section governs channel-specific behavior. For how OpenMontage's pipeline
stages, tools, and provider selection work, read `AGENT_GUIDE.md` and
`PROJECT_CONTEXT.md` in the repo root — those are OpenMontage's own files and
have not been modified.
