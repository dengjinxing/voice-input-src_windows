**[中文](README_CN.md) | English**

## Source Code

```bash
claude \
  --dangerously-skip-permissions \
  --output-format=stream-json \
  --verbose \
  -p "Please implement a Windows tray-based voice input application (C#, WPF, Windows 10+), with the following requirements:

1. Record audio while holding the Fn key, and insert the transcribed text into the currently focused input field upon release. Use streaming speech recognition (Windows Speech Recognition / Windows.Media.SpeechRecognition) as the primary method. Listen globally for the Fn key using a low-level keyboard hook (SetWindowsHookEx) and suppress the Fn event to prevent triggering system functions. If Fn key detection is unstable, provide Ctrl+Alt+Space as an optional global hotkey.
The default language must be Simplified Chinese (zh-CN) to ensure Chinese recognition out of the box. Provide a language selection submenu in the system tray, supporting English (en-US), Simplified Chinese (zh-CN), Traditional Chinese (zh-TW), Japanese (ja-JP), and Korean (ko-KR). Save the selected language in application settings (JSON or UserSettings).
Display an elegant, borderless capsule-shaped floating window at the bottom center of the screen during recording. It must have no title bar, no window controls, stay topmost, and not activate or steal focus. Use a custom WPF Window with WindowStyle=None, AllowsTransparency=True, Topmost=True, and AcrylicBrush for a modern translucent effect. The window height is 56px, corner radius 28px. It includes:
A 5-bar vertical waveform animation (44×32px) on the left, driven by real-time audio RMS levels (not fake fixed animations). The waveform amplifies with loud speech and shrinks when quiet. Use bar weights [0.5, 0.8, 1.0, 0.75, 0.55] for a natural middle-high shape. Apply smooth envelope (attack 40%, release 15%) and ±4% random jitter per bar for organic movement. The waveform must be large and clearly visible.
A text label on the right with elastic width (160–560px) that shows real-time transcription. The capsule expands smoothly as text grows.
Animations: spring fade-in on entry (0.35s), smooth width transition (0.25s), scale-out fade on exit (0.22s).
Insert text using the clipboard + simulated Ctrl+V method. Before pasting, detect the current input method via user32.dll / imm32.dll. If a CJK input method is active, temporarily switch to an ASCII/US keyboard layout, paste, then restore the original input method to avoid CJK input intercepting Ctrl+V. Restore the original clipboard content after insertion.
Integrate an OpenAI-compatible API to improve recognition accuracy, especially for mixed Chinese-English scenarios. Support configurable API Base URL, API Key, and Model. The LLM system prompt must be conservative: only correct obvious speech-to-text errors (homophones, technical terms misrecognized as Chinese, e.g., “peisen” → “Python”, “jiesen” → “JSON”). Do not rewrite, polish, add, or remove correct content; return input unchanged if accurate.
Add an LLM Refinement submenu in the system tray, with an on/off toggle and a Settings entry. The Settings window includes input fields for API Base URL, API Key (fully clearable), and Model, plus Test and Save buttons. After releasing Fn, if LLM is enabled and configured, show “Refining...” in the floating window and wait for the LLM result before inserting final text.
Run the app as a background tray-only application with no taskbar window. Build using .NET 6+, provide a PowerShell build script supporting build, run, install, clean commands, and produce a signed single-file executable.
```

## Dist

https://github.com/yetone/voice-input-dist
