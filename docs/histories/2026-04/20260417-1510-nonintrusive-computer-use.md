## [2026-04-17 15:10] | Task: 收敛非抢焦点交互

### 🤖 Execution Context
* **Agent ID**: `Codex`
* **Base Model**: `GPT-5 / Codex`
* **Runtime**: `Codex CLI`

### 📥 User Query
> 现在已经有官方 `computer-use` 和仓库内 `open-codex-computer-use` 两套工具，要求并行对比效果，并把两边的 tool call / 结果分别保存到同一目录下的两个子目录里；当前最明显的问题是我们的实现会抢用户鼠标和焦点，希望围绕这一点做改进。

### 🛠 Changes Overview
**Scope:** `OpenCodexComputerUseKit`, `docs/`, `artifacts/`

**Key Actions:**
- **[非侵入优先输入链路]**: 去掉 `get_app_state` 的强制 app 激活，把 `type_text` / `press_key` 改成按 PID 定向投递键盘事件。
- **[点击策略修正]**: 修复 raw AX actions 被错误过滤的问题，并为 coordinate click 增加 AX hit-test 优先路径，只有命中失败才退回全局 HID。
- **[对比样本留档]**: 新增 `artifacts/tool-comparisons/20260417-focus-behavior/`，分别保存官方 `computer-use` 和仓库实现的调用样本与前后台观测。
- **[文档同步]**: 更新架构与质量文档，补执行计划与本次 history。

### 🧠 Design Intent (Why)
“抢焦点/抢鼠标”本质上是当前实现把太多路径都建立在 `activate + cghidEventTap` 上。这个改动的目标不是假装所有鼠标路径都能彻底无副作用，而是把读状态、键盘输入和大部分可反解到 AX 元素的点击先收敛到更温和的通道，把真正需要全局 HID 的场景显式缩到最小。

### 📁 Files Modified
- `packages/OpenCodexComputerUseKit/Sources/OpenCodexComputerUseKit/InputSimulation.swift`
- `packages/OpenCodexComputerUseKit/Sources/OpenCodexComputerUseKit/ComputerUseService.swift`
- `packages/OpenCodexComputerUseKit/Sources/OpenCodexComputerUseKit/AccessibilitySnapshot.swift`
- `docs/ARCHITECTURE.md`
- `docs/QUALITY_SCORE.md`
- `docs/exec-plans/completed/20260417-nonintrusive-computer-use.md`
- `artifacts/tool-comparisons/20260417-focus-behavior/README.md`
- `artifacts/tool-comparisons/20260417-focus-behavior/computer-use/get_app_state-activity-monitor.json`
- `artifacts/tool-comparisons/20260417-focus-behavior/open-codex-computer-use/get_app_state-activity-monitor.json`
- `artifacts/tool-comparisons/20260417-focus-behavior/open-codex-computer-use/click-activity-monitor-coordinate.json`
