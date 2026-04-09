<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo-wide-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="assets/logo-wide-light.png">
    <img alt="MLX Studio" src="assets/logo-wide-light.png" width="400">
  </picture>
</p>

<h3 align="center">The native macOS desktop app for local AI on Apple Silicon</h3>

<p align="center">
  <a href="https://github.com/jjang-ai/mlxstudio/releases/latest"><img src="https://img.shields.io/github/v/release/jjang-ai/mlxstudio?style=flat-square&label=Latest%20Release&color=blue" alt="Latest Release"></a>
  <a href="https://github.com/jjang-ai/mlxstudio/releases"><img src="https://img.shields.io/github/downloads/jjang-ai/mlxstudio/total?style=flat-square&label=Downloads&color=green" alt="Downloads"></a>
  <img src="https://img.shields.io/badge/Platform-macOS%20ARM64-lightgrey?style=flat-square&logo=apple" alt="Platform">
  <a href="https://pypi.org/project/vmlx/"><img src="https://img.shields.io/pypi/v/vmlx?style=flat-square&label=vMLX%20Engine&color=%234B8BBE&logo=python&logoColor=white" alt="PyPI"></a>
  <a href="https://github.com/jjang-ai/mlxstudio/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-orange?style=flat-square" alt="License"></a>
  <a href="https://ko-fi.com/jangml"><img src="https://img.shields.io/badge/Support-Ko--fi-FF5E5B?style=flat-square&logo=ko-fi&logoColor=white" alt="Ko-fi"></a>
</p>

<p align="center">
  <a href="https://github.com/jjang-ai/mlxstudio/releases/latest">
    <img src="https://img.shields.io/badge/%E2%AC%87%EF%B8%8F_Download_DMG-Latest_Release-blue?style=for-the-badge&logo=apple&logoColor=white" alt="Download DMG" height="40">
  </a>
</p>

<p align="center">
  <b>No Python. No terminal. No config files.</b><br>
  Download the DMG, drag to Applications, and run AI models locally in seconds.
</p>

<p align="center">
  <a href="#features">Features</a> &bull;
  <a href="#screenshots">Screenshots</a> &bull;
  <a href="#api-server">API Server</a> &bull;
  <a href="#image-generation">Image Generation</a> &bull;
  <a href="#advanced-quantization">JANG Quantization</a> &bull;
  <a href="#system-requirements">Requirements</a> &bull;
  <a href="#build-from-source">Build</a> &bull;
  <a href="#한국어-korean">한국어</a>
</p>

---

