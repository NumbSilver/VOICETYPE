---
name: voicetype
description: >-
  Install and manage VoiceType, a macOS Fn-key dictation/send workflow.
  Guides users through hardware path selection (Mac mic only vs DJI Mic Mini),
  runs the CLI installer, diagnoses permission and config issues, and manages
  updates/uninstall. Use when the user mentions VoiceType, macOS dictation
  workflow, Fn dictation, voice typing setup, DJI Mic Mini trigger, or wants
  to install/update/troubleshoot this tool.
---

# VoiceType

macOS keyboard-first dictation workflow: `Fn` starts dictation, stops it, and confirms send. Works with any mic macOS Dictation supports.

## Step 1: Ask hardware path (required on first install)

Before running the installer, determine the user's setup. Use the AskQuestion tool:

```
Question: "Which microphone setup do you use?"
Options:
  - "Mac built-in mic / headset (no DJI receiver)"   → path = mac
  - "DJI Mic Mini with USB receiver"                  → path = dji
```

This determines:

| User chose | `--trigger-mode` | README to point to |
|------------|------------------|--------------------|
| Mac mic    | `keyboard`       | `README_MAC_MIC.md` / `README_MAC_MIC_CN.md` |
| DJI        | `keyboard+dji`   | `README_DJI.md` / `README_DJI_CN.md` |

## Step 2: Prerequisites check

Before installing, verify (or guide the user to install):

1. **Xcode CLI Tools** — `xcode-select --install`; if license not accepted: `sudo xcodebuild -license accept` (requires user's sudo password in their own terminal — agent cannot do this)
2. **Node.js ≥ 20** — `node --version`; install via `brew install node` or https://nodejs.org/
3. **Karabiner-Elements** — `brew install --cask karabiner-elements` (the CLI installer can also do this)
4. **macOS Dictation** — System Settings → Keyboard → Dictation → On
5. **Typeless** — download from https://www.typeless.com/referral?tl_src=macos and open once

## Step 3: Run the installer

```bash
npx github:NumbSilver/VOICETYPE install --trigger-mode <keyboard|keyboard+dji>
```

Add `--yes` to skip interactive confirmations. Add `--json` for machine-readable output.

The installer handles: Karabiner rule merge, script copy, config file creation, permission reminders.

If the user already cloned the repo, use `node cli/index.mjs install` from the repo root instead.

## Lifecycle commands

| Command | What it does |
|---------|-------------|
| `node cli/index.mjs update` | Refresh scripts/rules, preserve config and trigger mode |
| `node cli/index.mjs doctor` | Diagnose: Typeless DB, Karabiner state, permissions, update availability |
| `node cli/index.mjs config` | Change audio feedback / ready overlay / review window |
| `node cli/index.mjs uninstall` | Remove managed entries only |

## Troubleshooting

For detailed troubleshooting steps, read [references/troubleshooting.md](references/troubleshooting.md).

Quick first step: `cat /tmp/dji-dictation/debug.log`

## Permissions checklist

All in **System Settings → Privacy & Security**:

1. **Input Monitoring** → Karabiner-Elements, karabiner_grabber
2. **Accessibility** → Karabiner-Elements, terminal app (iTerm2 / Terminal.app)
3. **Dictation** → Keyboard → Dictation → On

## Config file

`~/.config/dji-mic-dictation/config.env`:

- `DJI_ENABLE_AUDIO_FEEDBACK=1|0`
- `DJI_PRECONFIRM_SOUND_NAME=<sound from /System/Library/Sounds>`
- `DJI_ENABLE_READY_HUD=1|0`
- `DJI_REVIEW_WINDOW_SECONDS=<seconds>`

Use `node cli/index.mjs config` to change interactively.

## Switching paths later

- Mac → DJI: `node cli/index.mjs install --trigger-mode keyboard+dji`
- DJI → Mac only: `node cli/index.mjs install --trigger-mode keyboard`
