# VoiceType — DJI Mic Mini 路径（第一套文档）

你拥有 **DJI Mic Mini** 及 **USB 接收器**，希望把接收器上的 **Consumer 按键**映射成与 **`Fn` 相同**的开始 / 结束 / 确认发送流程（在键盘工作流之外多一条硬件触发）。

← [返回总览](README_CN.md) · [English](README_DJI.md)

## 你能得到什么

与大家相同的 **三下 Fn** 逻辑：

```
Fn 第 1 下 → 开始听写
Fn 第 2 下 → 结束听写 → 就绪浮层 + 上屏后提示音
Fn 第 3 下 → 发送 Enter（须在短时间内完成）
```

**可选：** 安装为 `keyboard+dji` 且接收器被 Karabiner 正确抓取时，**接收器按键**可镜像上述流程。

**拾音：** 若系统听写使用 DJI 麦克风或本机麦，由 **系统听写 / 声音输入** 决定；本文侧重 **硬件触发** 的 Karabiner 配置，而非替换听写音频链路。

## 前置条件

| 需求 | 说明 |
|------|------|
| macOS | 已在 Sequoia 上验证 |
| [Karabiner-Elements](https://karabiner-elements.pqrs.org/) | 必需 |
| macOS 听写 | 系统设置 → 键盘 → 听写 → 开启 |
| [Typeless](https://www.typeless.com/referral?tl_src=macos) | 当前依赖 Typeless DB |
| DJI Mic Mini + 接收器 | 可选**触发器**；vendor_id **11427**，product_id **16401**（Consumer HID） |

执行 `node cli/index.mjs install` 时，在**第一步**选择 **有 DJI Mic Mini**。若已插入接收器，安装器可自动启用 **`keyboard+dji`**；若未插入，仍可预配置以便日后使用。

## 安装

```bash
npx github:NumbSilver/VOICETYPE install
```

首步选 **DJI Mic Mini** 路径，或直接使用 `--trigger-mode keyboard+dji`。

## 快速上手

1. 安装并打开过一次 **Typeless**。  
2. 安装 **Karabiner**，完成**输入监控**与**辅助功能**授权。  
3. 打开**听写**。  
4. 尽量**插入接收器**后运行 `node cli/index.mjs install`，并确认走 DJI 文档路径。

## 接收器与 Karabiner

- 接收器为 **Consumer HID**。启用 DJI 模式时，受管配置会写入 `"is_consumer": true, "ignore": false`。  
- 若按键**只调音量**，多为未启用 `keyboard+dji` 或设备未被抓取：插上接收器后重新安装，并检查 Karabiner 设备列表。

## 其他 Consumer HID（进阶）

```bash
'/Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_cli' --list-connected-devices
```

修改 vendor/product 后配合 `--trigger-mode keyboard+dji` 重装（需自行对齐规则模板）。

## 问题排查

```bash
cat /tmp/dji-dictation/debug.log
```

### 硬件键

| 现象 | 处理 |
|------|------|
| 键无反应 | 输入监控 → Karabiner |
| 只调音量 | 用 DJI 路径重装；确认 `keyboard+dji` 与设备条目 |

### 通用

| 现象 | 处理 |
|------|------|
| 无浮层/提示音 | `osascript`、终端辅助功能 |
| 无 Typeless DB | 打开一次 Typeless |
| 行为异常 | `node cli/index.mjs update` |

## 配置

`~/.config/dji-mic-dictation/config.env`，`node cli/index.mjs config`。

## 改回纯键盘 / Mac 麦

重新安装并选择 **Mac 麦克风路径**，或使用 `--trigger-mode keyboard`。详见 [README_MAC_MIC_CN.md](README_MAC_MIC_CN.md)。

## 许可

MIT，见 [LICENSE](LICENSE)。
