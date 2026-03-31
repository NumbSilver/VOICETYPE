# VoiceType — Mac microphone path (path 2)

You use **macOS Dictation** with your **Mac built-in microphone, headset mic, or any input macOS uses for dictation**. **No DJI Mic Mini** is involved. The **`Fn`** key still drives start / stop / send.

← [Back to hub](README.md) · [中文](README_MAC_MIC_CN.md)

## What you get

```
Fn press 1 → start dictation → speak (audio goes to the mic Dictation is using)
Fn press 2 → stop dictation → ready overlay + chime when text lands
Fn press 3 → send Enter to the frontmost app

No third press within 4s → quiet reset
```

## Microphone & Dictation

- Turn on **Dictation** under **System Settings → Keyboard → Dictation**.
- macOS uses your **current input device** for dictation. Pick it under **System Settings → Sound → Input** (or the menu-bar sound control) if needed.
- This project does **not** replace Dictation’s audio pipeline—it only automates **Fn** and the send/confirm flow after Typeless has written text.

## Prerequisites

| Requirement | Notes |
|-------------|-------|
| macOS | Tested on macOS Sequoia |
| [Karabiner-Elements](https://karabiner-elements.pqrs.org/) | `brew install --cask karabiner-elements` |
| macOS Dictation | On; input device set as you prefer |
| [Typeless](https://www.typeless.com/referral?tl_src=macos) | Required today: detection uses the Typeless DB |

**No DJI hardware.** During `node cli/index.mjs install`, choose **Mac microphone** when asked so the installer stays **keyboard-only** (no receiver button mapping).

## Install

```bash
git clone https://github.com/NumbSilver/VOICETYPE.git VoiceType
cd VoiceType
npm install
node cli/index.mjs install
```

When prompted, indicate you **do not** use a DJI Mic Mini receiver, or pass `--trigger-mode keyboard`.

Optional: `npm link` then `dji-mic-dictation install`.

## Quick start

1. Install and open **Typeless** at least once.  
2. Install **Karabiner-Elements**; grant **Input Monitoring** and **Accessibility** as prompted.  
3. Enable **Dictation** and verify your **input mic** in Sound settings.  
4. Run `node cli/index.mjs install` and pick the **Mac microphone** path.

## Troubleshooting (this path)

```bash
cat /tmp/dji-dictation/debug.log
```

| Symptom | Likely cause | What to try |
|---------|----------------|-------------|
| Dictation picks wrong mic | System input | Sound → Input; or Dictation language/input settings |
| Dictation never starts | Dictation off / Karabiner | Turn on Dictation; `node cli/index.mjs doctor` |
| No sound / no overlay | Accessibility | Grant to `osascript` and your terminal |
| Sound but no overlay | Missing Swift HUD binary | `node cli/index.mjs update` |
| Typeless DB missing | Typeless not opened | Open Typeless once, then `install` / `doctor` |
| Enter not sent | Terminal | Accessibility for iTerm2 / Terminal.app |

### Permissions

1. **Input Monitoring** → Karabiner-Elements, karabiner_grabber  
2. **Accessibility** → Karabiner-Elements, terminal app  
3. **Dictation** → Keyboard → Dictation → On  

## Configuration

`~/.config/dji-mic-dictation/config.env` — use `node cli/index.mjs config`.

## If you later buy a DJI Mic Mini

Run `node cli/index.mjs install` again and choose the DJI path, or use `--trigger-mode keyboard+dji`. See [README_DJI.md](README_DJI.md).

## License

MIT — see [LICENSE](LICENSE).
