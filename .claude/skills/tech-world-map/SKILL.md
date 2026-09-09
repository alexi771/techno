# tech-world-map

## Description
Maintains a living map of who's aligned with whom in the AI/tech/crypto world — not company org
charts, but the actual incentive-driven camps: who benefits from more regulation, who benefits from
less, whose rivalry is personal vs ideological vs commercial, and which alliances are real vs assumed
from a shared quote or a single news cycle.

This is a **standing knowledge artifact**, not a one-off analysis. The map lives at
`техно/knowledge/tech-world-map.md` and gets updated incrementally as new events test or confirm
existing placements — it is never fully rewritten from scratch.

## Why this exists

A pasted "4-quadrant camp map" is an easy shape to produce and a genuinely useful mental model when
it's right — but it's also the easiest place to smuggle in unverified conclusions, because it *feels*
like analysis while actually just repeating a viral framing. This skill exists to keep the map honest:
every placement on it must trace back to a specific action, statement, or financial relationship — not
vibes, not "he seems like that type."

## When to activate

- User shares a news item and wants to know "who benefits" / "which camp does this fit."
- Adding a new event to the map, or checking whether an existing placement still holds.
- Before writing a script/analysis that assumes a camp alignment — check the map first instead of
  re-deriving alliances from scratch each time.

## Core rule: verify before placing, and re-verify before reusing

Never adopt a pasted or remembered "camp" framing at face value, including ones from a previous session
of this same map. For every actor being placed or moved:

1. **What's the specific evidence?** A quote, a vote, a filing, an investment, a lawsuit, a hire/fire —
   not "he seems aligned with X because he was in the news with them once."
2. **Is this actor's position actually consistent, or does the pasted framing average together several
   different things?** (Classic failure mode: someone's *personal rivalry* with another founder gets
   relabeled as an *ideological* stance because it's a cleaner story. Check `elon-musk.md` for a live
   example — OpenAI rivalry, xAI competition, and libertarian-ish politics are three different vectors
   that a lazy map collapses into one "camp.")
3. **Who benefits materially from this actor's stated position, regardless of their stated reason?**
   Apply the actors-incentives-constraints model from `journalist-investigator` here — see that skill,
   don't restate it.
4. **What would the opposite camp say about the same facts?** If a "regulatory capture benefits
   incumbents" argument is being made, that's a real and common critique — but it's an *interpretation*
   of motive, not a fact, and must be labeled as such on the map, not stated flatly.

## Map structure (`техно/knowledge/tech-world-map.md`)

```
# Tech World Map

## Axes currently tracked
Short description of each active axis (e.g. "AI regulation: more oversight <-> less oversight"),
added only when a real, recurring fault line shows up — don't invent axes preemptively.

## Actors
### <Name>
- Position on axis: <camp>, with the specific evidence (quote/date/source) that puts them there.
- Known cross-camp complications: cases where this actor doesn't fit the camp cleanly.
- Known-person profile: техно/knowledge/people/<slug>.md (if one exists — check known behavioral
  patterns before placing).

## Events log
Reverse-chronological. Each entry: date, what happened, which actors it touched, what changed (or
was confirmed) about the map, fact/interpretation/unverified tags on each claim.
```

## Workflow when adding an event

1. **Verify the triggering claim first** — if a pasted analysis says "X published Y," check that X
   actually published Y, on the date claimed, saying roughly what's claimed. Don't build interpretation
   on top of an unverified premise.
2. **Separate fact from the pasted analysis's interpretation.** Rewrite in your own words — per this
   channel's standing rule, don't adopt someone else's framing verbatim even when the underlying facts
   check out. A correct fact wrapped in a sloppy "camps" narrative still needs the narrative rebuilt.
3. **Check existing actor entries** in the map before adding new placements — does this event confirm,
   complicate, or contradict where an actor already sits?
4. **Update the map file** — add/update actor entries, append to the events log, tag each interpretive
   claim (motive, "who benefits," alliance strength) as interpretation, not fact.
5. **Flag when the clean-camp framing breaks down.** A map that forces every actor into exactly one of
   two boxes is usually lying by omission. It's fine — better — for the map to say "this doesn't fit
   either camp cleanly, here's why."

## Style

Same calibration as the other channel skills: state confidence levels plainly, keep fact and
interpretation typographically distinct (e.g. **Факт:** / **Интерпретация:** / **Неподтверждено:**
prefixes in the map file itself), and prefer "the evidence for this alliance is thin" over silently
dropping a placement that doesn't hold up.
