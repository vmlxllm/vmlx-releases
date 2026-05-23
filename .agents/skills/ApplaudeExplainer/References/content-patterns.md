# Content Patterns — Writing Voice

The Applaudé look carries the design; this carries the words. Editorial, specific, short. Italic for tone, bold for facts.

## Hero lede formula (three sentences)

1. **The lazy story** — what people assume the topic is. *"The README sells Hokage as '5 verb skills, zero config'."*
2. **The real story** — what it actually is, with the pivot word in italics. *"The **real** Hokage is 129 shell scripts and 27 hooks that claim almost every lifecycle event."*
3. **The call to read** — what the page delivers. *"Six chapters: what it is, the loop, the hook surface, the safety teardown."*

Italicise the pivot word ("real", "actual", "quietly"). Bold the load-bearing facts.

## Chapter formula

Each chapter is one idea:
1. **`.chapter-num`** — "Chapter I" in italic clay.
2. **`.chapter-h`** — a phrase, not a sentence. Display serif. Wrap the secondary clause in `.muted` (italic, quiet).
3. **`.chapter-p`** — 2–4 sentences. State the fact, state the number, quote the ID. Then a component (flow grid / yaml card / ledger / table) that *shows* it.
4. **`.h-sub`** between sub-sections when a chapter has two beats.

## The "named numbers" rule

A page lives or dies on its numbers. **≥4 named, specific, source-cited numbers per chapter**, surfaced in the stat strip and inline.

- Bad: *"dramatically faster hooks."* Good: *"hooks fire in under 10ms vs v3's 40–60ms of Node overhead."*
- Bad: *"a huge plugin."* Good: *"33 skills, 4 agents, 27 hooks, ~2,411 always-on tokens."*

The 2nd and 3rd stat-strip numbers render italic clay — put your two most striking numbers there.

## The verbatim-ID rule

Every model ID, repo path, SKU, version, env var, command, or config key goes in a `<code>` chip, verbatim. It's the anchor a reader uses to verify and the string they'll paste into a terminal: `claude-code-harness@claude-code-harness-marketplace`, `HARNESS_MEM_HOST`, `permissionDecision: "deny"`, `CLAUDE_CONFIG_DIR`.

## The "what / when / why" card structure

For feature-by-feature breakdowns (ledger rows or grid cards):
- **What it is** → the tag / badge.
- **Title** → the `.ledger-t` / `h3`.
- **What it does** → the body.
- **What it costs you** → an optional stat.
- **Where to read more** → a source link.

## The bombshell

Find the one buried, non-obvious finding — the thing that reframes the topic — and give it the single dark `.callout`. One per page. It's the line a reader screenshots.

## The cheat sheet

Readers want the decision. End the analysis chapters with a `.tbl` decision matrix: *if you want X → do Y → why.* Three to five rows.

## Tone

- **Confident, not hedged.** "It does X," not "it seems to do X."
- **Editorial, not corporate.** "It *quietly* ships" not "it offers a comprehensive suite."
- **Specific over general.** Names, numbers, dates, exact quotes.
- **Short over long.** Cut every sentence in half until it stops cutting.
- **Italic = tone (clay, human). Bold = fact (ink). Mono = system speaking.** Don't mix.

Read every paragraph back. If a sentence adds neither a fact nor sharper framing, cut it.

## Honest mode (no hype)

When the brief is "explain it straight" — *is it good, how is it different, what's the catch* — answer the question in the reader's mind without sloganeering. State the real tradeoff. Name what it's bad at. A teardown earns trust precisely because it isn't selling. Sage = genuinely good, clay = the human caveat, never a fake superlative.
