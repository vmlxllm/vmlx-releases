# vMLX

**The most complete MLX inference engine for Mac.**

Run AI locally on Apple Silicon with voice, vision, Mamba, 5-layer caching, and 20+ agentic tools. No Python, pip, Docker, or command-line setup required.

## Download

**[Download vMLX for macOS](https://github.com/vmlxllm/vmlx-releases/releases/latest)** (Apple Silicon, arm64)

Or visit [vmlx.net/download](https://vmlx.net/download) for installation instructions.

## Requirements

| | Minimum | Recommended |
|---|---|---|
| **Platform** | macOS 26+ (Tahoe) | macOS 26+ (Tahoe) |
| **Chip** | Apple Silicon (M1) | M1 Pro or later |
| **RAM** | 8 GB unified memory | 16 GB+ (for 7B–20B models) |

> **Note:** MLX requires Metal 4.0, which is only available on macOS 26 (Tahoe) or later. Earlier macOS versions will not work.

More unified memory = larger models. 16 GB handles up to ~20B parameters, 32 GB handles ~35B, 64 GB handles ~70B, and 192 GB handles 400B+ MoE models.

## Installation

1. Download the DMG from [Releases](https://github.com/vmlxllm/vmlx-releases/releases/latest)
2. Open the DMG and drag vMLX to Applications
3. Launch vMLX — it auto-installs the MLX inference engine on first run
4. Search and download any MLX model from HuggingFace, or use your own
5. Start chatting — local AI with an OpenAI-compatible API at `http://127.0.0.1:8000`

The app is code-signed and notarized by Apple — no Gatekeeper warnings.

## Features

- **Multi-model sessions** — run multiple models simultaneously
- **Streaming chat** with OpenAI-compatible API
- **5-layer caching** — prefix + paged KV + q4/q8 quantization + batching + disk
- **Speculative decoding** — draft model acceleration for faster inference
- **50+ auto-detected architectures** — Llama, Qwen, Mistral, Gemma, Phi, Mamba, and more
- **Vision & multimodal** — image understanding with VLMs
- **Voice chat** — speak to your models
- **20+ agentic tools** — file, shell, git, web search, browser
- **14 tool call parsers** — Qwen, Hermes, Llama, DeepSeek, Mistral, and more
- **4 reasoning parsers** — thinking/reasoning content separation
- **Embeddings** and benchmarks
- **Mamba/SSM support** — state-space models with hybrid caching

## Models

We publish optimized MLX models at [huggingface.co/dealignai](https://huggingface.co/dealignai), including abliterated CRACK and REAP-optimized variants.

## Links

- [vmlx.net](https://vmlx.net) — Website
- [vmlx.net/download](https://vmlx.net/download) — Download & install guide
- [huggingface.co/dealignai](https://huggingface.co/dealignai) — Optimized models

---

Copyright 2026 ShieldStack LLC. All rights reserved.
