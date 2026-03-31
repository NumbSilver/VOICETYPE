# VoiceType Troubleshooting

## Debug log

```bash
cat /tmp/dji-dictation/debug.log
```

## Doctor command

```bash
node cli/index.mjs doctor
```

Reports: Typeless DB, Karabiner config, installed script/config, device status, update availability.

## Common issues

### Keyboard workflow (both paths)

| Symptom | Cause | Fix |
|---------|-------|-----|
| Dictation never starts | Dictation off or Karabiner rule missing | Enable Dictation; run `doctor` |
| No sound / overlay after dictation | Accessibility permission | Grant Accessibility to `osascript` and terminal app |
| Sound but no overlay | Swift HUD binary missing | `node cli/index.mjs update` |
| Typeless DB missing | Typeless not installed/opened | Download from https://www.typeless.com/referral?tl_src=macos, open once, then `install` or `doctor` |
| Enter not sent | Terminal lacks Accessibility | Grant Accessibility to iTerm2 / Terminal.app |
| Stale behavior | Outdated install | `node cli/index.mjs update` |

### DJI receiver (path 1 only)

| Symptom | Cause | Fix |
|---------|-------|-----|
| Button does nothing | Input Monitoring | Privacy & Security → Input Monitoring → Karabiner |
| Button only changes volume | `keyboard`-only install or device not grabbed | Connect receiver; reinstall with `--trigger-mode keyboard+dji`; verify `"is_consumer": true, "ignore": false` in Karabiner device list |

### Mac mic (path 2 only)

| Symptom | Cause | Fix |
|---------|-------|-----|
| Dictation picks wrong mic | System input setting | System Settings → Sound → Input; select correct device |

## Permissions checklist

All under **System Settings → Privacy & Security**:

1. **Input Monitoring** → Karabiner-Elements, karabiner_grabber
2. **Accessibility** → Karabiner-Elements, terminal app
3. **Dictation** → Keyboard → Dictation → On

## Key paths

| Path | Purpose |
|------|---------|
| `~/.config/karabiner/scripts/dictation-enter.sh` | Installed runtime script |
| `~/.config/dji-mic-dictation/config.env` | User config |
| `~/Library/Application Support/Typeless/typeless.db` | Typeless database |
| `/tmp/dji-dictation/debug.log` | Debug log |
| `~/.config/karabiner/karabiner.json` | Karabiner config (managed entries) |
