# Codex Thinking & Cost Simulator

一个单文件、纯前端、离线运行的 **OpenAI Codex 终端界面与会话成本模拟器**。无需安装任何依赖，直接在浏览器中打开即可体验 AI 编程助手（Agent）的流式思考过程与实时计费机制。

## ✨ 功能特性 (Features)

- **🖥️ 沉浸式终端 UI**：模仿现代开发者工具的暗色/亮色主题终端界面，支持动态打字机效果。
- **🧠 拟真 AI 思考链路**：完整模拟 `Thinking`（推理过程）→ `Explored`（工具调用）→ `Answer`（代码/文本输出）的流式交互体验。
- **💰 实时计费与 Token 统计**：
  - 实时计算并展示 Input、Cached、Reasoning、Answer 的 Token 消耗。
  - 动态渲染成本折线图（Sparkline），直观展示输出燃烧速率。
  - 严格区分 Cache Hit/Miss 的计费差异。
- **⚙️ 高度可调的模拟参数**：
  - **模型切换**：内置 `gpt-5-codex`, `gpt-5`, `o3` 等模型及其预设价格。
  - **推理强度**：Low / Medium / High（直接影响 reasoning token 的消耗）。
  - **输出速度**：1x / 2x / 4x / ∞ (无限速秒出结果)。
  - **上下文与缓存**：模拟不同大小的 Context (最高 200k) 和 Cache Hit Rate。
  - **计费模式**：标准、Batch 批处理（半价）、Priority 优先（两倍）。
- **📦 预置演练场景**：内置 4 个典型开发任务（修复并发测试、重构计费逻辑、分析请求链路、补充边界测试），一键运行。
- **⌨️ 快捷键支持**：
  - `Enter`：运行任务 / 发送
  - `Shift + Enter`：输入框内换行
  - `Space`：暂停 / 继续流式输出
  - `R`：重置当前会话

## 🚀 如何使用 (Usage)

1. **下载/保存**：将代码保存为 `codex-sim.html`。
2. **运行**：直接双击该文件，使用 Chrome、Edge 或 Safari 等现代浏览器打开即可。
3. **操作**：
   - 你可以直接在底部输入框中输入自定义的编码任务（按 `Enter` 运行），或者点击主界面中的“场景快捷按钮”（如 `01 修复 flaky 测试`）来快速体验。
   - 在右侧边栏调整模型、预算单价、上下文大小等参数，左侧的计算面板会**实时响应**。
   - 体验按 `Space` 暂停 AI 的“思考”过程。

## 📊 参数与计算说明

所有 Token 与成本计算**均在浏览器本地估算**，不涉及任何真实网络请求：

- **输入 Token**：`(Prompt 字符数 / 3.9) + 系统开销 + 设定的 Context 大小`。
- **推理 Token**：`(Reasoning 字符数 / 3.9) * 1.8 (推理系数) * 推理强度系数`。
- **成本公式**：
  ```text
  Cost = (Uncached_Tokens * Input_Price + Cached_Tokens * Cached_Price + Output_Tokens * Output_Price) / 1,000,000
  ```
- **计费系数**：最终成本还会乘以你选择的计费模式（Standard=1, Batch=0.5, Priority=2）。

## 🛠️ 自定义与扩展 (Customization)

如果你有一定的前端基础，可以直接修改 HTML 文件底部的 `<script>` 标签，扩展模拟器：

- **添加新场景**：在 `SCENARIOS` 对象中添加新的键值对，包含 `title`, `prompt`, `tools`, `reasoning`, `answer` 等字段。系统会自动将其加入空状态下的快捷按钮。
- **添加新模型**：在 `MODELS` 对象中添加新的模型名称与对应的单价配置（`in`, `cached`, `out`），即可在右侧下拉菜单中出现。

## ⚠️ 免责声明 (Disclaimer)

- 本项目仅用于 **UI 交互与成本计算逻辑的演示**。
- 所有输出的代码、思考过程、及价格数据均为预设或模拟计算，不代表 OpenAI 官方实际扣费标准。
- 所有数据完全在本地生成，**没有任何数据会被发送到互联网**。
