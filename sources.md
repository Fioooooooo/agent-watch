# Sources & Filtering Policy

> Agent Watch source policy V2

## 扫描模型

Agent Watch 使用两阶段发现机制：

1. **强制来源清单**：提供稳定的召回底线。每天必须逐项检查官方最新发布、版本说明、更新日志等入口，开放式搜索不能替代这一阶段。
2. **开放发现**：完成强制清单后，再通过更广泛的搜索发现固定来源之外的重要 Agent、Harness、Coding Agent 进展。

两个阶段先建立候选信息，再统一筛选。扫描可以细，但默认阅读内容必须短。

每个强制来源必须明确区分：

- `checked`：已可靠完成检查；
- `failed`：因访问、解析、搜索、API 或其他执行问题无法可靠完成检查。

`failed` 绝不能解释为“无更新”。任一强制来源失败，日报必须标记 `coverage incomplete` 并指出失败来源。

## 强制 Agent / Harness 来源清单

每天检查以下来源最新的官方 Blog、Engineering、Changelog、Release Notes、产品更新或 GitHub Releases，并与上次日报时间边界比较。

### OpenAI / Codex
- OpenAI 产品 / 研究发布入口
- OpenAI Release Notes / Changelog
- Codex 官方 GitHub Releases

### Anthropic / Claude Code
- Anthropic News
- Anthropic Engineering / 与 Agent 相关的研究文章
- Claude Code 官方 Changelog / GitHub Releases

### Google / Gemini CLI
- Google / Gemini 与 Agent 相关的官方产品及开发者发布
- Gemini CLI 官方 GitHub Releases

### Augment / Auggie
- Augment 官方 Blog / Engineering
- Auggie 官方 Release / Changelog（如有）

### Qwen / Qwen Code
- Qwen 官方 Blog
- Qwen Code 官方 GitHub Releases / Changelog

### Cursor
- Cursor 官方 Changelog
- Cursor 官方 Blog / Engineering

### Cognition / Devin
- Cognition 官方 Blog / Engineering
- Devin 官方产品更新 / Changelog

### GitHub Copilot
- GitHub Changelog 中的 Copilot 更新
- 公开 Copilot Agent 架构或运行机制的 GitHub Engineering / Blog
- Copilot CLI 官方发布来源（适用时）

### Zed / ACP
- Zed 与 Agent 相关的官方 Blog / Release Notes
- ACP 官方规范 / 协议更新
- Zed / ACP 官方 GitHub Releases（适用时）

### Windsurf
- Windsurf 官方 Changelog
- Windsurf 官方 Blog / Engineering

### Manus
- Manus 官方产品 / Engineering / Changelog

### Kimi / Kimi Code
- Kimi 官方 Blog
- Kimi Code What's New / Release Notes
- Kimi Code CLI Changelog / 官方 Releases

## 强制模型发布清单

每天同时检查以下厂商最新的官方模型发布：

- OpenAI
- Anthropic
- Google DeepMind / Gemini
- Qwen
- DeepSeek
- Kimi / Moonshot AI
- Z.ai / GLM

Meta 等其他模型厂商由开放发现阶段捕获，除非未来成为持续高价值来源。

只收录明显影响 Coding、Agent 能力、推理、工具调用、Computer Use、长上下文、推理效率，或会改变 Agent Harness 设计的 API / 架构能力。普通聊天模型、小参数衍生版本、Embedding、图像和语音模型默认排除，除非对 Agent 架构具有直接意义。

## Harness 技术观察清单

以下属于低频但重要的工程观察源，需要定期检查，但过滤普通版本噪音：

- LangChain / LangGraph
- Vercel AI SDK
- OpenHands

仅收录明显改变 Agent loop、Harness architecture、Context Engineering、memory、checkpoint、durable execution、long-running agents、recovery、multi-agent、sandbox、MCP 或 tool runtime 的内容。

## 开放发现

完成全部强制来源检查后，再进行开放式搜索，用于发现：

- 新的 Agent / Harness 项目或厂商
- 重要协议工作
- 深度工程文章
- 固定清单之外的重大模型或运行时发布
- 对工程实践有直接意义的研究
- Context Engineering、多 Agent 编排、沙箱、恢复机制、工具运行时、Computer Use、长时间任务等新方法

开放发现只能补充强制清单，不能替代它。

## 候选与筛选流程

对每个强制来源：

1. 打开官方最新发布 / Release / Changelog 列表；
2. 检查自上次日报之后的新条目；
3. 记录标题、发布时间、官方链接和来源；
4. 将可能相关的内容加入候选信息；
5. 完成全部强制来源后执行开放发现；
6. 按官方链接、标题或版本标识去重；
7. 统一进行相关性和价值筛选；
8. 保存完整技术材料；
9. 检查来源覆盖情况。

不要使用滑动历史补漏窗口替代强制清单的完整执行。

## 来源检查

每次日报必须内部维护全部强制来源的检查状态。只有所有来源均为 `checked`，才能认为扫描完整；存在 `failed` 时必须明确记录 `coverage incomplete`。只有成功检查的来源才能得出“没有重要更新”的结论。

## 高价值主题

重点关注 Agent architecture、Agent harness、Coding Agent、Context Engineering、memory 与 context provenance、multi-agent、sandbox 与 permissions、MCP / ACP / A2A、Skills 与 tool use、Computer Use / browser use、evaluation、long-running agents、checkpoint 与 recovery、CLI / SDK / protocol、agent runtime。

深度工程文章的权重高于普通功能公告，尤其关注真实 Agent loop、tool surface、session management、context management、token efficiency、sandbox、安全边界、任务恢复和多 Agent 编排中的设计取舍。

## 日报的双层结构

日报同时承担两种职责，但必须分层呈现：

1. **每日摘要**：默认阅读入口。目标是在很短时间内回答“今天真正发生了什么变化”。不要按新闻条目机械罗列，而应将多个相关更新合并成 1～3 个技术变化或信号，并说明这些变化为什么值得关注。优先使用自然中文，只有 Agent、Harness、MCP、ACP 等直接使用英文更准确的行业术语才保留英文，避免无必要的中英混排。
2. **完整材料**：保存来源、发布时间、版本、技术细节、官方原文和分析，作为后续周报、趋势判断和技术回溯的证据。完整性优先，不要求适合快速阅读。

扫描深度和收录标准不因为每日摘要变短而降低。每日摘要是对完整材料的二次提炼，不是删除材料。

每日摘要应优先回答：

- 今天形成了哪 1～3 个真正值得关注的技术变化？
- 哪些不同来源其实是在说明同一个方向？
- 哪一项值得读官方原文，哪一项只需持续观察？
- 如果没有形成值得关注的变化，应直接说明，不为了完整性制造趋势。

## 日报 → 周报职责

完整日报是事实与证据层；每日摘要是日常阅读层；技术周报负责跨天、跨厂商重新综合趋势。

技术周报以本周完整日报为主要证据，也参考每日摘要中的信号，但不能简单拼接每日摘要。必要时可以回查官方来源验证判断、补明显缺口或重大事件，但不重复执行整套日报扫描。

## 排除项

- 市场宣传
- 融资
- 客户案例
- 合作公告
- SEO 教程
- 泛 AI 新闻
- 普通 UI 更新
- 与 Agent / Harness 工程无关的模型资讯

不能为了填满日报而扩大收录范围。没有重要更新或没有形成值得关注的新变化时，应明确说明。