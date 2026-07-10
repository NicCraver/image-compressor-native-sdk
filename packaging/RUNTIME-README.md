# 运行说明 · 压缩器（Compressor）

这是 native-sdk 打包的桌面应用。打开即见界面，可拖入或浏览图片，调节质量后压缩为 WebP。

## ⚠️ 两个已知限制（请先读）

1. **压缩 / 预览依赖 Bun**
   压缩和预览由应用通过 `bun run scripts/*.ts` 调用脚本完成，因此**目标机器必须安装 [Bun](https://bun.sh) 并使其在 PATH 中**。`scripts/` 目录已随包附带（见下文位置）。未安装 Bun 时，界面可用但点「压缩」会报错。
   为使脚本能被找到，请从包含 `scripts/` 的目录启动可执行文件（详见下文各平台说明）。

2. **Windows 上中文显示为方框（tofu）**
   当前 UI 文案为中文。macOS 经 CoreText 系统字体回退可正常显示；Windows 的软件画布使用内置 Geist 字体（不含中文），在没有额外注册 CJK 字体的情况下，中文会渲染成 `□□□`。后续可通过随包附带 CJK 字体（如 Noto Sans SC）并注册为默认字体解决。

## 平台说明

### macOS（`image-compressor-macos-arm64.zip`）
- 解压得到 `image-compressor.app`，为 **Apple Silicon (arm64)**，Intel Mac 无法运行。
- 未做代码签名：首次打开若被 Gatekeeper 拦截，右键 → 「打开」，或在终端执行：
  ```bash
  xattr -dr com.apple.quarantine /path/to/image-compressor.app
  ```
- `scripts/` 位于 `image-compressor.app/Contents/Resources/scripts/`。压缩功能需 Bun 在 PATH。

### Windows（`image-compressor-windows-x64.zip`）
- 解压得到目录，运行 `bin\image-compressor.exe`（x64）。
- 未做代码签名：SmartScreen 拦截时选「更多信息」→「仍要运行」。
- `scripts/` 已复制到 `bin\scripts\`。为确保压缩可用，建议从 `bin\` 目录启动 exe（使 `scripts\` 的相对路径生效），并保证 Bun 在 PATH。

## 快捷键（primary 修饰键）
- macOS：`Cmd+,` 设置 · `Cmd+O` 浏览 · `Cmd+Enter` 压缩
- Windows：`Ctrl+,` 设置 · `Ctrl+O` 浏览 · `Ctrl+Enter` 压缩