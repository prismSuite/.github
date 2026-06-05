<div align="center">

<!-- prettier-ignore -->
<svg width="100%" viewBox="0 0 680 220" xmlns="http://www.w3.org/2000/svg">
<defs>
  <linearGradient id="spectrum" x1="0" y1="0" x2="1" y2="0">
    <stop offset="0%"   stop-color="#f28b82"/>
    <stop offset="20%"  stop-color="#fbbf24"/>
    <stop offset="40%"  stop-color="#a8e6a3"/>
    <stop offset="60%"  stop-color="#60a5fa"/>
    <stop offset="80%"  stop-color="#a78bfa"/>
    <stop offset="100%" stop-color="#f0abfc"/>
  </linearGradient>
  <linearGradient id="beam-in" x1="0" y1="0" x2="1" y2="0">
    <stop offset="0%" stop-color="#e0e0e0" stop-opacity="0.6"/>
    <stop offset="100%" stop-color="#e0e0e0" stop-opacity="0.15"/>
  </linearGradient>
</defs>
<rect width="680" height="220" fill="#080808"/>
<pattern id="dots" width="20" height="20" patternUnits="userSpaceOnUse">
  <circle cx="10" cy="10" r="0.75" fill="rgba(255,255,255,0.045)"/>
</pattern>
<rect width="680" height="220" fill="url(#dots)"/>
<polygon points="72,100 162,124 162,118" fill="url(#beam-in)"/>
<polygon points="215,38 148,166 282,166" fill="#1e1e1e" stroke="rgba(255,255,255,0.12)" stroke-width="0.8"/>
<line x1="215" y1="38" x2="282" y2="166" stroke="rgba(255,255,255,0.18)" stroke-width="1"/>
<line x1="268" y1="148" x2="620" y2="80"  stroke="#f28b82" stroke-width="1.4" opacity="0.9"/>
<line x1="268" y1="150" x2="620" y2="101" stroke="#fbbf24" stroke-width="1.3" opacity="0.9"/>
<line x1="268" y1="152" x2="620" y2="124" stroke="#a8e6a3" stroke-width="1.3" opacity="0.85"/>
<line x1="268" y1="154" x2="620" y2="148" stroke="#60a5fa" stroke-width="1.4" opacity="0.9"/>
<line x1="268" y1="156" x2="620" y2="172" stroke="#a78bfa" stroke-width="1.3" opacity="0.9"/>
<line x1="268" y1="158" x2="620" y2="196" stroke="#f0abfc" stroke-width="1.2" opacity="0.85"/>
<rect x="268" y="205" width="352" height="2" rx="1" fill="url(#spectrum)" opacity="0.5"/>
<text font-family="'DM Serif Display', Georgia, serif" font-size="54" fill="url(#spectrum)" x="318" y="138" text-anchor="middle">prism</text>
<text font-family="'DM Mono', monospace" font-size="22" letter-spacing="6" fill="rgba(255,255,255,0.35)" x="318" y="168" text-anchor="middle">SUITE</text>
<text font-family="'DM Mono', monospace" font-size="10" fill="rgba(255,255,255,0.2)" x="340" y="198" text-anchor="middle" letter-spacing="3">pitahayaDevSoft</text>
<line x1="40" y1="18" x2="640" y2="18" stroke="rgba(255,255,255,0.06)" stroke-width="0.5"/>
<line x1="40" y1="208" x2="640" y2="208" stroke="rgba(255,255,255,0.06)" stroke-width="0.5"/>
</svg>

</div>

---

Native desktop tools for audio production. Built under [pitahayaDevSoft](https://pitahayaDevSoft.com).

<br>

## Tools

| | Project | Stack | Description |
|---|---|---|---|
| 🎛 | [**prismConsole**](https://github.com/prismSuite/prismConsole) | Tauri · Rust · React | Desktop platform for AI agent orchestration and DSP. Real-time spectral analysis, agent lifecycle management, REAPER integration via ReaperBridge. |
| ✂️ | [**prismSplit**](https://github.com/prismSuite/prismSplit) | Rust · egui · Python | Audio stem separation. Karaoke isolation via MDX-Net and Demucs. Native binary, self-repairing Python engine, CUDA/MPS hardware acceleration. |
| 🎚 | [**prismControl**](https://github.com/prismSuite/prismControl) | Python · NumPy · Ollama | Agentic live mixing console control over OSC/UDP. Two-layer architecture: deterministic Math Engine + local LLM orchestration. Offline-first. |

<br>

## Design

All three tools share the **MonolithUI** design system — dark industrial surfaces, inset tactile depth, DM Sans + DM Mono typography. No WebViews in prismSplit (egui renders directly to OS graphics drivers). prismConsole and prismControl use Tauri + React.

<br>

## License

Commercial software. Contact [pitahayaDevSoft](https://pitahayaDevSoft.com) for licensing.
