---
name: applaude-explainer
description: Build a beautiful, source-cited, single-file HTML explainer on any topic in the Applaudé editorial design language — warm pampas canvas, clay-italic accents, Fraunces serif + Geist, hairline dividers, flow diagrams, stat strips, mac-window YAML/code cards, sage "verified" note cards, and a dark "bombshell" callout — then save it to ~/Desktop/Explainers and open it. Two modes — DEFAULT (#exap, any topic) and REPO/16W (#16w, drop a GitHub repo and it honestly answers the 10 questions of the 16-word sales-letter framework — what is this, is it good, how is it different — with zero hype, plus an optional 10-part video script pack). Same research rigor as a topic explainer (named numbers, verbatim <code> IDs, decision matrix, sources block) in the "Apple × Claude" Applaudé look. USE WHEN the message contains #exap or #16w, or says — applaude explainer, exap this, exap X, make an applaude explainer of X, explain X in the applaude style, explain this github repo, is this repo any good, drop in a repo and explain it, 16 word, ten questions explainer, do an applaude deep-dive on X. NOT FOR the dark editorial topic-explainer theme (use topic-explainer) or one-paragraph summaries.
---

# Applaudé Explainer

Turn any topic into an editorial-grade, source-cited, single-file HTML explainer in the **Applaudé** design language — *"Apple × Claude editorial."* Warm pampas paper, warm-ink type, clay-italic accents, hairlines instead of borders, big breathing whitespace.

Trigger: **`#exap`** (anywhere in the message), or any close variant ("make an applaude explainer of X", "exap the X keynote", "explain X in the applaude style").

## Two modes

- **Default — `#exap` / any topic.** Free-form explainer. Chapters follow the topic's own structure. Process below.
- **Repo / 16W — `#16w` + a GitHub URL.** Drop in a repo; the page *answers* the 10 questions of the 16-word sales-letter framework (what is this · is it good · how is it different · why trust it · how to start · what to lose…) **honestly, no hype, question never stated.** Can also emit a 10-part video script pack (one per question). Full intake steps, the 10-answer → component map, the no-sales rules, and the video spec are in **`References/sixteen-word.md`** — read it when `#16w` fires. Everything below (design system, template, voice) still applies; only the chapter scaffold changes to the 10 answers.

## What it produces

- **One self-contained `.html` file.** No build step, no framework. Only Google Fonts (Fraunces + Geist + Geist Mono) over CDN.
- **Saved to `$HOME/Desktop/Explainers/{topic-slug}-explainer.html`** — always. Then opened with `open`.
- Light, warm, editorial. The opposite of the dark `topic-explainer` theme. Same content rigor, different skin.

## Three-stage process

### Stage A — Research (spend the first half here)
Use web search + fetch. Launch 2–4 parallel research probes via the Agent tool for broad topics.
1. **Hit primary sources** — official docs, GitHub READMEs, blog posts, papers, press releases. Capture before summarizing.
2. **Quote IDs verbatim** — model names, repo paths, SKUs, version numbers, env vars. Never paraphrase identifiers; wrap each in `<code>`.
3. **Capture exact numbers** — counts, scores, dollars, percentages, latencies. These become the stat strip and decision table.
4. **Find the under-the-radar story** — the buried detail. It becomes the dark "bombshell" callout.
5. **Flag what you can't confirm** — write "could not verify," never confabulate.
6. **Keep every URL** — they go in the bottom sources block.

If the topic is something just produced in this session (research, a teardown, a build), use that first-hand verified material directly — it's the strongest source you have.

### Stage B — Build from the template
1. Copy `References/template.html` as the scaffold. **Keep the entire `<style>` block unchanged** — it *is* the Applaudé design system. Only swap content in the `<body>`.
2. Fill the components in order: nav → hero (eyebrow pill + serif h1 with one clay-italic accent word + 3-sentence lede + CTA pair) → 4-up stat strip → 4–7 chapters → dark callout → decision matrix → closing → footer + sources.
3. Map content to the right component (see `References/design-system.md`):
   - **Flow grid** → any sequence/loop/pipeline (3–4 steps + arrows).
   - **YAML/code card** → commands, config, code (mac traffic-lights + token coloring).
   - **Stat strip** → the 4 headline numbers (2nd & 3rd render italic clay).
   - **Note card** → a verified/synced state (sage dot = good).
   - **Dark callout** → the one bombshell finding.
   - **Decision matrix** → the "if you want X, do Y" cheat sheet readers crave.
4. Alternate `.chapter` and `.chapter chapter-flip` (pampas-deep) backgrounds for rhythm.

### Stage C — Save, verify, open
1. Save to `$HOME/Desktop/Explainers/{topic-slug}-explainer.html`.
2. **Verify in a real browser** before claiming done — open the file and screenshot the hero + 2–3 interior sections; confirm Applaudé styling rendered (pampas bg, Fraunces hero, clay italic, hairlines). Use the Interceptor skill if installed; otherwise fall back to the session's Chrome tooling (`chrome-devtools-axi open <file://…>` + `screenshot`). Delete temp screenshots after.
3. `open "$HOME/Desktop/Explainers/{slug}-explainer.html"`.

## Quick design tokens (full set in References/design-system.md)

- **Canvas** `--pampas #F0EEE6` · **ink** `#1F1E1D` · **clay accent** `--crail #C96442` · **sage** `--leaf #8B9D7E` (good/synced) · **sky** `--sky #6B8AA8` (numbers).
- **Type** — display/body serif `Fraunces` (Tiempos if licensed), UI/sans `Geist`, mono `Geist Mono`.
- **Voice rules** — `em` = clay italic (human voice). Mono = system speaking. Hairlines (`0.5px @ 8–18% ink`), never solid borders. Clay is a verb, not a fill — it punctuates, never floods. Big editorial whitespace (120–140px chapter padding). Centered columns 640–880px.

## Content rules (full set in References/content-patterns.md)

- **Hero lede** = three sentences: the lazy story → the *real* story (italic pivot word) → the call to read.
- **Named numbers** — ≥4 specific, source-cited numbers per chapter. "jumped AIME 20.8% → 89.2%", not "dramatically improves".
- **Verbatim IDs** — every model/SKU/repo/env-var in `<code>`.
- **Tone** — confident, editorial, specific, short. Italic for tone, bold for facts. Cut every sentence in half until it stops cutting.

## Reference files

- **`References/template.html`** — the proven scaffold. Full Applaudé CSS + a one-of-each component skeleton with `{{PLACEHOLDER}}` markers. Copy and refill.
- **`References/design-system.md`** — palette meaning, type scale, every component (nav, hero, stats, chapters, flow grid, YAML card, note card, callout, decision matrix, closing, footer), motion, responsive rules.
- **`References/content-patterns.md`** — hero-lede formula, big-card formula, named-numbers rule, verbatim-ID rule, tone.

## Quality checklist

- [ ] Saved to `$HOME/Desktop/Explainers/{slug}-explainer.html` and opened.
- [ ] Pampas canvas, warm ink, Fraunces serif hero with exactly one clay-italic accent word.
- [ ] Hairlines everywhere — no solid 1px borders.
- [ ] Clay used only as accent (italic words, links, live dot, one callout) — never as a fill background except the single dark callout.
- [ ] 4-up stat strip; 2nd & 3rd numbers italic clay.
- [ ] ≥4 named, source-cited numbers per chapter; every ID in `<code>`.
- [ ] One dark "bombshell" callout for the buried finding.
- [ ] Decision matrix present.
- [ ] Sources block at the foot with every URL.
- [ ] Single self-contained `.html`; verified rendered in a browser.
