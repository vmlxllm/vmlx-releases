# Applaudé — Design System (for the explainer skill)

*"Apple × Claude editorial language."* Warm paper, warm ink, clay-italic accents, hairlines, big whitespace. The exact CSS lives in `template.html` — **keep that `<style>` block verbatim**. This file explains *what each token and component means* so you fill content into the right place.

## 1. Palette — "Claude warm neutral + clay"

| Token | Hex | Role |
|---|---|---|
| `--pampas` | `#F0EEE6` | Warm off-white **canvas** (page bg) |
| `--pampas-deep` | `#E8E5DA` | Alt sections — alternate chapters with `.chapter-flip` |
| `--bone` | `#FAF9F5` | Lightest neutral — cards, code blocks |
| `--ink` | `#1F1E1D` | Warm near-black — primary text, primary button, the one dark callout |
| `--ink-soft` `--ink-quiet` `--ink-whisper` | `#3D3D3A` `#6B6A65` `#A09E96` | Secondary / tertiary / caption text |
| `--crail` | `#C96442` | **Signature Claude clay** — accent, italic words, link hover, live dot, CTA hover |
| `--crail-deep` `--crail-tint` | `#A84F31` `#E8B89F` | Clay hover; soft clay for accents on dark surfaces |
| `--leaf` | `#8B9D7E` | Sage — "approved / synced / verified" state only |
| `--sky` | `#6B8AA8` | Cool — numbers / value types only, used sparingly |

Window-chrome dots (code cards): red `#E66B5C`, yellow `#E5C76B`, green `#8DBE7A`.

## 2. Type

- `--font-display` / `--font-body` → `'Tiempos Headline'/'Tiempos Text'` (if licensed) then **`Fraunces`** serif. Hero, chapter heads, stats, long-form prose.
- `--font-ui` / `--font-sans` → **`Geist`**. Buttons, eyebrows, labels, nav, table headers.
- `--font-mono` → **`Geist Mono`**. Code, YAML, file names, timestamps, micro-meta, sync lines.

Letter-spacing: **negative on display** (`-0.045em` hero, `-0.025em` chapter heads), **positive on uppercase UI** (`+0.16em` eyebrows, `+0.04em` mono meta). `text-wrap: balance` on heads.

Type scale: `--t-mega 168 / --t-hero 104 / --t-display 64 / --t-h1 48 / --t-h2 32 / --t-h3 20 / body 18 / small 15 / caption 13 / micro 11` (all responsive `clamp`).

## 3. Voice & rules (memorize these — they ARE the look)

1. **Editorial, not productized.** Centered columns 640–880px, heavy whitespace, italic clay emphasis (`em { color: crail; font-style: italic }`).
2. **Hairlines, not borders.** Every divider `0.5px @ 8–18% ink`. Never solid 1px.
3. **Mono = "system speaking."** YAML, filenames, timestamps, eyebrow micro-meta.
4. **Italic serif = "voice / human."** Hero accent word, chapter numerals, captions.
5. **Clay is a verb, not a fill.** It punctuates — hero accent word, em, link hover, live dot, CTA hover, and the single dark callout's accent. It never floods areas.
6. **Two-tone temperature.** Warm pampas/bone + warm ink + clay. Sage and sky are *condiments* — state and numbers only.
7. **Generous breathing.** Chapters `120–140px` padding; hero full-viewport.
8. **Soft warm shadows.** Tinted with ink, large/soft (`--shadow-soft/lift/deep`), editorial not material.

One-liner: *Pampas canvas + warm ink + clay-italic accents. Hairlines not borders. Mono for system, italic serif for voice. Big whitespace. Sage = good, sky = number, clay = human.*

## 4. Components (class → when to use → content)

| Component | Class | Use it for |
|---|---|---|
| **Nav** | `.app-nav` | Fixed glass bar. Mark in display-serif (`<word> <em>teardown/guide</em>`), section links as pills, right meta in mono (version · license). |
| **Hero** | `.hero` | Full-viewport. `.hero-eyebrow` pill with pulsing `.hero-dot`, serif `h1` with **one** `<em>` clay-italic accent word, `.hero-lede` (3-sentence lazy→real→read), `.hero-cta` button pair, `.lede-note` mono provenance line. |
| **Stat strip** | `.stats > .stat` | The 4 headline numbers. `.stat-n` display; 2nd & 3rd auto-render italic clay. `.stat-l` mono-ish label. Use `<span class="u">` for units (k, M, %). |
| **Chapter** | `.chapter` / `.chapter chapter-flip` | The narrative. `.chapter-num` (italic clay "Chapter I"), `.chapter-h` (display head; wrap secondary clause in `.muted`), `.chapter-p` body. `.h-sub` = mono uppercase sub-section header with trailing hairline. Alternate flip bg. |
| **Flow grid** | `.flow-grid > .flow-step / .flow-arrow` | Any sequence/loop/pipeline. 3–4 steps + `→` arrows. Each step: `.flow-num` (mono), `.flow-title` (display), `.flow-sub` (mono clay), `.flow-body`. Collapses to 1 column on mobile, arrows rotate. |
| **YAML/code card** | `.yaml-card` | Commands, config, code. `.yaml-head` with 3 traffic-light `.dot`s + mono `.yaml-file` name. `.yaml-body` lines as `<span class="l">`; token classes `.k` (keys=clay) `.s` (strings=sage) `.n` (numbers=sky) `.c` (comments) `.d` (dim). |
| **Note card** | `.note-card` | A verified / synced state. `.note-circle` (clay ring), mono `.note-title`, mono `.note-body`, `.note-sync` row with `.sync-dot` (sage = good). |
| **Dark callout** | `.callout > .callout-inner` | The ONE bombshell finding. Dark ink card, `.callout-eye` clay-tint eyebrow, `.callout-h` with `<em>` crail-tint accents, `.callout-p`. |
| **Decision matrix** | `.tbl-wrap > table.tbl` | The "if you want X → do Y → why" cheat sheet. `.pick` (the choice) + `.why`. |
| **Ledger** | `.ledger > .ledger-row` | Numbered findings list. `.ledger-i` (clay numeral or ✓ in sage), `.ledger-t` (display), `.ledger-b` (body). Use `.tag-good`/`.tag-warn` mono tags. |
| **Closing** | `.closing` | `.closing-mark` (clay glyph ✦), `.closing-h`, `.closing-p`, `.closing-cta` button pair. |
| **Footer** | `footer` | `.foot-gift` (display line w/ italic clay em), `.foot-meta` mono column, `.sources` block with every URL (`↗` prefixed mono links). |

## 5. Motion

- Reveal-on-scroll: `.reveal` → `.in`, `opacity + translateY(24→0)` over `1.2s cubic-bezier(.2,.7,.2,1)`, IntersectionObserver `threshold 0.08`. Add `.reveal` to every section/inner.
- Live dot: `pulse 2.4s` clay ring. Sync dot: static sage with soft ring. Button hover: `translateY(-1px) + shadow-lift`, bg → clay on primary.
- Nav active: highlight the link for the section in view (script at bottom of template).

## 6. Responsive

- `≤880px`: flow grid → 1 column, arrows rotate 90°; stats → 2-up.
- `≤760px`: nav links hide; tighter paddings.

## 7. Drop-in token block

The full `:root` token block is the first thing in `template.html`'s `<style>`. Copy the template; don't re-derive it.
