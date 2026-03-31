# VoiceType

在 macOS 上用 **`Fn`** 完成「开始听写 → 结束 → 确认发送」。听写输入来自 **系统听写所用的麦克风**：可以是 **Mac 自带麦克风**、耳机麦，或（可选）你另购的无线麦方案。

适用于 Claude Code、微信、飞书、Telegram、Slack、VS Code、备忘录等所有能输入文字的场景。

[English hub](README.md)

## 先选对文档路径

1. 在本仓库执行 **安装器**（见下）。在**交互模式**下，它会**首先询问**你是否拥有 **DJI Mic Mini 接收器**（该套装里的 USB 接收端）。
2. **按你的选择阅读对应文档：**
   - **有 DJI Mic Mini** → **[README_DJI_CN.md](README_DJI_CN.md)**（中文）· [README_DJI.md](README_DJI.md)（英文）— **第一套 / 路径 1**
   - **没有**（只用 **Mac / 耳机麦克风** + 系统听写）→ **[README_MAC_MIC_CN.md](README_MAC_MIC_CN.md)** · [README_MAC_MIC.md](README_MAC_MIC.md) — **第二套 / 路径 2**

非交互安装（`--yes`、`--json` 等）不会提问；请自行传 `--trigger-mode keyboard`（仅键盘与 Mac 听写）或 `--trigger-mode keyboard+dji`（含接收器按键映射）。

## 最短安装命令

```bash
git clone https://github.com/NumbSilver/VOICETYPE.git VoiceType
cd VoiceType
npm install
node cli/index.mjs install
```

可选：在本目录 `npm link` 后使用全局命令 `dji-mic-dictation install`。

## 两条路径的共同前置

| 需求 | 说明 |
|------|------|
| macOS | 已在 Sequoia 上验证 |
| [Karabiner-Elements](https://karabiner-elements.pqrs.org/) | `Fn` 工作流依赖 |
| macOS 听写 | 系统设置 → 键盘 → 听写 → 开启 |
| [Typeless](https://www.typeless.com/referral?tl_src=macos) | 当前版本依赖其数据库做文本检测 |

## 仓库结构（文档）

```
VoiceType/
├── README.md / README_CN.md           # 总览（本文）
├── README_DJI.md / README_DJI_CN.md   # 路径 1：DJI 接收器 + Fn
├── README_MAC_MIC.md / …_CN.md         # 路径 2：Mac/耳机麦 + Fn
├── cli/ …
```

## 许可

MIT，见 [LICENSE](LICENSE)。
