# Sources & Filtering Policy

> Agent Watch source policy V2.1

## 扫描模型

Agent Watch 使用两阶段发现机制：

1. **强制来源清单**：提供稳定的召回底线。每天必须逐项检查官方最新发布、版本说明、更新日志等入口，开放式搜索不能替代这一阶段。
2. **开放发现**：完成强制清单后，再通过更广泛的搜索发现固定来源之外的重要 Agent、Harness、Coding Agent 进展。

两个阶段先建立候选信息，再统一筛选。扫描可以细，但默认阅读内容必须短。

每个强制来源必须明确区分：

- `checked`：已可靠完成检查，并留下可验证的检查证据；
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

## 强制来源检查证据

`checked` 不能只是任务执行过程中的布尔标记。每个强制来源必须留下足以证明“确实看过官方最新入口”的检查证据。

对每个强制来源，至少完成以下动作：

1. 打开该来源对应的官方最新发布入口；
2. 尽可能读取按时间排序的最新 3～5 条内容，而不是只看搜索摘要或单一搜索结果；
3. 记录该来源本次实际看到的最新条目，至少包括 `latest_seen_title`、`latest_seen_date` 和官方 URL；
4. 从这些最新条目中提取自上次日报时间边界之后的候选信息；
5. 只有完成以上步骤，才能标记为 `checked`。

如果官方入口无法可靠打开、无法确认最新条目、页面排序不可信且无法交叉验证，或其他原因导致无法证明已看到最新内容，应标记为 `failed`，而不是猜测“没有更新”。

“没有收录”与“没有看到”必须严格区分：某条内容可以因为客户案例、市场宣传、普通 UI 更新等原因被筛除，但必须先被扫描到，才能证明该来源没有被漏查。

日报末尾应保存一个折叠的“来源检查”区，记录每个强制来源的状态及检查证据。至少包含：来源、状态、最新看到的内容、日期；必要时可补充失败原因。该区域用于审计召回质量，不进入默认的每日摘要。

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
2. 尽可能读取最新 3～5 条，并记录 `latest_seen_title`、`latest_seen_date`、官方 URL；
3. 检查自上次日报之后的新条目；
4. 记录候选信息的标题、发布时间、官方链接和来源；
5. 将可能相关的内容加入候选信息；
6. 完成全部强制来源后执行开放发现；
7. 按官方链接、标题或版本标识去重；
8. 统一进行相关性和价值筛选；
9. 保存完整技术材料；
10. 检查来源覆盖情况并写入来源检查证据。

不要使用滑动历史补漏窗口替代强制清单的完整执行。

## 来源检查

每次日报必须维护全部强制来源的检查状态与检查证据。只有所有来源均为 `checked`，且每个 `checked` 都有可验证的 `latest_seen` 证据，才能认为扫描完整；存在 `failed` 或缺失检查证据时，都必须认为 `coverage incomplete`。

只有成功检查并留下证据的来源，才能得出“没有重要更新”的结论。

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