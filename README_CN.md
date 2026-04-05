**中文 | [English](README.md)**

## Source Code

```bash
claude \
  --dangerously-skip-permissions \
  --output-format=stream-json \
  --verbose \
  -p "请实现一个 Windows menu-bar 语音输入法应用（Swift，Windows 10+），具体要求：

请实现一个 Windows 系统托盘语音输入法应用（C#，WPF，Windows 10+），具体要求：

1. 按住 Fn 键开始录音，松开后将转录文字注入当前聚焦输入框，优先使用 Windows 语音识别框架实现流式识别。通过 SetWindowsHookEx 全局低级别键盘钩子监听 Fn 键，拦截并抑制 Fn 事件传递，避免触发系统功能；若 Fn 键监听不稳定，提供 Ctrl+Alt+Space 自定义热键作为备选触发方式。
2. 默认语言为简体中文（zh-CN），确保开箱即用识别中文；在系统托盘菜单提供语言切换选项，支持英语（en-US）、简体中文（zh-CN）、繁体中文（zh-TW）、日语（ja-JP）、韩语（ko-KR），语言选择存储到应用配置文件（JSON）或 UserSettings 中。
3. 录音时在屏幕底部居中显示无边框、无标题栏、无系统按钮的胶囊状悬浮窗，始终置顶且不抢占焦点。使用 WPF 自定义 Window（WindowStyle=None、AllowsTransparency=True、Topmost=True），搭配 AcrylicBrush 亚克力毛玻璃效果，高度 56px、圆角半径 28px，包含：
   - 左侧 5 根竖条波形动画（44×32px），由 NAudio 实时采集的音频 RMS 电平驱动，非固定假动画；说话音量大则波形幅度大，安静时幅度小。各竖条权重为 [0.5, 0.8, 1.0, 0.75, 0.55]，形成中间高、两侧低的自然效果；添加平滑包络（attack 40%、release 15%），每根竖条叠加 ±4% 随机抖动增强有机感，波形需清晰醒目。
   - 右侧实时显示转录文本的标签，宽度弹性范围 160-560px，随文字长度自动扩展，胶囊宽度同步平滑变化。
   - 入场弹簧缩放淡入动画（0.35s）、文本宽度平滑过渡动画（0.25s）、退场缩放淡出动画（0.22s）。
4. 文字注入采用剪贴板复制 + 模拟 Ctrl+V 粘贴方式；注入前通过 user32.dll、imm32.dll API 检测当前输入法，若为中文/日文/韩文等 CJK 输入法，先临时切换到英文（US/ABC）键盘布局，粘贴完成后恢复原输入法，避免 CJK 输入法拦截粘贴操作；注入后恢复剪贴板原始内容。
5. 接入 OpenAI 兼容 API 提升语音识别准确率，适配中英文混杂场景；支持配置 API Base URL、API Key、模型名称。LLM 系统提示词需严格保守纠错：仅修复明显语音识别错误（如中文谐音错误、英文技术术语误转中文，例：“配森”→“Python”、“杰森”→“JSON”），绝不改写、润色、增删正确内容，输入无误则原样返回。
6. 系统托盘菜单添加 LLM Refinement 子菜单，包含启用/禁用开关和设置入口；设置窗口包含 API Base URL、API Key（支持完全清空）、模型名称输入框，以及测试连接、保存配置按钮；松开 Fn 键后，若 LLM 已启用且配置完成，悬浮窗显示“Refining...”状态，等待 LLM 返回结果后再注入最终文本。
7. 应用以仅系统托盘图标模式运行，无任务栏窗口；使用 .NET 6+ 构建，提供 PowerShell 脚本（build.ps1）支持 build/run/install/clean 命令，构建产物为单文件部署的签名 exe 程序。
```

## Dist

https://github.com/yetone/voice-input-dist
