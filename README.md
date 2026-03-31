# VoiceType

**Keyboard-first** dictation and send on macOS: **`Fn`** starts and stops dictation, then confirms send. It works with **any microphone** macOS Dictation can use—including the **built-in Mac mic** or a headset.

Works in any app that accepts text: Claude Code, WeChat, Feishu/Lark, Telegram, Slack, VS Code, Notes, and more.

[中文总览](README_CN.md)

## Choose your setup path

1. **Run the installer** from this repo (see below). In interactive mode it **first asks** whether you have a **DJI Mic Mini receiver** (the USB receiver used with that kit).
2. **Follow the README that matches your answer:**
   - **You have a DJI Mic Mini** → **[README_DJI.md](README_DJI.md)** (English) · **[README_DJI_CN.md](README_DJI_CN.md)** (中文) — *path 1*
   - **You do not** (you use only the **Mac / headset mic** with Dictation) → **[README_MAC_MIC.md](README_MAC_MIC.md)** · **[README_MAC_MIC_CN.md](README_MAC_MIC_CN.md)** — *path 2*

Non-interactive installs (`--yes`, `--json`, or CI) skip that question; pass `--trigger-mode keyboard` for Mac-mic-only, or `--trigger-mode keyboard+dji` when you want receiver mappings.

## One-line install

```bash
npx github:NumbSilver/VOICETYPE install
```

That's it. `npx` fetches the repo, installs dependencies, and runs the interactive installer.

<details>
<summary>Alternative: clone first, then install</summary>

```bash
git clone https://github.com/NumbSilver/VOICETYPE.git VoiceType
cd VoiceType
npm install
node cli/index.mjs install
```

</details>

## Shared prerequisites (both paths)

| Requirement | Notes |
|-------------|-------|
| macOS | Tested on macOS Sequoia |
| Xcode CLI Tools | `xcode-select --install` — if prompted for license: `sudo xcodebuild -license accept` |
| [Node.js](https://nodejs.org/) ≥ 20 | `brew install node` or [download](https://nodejs.org/) |
| [Karabiner-Elements](https://karabiner-elements.pqrs.org/) | The installer can `brew install` it for you |
| macOS Dictation | System Settings → Keyboard → Dictation → On |
| [Typeless](https://www.typeless.com/referral?tl_src=macos) | Required today (text detection uses its database) |

## Repository layout

```
VoiceType/
├── README.md / README_CN.md           # This hub (pick your path)
├── README_DJI.md / README_DJI_CN.md   # Path 1: DJI Mic Mini + Fn
├── README_MAC_MIC.md / …_CN.md         # Path 2: Mac / headset mic + Fn
├── cli/
├── scripts/dictation-enter.sh
├── karabiner/
└── …
```

## License

MIT — see [LICENSE](LICENSE).
