# bio-research

## Description
Research and verification skill for building/upgrading a single person's profile in
`техно/knowledge/people/<slug>.md`. Where `podcast-research` digs into one piece of content,
this skill digs into one *person* across their whole public record — and treats source
tiering and cross-checking as first-class steps, not an afterthought.

Inspired by how serious biographical research separates "the subject talking about themselves"
from "someone else's record of the subject" from "someone checking whether those two agree"
(see e.g. github.com/moradology/arday-research for one public example of that structure) —
adapted here for a tech/crypto/AI figure profile, not copied wholesale.

## When to activate

- Building a new `техно/knowledge/people/<slug>.md` profile from scratch.
- Upgrading an existing profile that only has a thin/single-source bio.
- User asks to "прогони био" / "проверь биографию" / "обнови карточку" for a tracked person.

Not for quick one-off fact lookups ("when was X born") — just answer those directly.

## Step 1 — Source tiers (gather before writing)

Don't blend everything into one undifferentiated pile of facts. Pull from each tier that's
actually available, and keep track of which tier each fact came from — that tracking is what
makes Step 2 possible.

1. **First-person primary** — memoir/autobiography, long interviews/podcasts where the subject
   speaks in their own words, official bio pages they control, direct social-media statements.
   Rich detail, but self-serving by construction: flattering framing, omitted failures,
   rounded-up numbers.
2. **Institutional record** — company filings, university records, patents, court records,
   regulatory filings, official press releases from organizations they're affiliated with.
   Harder to fake, but narrow — tells you dates and titles, not motives.
3. **Scholarly & investigative journalism** — profiles, investigations, and fact-checked
   reporting from outlets with an editorial/correction process. This is where disputed claims
   usually first get surfaced.
4. **Corrections & disputes** — published corrections, retractions, or documented factual
   disputes about *this specific person's* public claims (a wrong founding date, an inflated
   title, a disputed timeline). If none are found, say so explicitly rather than leaving the
   section out silently — "no known disputes found" is itself information.
5. **Independent cross-checks** — anyone who has compared the subject's own account against
   tiers 2-3 and flagged mismatches (a journalist noting a resume claim doesn't match public
   filings, etc). Distinct from tier 3 because the point here specifically is comparison, not
   just reporting.

If a tier has nothing findable, don't pad it — move on. A profile built entirely from tier 1
is a red flag worth noting in the profile itself (means everything is self-reported).

## Step 2 — Cross-check, don't silently pick a winner

When two sources disagree on a fact (birth year, founding story, a quote's wording, who did
what first), do not just choose the one that sounds more authoritative and drop the other.
Record the disagreement:

- What each source says.
- Which tier each source belongs to (a tier-2 filing beats a tier-1 self-report on a date;
  a tier-1 quote beats a tier-3 paraphrase of that same quote).
- Whether it's resolvable now or stays open.

This becomes the profile's **Расхождения между источниками** section — only include it when
something was actually found; don't manufacture a section for the sake of the template.

## Step 3 — Write/update the profile

Keep the existing file shape used across `техно/knowledge/people/*.md` — don't reinvent it per
person:

```
# <Name>

<one-line role/company summary>

## Краткая биография
- bullets, **bold** field labels (rendition/education/family/etc.)

## Чем занимается сейчас
narrative section, most-recent-relevant activity

## Расхождения между источниками   <- only if Step 2 found something
- what disagrees, which sources, which tier, resolved or open

## Известные паттерны поведения (для сверки новостей)
- behavioral patterns useful for sanity-checking future news about this person
  (see podcast-research / techno-news-style — this section is what those skills read)

## Источники
- group by tier if there are 5+ sources; otherwise a flat list is fine
- [label](url)

*Собрано агентом в сессии <date>, актуальность бизнес-фактов проверять на дату использования.*
```

When upgrading an existing profile: preserve what's already correct, add what's missing,
don't rewrite sections that don't need it. If the existing profile only drew on tier-1/thin
sources, that's exactly the case this skill exists to fix — prioritize tiers 2-4 on the
upgrade pass.

## Step 4 — Known-person check stays intact

This profile *is* the known-person check that `podcast-research` and `techno-news-style` read
from. Don't weaken the "Известные паттерны поведения" section while upgrading everything
else around it — if anything, sharpen it using what Steps 1-2 turned up.

## Style

Same calibration as the other channel skills: state uncertainty plainly ("disputed",
"self-reported, unverified elsewhere") rather than smoothing disagreements into a single
confident narrative. A profile that admits what it doesn't know is more useful downstream
than one that reads clean but is built on one flattering source.
