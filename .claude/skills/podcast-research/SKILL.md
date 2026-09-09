# podcast-research

## Description
Research skill for podcasts, interviews, and long-form content about AI, crypto, and tech.
Turns a source into a compact, evidence-graded brief: what was claimed, by whom, why now, who benefits, what's verified vs not.

This is an **upstream research step**, not a script writer. Its output feeds into script writing
(see the `techno-news-style` skill, when it exists) — it does not itself produce narration.

## When to activate

- User gives a URL/transcript/topic and asks to "разбери", "проверь", "сделай бриф".
- User asks for a weekly/periodic scan of AI+crypto+tech sources.
- User is prepping their own interview and wants to see what's already been asked/claimed.

Do **not** run the full workflow for a simple "что там вкратце" — give a plain 3–5 sentence summary instead. This skill is for when the user wants depth, not every time a URL appears.

## Step 0 — Source legitimacy gate (always first, non-skippable)

Before analyzing content, spend one paragraph on the source itself:
- Who publishes this — a known outlet/creator with a track record, or unknown/anonymous?
- Any tells of fabrication: composite/anonymous anecdotes presented as real, no verifiable named sources, generic "best practices" with no citations, an SEO-farm-shaped domain?
- If the source looks like filler/content-farm material (this has happened before — see the thenarrativepost.com / infostreamglobal.com case), say so explicitly and either stop or clearly mark everything downstream as low-confidence. Do not let a confident tone substitute for a track record.

This gate is cheap (a few sentences) and prevents building an elaborate analysis on a source that shouldn't have earned it.

## Step 1 — Pick a depth tier

Don't default to maximum depth. Match effort to what was asked:

- **Quick take** (weekly digest item, or user just wants the gist): 2–3 sentences on what happened + who benefits + one thing to verify. No table, no full actor map.
- **Deep dive** (user picked one specific episode/interview to actually dig into): full analysis below.
- **Interview prep** (user is about to interview someone and wants prior-art): skip narrative/ecosystem sections, go straight to "what's already been asked" + "what's still open."

If unsure which tier, ask — don't guess and over-deliver.

## Step 2 — Transcript / content access (be honest about limits)

- If a written transcript, recap article, or detailed coverage exists, use it via web search.
- If only a video/audio exists with no accessible text, **say so explicitly**: "no transcript available, analysis is based on the description/coverage only" — never invent quotes or claim to have watched something you only found a title for.
- Prefer primary material (the episode page, official show notes) over secondary recaps when both exist.

**Getting raw text off a YouTube source — in this order:**

1. **Check for an official transcript page first** (e.g. `lexfridman.com/<slug>-transcript` — Lex Fridman publishes these; other shows have similar patterns). If it exists, use it directly — it's clean, complete, and free.
2. **Pull YouTube's own auto-captions before transcribing anything locally**: `yt-dlp --write-auto-sub --skip-download <url>`. Ten seconds, free, no service, works regardless of video length — this has no memory ceiling because it isn't running a model, just downloading captions YouTube already generated. This should be the default first move for any YouTube source, long or short.
3. **Only fall back to local Whisper transcription (mcp-transcribe)** when auto-captions genuinely don't exist. Know its limit: it downloads full audio and transcribes locally, which runs out of memory on very long single files (a 2h26m episode failed outright — the base model choked on the raw audio array). It's fine for anything up to roughly 30-60 minutes; for longer files either rely on step 2 instead, or accept that a full local transcription isn't feasible without chunking the audio first (not currently automated here).
4. **For interactively exploring a long interview** rather than extracting full raw text (e.g. "what does he say about X," jump straight to a topic) — NotebookLM is a solid free option: paste the YouTube link directly (natively supported), answers come with footnotes linking to the actual timecode in the transcript, zero setup. Real limitation: it only processes the spoken/text transcript, not on-screen visuals — irrelevant for a straight interview, but a problem for a talk built around slides.