MLX Studio is a complete desktop app for running LLMs, VLMs, and image generation models locally on your Mac. No cloud, no API keys, no data leaving your machine. Supports every model on [mlx-community](https://huggingface.co/mlx-community) -- Qwen, Llama, Mistral, Gemma, Phi, DeepSeek, and thousands more. Built on [vMLX Engine](https://github.com/jjang-ai/vmlx) and Apple's [MLX](https://github.com/ml-explore/mlx) framework.

> **JANG 2-bit destroys MLX 4-bit on [MiniMax M2.5](https://huggingface.co/JANGQ-AI/MiniMax-M2.5-JANG_2L):**
>
> | Quantization | MMLU (200q) | Size |
> |---|---|---|
> | **JANG\_2L (2-bit)** | **74%** | **89 GB** |
> | MLX 4-bit | 26.5% | 120 GB |
> | MLX 3-bit | 24.5% | 93 GB |
> | MLX 2-bit | 25% | 68 GB |
>
> Adaptive mixed-precision quantization keeps critical layers at higher precision while compressing the rest. Check scores at [jangq.ai](https://jangq.ai). Models at [JANGQ-AI](https://huggingface.co/JANGQ-AI).

---

## Install

### Option 1: Download the App (Recommended)

> **[Download the latest DMG](https://github.com/jjang-ai/mlxstudio/releases/latest)** -- one file, ready to go.

1. Download `vMLX-X.Y.Z-arm64.dmg`
2. Open the DMG and drag to Applications
3. Launch -- that's it

All releases are code-signed and notarized by Apple for macOS Gatekeeper. No Homebrew, no pip, no Xcode required.

### Option 2: CLI via pip (Engine Only)

The vMLX inference engine is published on [PyPI as `vmlx`](https://pypi.org/project/vmlx/) -- same engine that powers the desktop app, available as a standalone CLI. This is real, published software with 1,894+ tests.

```bash
# Recommended: use uv (fast, no venv hassle)
brew install uv
uv tool install vmlx
vmlx serve mlx-community/Qwen3-8B-4bit

# Or with pipx (isolates from system Python)
brew install pipx
pipx install vmlx
vmlx serve mlx-community/Qwen3-8B-4bit

# Or with pip in a virtual environment
python3 -m venv ~/.vmlx-env && source ~/.vmlx-env/bin/activate
pip install vmlx
vmlx serve mlx-community/Qwen3-8B-4bit
```

> **Note:** On macOS 14+, `pip install vmlx` without a venv will fail with "externally-managed-environment". Use `uv`, `pipx`, or create a venv first.

Once running, your local OpenAI-compatible API server is live at `http://localhost:8000`. Point any OpenAI or Anthropic SDK client at it.

---

## Quick Start

1. **Launch** MLX Studio from Applications
2. **Pick a model** -- browse HuggingFace models in the Server tab, or enter a repo name (e.g., `mlx-community/Qwen3-8B-4bit`)
3. **Start the session** -- the model downloads automatically and the server starts
4. **Chat** -- switch to the Chat tab and start talking

That's it. The app manages the entire Python engine, model downloads, and server lifecycle for you.

---

## Screenshots

<table>
  <tr>
    <td align="center"><img src="assets/chat-tab.png" width="450"><br><b>Chat Interface</b><br><em>Streaming conversations with thinking mode, code highlighting, and markdown</em></td>
    <td align="center"><img src="assets/agentic-chat.png" width="450"><br><b>Agentic Coding</b><br><em>Full tool calling with file I/O, shell execution, and web search</em></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/image-tab.png" width="450"><br><b>Image Generation & Editing</b><br><em>Flux Schnell, Dev, Z-Image Turbo, Klein + Qwen Image Edit</em></td>
    <td align="center"><img src="assets/anthropic-api.png" width="450"><br><b>Anthropic API Compatible</b><br><em>Drop-in /v1/messages endpoint for Anthropic SDK clients</em></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/tools-tab.png" width="450"><br><b>Developer Tools</b><br><em>Convert, inspect, and diagnose models</em></td>
    <td align="center"><img src="assets/gguf-to-mlx.png" width="450"><br><b>Model Conversion</b><br><em>GGUF to MLX, 16-bit to quantized, and JANG adaptive mixed-precision</em></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/jangq-models.png" width="450"><br><b>HuggingFace Browser</b><br><em>Search and download models directly in-app</em></td>
    <td align="center"><img src="assets/menu-bar.png" width="300"><br><b>Menu Bar</b><br><em>Running models, GPU memory, and quick controls</em></td>
  </tr>
</table>

---

## Features

### Model Support (65+ Model Families)

Run any MLX model from HuggingFace -- thousands of models, zero configuration:

- **Text LLMs** -- Qwen 2/2.5/3/3.5, Llama 3/3.1/3.2/3.3/4, Mistral/Mixtral/Codestral, Gemma 2/3, Phi-3/4, DeepSeek V2/V3/R1, GLM-4/4.7, Nemotron, MiniMax, Kimi, Step, XVERSE, Yi, InternLM, ChatGLM, CodeLlama, and any mlx-lm compatible model
- **Vision LLMs (VL)** -- Qwen-VL, Qwen2.5-VL, Qwen3.5-VL, Pixtral, InternVL, LLaVA, Gemma 3n, Phi-3-Vision -- send images and video directly in chat
- **Mixture-of-Experts** -- Qwen 3.5 MoE, Mixtral 8x7B/8x22B, DeepSeek V2/V3, MiniMax M2.5, Llama 4 Scout/Maverick
- **Hybrid SSM Models** -- Nemotron-H, Jamba, GatedDeltaNet (Mamba + Attention architectures with dedicated hybrid cache)
- **Image Generation** -- Flux Schnell/Dev, Z-Image Turbo, FLUX.2 Klein 4B/9B (via mflux)
- **Image Editing** -- Qwen Image Edit (instruction-based editing, full precision)
- **Audio** -- Kokoro TTS, Whisper STT, Qwen3-Audio (via mlx-audio)
- **JANG Models** -- Adaptive mixed-precision quantized models from [JANGQ-AI](https://huggingface.co/JANGQ-AI), stay quantized in GPU memory via native `QuantizedLinear`
- **GGUF Import** -- Convert GGUF models to MLX format directly in-app

### OpenAI-Compatible API Server

Every session launches a full API server. Point any OpenAI SDK client at your local endpoint:

- `POST /v1/chat/completions` -- Chat Completions API with streaming, tool calling, vision, structured output
- `POST /v1/responses` -- OpenAI Responses API (agentic format) with streaming
- `POST /v1/completions` -- Text completions
- `POST /v1/images/generations` -- Image generation (Flux/Z-Image models, OpenAI format with `usage` field)
- `POST /v1/images/edits` -- Image editing (Qwen Image Edit, instruction-based)
- `POST /v1/embeddings` -- Text embeddings with dimension control and batch processing
- `POST /v1/rerank` -- Document reranking
- `POST /v1/audio/speech` -- Text-to-speech (Kokoro TTS)
- `POST /v1/audio/transcriptions` -- Speech-to-text (Whisper)
- `GET /v1/models` -- List loaded models
- `GET /health` -- Server health with VRAM usage, queue length, load times

### Anthropic API Compatibility

Drop-in replacement for the Anthropic Claude API:

- `POST /v1/messages` -- Anthropic Messages API format
- Anthropic SDK tool calling format (auto-translated to internal format)
- Vision/multimodal support via Anthropic content blocks
- Use the Anthropic Python/TypeScript SDK -- just change the `base_url` to your local server
- Copy-paste code snippets in the API tab for curl, Python, and JavaScript

### Tool Calling & Agentic Workflows (14 Parsers)

Auto-detected tool call parsers for every major model family:

- **Qwen** (qwen3, qwen2.5) -- `<tool_call>` XML format
- **Llama 3** -- `<function=name>` format
- **Mistral** -- `[TOOL_CALLS]` format
- **Hermes** -- `<tool_call>` JSON format
- **DeepSeek** -- function call blocks
- **GLM-4.7** -- GLM tool format
- **MiniMax** -- MiniMax function calling
- **Nemotron** -- NVIDIA Nemotron tool format
- **Granite** -- IBM Granite format
- **Functionary** -- Functionary v3 format
- **XLAM** -- Salesforce xLAM format
- **Kimi** -- Moonshot Kimi format
- **Step-3.5** -- StepFun format
- Auto-detection from `model_type` in config.json with regex name fallback

**26+ Built-in Tools:**
- **File I/O** -- read, write, edit, patch, copy, move, delete, create directory, list directory, file info, insert text, replace lines, directory tree
- **Search** -- ripgrep file search with regex and glob, glob file finder, unified diff
- **Execution** -- shell commands (60s timeout), background processes (5m auto-kill), process output polling
- **Web** -- DuckDuckGo search, Brave Search API, URL fetch with HTML-to-text
- **Developer** -- token counter, regex find-replace across files, git operations, clipboard read/write, diagnostics (TypeScript/ESLint/Python linting)
- **Interactive** -- `ask_user` tool for human-in-the-loop interrupts
- Per-category toggles: enable/disable file, search, shell, web tools independently
- Auto-continue agent loops (up to 10 tool iterations per request)
- **MCP (Model Context Protocol)** -- connect external tool servers, merge tool definitions, execute MCP tools via API

### Reasoning Model Support (4 Parsers)

Collapsible thinking blocks with dedicated parsing for reasoning models:

- **Qwen3 / Qwen3.5** -- `<think>...</think>` blocks
- **DeepSeek-R1** -- DeepSeek reasoning format
- **OpenAI GPT-OSS / GLM-4.7** -- GPT-OSS thinking format
- **Phi-4-reasoning** -- reasoning content extraction
- Enable/disable thinking per request
- Reasoning effort control (low/medium/high)
- Streaming reasoning content with proper tokenization

### Vision & Multimodal (VLM)

Full multimodal input support for vision-language models:

- **Images** -- PNG, JPEG, WebP via base64 or URL (up to 50 MB)
- **Video** -- MP4, MOV, WebM via base64 or URL (up to 200 MB), smart frame extraction (8-64 frames), configurable FPS
- **Audio** -- Base64 or URL audio input (Qwen3-Audio)
- Image detail levels: auto, low, high
- Dedicated MLLM cache for image/video embeddings (separate from KV cache)
- Send images directly in chat to any VL model

### Continuous Batching & Concurrency

Production-grade multi-user serving:

- **Continuous batching** -- handle 32+ concurrent requests with dynamic slot allocation
- **Prefill batching** -- batch prompt processing with configurable batch size (prevents Metal GPU timeouts)
- **Completion batching** -- batch token generation across sequences
- **Stream interval control** -- configure streaming frequency
- **Request pooling** -- efficiently share GPU memory across concurrent sequences
- **Rate limiting** -- optional per-client request limits
- **API key authentication** -- optional `--api-key` flag for secured access

### 5-Layer Cache Stack

Multi-tier caching for maximum throughput and memory efficiency:

- **L1: Memory-Aware Prefix Cache** -- token-level semantic caching with LRU eviction, configurable memory allocation
- **L1 alt: Paged KV Cache** -- block-aware cache with reduced fragmentation for long contexts
- **L2: Disk Cache** -- persistent spillover to disk for large context windows
- **L2 alt: Block Disk Store** -- block-level disk persistence
- **KV Quantization** -- q4/q8 quantized KV cache at storage boundary (2-4x memory savings, no accuracy loss)
- **Hybrid SSM Cache** -- dedicated cache for Mamba + Attention architectures (Nemotron-H, Jamba, GatedDeltaNet)
- Automatic cache type selection based on model architecture
- Cache warming API (`POST /v1/cache/warm`) for pre-loading common prompts
- Cache stats API (`GET /v1/cache/stats`) for monitoring hit rates and memory usage

### Sampling & Generation Control

Full control over text generation:

- **Temperature** (0.0 - 2.0) -- creativity control
- **Top-P** (0.0 - 1.0) -- nucleus sampling
- **Top-K** (integer) -- top-K token filtering
- **Min-P** (0.0 - 1.0) -- minimum probability threshold
- **Repetition Penalty** -- penalize repeated tokens
- **Stop Sequences** -- custom stopping strings
- **Max Tokens** -- output length limit (up to 131072)
- **Request Timeout** -- per-request timeout override
- **Structured Output** -- `response_format` with `json_object` or `json_schema` modes for guaranteed valid JSON
- **Streaming** with proper Unicode handling (emoji, CJK, Arabic multi-byte characters)
- **Usage stats** in streaming responses (`stream_options.include_usage`)

### Model Conversion & Quantization

Convert models directly in-app via the Tools tab:

- **16-bit to MLX** -- convert HuggingFace safetensors to MLX format
- **16-bit to quantized** -- quantize to 2-bit, 4-bit, or 8-bit MLX
- **GGUF to MLX** -- import GGUF models into MLX safetensors format
- **MLX to JANG** -- adaptive mixed-precision quantization (different bits per layer type)
- **Model Inspector** -- view config.json, architecture, layer structure
- **Model Doctor** -- diagnostic checks (load test, token count, memory estimation)
- Progress tracking with real-time status

### Image Generation

Generate images locally with Flux and Z-Image models:

- **Flux Schnell** -- 4-step fast generation
- **Flux Dev** -- 20-step high-quality generation
- **Z-Image Turbo** -- fast turbo generation (4-bit and 8-bit)
- **Flux Klein** -- lightweight 4B parameter model
- **Flux Kontext** -- subject-consistent editing
- **Flux Krea** -- aesthetic fine-tuned generation
- Configurable steps, guidance scale, height, width, seed, sampler
- Multiple samplers: euler, euler_ancestral, heun, dpmpp_2m_sde, dpmpp_sde
- Quantized model support (2-bit to 8-bit)
- Image gallery with generation history, save, and settings persistence
- OpenAI-compatible `/v1/images/generations` endpoint with `usage` field

### Chat Interface

Full-featured conversation UI:

- **Persistent history** -- SQLite (WAL mode) with full message, metrics, and tool call history
- **Markdown rendering** -- GitHub-flavored markdown with syntax highlighting
- **Reasoning display** -- collapsible thinking sections for reasoning models
- **Tool call display** -- inline tool execution with status and results
- **Streaming metrics** -- live tokens/second, time-to-first-token (TTFT), prompt processing speed, prefix cache hit rate
- **System prompts** -- per-chat custom system message
- **Chat settings** -- per-chat overrides for temperature, top-p, top-k, min-p, repetition penalty, max tokens, stop sequences
- **Chat folders** -- hierarchical organization
- **Message search** -- full-text search across chat history
- **Export/Import** -- ShareGPT format
- **Voice chat** -- STT + TTS integration

### Model Management

- **HuggingFace browser** -- search, filter by text/image, and download models directly in-app
- **Download queue** -- multiple concurrent downloads with real-time progress bars and cancel support
- **Model size display** -- file sizes from safetensors metadata before downloading
- **Local model discovery** -- auto-scan `~/.mlxstudio/models`, `~/.cache/huggingface/hub`, `~/.exo/models`, and custom directories
- **Deduplication** -- strict format detection prevents false positive model matches
- **Zero-config detection** -- reads model config.json to auto-set tool parsers, reasoning parsers, cache types, and chat templates
- **65+ model families** in the auto-detection registry with two-tier detection (config.json `model_type` primary, name regex fallback)

### Desktop Experience

- **5 app modes** -- Chat, Server, Image, Tools, API
- **Menu bar tray** -- live server status, GPU memory, running models, quick controls
- **Multi-session** -- run multiple models simultaneously on different ports
- **Dock icon** -- restore on click, close-to-tray support
- **Dark and light themes** -- system-respecting
- **Keyboard shortcuts** -- common actions
- **Toast notifications** -- user feedback
- **Update banner** -- new version detection

---

## Advanced Quantization

MLX Studio supports standard MLX quantization (4-bit, 8-bit) as well as **JANG adaptive mixed-precision** -- an advanced format that assigns different bit widths to different layer types for better quality at the same model size.

- Convert in-app via the Tools tab, or via CLI: `vmlx convert model --jang-profile JANG_3M`
- Pre-quantized models available at [JANGQ-AI on HuggingFace](https://huggingface.co/JANGQ-AI)
- Stays quantized in GPU memory -- native MLX `QuantizedLinear` + `quantized_matmul`
- Compatible with all caching layers (prefix, paged, disk, KV quant)

See the [vMLX source repo](https://github.com/jjang-ai/vmlx#advanced-quantization) for profiles and conversion details.

### Smelt Mode (Partial Expert Loading)

For MoE models that don't fit in RAM, **Smelt** loads only a subset of experts per layer from SSD and keeps the backbone resident. Response quality stays coherent while RAM usage drops; throughput scales inversely with expert % loaded because expert swaps hit SSD on the hot path.

Verified coherent (non-looping) on `Nemotron-Cascade-2-30B-A3B-JANG_4M-CRACK` at 25 %, 50 %, and 100 % expert loading. Clean RAM / tok-s benchmarks to follow.

**Smelt is mutually exclusive with VLM mode.** MLX Studio / vMLX v1.3.33+ automatically disables `--is-mllm` when smelt is active (with a warning) because the vision tower is not wired through the partial-expert loader — image input on a smelt-loaded VLM would produce garbage logits. Use a text-only model when running smelt, or disable smelt when running a VLM.

Requires an MoE model in JANG format (e.g. `Nemotron-Cascade-2-30B-A3B-JANG_4M-CRACK`, `Qwen3.5-35B-A3B-JANG_2S-TEXT`). Not compatible with dense models (no experts to partial-load).

---

## System Requirements

| Requirement | Minimum |
|---|---|
| **macOS** | 14.0 Sonoma or later |
| **Chip** | Apple Silicon (M1 / M2 / M3 / M4) |
| **RAM** | 8 GB (16 GB+ recommended for larger models) |
| **Disk** | ~500 MB for app; models range from 1-50 GB each |

---

## Build from Source

```bash
git clone https://github.com/jjang-ai/vmlx.git
cd vmlx

# Python engine
python3 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"

# Electron app
cd panel && npm install && npm run build
npx electron-builder --mac --dir   # .app bundle
npx electron-builder --mac dmg     # DMG installer
```

---

## Links

| Resource | Link |
|---|---|
| **Source Code** | [github.com/jjang-ai/vmlx](https://github.com/jjang-ai/vmlx) |
| **PyPI** | [pypi.org/project/vmlx](https://pypi.org/project/vmlx/) |
| **MLX Models** | [huggingface.co/mlx-community](https://huggingface.co/mlx-community) |
| **JANG Models** | [huggingface.co/JANGQ-AI](https://huggingface.co/JANGQ-AI) |
| **Website** | [vmlx.net](https://vmlx.net) |

---

## License

Apache License 2.0

---

<p align="center">
  Built by <a href="https://github.com/jjang-ai">Jinho Jang</a> &bull; <a href="mailto:eric@jangq.ai">eric@jangq.ai</a> &bull; <a href="https://jangq.ai">JANGQ AI</a> &bull; <a href="https://ko-fi.com/jangml">Support on Ko-fi</a>
</p>

---

## 한국어 (Korean)

### MLX Studio — Apple Silicon을 위한 네이티브 macOS AI 앱

Mac에서 LLM, VLM, 이미지 생성 및 편집 모델을 완전히 로컬로 실행하세요.

> **JANG 2비트가 MLX 4/3/2비트보다 높은 성능** — 적응형 혼합 정밀도 양자화(JANG\_2S, JANG\_2.6)가 MiniMax M2.5, Qwen3 등에서 표준 MLX 양자화를 능가합니다. [jangq.ai](https://jangq.ai)에서 벤치마크 확인. [JANGQ-AI](https://huggingface.co/JANGQ-AI)에서 사전 양자화 모델 다운로드.

**설치:** [최신 DMG 다운로드](https://github.com/jjang-ai/mlxstudio/releases/latest) — 드래그 앤 드롭으로 설치.

### 주요 기능

| 기능 | 설명 |
|------|------|
| **채팅** | 대화 인터페이스, 도구 호출, 에이전트 코딩 |
| **이미지 생성** | Flux Schnell/Dev, Z-Image Turbo, FLUX.2 Klein |
| **이미지 편집** | Qwen Image Edit (텍스트 지시 기반 편집) |
| **5단계 캐싱** | 프리픽스, 페이지드, KV 양자화, 디스크 캐시 |
| **API 서버** | OpenAI + Anthropic 호환 API |
| **30개 도구** | 파일, 웹 검색, Git, 터미널 내장 도구 |

<p align="center">
  개발자: <a href="https://github.com/jjang-ai">장진호</a> (eric@jangq.ai)<br>
  <a href="https://jangq.ai">JANGQ AI</a> &bull;
  <a href="https://ko-fi.com/jangml">Ko-fi로 후원하기</a>
</p>
