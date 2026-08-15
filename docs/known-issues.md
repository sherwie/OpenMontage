# Known Issues

Cross-cutting gaps found during production that are worth fixing at the
schema/skill level, not just patching per-episode. Entries here should be
resolved by editing the referenced schema/skill directly when someone picks
them up — this file is a queue, not a permanent home for the fix.

## `scene_plan.schema.json` has no layer/compositing concept

**Found**: 2026-08-15, business-history-documentary channel,
`live-nation-ticketmaster-monopoly` episode, Storyboard stage.

**The gap**: `schemas/artifacts/scene_plan.schema.json` models `scenes[]` as
a flat, implicitly-sequential list. Every scene has `start_seconds`/
`end_seconds`, but there is no field expressing that one scene composites on
top of another (e.g. a `text_card` overlay appearing over continuous `broll`
footage) versus replacing it (a hard cut to a different shot). There's also
no z-order/layer/track concept at all.

**Why this recurs, not just here**: `pipelines/documentary-montage/scene-
director.md` and the explainer-style script directors both produce
`enhancement_cues`/slot lists that frequently use the word "overlay" for
exactly this relationship (a quote card, stat card, or label appearing over
footage that keeps rolling underneath). Any scene planner that translates
those cues into `scene_plan.schema.json`'s flat scene list will hit the same
lossy translation this episode did: "overlay" cues collapse into scenes that
read as competing, exclusive-slot cutaways unless the author manually
compensates (as this episode did, after the gap was caught — see its
`decision_log.md` for the full before/after). Nothing in the schema or the
scene-director skill currently prevents this from recurring on every future
narration-led episode across any pipeline that reuses this schema.

**Concrete symptom this produces**: computing "real-footage coverage by
time" from a scene_plan built without manual compensation undercounts
footage severely — in this episode's case, an initial naive build measured
2.4% real-footage coverage by time, when the intended design was closer to
continuous footage under nearly the entire runtime with graphics overlaid on
top.

**Suggested fix** (not implemented here — flagged for whoever picks this up,
since it's a shared schema affecting every pipeline that uses it, out of
scope for a single episode's production work): add an optional field to each
scene object — something like `compositing: {"mode": "cutaway" | "overlay",
"base_scene_id": "<id>"}` — so a scene planner can express "this text_card
overlays on top of `<base_scene_id>`" structurally, and downstream tooling
(coverage calculators, the Edit/Compose stages, the Backlot board) can
compute real-footage-time correctly without every scene planner having to
reinvent the same manual workaround this episode used (duplicate per-section
base-layer `broll` scenes spanning the full section, with graphic scenes
carrying a free-text `overlay_notes` explanation instead of a structured
reference).

**Workaround used in the interim** (this episode, and reusable elsewhere
until the schema is fixed): one `broll` scene per section spanning that
section's full `start_seconds`–`end_seconds`, with all graphic-type scenes
inside that window marked via the existing free-text `overlay_notes` field
explaining what they composite over. Functional, but relies on prose
convention rather than a field a script can check.
