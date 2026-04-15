<p align="center">
  <img src="assets/vmlx.ai/svg/vmlx-lockup.svg#gh-light-mode-only" alt="vMLX" height="88" />
  <img src="assets/vmlx.ai/svg/vmlx-lockup-light.svg#gh-dark-mode-only" alt="vMLX" height="88" />
</p>

<h1 align="center">vMLX — Swift (dev branch)</h1>

<p align="center">
  <strong>For a production Swift engine with a more streamlined, user-ready feature set, please use <a href="https://osaurus.ai">osaurus.ai</a>.</strong><br/>
  <em>This tree is where the more experimental engine paths live — DDFlash, JANG smelt, JANGTQ, Flash MoE, hybrid-SSM cache work, and other research-y directions that aren't ready for a shipping product yet.</em>
</p>

---

> # ⚠️ EXPERIMENTAL SANDBOX — NOT A REAL APP ⚠️
>
> **This `dev` branch is NOT a product. It is not meant to be used.
> It is not meant to be "tested" the way you'd test an app.**
>
> This tree is an **experimental workbench** for trying new low-level
> research directions that have no place in the stable user app yet.
> Specifically:
>
> - **DDFlash / JANG-DFlash speculative decoding** — block-diffusion
>   drafter + DDTree beam + coordinator-aware verify. See
>   `Sources/vMLXLMCommon/DFlash/`.
> - **JANG smelt** — partial-expert streaming / smelting. The UI flag
>   is live; the Swift-side loader is not — Stream emits an honest
>   per-request warning when the toggle is on.
> - **JANGTQ / MXTQ quant formats** — native Swift repack, TurboQuant
>   KV cache, MXTQ packed dequant (PRNG parity still WIP). See
>   `Sources/vMLXLMCommon/JangMXTQDequant.swift`,
>   `JangSpecBundleLoader.swift`, `TurboQuantKVCache` in
>   `Sources/vMLXLMCommon/TurboQuant/`.
> - **Flash MoE expert streaming** from SSD, cache coordinator work,
>   hybrid-SSM + sliding-window disk round-trip, Llama 4 iRope, etc.
>
> If you want to **use** vMLX, run the stable Electron +
> bundled-Python app at
> **[jjang-ai/mlxstudio](https://github.com/jjang-ai/mlxstudio)**
> (current release **v1.3.54**). That is the shipping product.
>
> If you want to **use** this Swift dev branch: don't. It's not for
> that. It exists so a handful of people can try experimental engine
> paths end-to-end and break things in isolation without putting user
> installs at risk.
>
> **Do not treat dev DMGs as app beta builds.** `vdev-*` tags on
> [mlxstudio releases](https://github.com/jjang-ai/mlxstudio/releases)
> are engineering snapshots — prereleased so the five people touching
> this tree can grab a notarized binary quickly. They are never
> promoted to user channels. Do not file "this is broken" bug reports
> against them as if they were products; reproductions welcome,
> expectations of stability are not.
>
> Things break. APIs shift. Whole model families don't work yet. Cache
> tiers have known correctness gaps. Multi-turn reuse is incomplete on
> some hybrid paths. **Do not deploy this. Do not integrate it into
> anything that matters. Do not rely on it for any production
> workload.**

---

## What this is

The entire MLX inference stack — Metal kernels, quant paths, attention
paths, scheduler, tokenizer, chat loop, HTTP routes, desktop UI —
in a single SwiftPM package. No external `path:` dependencies, no
upstream drift risk. We control every layer, and when we need a
change we commit it here directly instead of coordinating with
`mlx-swift`, `mlx-swift-examples`, or `vmlx-swift-lm` upstreams.

As of 2026-04-13 the vendoring is complete: `Cmlx` + all 8 MLX Swift
targets live next to the `vMLX*` targets under one `Package.swift`
(23 targets, 5 external deps only).

**Binaries produced:**
- `vmlxctl` — CLI (`serve`, `chat`, `pull`, `ls`, `dflash-smoke`)
- `vMLX` — SwiftUI macOS app (5 modes: Chat, Server, Image, Terminal, API)

---

## Status & limitations

Honest snapshot of the `dev` branch. Anything not listed here should be
assumed broken or absent.

### ✅ Works (live-verified today)

| Area | State |
|---|---|
| Model load + text generation | ✅ Llama 3.2 1B, Qwen3 0.6B, Gemma 4 e2b (4-bit MLX) |
| Full `swift build` | ✅ clean, all 23 targets |
| Dev DMG build | ✅ notarized + stapled, `vdev-20260415-0612` shipped |
| `vmlxctl chat / serve / pull / ls` | ✅ basic paths |
| HTTP server: OpenAI `/v1/chat/completions`, `/v1/models` | ✅ streaming + non-streaming |
| HTTP server: Ollama `/api/{chat,generate,tags,...}` | ✅ |
| HTTP server: Anthropic `/v1/messages` | ✅ |
| Admin: `/admin/{soft,deep}-sleep`, `/wake`, `/cache/*`, `/dflash/*` | ✅ |
| Model library auto-scan (HuggingFace cache) | ✅ |
| Model-family auto-detection (4-tier: JANG gold → silver → bronze → fallback) | ✅ |
| Cache stack: paged (L1) + memory (L1.5) + disk (L2) + SSM companion | ✅ live, with known gaps below |
| Prefix cache multi-turn reuse | ✅ standard path; ⚠️ partial on DFlash |
| Sliding-window attention disk round-trip (Gemma 3/4, Mistral 4 maxKVSize) | ✅ via `.rotating` LayerKind |
| BaichuanM1 `CacheList` disk serialization | ✅ via `.cachelist` LayerKind (F-G2) |
| JANG-DFlash speculative decoding | ✅ text-only, MiniMax / Mistral 4 / DeepSeek V3 targets, coordinator-aware |
| Flash MoE expert streaming (Phase 2b on some families) | ✅ opt-in per model |
| TurboQuant KV cache integration | ✅ via `make_cache` patch |
| Reasoning/tool parsers | ✅ 13 reasoning + 15 tool parsers registered |
| §15 reasoning-off → content reroute | ✅ |
| Logs: `LogStore` ring + SwiftUI `LogsPanel` + per-request `RequestLogger` | ✅ |
| Settings: 4-tier merge (global → session → chat → request) | ✅ |
| Download manager: HF auth, byte resume, progress bar | ✅ |
| Embeddings endpoint | ✅ |
| Whisper ASR `/v1/audio/transcriptions` | ✅ |
| TTS `/v1/audio/speech` | ⚠️ placeholder tone backend only (Kokoro scaffolded) |
| MCP stdio JSON-RPC + tool dispatch | ✅ |
| Terminal mode with `bash` tool auto-inject | ✅ |
| `/metrics` Prometheus endpoint | ✅ |

### ⚠️ Partial / flaky

- **MXTQ PRNG mismatch** — Swift `JangMXTQDequant` uses POSIX
  `srand48`; Python writer uses NumPy PCG64. Sign sequences diverge →
  some MXTQ bundles decode garbage weights. Known blocker for several
  JANGTQ checkpoints. Fix: port PCG64 to Swift or re-seed the Python
  writer.
- **Engine.LoadOptions default drift** — stricter cache defaults
  (`cacheMemoryPercent=0.10`, `maxCacheBlocks=500`) than
  `GlobalSettings` (`0.30` / `1000`). Code paths that construct
  `LoadOptions()` directly get smaller caches than configured.
- **Smelt mode** — UI toggle + settings field exist, but the Swift
  engine has no partial-expert-loader equivalent to Python's
  `smelt_loader.py`. Labelled honestly as "Python engine only";
  Stream emits a per-request warning when `smelt=true`.
- **DFlash streaming reasoning split** — DFlash emits N-token blocks;
  v1 routes all decoded text as `.content`. Client-side
  reasoning-extractor still works after the fact, but live
  `<think>...</think>` delta routing is not live on the DFlash path.
- **DFlash tools/images** — falls back to standard path (logged) when
  the request includes tools or images. Text-only path only for v1.
- **xcodegen + SwiftPM app bundling** — the `xcodebuild archive` path
  produces a bare executable instead of a `.app`. The ship-DMG script
  assembles the bundle manually from DerivedData products. Root cause
  not yet diagnosed.

### ❌ Broken or not yet implemented

- **Image generation `.generate()` bodies** — Flux / Qwen-Image /
  Z-Image / SeedVR2 / FIBO DiT forward passes are still scaffolded.
  Biggest user-visible gap versus the Electron app.
- **Several model families stamped in silver table but no Swift class**
  — CogVLM, Molmo, InternVL, Florence, GOT-OCR (F-G22), DeepSeek VL
  (F-G10). Silver rows resolve but `Engine.load` falls through.
- **FlashMoE family conformance gaps** — DeepSeek V3 (F-G6),
  GLM-5 `glm_moe_dsa` (F-G7), Jamba (F-G8), Granite3 MoE (F-G9).
  Protocol is ready, per-model `FlashMoEReplaceable` conformance
  not wired.
- **Tool-parser silver rows missing** — XLaM, Functionary (F-G11);
  OlmoE, BailingMoe (F-G12). Fall through to `native`.
- **Mistral 4 VLM dedicated text config** (F-G13), **Phi-4 reasoning
  parser verification** (F-G14), **Llama 4 tool format verification**
  (F-G15), **RWKVCache dedicated class** (F-G16), **MiniMax Lightning
  Attention cache verification** (F-G17).
- **CacheList multi-sub-cache walker** (F-G18) — partially addressed
  by F-G2 for the `(Mamba, KV)` case; hypothetical `(Mamba, Rotating,
  Full)` wrappers would still lose the second KV.
- **Step-3.5 reasoning + tool-call interleave** (F-G19) — no test
  coverage.
- **GPT-OSS tool parser verification** (F-G20) — silver row stamps
  `glm47` parser; unverified against real checkpoint.
- **Gemma 4 image-token defensive assertion** (F-G21).
- **PaliGemma template probe edge case** (F-G23).
- **Kokoro neural TTS backend** — scaffolded in
  `vMLXTTS/Kokoro/KokoroBackend.swift`; `/v1/audio/speech` returns
  deterministic placeholder-tone WAV until the 9-step port lands.
- **Whisper sliding-window for audio > 30s** — single-pass only; no
  temperature fallback, no beam search, no word-level timestamps.
- **Universal binary** — arm64-only. `HasDType` gates Float16 on
  `#if !arch(x86_64)` upstream, so x86_64 slices won't type-check.
- **App target bundling via xcodegen** — see above; manual assembly
  works but needs proper fix.

---

## Stack layout

```
Package.swift               23 local targets + 5 external deps
project.yml                 XcodeGen spec for the .app wrapper
scripts/
  stage-metallib.sh         stages mlx.metallib next to SwiftPM binaries

Sources/
  Cmlx/                     vendored MLX + mlx-c C++ (metal kernels inline)
                            + default.metallib (prebuilt, for SwiftPM)
  MLX/ MLXNN/ MLXFast/      MLX Swift runtime (vendored from mlx-swift)
  MLXFFT/ MLXLinalg/
  MLXOptimizers/ MLXRandom/

  vMLXLMCommon/             caches, paged cache, SSM companion, TQ,
                            Flash MoE, DFlash, evaluate loop, JANG loader,
                            MXTQ dequant
  vMLXLLM/                  ~50 LLM model classes
  vMLXVLM/                  ~15 vision-language model classes
  vMLXEmbedders/            embedding model classes
  vMLXFluxKit/ vMLXFluxModels/ vMLXFluxVideo/ vMLXFlux/
                            image / video generation stack (WIP)
  vMLXWhisper/ vMLXTTS/     audio IO
  vMLXEngine/               Engine actor: load, stream, cache, MCP,
                            Flash MoE, DFlash, ModelCapabilities,
                            CapabilityDetector, settings, metrics
  vMLXServer/               Hummingbird routes:
                              OpenAI / Ollama / Anthropic / Admin / MCP
                              / Metrics / Gateway
  vMLXApp/                  SwiftUI app (5 modes)
  vMLXTheme/                Linear-inspired tokens
  vMLXCLI/                  vmlxctl

vMLX/
  Assets.xcassets/          app icon set
  Info.plist                template (xcodegen fills $(...))
  vMLX.entitlements         App Sandbox disabled (Terminal mode)
```

---

## Build

```sh
# Requires: macOS 14+, Xcode 15.4+ (Swift 5.10), xcodegen (brew install xcodegen)

git clone -b dev https://github.com/jjang-ai/vmlx.git
cd vmlx

# --- CLI (SwiftPM) ---
swift build -c release
# CRITICAL: colocate mlx.metallib next to the binary. Without this
# every model load fails with "Failed to load the default metallib."
# (This is because the SwiftPM flat bundle layout doesn't match what
# `load_swiftpm_library` in device.cpp expects, so we fall through to
# the first-try `load_colocated_library` path instead.)
./scripts/stage-metallib.sh release

./.build/release/vmlxctl serve --model /path/to/model
./.build/release/vmlxctl chat  --model /path/to/model
./.build/release/vmlxctl pull  mlx-community/Qwen3-32B-4bit
./.build/release/vmlxctl list

# --- SwiftUI app (Xcode archive path) ---
# xcodegen produces vMLX.xcodeproj; current archive path builds a bare
# executable, not a .app bundle (known bundling quirk). The ship-DMG
# script manually assembles the .app from DerivedData products — see
# PROGRESS.md for the exact steps until we fix the xcodegen config.
xcodegen
open vMLX.xcodeproj
```

arm64 only.

---

## HTTP surfaces

| Family | Endpoints |
|---|---|
| OpenAI | `/v1/{chat/completions, completions, responses, embeddings, models, rerank, images/generations, images/edits, audio/transcriptions, audio/speech}` |
| Ollama | `/api/{chat, generate, embeddings, embed, tags, show, ps, version, pull}` |
| Anthropic | `/v1/messages` (streaming, vision, `document`, `server_tool_use`) |
| Admin | `/health`, `/admin/{soft-sleep, deep-sleep, wake, cache/stats, dflash, dflash/load, dflash/unload, models/:id}` |
| MCP | `/v1/mcp/{tools, servers, execute}`, `/mcp/:server/:method` |
| Metrics | `/metrics` (Prometheus text) |
| Gateway | multiplexes single base-URL across N model sessions |

Responses API (`/v1/responses`) covers both string and structured
`input` shapes (`message` / `function_call` / `function_call_output` /
`input_text` / `input_image`), tools, `tool_choice`,
`reasoning.effort` bucketing, and streams the full Responses event
family (`response.created`, `output_item.added`, `output_text.delta`,
`reasoning_summary_text.delta`, `function_call_arguments.delta`,
`output_item.done`, `response.completed`, `[DONE]`).

---

## Roadmap / TODO

Tracked day-to-day in `PROGRESS.md`. High-level headline items in
priority order:

**Blockers for a first user-visible release:**
1. **MXTQ PRNG parity** — currently produces garbage for some JANGTQ
   bundles.
2. **Image generation `.generate()` bodies** — Flux/Qwen-Image/Z-Image
   forward passes still scaffolded.
3. **xcodegen .app bundling** — manual assembly works; fix so
   `xcodebuild archive` produces a proper `.app`.

**Model-family coverage (F-G matrix — 23 items tracked):**
- F-G1 ✅ SSMStateCache mediaSalt
- F-G2 ✅ BaichuanM1 CacheList disk walker
- F-G3 ✅ Llama 4 dedicated model class (iRope + MoE + ChunkedKVCache)
- F-G4 ✅ Gemma 3 tool parser hermes → gemma4
- F-G5 ✅ Gemma 3 mixed SWA+full detection
- F-G6..F-G23 🟡 pending — see `PROGRESS.md` + `SWIFT-PER-FAMILY-MATRIX-2026-04-15.md`
  - FlashMoE conformance: DeepSeek V3, GLM-5, Jamba, Granite3 MoE
  - Missing Swift classes: DeepSeek VL, CogVLM, Molmo, InternVL,
    Florence, GOT-OCR
  - Tool parser silver rows: XLaM, Functionary, OlmoE, BailingMoe
  - Verification: Phi-4 reasoning, Llama 4 tool format, MiniMax
    Lightning Attention, GPT-OSS tool parser
  - Cache correctness: RWKVCache dedicated class, CacheList multi-sub walker
  - Defensive: Gemma 4 image token assertion, PaliGemma probe

**Cache correctness tail:**
- Engine.LoadOptions ↔ GlobalSettings default drift
- Smelt partial-expert loader in Swift (or honestly strip the toggle)
- DFlash streaming reasoning parser
- DFlash tool-call path

**Audio:**
- Kokoro neural TTS backend (9-step port plan in `vMLXTTS/Kokoro/KokoroBackend.swift`)
- Whisper long-form (sliding window, temperature fallback, word timestamps)
- TTS mp3 / opus / flac transcoding

**Build + shipping:**
- xcodegen/SwiftPM application-bundle wrapping (see quirk above)
- Automated ship-DMG script for future dev releases

---

## Related docs in-tree

- **`PROGRESS.md`** — per-session changelog, newest at top. Read this
  first if you want to know what moved recently.
- **`NO-REGRESSION-CHECKLIST.md`** — release regression matrix.
- **`Sources/vMLXLMCommon/FlashMoE/README.md`** — Flash MoE phase
  architecture.
- **`SWIFT-PER-FAMILY-MATRIX-2026-04-15.md`** *(local only, not
  pushed)* — per-family F-G1..F-G23 audit with file:line citations.

---

## Not in this tree

- **Production Electron app** — `panel/` subtree kept for reference
  but never built in this pipeline. Real v1.3.x releases come out of
  `jjang-ai/vmlx` `main` branch via electron-builder.
- **User documentation** — this README is a dev log, not a user
  manual. User docs live on `jjang-ai/mlxstudio` when the Swift path
  is mature enough to document for users.

---

## Legal

© 2026 Jinho Jang. Source licensed as-is, no warranty, dev-preview
only. Do not redistribute dev DMGs to end users.
