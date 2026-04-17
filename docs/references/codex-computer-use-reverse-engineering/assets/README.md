# Extracted Visual Assets

这个目录存放从官方 `Codex Computer Use.app` bundle 中直接导出的可视资源，用来支撑逆向分析文档里的视觉层结论。

## 当前归档

- `extracted-2026-04-17/hint-arrow.png`
  - 从 `Package_SlimCore.bundle` 导出的 `HintArrow` 资源，尺寸 `57x66`。
- `extracted-2026-04-17/software-cursor-slimcore.png`
  - 从 `Package_SlimCore.bundle` 导出的 `SoftwareCursor` 资源，尺寸 `200x230`。
- `extracted-2026-04-17/software-cursor-computeruse.png`
  - 从 `Package_ComputerUse.bundle` 导出的 `SoftwareCursor` 资源，尺寸 `200x230`；与 `SlimCore` 版本二进制一致。
- `extracted-2026-04-17/appicon-cursor.png`
  - 从主 app `Assets.car` 中导出的 `CUAAppIcon_Assets/cursor`，尺寸 `1024x1024`。
- `extracted-2026-04-17/appicon-cursor-dark.png`
  - 从主 app `Assets.car` 中导出的 `CUAAppIcon_Assets/cursor dark`，尺寸 `1024x1024`。
- `extracted-2026-04-17/menubar-cursor.png`
  - 从主 app bundle 导出的 `menubar-cursor`，尺寸 `19x17`。

## 说明

- 这些文件不是截图，而是直接从 bundle 资源加载并转存为 PNG。
- 当前导出方式基于 AppKit `Bundle.image(forResource:)`，适合提取已经命名的 asset。
- 权限 onboarding 的大部分 UI 仍然更像 SwiftUI / 窗口组合逻辑，而不是一组大量静态图片，因此目前能导出的“权限视觉资源”主要是 `HintArrow`。
