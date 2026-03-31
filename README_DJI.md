# VoiceType — DJI Mic Mini path (path 1)

You have a **DJI Mic Mini** and its **USB receiver**. You can map the receiver’s consumer button to the **same** **`Fn`** workflow (start / stop / send) in addition to the keyboard.

← [Back to hub](README.md) · [中文](README_DJI_CN.md)

## What you get

Same **triple-`Fn`** sequence as everyone else:

```
Fn press 1 → start dictation
Fn press 2 → stop + ready overlay + chime when text lands
Fn press 3 → send Enter (within 4s)
```

**Optional:** with `keyboard+dji` installed, the **receiver button** mirrors that sequence when the receiver is connected and Karabiner can grab the device.

**Audio:** you can still use the **DJI mic** for speech if that is what macOS Dictation hears, or mix setups—this README focuses on **hardware trigger** wiring, not replacing Dictation’s mic picker.

## Prerequisites

| Requirement | Notes |
|-------------|-------|
| macOS | Tested on macOS Sequoia |
| [Karabiner-Elements](https://karabiner-elements.pqrs.org/) | Required |
| macOS Dictation | System Settings → Keyboard → Dictation → On |
| [Typeless](https://www.typeless.com/referral?tl_src=macos) | Required today (Typeless DB) |
| DJI Mic Mini + receiver | Optional **trigger**; vendor_id **11427**, product_id **16401** (Consumer HID) |

During `node cli/index.mjs install`, choose **DJI Mic Mini** when asked. If the receiver is plugged in, the installer can enable **`keyboard+dji`** automatically; if not, you can still preconfigure mappings for later.

## Install

```bash
git clone https://github.com/NumbSilver/VOICETYPE.git VoiceType
cd VoiceType
npm install
node cli/index.mjs install
```

Use the **DJI** path at the first prompt, or `--trigger-mode keyboard+dji`.

Optional: `npm link` then `dji-mic-dictation install`.

## Quick start

1. **Typeless** installed and opened once.  
2. **Karabiner-Elements** + permissions (**Input Monitoring**, **Accessibility**).  
3. **Dictation** enabled.  
4. Plug in the **DJI receiver** when possible, then run `node cli/index.mjs install` and confirm the DJI path.

## Receiver / Karabiner notes

- The receiver is a **Consumer HID** device. Managed installs set `"is_consumer": true, "ignore": false` in Karabiner’s device list when DJI mode is on.  
- If the button **only changes volume**, the DJI trigger profile is not active or the device is not grabbed—re-run install with the receiver connected or check Karabiner device settings.

## Custom HID trigger (advanced)

```bash
'/Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_cli' --list-connected-devices
```

Adjust vendor/product IDs and reinstall with `--trigger-mode keyboard+dji` if you adapt the template.

## Troubleshooting

```bash
cat /tmp/dji-dictation/debug.log
```

### Hardware button

| Symptom | Likely cause | What to try |
|---------|----------------|-------------|
| Button does nothing | Input Monitoring | Privacy & Security → Input Monitoring → Karabiner |
| Button changes volume only | `keyboard`-only install or device not grabbed | Receiver connected; `install` with DJI path; verify Karabiner device entry |

### Shared (keyboard + Typeless)

| Symptom | What to try |
|---------|-------------|
| No overlay / sound | Accessibility for `osascript` / terminal |
| Typeless DB missing | Open Typeless once |
| Stale behavior | `node cli/index.mjs update` |

## Configuration

`~/.config/dji-mic-dictation/config.env` — `node cli/index.mjs config`.

## Keyboard-only fallback

If you want **no** receiver mappings, reinstall with the **Mac microphone** path or `--trigger-mode keyboard`. See [README_MAC_MIC.md](README_MAC_MIC.md).

## License

MIT — see [LICENSE](LICENSE).
