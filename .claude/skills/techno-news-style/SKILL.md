# techno-news-style

## Description
Writes video scripts about AI, crypto, and tech news in the channel's voice: not "what happened" but
"why this was released, who benefits, how it fits the bigger picture." Produces the actual narration —
digest episodes, deep dives on one event, or thematic series.

## Relationship to `podcast-research`

Don't duplicate that skill's analysis machinery. Two ways this runs:

- **Research already done:** the user hands you a `podcast-research` brief (or you just produced one this
  session). Skip straight to Step 3 (script assembly) — the actors/claims/ecosystem work is already there.
- **Raw topic/news, no prior research:** do a *lighter* version of Step 1 yourself (a person's worth of
  WebSearch, not a full brief) — enough to write an honest script, not a research document. If the topic
  is genuinely dense (a single complex event worth real digging), say so and suggest running
  `podcast-research` on it first rather than half-assing the research inline.

## When to activate

- "напиши сценарий на канал", "сделай техно-дайджест", "разбери эту новость для видео", "weekly ai news"
- User hands over a `podcast-research` brief and asks for the script version of it.

## Step 1 — Pick the format

- **Digest** (3–5 items, weekly cadence): condensed treatment per item, see template below.
- **Deep dive** (one event, one episode): full treatment, all sections.
- **Thematic series** (a throughline across several events — "гонка ИИ-моделей", "крипта как инфраструктура для ИИ"): frame around the theme, individual events become supporting evidence rather than standalone sections.

If unclear which, ask rather than guessing scope.

## Step 2 — Research (only if not already done)

For each item: what happened (dates, numbers, official statements — facts only, no spin), who's involved,
what's the immediate context (product launch, funding round, conference, scandal).

**Known-person check** — same mechanism as `podcast-research`: for any named figure (Jensen Huang, Sam
Altman, CZ, etc.), check `техно/knowledge/people/<slug>.md`. If a profile exists, use its "Известные
паттерны поведения" to ground the "зачем" section in something more specific than generic incentive
reasoning — e.g. knowing Bill Gates has had zero operational role in Microsoft's AI strategy for 20 years
changes how you'd frame a headline that implies otherwise. If the source contradicts the known pattern,
that contradiction is itself worth a line in the script, not something to smooth over.

## Step 3 — Run through the 5 principles (internal reasoning, not spoken labels)

These structure *how you think about* the material. They don't appear as headers or spoken phrases in the
final script — see Style below for how that plays out in the actual words.

1. **Intent-first** — why was this released now? What does the releasing party want changed (capital,
   attention, competitive positioning, regulatory posture)?
2. **Multi-perspective** — company, investors, developers/builders, end users, regulators. Not all five
   apply to every story; use the ones that carry real weight for this particular item.
3. **Facts vs. interpretation vs. hype vs. fake** — sort claims before writing. This sorting shapes word
   choice and hedging later; it is not something the viewer hears named.
4. **Ecosystem connections** — how does this link to the same actor's prior moves, to competitors, to the
   broader trend (model race, regulatory push, capital flows, US-China dynamics)?
5. **Practical takeaway** — what should an investor / builder / regular user actually watch or do
   differently because of this?

## Step 4 — Assemble the script

### Deep-dive template (with timecodes as a guide, not a rigid clock)

1. **Hook** (0:00–0:40) — one sharp claim or question. "Почему этот анонс — не про технологии, а про
   деньги?" Not a teaser that oversells what follows.
2. **What happened** (0:40–2:30) — facts only: dates, numbers, official statements. No interpretation yet.
3. **Why now** (2:30–6:00) — intent-first reasoning: who benefits, what narrative they're pushing, what
   they need this to accomplish.
4. **Multi-perspective breakdown** (6:00–12:00) — walk the angles that matter for this story.
5. **Ecosystem link** (12:00–16:00) — connect to prior moves, competitors, the larger trend.
6. **What's solid vs. overstated** (16:00–20:00) — the calibration pass. Say plainly what's backed by
   evidence and what's marketing framing — through word choice and specificity, not through announcing
   "this part is hype."
7. **Practical takeaways** (20:00–22:00) — per audience: investor, builder, user.
8. **Close** (22:00–23:00) — brief recap, one line pointing at what to watch next.

### Digest template (per item, condensed)

What happened (1–2 sentences) → why now / who benefits (1–2 sentences) → one thing that's overstated or
still unverified (1 sentence) → ecosystem note if it's non-obvious (optional, 1 sentence).

End the digest with: top 2–3 themes of the period, 1–2 under-discussed signals, 1–2 over-hyped stories,
and — if this is genuinely useful, not filler — a couple of content angle ideas for follow-up videos.

## Style

- Calm, analytical, not sensational. No "you won't believe," no fake urgency.
- Explain jargon briefly on first use; don't assume the viewer already knows every acronym.
- Hedge honestly where the evidence is thin: "скорее всего," "судя по всему," "если это подтвердится" —
  not as filler on every sentence, but where genuine uncertainty exists.
- Never say "это факт" / "это хайп" / "это интерпретация" out loud. The fact/hype distinction from Step 3
  should be legible from *how* something is described — specific numbers and sourcing read as solid;
  vague superlatives and unverified projections read as hype — not from a label glued onto the sentence.
- Chapter the deep-dive script clearly (even just as script section markers) so it works as a navigable
  reference, not only a linear watch — viewers should be able to find "the NVIDIA bit" without scrubbing.
- Position: a guide helping the viewer build a map of the ecosystem, not a hype man and not a debunker
  performing contrarianism for its own sake.

## Before delivering: checklist

- Did every item get the intent-first question, not just a recap of the announcement?
- Is there at least one concrete practical takeaway, not just "interesting to watch"?
- Did a named actor with a `техно/knowledge/people/` profile get checked against it — and does the script
  reflect that (or flag a contradiction) rather than ignore it?
- Any claim stated as settled fact that was actually only claimed by an interested party? Reword as
  attributed claim, not narrator's own assertion.
- Read the hook back — does it oversell relative to what the rest of the script actually supports?
