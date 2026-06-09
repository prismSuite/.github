<img src="https://raw.githubusercontent.com/prismSuite/.github/main/prismsuite-header.svg" width="100%" alt="prismSuite"/>

<br/>

[![prismSplit](https://img.shields.io/badge/prismSplit-stem_separation-6C3FC5?style=for-the-badge&logo=rust&logoColor=white)](https://github.com/prismSuite/prismSplit)
[![prismConsole](https://img.shields.io/badge/prismConsole-AI_orchestration-6C3FC5?style=for-the-badge&logo=tauri&logoColor=white)](https://github.com/prismSuite/prismConsole)
[![prismController](https://img.shields.io/badge/prismController-OSC_mixer_control-6C3FC5?style=for-the-badge&logo=python&logoColor=white)](https://github.com/prismSuite/prismController)
[![License](https://img.shields.io/badge/license-proprietary-1a1a2e?style=for-the-badge)](https://github.com/prismSuite)

---

## What is prismSuite?

```
prismSuite is a collection of native audio production tools.

No Electron. No WebView. No browser runtime in your DAW workflow.

Each tool is a standalone application. Together they form a unified
production environment — from stem separation to real-time mixer
control to AI agent orchestration, all integrated with REAPER.

Design language: MonolithUI — Industrial Audio Skeuomorphism.
Dark anodized aluminum aesthetic. Exposed hardware elements.
Built for engineers who work in dark rooms with bright monitors.
```

---

## Repos

### [prismSplit](https://github.com/prismSuite/prismSplit)

> Stem separation and audio isolation platform.

**Stack:** Rust · egui · eframe · Python 3.9–3.11 · ONNX Runtime · PyTorch · Demucs · MDX-Net

Separates audio into specialized stems — vocals, drums, bass, other — with a focus on high-quality karaoke separation. Built as a native binary using `egui`/`eframe` for GPU-rendered UI, zero WebView dependency. The Rust chassis orchestrates an isolated, self-repairing Python inference subprocess over a stdio JSON protocol.

| | |
|---|---|
| Inference | ONNX (MDX-Net) + PyTorch (Demucs) |
| Hardware | NVIDIA CUDA (Win/Linux) · Apple Silicon MPS/CoreML (macOS) |
| Models | Downloads from UVR servers, SHA-256 verified, MD5 local dedup |
| Binary size | 5–8MB native executable |
| Runtime | Self-repairing Python venv — repairs broken `numpy`/`onnxruntime` in-place |

```
Architecture:

  [ egui Native UI Chassis ]
            ▲
            │  Rust channels / AppMsg
            ▼
  [ Rust Orchestration Core ]
            │
            │  stdio JSON protocol
            ▼
  [ Embedded Python Inference ] ──► [ ONNX Runtime / PyTorch ]
                                    ├── CUDA (Windows / Linux)
                                    └── CoreML / MPS (macOS)
```

```bash
git clone https://github.com/prismSuite/prismSplit
cd prismSplit
cargo run          # dev
cargo build --release
```

---

### [prismConsole](https://github.com/prismSuite/prismConsole)

> Desktop platform for AI agent orchestration and DSP telemetry.

**Stack:** Tauri v2 · Rust · React 19 · TypeScript (strict) · rustfft · rayon · Tokio

Integrates Digital Signal Processing with AI agent orchestration. The Rust backend handles spectral analysis (FFT), agent lifecycle management, and REAPER bridge — without blocking the frontend. The React 19 frontend renders real-time oscilloscope telemetry using the MonolithUI design system.

| Layer | Responsibility |
|---|---|
| DSP Engine | FFT spectral analysis via `rustfft` + `rayon` |
| Agent Server Protocol | Manages local AI executables (`claude-code`, `gemini-cli`) via `tokio` |
| ReaperBridge | REAPER transport, tracks, effects via local control protocols |
| MonolithUI Frontend | Real-time telemetry · oscilloscope grid · suite integration |

Features:
- Detects and cross-launches `prismSplit` automatically when installed
- Real-time CPU / RAM / disk monitoring via `sysinfo`
- Strictly-typed IPC — errors propagate from Rust to UI with no silent failures
- Agent stdout monitoring with task queues per executable

```bash
git clone https://github.com/prismSuite/prismConsole
cd prismConsole
npm install
cargo tauri dev       # dev
cargo tauri build     # production
```

---

### [prismController](https://github.com/prismSuite/prismController)

> Agentic OSC interface for real-time Behringer XR12 mixer control.

**Stack:** Python 3.11+ · python-osc · Ollama (Qwen2.5:3b) · numpy · Pydantic · Rich

Local, offline agentic interface for the Behringer XR12 mixing console. Combines a deterministic Math Engine with a local LLM orchestrator. The LLM handles intent — it never dispatches OSC commands directly. All execution goes through the Math Engine with parameter locks and hard limiters enforced at the dispatch layer.

Architecture laws (non-negotiable):

```
1. Separation of Concerns  — LLM manages intent, not execution
2. Safety First            — parameter locks enforced at dispatch layer
3. Console Sync            — OSC listener return stream is single source of truth
4. Live Mode Immunity      — agent is strictly read-only during LIVE mode
```

Operative modes:

| Mode | Behavior |
|---|---|
| `SOUNDCHECK` | Full agent + Math Engine access. Gain staging, EQ adjustments |
| `STAGE` | Reduced automation. Manual overrides prioritized |
| `LIVE` | Agent read-only. Math Engine only — deterministic auto-notch feedback suppression |

```bash
python -m venv .venv && source .venv/bin/activate
pip install python-osc numpy ollama pydantic rich
python main.py
```

CLI commands: `/mode <soundcheck\|stage\|live>` · `/lock <address>` · `/gain <channels...>`

---

## Design Language

```
MonolithUI — Industrial Audio Skeuomorphism · Dark Brutalism

Surfaces:    Dark anodized aluminum · #0a0a0c base
Accent:      Prism violet #6C3FC5
Typography:  Share Tech Mono (labels) · Arial Black (headers)
Motion:      Fade-in staggered · no bounce · no ease-out curves
Hardware:    Beveled panels · blocky status meters · Tahoma-style spacing
Inspiration: Rack gear UIs · oscilloscope displays · vintage mixing desks
```

---

## Suite Integration Map

```
prismConsole ──────── detects ──────► prismSplit
     │                                    │
     │  REAPER Bridge                     │  Inference Engine
     ▼                                    ▼
  REAPER DAW ◄──── OSC ──── prismController (XR12 Mixer)
```

All three tools are standalone. The integration is opt-in and detection-based — no shared daemon, no required install order.

---

## Build Requirements

| Tool | Version |
|---|---|
| Rust | Stable 1.80+ |
| Python | 3.9 / 3.10 / 3.11 (prismSplit, prismController) |
| Node.js | v18+ (prismConsole) |
| Ollama | Latest (prismController) |
| CUDA | Optional — GPU acceleration for prismSplit |

---

<div align="right">

*prismSuite — Designed for precision and performance.*
*Part of the [julesklord](https://github.com/julesklord) ecosystem.*

</div>
