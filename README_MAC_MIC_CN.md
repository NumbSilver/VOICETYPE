# VoiceType — Mac / 耳机麦克风路径（第二套文档）

你使用 **系统听写**，音频来自 **Mac 自带麦克风、耳机麦或系统在「声音 → 输入」里选中的设备**。**不需要** DJI Mic Mini。流程仍由 **`Fn`** 负责开始 / 结束 / 确认发送。

← [返回总览](README_CN.md) · [English](README_MAC_MIC.md)

## 你能得到什么

```
Fn 第 1 下 → 开始听写（声音走当前听写所用的输入设备）
Fn 第 2 下 → 结束听写 → 就绪浮层 + 上屏后提示音
Fn 第 3 下 → 对前台 App 发送 Enter

4 秒内没有第 3 下 → 静默重置
```

## 麦克风与听写

- **系统设置 → 键盘 → 听写** 中打开听写。  
- 听写使用的麦克风由 **系统设置 → 声音 → 输入**（或菜单栏音量）决定，请选对你习惯的设备。  
- 本方案**不替换**系统听写的拾音链路，只在 Typeless 落字之后配合 **Fn** 与发送确认。

## 前置条件

| 需求 | 说明 |
|------|------|
| macOS | 已在 Sequoia 上验证 |
| [Karabiner-Elements](https://karabiner-elements.pqrs.org/) | `Fn` 工作流依赖 |
| macOS 听写 | 已开启；输入设备按需选择 |
| [Typeless](https://www.typeless.com/referral?tl_src=macos) | 当前版本依赖 Typeless DB |

**无大疆硬件。** 执行 `node cli/index.mjs install` 时请选择 **不使用 DJI 接收器 / Mac 麦克风路径**，安装器会保持 **仅键盘**（不映射接收器按键）。也可直接传 `--trigger-mode keyboard`。

## 安装

```bash
git clone https://github.com/NumbSilver/VOICETYPE.git VoiceType
cd VoiceType
npm install
node cli/index.mjs install
```

可选：`npm link` 后使用 `dji-mic-dictation install`。

## 三步上手

1. 安装并至少打开一次 **Typeless**。  
2. 安装 **Karabiner**，授予**输入监控**与**辅助功能**。  
3. 打开**听写**，在**声音 → 输入**里确认麦克风；再运行 `node cli/index.mjs install`，按提示选择 **Mac 麦克风路径**。

## 问题排查（本路径）

```bash
cat /tmp/dji-dictation/debug.log
```

| 现象 | 可能原因 | 处理 |
|------|----------|------|
| 听写用了错的麦克风 | 系统输入设备 | 声音 → 输入；或听写相关设置 |
| 听写起不来 | 听写未开 / 规则未合并 | 打开听写；`node cli/index.mjs doctor` |
| 无提示音/浮层 | 辅助功能 | `osascript`、终端 |
| 有声音无浮层 | Swift 浮层未更新 | `node cli/index.mjs update` |
| 找不到 Typeless DB | 未启动过 Typeless | 打开一次后再 `install` / `doctor` |
| Enter 未发出 | 终端权限 | iTerm2 / Terminal 辅助功能 |

### 权限清单

1. **输入监控** → Karabiner-Elements、karabiner_grabber  
2. **辅助功能** → Karabiner-Elements、终端  
3. **听写** → 键盘 → 听写 → 开启  

## 配置

`~/.config/dji-mic-dictation/config.env`，可用 `node cli/index.mjs config`。

## 以后若购买 DJI Mic Mini

重新执行 `node cli/index.mjs install` 并选择 DJI 路径，或使用 `--trigger-mode keyboard+dji`。详见 [README_DJI_CN.md](README_DJI_CN.md)。

## 许可

MIT，见 [LICENSE](LICENSE)。