**Always save the full transcript to the repo before condensing it.** The sheet's "текст" cell has a hard size limit (Google Sheets caps a cell at 50,000 characters), so anything longer — a real interview transcript routinely runs 90,000-330,000 characters — cannot fit whole. What goes into the sheet is a dense paraphrase; the paraphrase is lossy by construction. Before writing that paraphrase anywhere, save the actual full transcript text to `техно/knowledge/transcripts/<person-slug>_<episode-slug>_<video-id>.txt`, with a short header (source title, URL, extraction method, date) prepended. This is what lets anyone come back later and re-derive a different angle, check a quote, or catch something the first pass missed — without redoing the extraction. Never leave the full transcript sitting only in a scratch/temp directory; scratch is for intermediate working files, not the source of record.

## Step 3 — Analysis core (deep dive only)

Uses the actors-incentives-constraints and timeline-tagging model from `journalist-investigator` — see that
skill for the full definitions. Below is the podcast/interview-specific application of it, not a
restatement:

**Actors & incentives** — for each actor mentioned (guest, host, their companies, backers, competitors): what do they want from this appearance, what do they gain if their framing wins, what would they lose by being more honest, what's undisclosed (sponsorship, investment, hiring).

*Known-person check:* for any named actor, look for a matching profile in `техно/knowledge/people/<slug>.md` (slug = lowercase-hyphenated name, e.g. `elon-musk.md`). If one exists:
- Use its "Известные паттерны поведения" section to sanity-check what's being claimed in this source — does this news fit the person's established pattern, or does it contradict it? A contradiction isn't automatically wrong, but it's worth flagging as needing extra verification rather than taken at face value.
- If the source attributes a decision/statement to someone whose profile notes they're no longer operationally involved (e.g. Bill Gates and Microsoft product strategy, Zhang Yiming and ByteDance day-to-day) treat that attribution as a red flag until confirmed.
- If no profile exists for a named actor who recurs across multiple analyses, that's a signal this knowledge base should grow — mention it in the bottom line so the user knows who's worth adding next.
- The knowledge base is a starting point, not a ceiling: its bios were compiled once and go stale. Treat it as prior context to check *against* fresh reporting, never as a substitute for actually verifying what the source under analysis claims.

**Claims & evidence** — for each load-bearing claim: what's the evidence (data/docs/on-chain vs "trust me"), does it match independent sources, has this person made similar claims before and what happened, what's conspicuously not discussed.

**Narrative** — the 1–2 dominant stories being told, who they serve, what they assume, what a competing narrative would say instead.

**Ecosystem link** — how this connects to this guest's/company's prior statements, to competitors, to the broader trend it's riding (model race, regulation, capital flows). One paragraph, not a diagram, unless the connections are genuinely tangled.

**Open questions** — 8–12 non-redundant questions, split only by *who they're for* (guest / competitor / investor / user), not by six overlapping thematic buckets. Every question should fail a "haven't I basically asked this already in Actors & incentives?" check before it makes the list.

No fixed quota. If a 10-minute clip only supports 4 good questions, list 4.

## Output format

**Quick take:** 2–4 sentences, plain prose, no headers.

**Deep dive:**
1. What it is (show, guest, date, why released now) — 2–3 sentences.
2. Actors & incentives — short list, not a formal table unless there are 5+ actors worth tracking.
3. Claims worth checking — a compact table is fine *here* (this is a working document, not narration): claim | evidence | confidence (state your basis for the confidence level, not just a label) | how to verify.
4. Narrative & ecosystem link — 1 paragraph each.
5. Open questions — grouped by who they're for.
6. Bottom line — 2–3 sentences: what's solid, what's hype, what to watch next.

**Interview prep:** open questions (already-asked vs still-open) + bottom line. Skip 2–4.

## A note for when this feeds a script

The claim-type labels and confidence table above are workbench tools — they stay in this brief.
When this research becomes narration (via `techno-news-style` or similar), don't carry the labels
into the text as words ("это факт", "это хайп"); let the framing and hedging language do that work instead.

## Style

Skeptical but not cynical — the goal is calibration, not dunking. State uncertainty plainly
("unverified", "no evidence found", "worth checking X") rather than hedging every sentence into mush.
