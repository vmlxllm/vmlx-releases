# `#16w` Mode — Drop a Repo, Answer the 10 Questions (No Sales Shit)

Trigger: **`#16w`** + a GitHub URL (or repo path). Produces an Applaudé explainer whose structure *answers* the 10 questions of the 16-word sales-letter framework — **without ever stating the question, and without a word of hype.** A teardown earns belief precisely because it isn't selling.

## Intake (do this first)

1. **Clone shallow to `/tmp`** and read for real — README, `package.json`/`go.mod`/`Cargo.toml`, `LICENSE`, `/docs`, the actual entry-point source, and `hooks`/config if present. Don't explain from the README alone.
2. **Capture hard facts**: stars, last-commit date, open issues, test count, license, language, dependency count, version, benchmark numbers, install command.
3. **Trace anything that runs on the user's machine** (binaries, hooks, postinstall scripts, network calls). Honesty about risk is the trust currency.
4. Keep every URL for the sources block.

## The 10 answers → where they live on the page

Answer each in the reader's mind. **Never print the question.** Deliver the answer as fact.

| # | Question (never shown) | How to answer it, honestly | Applaudé component |
|---|---|---|---|
| 1 | How is this different? | The one structural thing it does that nothing else does. State the delta, not "revolutionary". | Hero accent line + a `vs` decision matrix |
| 2 | What's in it for me? | The concrete outcome, as a fact: *"hooks fire in <10ms"* not *"blazing fast"*. | Hero lede real-story + stat strip |
| 3 | How do I know it's real? | Proof from the repo — stars, tests passing, benchmark numbers, real commit cadence. | Stat strip + `note-card` (verified) + ledger with `tag-good` |
| 4 | What's holding me back? | The genuine friction it removes — name the real pain, specifically. | A "the friction" chapter |
| 5 | Who/what's to blame? | The honest limitation of the *current* approach it replaces — the old way, not a strawman enemy. | "the old way" chapter (`.chapter-flip`) |
| 6 | Why now? | What changed that makes it possible/worthwhile today (a model, a primitive, a cost curve). | A short "why now" chapter |
| 7 | Why trust it? | Provenance: author, license, maintenance, and the **safety/egress teardown**. Show the receipts. | `note-card` + the egress ledger (sage = clean) |
| 8 | How does it work? | The mechanism, plainly. | `flow-grid` (the pipeline) + `yaml-card` (real config) |
| 9 | How to start? | The exact commands. No friction, no upsell. | `yaml-card` with verbatim install lines |
| 10 | What do I have to lose? | The real cons + how reversible it is (uninstall, sandbox, cost). Name what it's bad at. | Final ledger with `tag-warn` + `tbl` cheat sheet |

The single dark `.callout` carries the **most honest** line on the page — the buried tradeoff or the genuine "this is the catch." That candor is what makes the rest believed.

## No-sales-shit rules

- **No superlatives without a number.** "fast" → a latency. "powerful" → a capability + its cost.
- **State the cons.** Every honest teardown names what the thing is bad at. Question 10 is not a formality.
- **Sage = genuinely good, clay = the human caveat.** Never paint a green where a tradeoff exists.
- **Answer, don't ask.** The reader should finish each section with the answer settled — never having been asked.
- Verdict over verdict-shaped marketing: end with *who should and shouldn't use it*, not a CTA to "get started now".

## The 10 videos (one per answer)

`#16w` can also emit a **10-part video pack** — one short per question, each landing that single answer, the question never spoken. Each script is a tight beat:

1. **Cold-open hook** (2–4s) — a concrete image or number, not a claim.
2. **The answer** (the body) — deliver the clarity for that question as lived fact / demo.
3. **The land** (1 line) — the takeaway the viewer now believes.

Script spec per video: `~20–45s`, plain spoken VO, on-screen `<code>`/number callouts, no question text, no hype words. Output as a numbered script pack (`01-different.md` … `10-what-to-lose.md`) with: hook · VO · on-screen text · b-roll/demo note · the one number it must show.

**Render path is a separate choice** — the scripts are tool-agnostic. Options: `Remotion` (code-driven, on-brand Applaudé motion), `video-use` (edit existing footage), or an avatar/TTS tool. Confirm tool + aspect ratio (vertical 9:16 for shorts vs 16:9) before rendering; default to a script pack first.
