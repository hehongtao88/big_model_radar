# OpenClaw 生态日报 2026-06-10

> Issues: 445 | PRs: 492 | 覆盖项目: 12 个 | 生成时间: 2026-06-09 19:24 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyclaw)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [EasyClaw](https://github.com/gaoyangz77/easyclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报
**日期：2026-06-10 | 数据周期：过去 24 小时**

---

## 📊 今日速览

OpenClaw 项目今日活跃度极高，在 24 小时内产生了 **445 条 Issue 更新**和 **492 条 PR 活动**，表明项目处于活跃迭代阶段。发布了 **4 个版本**（包括 v2026.6.5 正式版及多个 beta 版），重点关闭了 QQBot 内容泄露的安全漏洞。目前积压的待合并 PR 达 358 条，需要加快审查速度以避免审查瓶颈。项目健康度整体良好，但安全问题和消息丢失类 Bug 需要优先关注。

---

## 🚀 版本发布

### 🎯 v2026.6.5（正式版）与 Beta 系列

**发布时间**：2026-06-09 及之前  
**版本树**：v2026.6.5 → v2026.6.5-beta.6 → beta.5 → beta.3

**核心亮点**：

| 特性 | 说明 | 关联 Issue |
|------|------|----------|
| **QQBot 内容泄露修复** | 现在在本地交付前会剥离模型推理/思考脚手架，防止原始 `<thinking>` 标签内容泄露到频道回复 | #89913, #90132 |
| **MCP 工具结果强制转换** | 对 `resource_link`, `resource`, `audio`, 格式不正确的图像等进行强制转换和处理 | - |

**破坏性变更**：  
无明显破坏性变更提及，主要为缺陷修复。

**迁移建议**：  
- 使用 QQBot 的用户应立即升级以防止内容泄露
- MCP 集成用户需测试工具结果的类型转换行为是否符合预期

👉 **GitHub Release**：[v2026.6.5 Release Notes](https://github.com/openclaw/openclaw/releases)

---

## ✨ 项目进展

### 🔄 今日关闭的关键 PR

| PR | 标题 | 影响范围 | 状态 |
|----|----|--------|------|
| #90798 | `fix(agents): materialize sandbox skills for rw sandboxes` | 沙箱读写权限修复 | ✅ 已合并 |
| #90838 | `fix(config): warn for retired skill-workshop plugin` | 配置兼容性 | ✅ 已合并 |
| #91753 | `docs: clarify Matrix plugin upgrade repair` | 文档更新 | ✅ 已合并 |
| #87291 | `Reply context body truncated at 500 chars` | 回复上下文处理 | ✅ 已合并 |
| #85669 | `sessions_history returns unfiltered delivery-mirror messages` | 会话历史去重 | ✅ 已合并 |

### 📈 关键提交方向

1. **安全强化（6+ 个 PR）**：
   - #91747 浏览器 CDP WebSocket URL 验证
   - #91752 Codex 沙箱 HTTP 请求防护
   - #91749 网关非所有者环回工具限制
   - #91748 禁止群组 ID 作为发送者
   - #91746 MS Teams 群组管理权限检查

2. **性能优化**：
   - #89040 嵌入式运行时事件循环优化（避免 14-22s 停顿）

3. **功能增强**：
   - #91093 ACP 中心会话委托（支持无线程的持久外部工作进程）
   - #91256 诊断 OTel 工具输入/输出内容捕获

**项目整体向前推进**：在 24h 内完成 ~134 个 PR 合并/关闭，维持稳定的交付速度。主要精力投入安全边界加固与性能问题根治。

---

## 🔥 社区热点

### 最受关注的 Issue/PR（按评论数排序）

#### 🥇 顶级问题

**1. Issue #25592**（29 条评论）- ⚠️ 安全优先级  
📌 **标题**：[Bug] Text between tool calls leaks to messaging channels  
**标签**：P1, impact:security, impact:message-loss, 🦞 diamond lobster  
**作者**：@doomclaw | **更新**：2026-06-09

**问题核心**：当 Agent 在工具调用之间生成文本（如错误处理、处理确认、叙述）时，这些文本被路由到活跃消息频道（Slack、iMessage 等）作为可见消息。这是严重的 UX 问题——内部处理输出、失败执行等不应该对用户暴露。

**社区反应**：v2026.6.5 已在 QQBot 实现了修复（#89913），但问题仍然在其他频道（Discord、Telegram、Feishu 等）存在。

👉 [查看 Issue #25592](https://github.com/openclaw/openclaw/issues/25592)

---

**2. Issue #90083**（15 条评论）- 🚨 关键集成故障  
📌 **标题**：[Bug] OpenAI ChatGPT Responses transport fails with invalid_provider_content_type  
**标签**：P1, impact:auth-provider, 🐚 platinum hermit  
**作者**：@jimmielightner | **更新**：2026-06-08

**问题核心**：升级到 v2026.6.1 后，OpenAI/ChatGPT 推理在 `gpt-5.4` 和 `gpt-5.5` 上失败，报错 `invalid_provider_content_type`，导致连接错误。

**社区反应**：已确认影响多个用户，需要 OpenAI provider transport 层修复。

👉 [查看 Issue #90083](https://github.com/openclaw/openclaw/issues/90083)

---

**3. Issue #54253**（13 条评论）- 💻 架构兼容性  
📌 **标题**：[Bug] OpenClaw returns "LLM Request Failed" on RISC-V64 System  
**标签**：P2, impact:auth-provider, 🦪 silver shellfish  
**作者**：@iravikiran | **更新**：2026-06-09

**问题核心**：在 RISC-V64 架构上运行失败，而 macOS 和 x86 运行正常。提示 LLM 请求失败。

**社区反应**：虽然标记为 P2，但涉及架构兼容性，需要排查字节序、库依赖等问题。

👉 [查看 Issue #54253](https://github.com/openclaw/openclaw/issues/54253)

---

#### 🥈 高热度功能与回归问题

| Issue | 评论数 | 类型 | 关键词 |
|-------|--------|------|--------|
| #53628 | 13 | Bug | XDG_CONFIG_HOME 未被处理（Docker） |
| #86599 | 13 | Bug/Regression | Windows 本地模型卡顿（4分钟） |
| #48003 | 12 | Bug | Steer 模式不注入消息到主会话 |
| #54531 | 10 | Feature | 强制回复到原始频道（Telegram/Discord） |
| #44905 | 10 | Bug | Discord 泄露内部工具调用跟踪 |
| #74586 | 9 | Bug | AM 嵌入式运行超时误分类 |
| #31331 | 9 | Bug | Docker 沙箱无法访问工作区 |

---

## 🐛 Bug 与稳定性

### 按严重程度排列

#### 🚨 **P1 关键问题**（9 个，均需优先处理）

| Issue | 标题 | 影响 | Fix PR | 状态 |
|-------|------|------|--------|------|
| #25592 | 文本泄露到消息频道 | 安全/UX | #89913 (QQBot 已修复) | ⚠️ 其他频道仍需修 |
| #90083 | OpenAI provider 传输失败 | 集成中断 | 🔍 搜索中 | ⏳ 未分配 |
| #48003 | Steer 模式不注入消息 | 消息丢失 | - | 🔴 无 PR |
| #54531 | 频道回复路由失败 | 用户体验 | - | 🔴 无 PR |
| #44905 | Discord 工具调用泄露 | 安全信息暴露 | - | 🔴 无 PR |
| #83184 | 心跳交付卡死阻塞 | 消息丢失 | - | 🔴 无 PR |
| #86996 | 主动记忆+Codex 响应延迟 | 性能/可靠性 | - | 🔴 无 PR |
| #54488 | 跟进排空垄断会话车道 | 调度饥饿 | - | 🔴 无 PR |
| #56263 | 文件权限硬编码 (0o600) | 多用户部署 | - | 🔴 无 PR |

**关键观察**：9 个 P1 问题中，仅 1 个有部分 fix（QQBot），其余 8 个均无 PR 分配，积压严重。

---

#### ⚠️ **P2 中等问题**（25+ 个）

**重点回归问题**：
- #86599：Windows 本地模型 4 分钟延迟（已关闭，已修复 ✅）
- #52186：ElevenLabs TTS 播放错误的 OpenAI 声音
- #73424：图像优化失败（已关闭 ✅）
- #85669：会话历史去重（已关闭 ✅）
- #44599：配置路径不能有空格

**数据丢失风险**：
- #50442：备份超时留下大 .tmp 文件导致磁盘耗尽
- #54634：更新后静默丢弃配置（P1 数据丢失）
- #53540：参数生成延迟超时导致网络连接丢失

---

#### 🔴 **回归问题**（6 个，标注 regression）

| Issue | 引入版本 | 修复状态 |
|-------|--------|--------|
| #86599 | 2026.5.24-beta.1 | ✅ 已关闭 |
| #52186 | ~2026.3.x | ⏳ 未修 |
| #44599 | 回归 | ⏳ 未修 |
| #87999+ | 多个版本 | 分散 |
| #53599 | 2026.3.22 | ⏳ 未修 (Chrome 扩展移除) |
| #54909 | 未定 | ⏳ 未修 (Telegram inline) |

**回归问题多集中在 2026.3.x 和 2026.5.x**，需要专项审视版本间的破坏性变更。

---

#### 💥 **消息丢失相关** (impact:message-loss, 8+ 个)

- #25592、#44905、#54531：内容泄露或不送达
- #48003、#83184：会话状态问题导致丢失
- #54488：调度饥饿导致消息排队 20-30 分钟
- #56096：Telegram sendChatAction 无限重试循环

**模式**：多涉及频道分发、心跳机制、调度器，是项目的薄弱点。

---

## 🎯 功能请求与路线图信号

### 用户提出的新需求

| Issue | 需求类型 | 优先级 | 关联 PR | 信号 |
|-------|--------|--------|--------|------|
| #54531 | 频道回复保障 | P1 | - | 🔴 计划中 |

---

## 横向生态对比

# AI 智能体开源生态日报 | 2026-06-10 横向对比分析

---

## 1. 🌍 生态全景

**当前态势**：AI 个人助手与自主智能体开源生态呈现**快速演进、安全成为关键议题、多渠道集成竞争加剧**的特点。在调研的 8 个活跃项目中，**超 70% 的项目处于高速迭代阶段**（日均 30+ PR/Issue 活动），但**P0 级安全漏洞（如 SSRF、权限隔离、数据泄露）集中涌现**，表明开发速度与安全防护的矛盾日益突出。同时，**多模型协作、跨频道统一体验、细粒度权限控制**成为新的竞争焦点，标志着从单智能体向多智能体企业应用的升级。

---

## 2. 📊 各项目活跃度对比

### 核心指标汇总表

| 项目 | Issues | PRs | Release | 待合并PR | 健康度 | 活跃阶段 | 关键指标 |
|------|--------|-----|---------|---------|--------|---------|---------|
| **OpenClaw** | 445 | 492 | ✅ v2026.6.5 | 358 | 🟡 良好 | ⚡ **超高活跃** | PR积压严重，审查瓶颈 |
| **CoPaw** | 34 | 35 | ✅ v1.1.11-β2 | 20 | 🟢 优秀 | ⚡ **快速迭代** | 合并效率70%，质量有保障 |
| **IronClaw** | 48 | 50 | ❌ 筹备中 | 21 | 🟢 优秀 | ⚡ **快速迭代** | Reborn生产化冲刺 |
| **Zeroclaw** | 50 | 50 | ❌ v0.8.0-β | 49 | 🟡 良好 | ⚡ **超高活跃** | 功能迭代快，安全风险高 |
| **PicoClaw** | 17 | 21 | ✅ v0.2.9-nightly | 15 | 🟡 良好 | ⚡ **中高活跃** | 安全审计密集，社区响应快 |
| **NanoBot** | 6 | 25 | ❌ 无 | 13 | 🟢 优秀 | 🟢 **稳健推进** | PR合并率52%，文档完善 |
| **LobsterAI** | 2 | 5 | ❌ 无 | 1 | 🟢 优秀 | 🟢 **质量优先** | 用户反馈高质，架构深化 |
| **NanoClaw** | 0 | 4 | ❌ 无 | 2 | 🟢 优秀 | 🟢 **稳健推进** | 生产bug响应快，积压少 |

### 活跃度分层

```
🔴 超高活跃 (日均 >40 PR/Issue):
  ├─ OpenClaw (937 合计)  — 架构重构 + 安全加固同步
  ├─ Zeroclaw (100 合计)         — 多渠道扩展 + RFC设计
  └─ IronClaw (98 合计)          — Reborn生产化冲刺

🟠 高活跃 (日均 20-40):
  ├─ CoPaw (69 合计)             — Windows稳定性 + 测试覆盖
  └─ PicoClaw (38 合计)          — 安全审计反馈处理

🟡 中活跃 (日均 5-20):
  ├─ NanoBot (31 合计)           — 工具调用安全 + 渠道优化
  └─ LobsterAI (7 合计)          — 协作功能完善

🟢 稳健推进 (日均 <5):
  └─ NanoClaw (4 合计)           — 生产质量聚焦
```

---

## 3. 🎯 OpenClaw 在生态中的定位

### 优势维度

| 维度 | OpenClaw | 竞争对手 | 评价 |
|------|---|---|---|
| **开发速度** | 937 activities/day | Zeroclaw (100), IronClaw (98) | 🥇 **绝对领先** — 单日PR/Issue流量是Zeroclaw 10倍，显示庞大研发团队 |
| **版本发布频率** | 4 releases/day (含beta) | PicoClaw (1 nightly), CoPaw (1 beta) | 🥇 **频繁迭代** — 快速反馈用户需求，但风险是版本质量参差 |
| **功能广度** | QQBot/Discord/Telegram/Matrix/Teams 等6+ 频道 + MCP工具集成 + 沙箱 | IronClaw (Slack/DM), NanoBot (多渠道优化) | 🥈 **全面但复杂** — 覆盖面广，但集成复杂度高，维护成本大 |
| **架构复杂度** | Agent框架 + MCP工具结果强制转换 + 频道路由 | PicoClaw (Agent Collaboration Bus), IronClaw (多租户) | ⚠️ **平衡兼容性** — 为支持多频道做出架构妥协，导致内容泄露等边界问题 |

### 技术路线差异

```
OpenClaw:
├─ 频道聚焦: 将"频道适配"作为核心能力，支持QQ/Discord/Telegram等多种消息生态
├─ 工具集成: MCP 标准化 + 工具结果强制转换 (统一异构工具接口)
├─ 安全模式: 事后修复型 (发现QQBot内容泄露后打补丁)
└─ 目标用户: 多渠道、多工具整合的中重度用户

竞争项目对比:
├─ IronClaw:   多租户优先 (per-user auth, shared tools) → 企业应用
├─ CoPaw:      浏览器自动化优先 (页面交互、UI自动化) → 任务自动化
├─ Zeroclaw:   Cron + Web管理优先 (后台任务、Web仪表板) → 生产运维
├─ PicoClaw:   安全优先 (多层隔离、审计) → 企业安全敏感场景
└─ NanoBot:    轻量化优先 (内存效率、CLI友好) → 边缘设备、本地部署
```

### 社区规模对比

| 项目 | 今日评论热度 | Issue讨论深度 | 用户反馈质量 | 推论 |
|------|---|---|---|---|
| **OpenClaw** | 29条评论 (Issue #25592) | 多频道、多工具、架构跨度大 | 用户反馈覆盖面广，但多为"发现bug后报告" | 📊 **大社区，快速反馈循环** |
| **IronClaw** | 3条评论 (Issue #3026) | 企业特性 (多租户、权限)，聚焦产业化 | 用户反馈精准，需求与路线图高度对齐 | 📊 **专业社区，需求导向强** |
| **CoPaw** | 10条评论 (Issue #5017) | 模型效能、自动化学习循环 | 用户期待高，参与度高（建议学习循环） | 📊 **活跃社区，创意驱动** |
| **PicoClaw** | 1条评论 (新安全Issue) | 安全审计，工程化建议 | 专业安全审计团队反馈，质量高 | 📊 **垂直社区，安全审计活跃** |

**定位结论**：
- OpenClaw = **"渠道集成旗舰"** —— 广泛覆盖但需加强边界安全测试
- IronClaw = **"企业多租户标杆"** —— 产业应用方向清晰
- CoPaw = **"自动化体验先锋"** —— 用户体验和创新意愿最强
- PicoClaw = **"安全审计样本"** —— 工程化安全指导性强

---

## 4. 🔄 共同关注的技术方向

### 跨项目热点汇总

#### 🔴 **优先级 P0：安全隔离与数据保护**

| 技术问题 | 涉及项目 | 具体表现 | 行业意义 |
|---------|---------|---------|---------|
| **内容泄露** | OpenClaw, PicoClaw, Zeroclaw | 工具调用中间内容、思考过程、内部工具跟踪泄露到用户可见消息 | 🔴 **信息安全基线**，会动摇用户信任 |
| **SSRF 防护** | PicoClaw (15个审计Issue), CoPaw (文件预览) | web_fetch/file-preview 可被绕过（IPv6嵌入、代理链、特殊网段） | 🔴 **基础架构安全**，能导致内部网络暴露 |
| **权限隔离** | IronClaw (#4628), Zeroclaw (#6917), PicoClaw (#3081-3082) | MCP工具、Approval Hook、Feishu回复上下文可越权访问 | 🔴 **多租户/多用户**的必要条件 |
| **子进程资源限制** | Zeroclaw (#6916), PicoClaw (exec沙箱逃逸) | Shell/Skill 子进程无内存/CPU/文件描述符限制，可导致DoS | 🔴 **生产稳定性**，企业部署前置需求 |

**协同趋势**：安全不再是"后验修复"，而是**设计阶段的约束条件**。PicoClaw的15个安全审计Issue形成了最佳实践参考。

---

#### 🟠 **优先级 P1：多模型/多智能体协作**

| 需求类型 | 涉及项目 | 具体诉求 | 预期影响 |
|---------|---------|---------|---------|
| **跨模型子任务** | LobsterAI (#2132), CoPaw (#5017) | 不同模型的特长分工（M3规划+DeepSeek执行；Hermes学习循环） | 📈 **多模型经济** — 用户可以用成本最优模型组合完成复杂任务 |
| **Model per conversation** | NanoBot (#4253) | 在对话粒度切换模型预设（隐私/速度/成本权衡） | 📈 **细粒度成本控制** — 敏感任务用高成本模型，常规任务用廉价模型 |
| **Agent Collaboration Bus** | PicoClaw (已合并 #2937) | 多智能体间消息传递、分工协作 | 📈 **复杂系统工程** — 单Agent能力有限，合作才能解决现实问题 |

**协同趋势**：从"单Agent万能"向"多智能体分工"演进，对应企业场景中的"部门协作"需求。

---

#### 🟡 **优先级 P2：频道体验与消息路由**

| 技术问题 | 涉及项目 | 现状 | 改进方向 |
|---------|---------|------|---------|
| **消息丢失** | OpenClaw (8+ issue), Zeroclaw (#6034) | 心跳交付卡死、调度饥饿、频道路由失败 | ✅ 已有修复PR，需加速合并 |
| **频道级别隔离** | Zeroclaw (#6378), IronClaw (#4625) | Discord/Slack 无法限制bot响应到特定频道 | 🔄 **团队Agent** 的基础需求 |
| **Per-turn

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报
**日期：2026-06-10**

---

## 📊 今日速览

NanoBot 项目保持高度活跃，过去24小时PR合并率达到52%（13/25已处理），显示核心功能迭代进行中。同时有6条新Issue被创建/激活，社区反馈积极。虽无版本发布，但多个重要修复和功能已合并，包括WebUI数学公式支持、Email多渠道增强和文档完善，项目整体向前推进稳健。

---

## 🔧 项目进展

**已合并/关闭的关键PR（8项）：**

| PR编号 | 标题 | 类型 | 影响范围 |
|-------|------|------|--------|
| [#4252](https://github.com/HKUDS/nanobot/pull/4252) | fix(webui): render TeX math delimiters | 修复 | WebUI渲染，支持 `\(...\)` 和 `$...$` LaTeX语法 |
| [#4258](https://github.com/HKUDS/nanobot/pull/4258) | feat(email): add configurable IMAP post-actions | 功能 | Email频道，处理后可自动移动/删除消息 |
| [#4190](https://github.com/HKUDS/nanobot/pull/4190) | Improve tool call validation strictness | 增强 | 工具调用安全性，提升参数验证严格度 |
| [#4177](https://github.com/HKUDS/nanobot/pull/4177) | docs: make onboarding friendlier for beginners | 文档 | 重组入门文档，添加配置任务地图 |
| [#3400](https://github.com/HKUDS/nanobot/pull/3400) | feat(dream): allow users to decide whether dream can edit USER.md and SOUL.md | 功能 | Dream权限控制，新增 `allow_edit_identity_files` 选项 |
| [#3434](https://github.com/HKUDS/nanobot/pull/3434) | feat(lateX): add lateX to feishu channel using codecogs | 功能 | 飞书频道LaTeX支持，集成CodeCogs API |
| [#4034](https://github.com/HKUDS/nanobot/pull/4034) | Add GitAgent Protocol support (agent.yaml + SOUL.md) | 功能 | GitAgent协议支持，增强可移植性 |
| [#4265](https://github.com/HKUDS/nanobot/pull/4265) | feat(english-read): change cron schedule from daily to every 2 days | 增强 | Cron调度优化，从每天改为每2天执行 |

**进展评估：** 13个PR已处理反映了文档、安全性、渠道功能和工具调用的全面推进，WebUI/Email/飞书等多个交互层面同步优化。

---

## 🔥 社区热点

**高活跃Issue：**

1. **[#4259](https://github.com/HKUDS/nanobot/issues/4259) - history.jsonl 跨会话注入导致上下文污染** ⚠️ 严重
   - 作者：@chxuan | 评论：2 | 更新：2026-06-09
   - **问题本质：** `ContextBuilder` 在构建system prompt时，将 `history.jsonl` 中来自不同会话的entry混入当前会话，造成上下文污染。存在数据隔离设计缺陷。
   - **影响：** 会话间对话历史泄露，多轮对话中模型可能被前序其他会话的内容干扰

2. **[#4253](https://github.com/HKUDS/nanobot/issues/4253) - support overriding model per conversation** 💡 需求
   - 作者：@rombert | 评论：3 | 创建：2026-06-08
   - **用户诉求：** 支持按对话粒度切换模型预设（如隐私/速度敏感度不同，在openrouter和local llamacpp间切换）
   - **使用场景：** 多模型策略化部署，平衡隐私、性能和成本

3. **[#4264](https://github.com/HKUDS/nanobot/issues/4264) - idleCompact should use complete session history** 🐛 核心Bug
   - 作者：@imkuan | 评论：0 | 创建：2026-06-09
   - **问题根因：** idleCompact仅对除最后8条消息外的历史总结，导致最后的纠错和正确结果可能被遗漏，在 history.jsonl 留下错误记录
   - **场景：** 用户多轮纠正后完成任务，最终正确状态未被完整记录

---

## 🐛 Bug与稳定性

**严重级别（需关注）：**

| Issue | 描述 | 状态 | Fix PR |
|-------|------|------|--------|
| [#4259](https://github.com/HKUDS/nanobot/issues/4259) | history.jsonl 跨会话上下文污染 | OPEN | ❌ 未有 |
| [#4264](https://github.com/HKUDS/nanobot/issues/4264) | idleCompact遗漏最后8条消息的纠正内容 | OPEN | ❌ 未有 |
| [#4061](https://github.com/HKUDS/nanobot/issues/4061) | OpenAI兼容text格式工具调用未解析 | OPEN | ❌ 未有 |

**中等级别（已有修复）：**

| Issue | 描述 | Fix PR | 状态 |
|-------|------|--------|------|
| [#4261](https://github.com/HKUDS/nanobot/issues/4261) | GPT-5.x期望 `max_completion_tokens` 而非 `max_tokens` | [#4263](https://github.com/HKUDS/nanobot/pull/4263) | ✅ 已处理 |

**其他修复待合并：**
- [#4266](https://github.com/HKUDS/nanobot/pull/4266) - apply_patch 行分隔符处理（OPEN）
- [#4256](https://github.com/HKUDS/nanobot/pull/4256) - 保持memory cursor单调性（OPEN）
- [#4257](https://github.com/HKUDS/nanobot/pull/4257) - split_message 栅栏代码块感知（OPEN）
- [#4119](https://github.com/HKUDS/nanobot/pull/4119) - 阻止相对符号链接workspace逃逸（安全修复）

---

## 💡 功能请求与路线图信号

**新功能需求热度：**

| 需求 | Issue | PR进展 | 优先级 |
|------|-------|--------|--------|
| **按对话切换模型预设** | [#4253](https://github.com/HKUDS/nanobot/issues/4253) | 讨论中（3条评论） | 🔴 待评估 |
| **Agent启动时显示自定义botIcon** | [#4262](https://github.com/HKUDS/nanobot/issues/4262) | 无PR | 🟡 低优先 |
| **StepFun ASR transcription provider** | [#4260](https://github.com/HKUDS/nanobot/pull/4260) (新增ASR) | [#4260](https://github.com/HKUDS/nanobot/pull/4260) OPEN | 🟢 进行中 |
| **OpenAI text格式工具调用支持** | [#4061](https://github.com/HKUDS/nanobot/issues/4061) | 无PR | 🔴 待处理 |

**已合并信号（下一版本可能包含）：**
- 📐 LaTeX数学公式渲染（WebUI + 飞书频道）
- 📧 Email渠道IMAP后处理动作
- 🔐 Dream编辑权限细粒度控制
- 🔗 GitAgent Protocol互操作性

---

## 👥 用户反馈摘要

**核心痛点：**

1. **多模型策略需求强烈** (@rombert) - 用户有差异化模型需求（隐私/速度/成本权衡），期望在会话级或任务级选择，而非全局配置

2. **会话上下文隔离缺失** (@chxuan) - 在多轮对话、会话归档、历史重用的流程中，跨会话数据混入导致模型决策被污染，反映了内存管理和隔离的设计问题

3. **会话压缩策略不完善** (@imkuan) - idleCompact移除最后N条消息的方式过于固定，无法适应"纠错-完成"的真实对话模式，建议采用更灵活的token/语义预算方式

4. **工具调用兼容性** (@hamb1y) - 第三方OpenAI兼容provider的text格式工具调用与nanobot的结构化工具调用期望不匹配，跨provider支持不足

5. **配置细节完善** (@mraad) - UI细节和配置选项期望更加人性化（botIcon一致性、max_tokens字段）

**满意指标：** 
- 文档改进获得合并（用户入门体验重视）
- 多渠道功能持续增强（飞书、Email等）
- 工具调用验证严格度提升（安全第一）

---

## 📋 待处理积压

**需要维护者关注的重要Issue（无PR、讨论活跃）：**

| Issue | 标题 | 天数 | 评论 | 建议 |
|-------|------|------|------|------|
| [#4259](https://github.com/HKUDS/nanobot/issues/4259) | history.jsonl 跨会话污染 | 1天 | 2 | 🔴 **优先** - 数据隔离bug，影响多会话可靠性 |
| [#4264](https://github.com/HKUDS/nanobot/issues/4264) | idleCompact遗漏纠错 | 1天 | 0 | 🔴 **优先** - 会话压缩策略bug，影响长对话准确性 |
| [#4253](https://github.com/HKUDS/nanobot/issues/4253) | 按对话覆盖模型 | 2天 | 3 | 🟡 **设计讨论** - 需架构评审后规划 |
| [#4061](https://github.com/HKUDS/nanobot/issues/4061) | OpenAI文本工具调用 | 12天 | 1 | 🟡 **待所有者响应** - 长期未跟进，影响provider兼容性 |

**待合并的关键PR（已ready但未merge）：**

- [#4256](https://github.com/HKUDS/nanobot/pull/4256) - Memory cursor单调性（安全相关）
- [#4266](https://github.com/HKUDS/nanobot/pull/4266) - apply_patch行分隔（修复）
- [#4257](https://github.com/HKUDS/nanobot/pull/4257

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报｜2026-06-10

---

## 📊 今日速览

Zeroclaw 项目今日**保持高度活跃**，24 小时内新增 50 条 Issue（49 条活跃）和 50 条 PR（49 条待合并），团队工程速度处于显著高峰。虽然无新版本发布，但可见后端正在进行大规模功能迭代（RFC 架构改进、安全加固、多渠道集成、工具链扩展等），这表明项目正在为下一阶段重大更新进行筹备。核心风险点集中在**消息路由、权限隔离、进程资源限制**等生产环保护方面。

---

## 🔄 版本发布

本日无新版本发布。上一稳定版本为 v0.7.5，当前有 v0.8.0-beta-1 进行中（已发现多项配置 UX 和 API 网关问题）。

---

## 🚀 项目进展

### 合并/关闭的关键 PR（昨日）

| PR | 作者 | 标签 | 摘要 |
|---|---|---|---|
| **#7425** ✅ | @garacio | `bug`, `risk:high`, `agent` | **[已合并]** Channel 成本追踪修复：通过 bare-type fallback 解决成本记录为 0 导致每日预算失效的问题 |

### 待合并的重要 PR（今日热度较高）

| PR | 模块 | 风险 | 内容 |
|---|---|---|---|
| **#7417** | Cron / Web | `medium` | [**Cron 任务编辑 Modal 完整性修复**](https://github.com/zeroclaw-labs/zeroclaw/pull/7417)  — 扩展 `CronPatchBody` 以暴露 `delivery`, `model`, `session_target`, `allowed_tools`, `delete_after_run` 等全部字段，匹配添加表单 UX |
| **#7361** | Agent / Channels | `high` | [**Per-turn output routing & Voice delivery 修复**](https://github.com/zeroclaw-labs/zeroclaw/pull/7361) — 修复双发送 bug（TelegramChannel 缺失语音对等检查），规范化纯语音端点的草稿删除逻辑 (涉及 Slack/Telegram/Discord/Matrix 等 6 个渠道) |
| **#7367** | Gateway | `high` | [**Webhook 按渠道别名路由**](https://github.com/zeroclaw-labs/zeroclaw/pull/7367) — 多实例配置（如 `whatsapp.work` + `whatsapp.personal`）之前只路由到首个实例，现已支持路径级别的别名解析 |
| **#7344** | Gateway | `high` | [**远程管理端点选项**](https://github.com/zeroclaw-labs/zeroclaw/pull/7344) — `gateway.allow_remote_admin` 新配置项，允许远程仪表板通过 `/admin/reload` 应用配置变更（默认关闭，localhost 始终允许） |
| **#7438** | Channels | — | [**Telegram 交付指令优化**](https://github.com/zeroclaw-labs/zeroclaw/pull/7438) — 移除模型不鼓励工具使用的指令文本，修复小型 OpenAI 兼容模型（如 qwen3 via LM Studio）的工具调用率 |

**进度评估**：每日 50 条 PR 流转表明项目正在**快速迭代多个并行工作流**（多渠道、安全加固、Web 仪表板、架构重构），预计下一版本会包含显著的功能和稳定性提升。

---

## 💬 社区热点

### 评论最活跃的 Issues（真实用户诉求反映）

| Issue | 评论数 | 热度指标 | 核心诉求 | 链接 |
|---|---|---|---|---|
| **#5862** | 12 💬 | 🔴 **`blocked` + 需要复现** | **Agent 工具发现问题**：用户要求设置 8:00 PM 定时任务，但 zeroclaw 声称没有工具支持，实际上 `zeroclaw cron` 命令存在但未被 agent 识别；反映 Agent 对内置命令的可见性问题 | [查看](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) |
| **#5937** | 10 💬 | 🔴 **`risk:high` 架构问题** | **Provider 架构统一**：providers 模块存在 `reqwest` 和模型构造参数的不一致使用和代码重复，提出全局重构提案 | [查看](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) |
| **#6378** | 7 💬 | 🟠 `enhancement` | **Discord 频道级隔离**：用户希望限制 bot 响应到特定 Discord 频道（仿 `allowed_rooms` 在 Matrix/Nextcloud Talk 中的实现） | [查看](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) |
| **#5844** | 6 💬 | 🔴 `risk:high` P1 | **内存权重过高**：系统 prompt 对内存的强调度过高，导致 cron 任务中 memory 优先级覆盖当前指令 | [查看](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) |

### 高风险 / 待梳理的 RFC 类讨论

| # | 标题 | 作者 | 类型 | 影响范围 |
|---|---|---|---|---|
| **#7415** | [RFC] 统一三个 Agent Turn 引擎 | @Nillth | `architecture` | 核心 agent 循环实现了 3 次，其中 2 次缺失已审计的安全保护；建议统一实现 |
| **#7232** | [RFC] 结构化可观测性增强 | @FTDGRT | `observability` | 补充 ObserverEvent 的 channel 属性、agent 别名、成本信息，对多 agent 部署至关重要 |
| **#7184** | [RFC] 翻译文件移入 Git Submodule | @singlerider | `i18n / repo structure` | 将 `.ftl` 和 `.po` 翻译文件移出主树，隔离翻译提交历史 |

---

## 🐛 Bug 与稳定性

### P1 / S1 级（工作流阻塞）

| # | 标题 | 症状 | 状态 | Fix PR |
|---|---|---|---|---|
| **#6646** | [Web search tool & web_fetch 在 Telegram 无反应](https://github.com/zeroclaw-labs/zeroclaw/issues/6646) | 用户在 Telegram 通过 qwen3.5 模型请求网络搜索，工具调用被吞掉 | `accepted` | **#7438** (Telegram delivery prompt 重新表述) |
| **#6034** | [单轮/多轮对话丢失 user message](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) | 自定义 HTTP 兼容 API 返回 400 Bad Request，消息丢失 | `accepted` | 🔍 开放 |
| **#6037** | [Cron 任务重复启动](https://github.com/zeroclaw-labs/zeroclaw/issues/6037) | 单个日度 cron 任务被并发启动 20 次（运行时间 > 轮询间隔） | `in-progress` | 🔍 Pending |

### P2 / S2-S3 级（降级行为/小问题）

| # | 标题 | 症状 | 影响 |
|---|---|---|---|
| **#5844** | [内存权重过高](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | System prompt 过度强调内存历史 | Cron 任务优先级反转 |
| **#6876** | [MCP tools 不受 risk_profile.allowed_tools 限制](https://github.com/zeroclaw-labs/zeroclaw/issues/6876) | `allowed_tools` 配置仅对内置工具生效 | ⚠️ 文档缺陷或设计意图不清 |
| **#6584** | [OpenAI 兼容提供者忽略 `reasoning` 字段](https://github.com/zeroclaw-labs/zeroclaw/issues/6584) | 仅读取 `reasoning_content`，不读 `reasoning` | 与 OpenRouter/vLLM 标准不对齐 |
| **#6002** | [Telegram 消息未清晰寻址](https://github.com/zeroclaw-labs/zeroclaw/issues/6002) | llama.cpp + Telegram 集成中消息路由混乱 | 提供者兼容性问题 |
| **#7376** | [Dashboard 隐藏错误状态/标签历史为活跃会话](https://github.com/zeroclaw-labs/zeroclaw/issues/7376) | zerocode Dashboard TUI 在 macOS 隐藏有用错误信息 | 可观测性降级 |
| **#7377** | [深色主题文本无法读](https://github.com/zeroclaw-labs/zeroclaw/issues/7377) | zerocode TUI 继承终端前景色导致文本不可读 | UX 问题 |
| **#7378** | [macOS Cmd-C 误被识为退出快捷键](https://github.com/zeroclaw-labs/zeroclaw/issues/7378) | 尝试复制文本时意外退出 | macOS 特有 bug |

### 高风险安全类 Issue（需加急）

| # | 标题 | 风险 | 状态 |
|---|---|---|---|
| **#6916** | [Shell/Skill 子进程无内存限制](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) | 单个工具进程可耗尽容器全部内存（已在生产观察） | `accepted` — 需要 OOM 防护 |
| **#6917** | [Composio 工具缺少 action-scope 过滤](https://github.com/zeroclaw-labs/zeroclaw/issues/6917) | Agent 可访问已授权工具包的全部 action（如邮件的发送权限） | `blocked, accepted` |
| **#5775** | [Skill 权限粒度缺失](https://github.com/zeroclaw-labs/zeroclaw/issues/5775) | `allow_scripts` 和 `allowed_commands` 是全局开关，无法按 skill 隔离 | `blocked, accepted` |

---

## ✨ 功能请求与路线图信号

### 明确来自用户的新增功能需求

| Issue | 类型 | 描述 | 预期价值 | PR 进展 |
|---|---|---|---|---|
| **#6378** | `enhancement` | Discord 频道

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 | 2026-06-10

## 📊 今日速览

PicoClaw 项目今日呈现**超高活跃度状态**，创下单日数据高峰。过去24小时新增/活跃 Issues 17 条、PR 21 条，共发布 1 个 Nightly 版本。值得关注的是，**15 个安全问题在同一时间窗口被批量报告**，暗示项目已接收并处理了系统性的安全审计反馈；同时有 6 个 PR 完成合并/关闭，显示团队在并行处理多个功能迭代与缺陷修复。整体健康度评估：**活跃度高 ✓ | 响应速度快 ✓ | 安全重视度高 ✓**

---

## 🚀 版本发布

**Nightly: v0.2.9-nightly.20260609.46b29a0a**
- **发布时间**: 2026-06-09 
- **变更范围**: 自 `v0.2.9` 至 `main` 分支所有提交
- **特性**: 自动化构建产物，标记为不稳定，仅供测试使用
- **更新链接**: [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

⚠️ **提醒**: 该版本包含15项安全补丁与多项bug修复，**生产环境应等待正式版本发布**；测试环境可用于验证安全修复有效性。

---

## ✅ 项目进展

### 已合并/关闭的主要 PR （6 条）

| PR | 标题 | 影响范围 | 进度 |
|---|---|---|---|
| #3064 | [fix(config): type assertion safety check](https://github.com/sipeed/picoclaw/pull/3064) | 配置迁移健壮性 | ✅ 已合并 |
| #2942 | [fix(config): canonical model ID for claude-sonnet](https://github.com/sipeed/picoclaw/pull/2942) | Anthropic 提供商兼容性 | ✅ 已合并 |
| #2940 | [fix(providers): omit temperature for claude-opus-4-7](https://github.com/sipeed/picoclaw/pull/2940) | Claude Opus 4.7 适配 | ✅ 已合并 |
| #2937 | [feat(agent): Agent Collaboration Bus](https://github.com/sipeed/picoclaw/pull/2937) | **多智能体协作** | ✅ 已合并 |
| #3086 | [docs: update wechat qrcode](https://github.com/sipeed/picoclaw/pull/3086) | 文档维护 | ✅ 已合并 |
| #3064 | [fix(config): model name indexing panic prevention](https://github.com/sipeed/picoclaw/pull/3064) | 运行时稳定性 | ✅ 已合并 |

**核心推进**: 
- **Agent Collaboration Bus** (#2937) 是重要的架构完善，为多智能体间协作奠定基础
- **模型兼容性修复** (#2940, #2942) 直接解决用户在 Claude 最新模型上的使用障碍
- **配置健壮性** 改进系列确保极端配置场景的安全性

---

## 🔥 社区热点

### 一级热点：安全审计批量报告

**15 个安全问题在 2026-06-09 同时报告**，报告人 @YLChen-007，覆盖以下关键领域：

#### Web & 访问控制（5 项）
1. **[#3072](https://github.com/sipeed/picoclaw/issues/3072)** - 首轮密码设置的 CSRF 漏洞允许本地控制平面接管
2. **[#3071](https://github.com/sipeed/picoclaw/issues/3071)** - WebSocket 认证客户端可触发未授权的网关配置重载
3. **[#3069](https://github.com/sipeed/picoclaw/issues/3069)** - `allowed_cidrs` 可通过反向代理绕过（RemoteAddr 信任问题）
4. **[#3080](https://github.com/sipeed/picoclaw/issues/3080)** - `allowed_cidrs` 可通过本地环回代理绕过

#### 数据获取安全（6 项）
5. **[#3078](https://github.com/sipeed/picoclaw/issues/3078)** - `web_fetch` SSRF 保护可通过环境配置的 HTTP 代理绕过
6. **[#3077](https://github.com/sipeed/picoclaw/issues/3077)** - `web_fetch` SSRF 可通过特殊用途 IPv4 198.18.0.0/15 绕过
7. **[#3074](https://github.com/sipeed/picoclaw/issues/3074)** - `web_fetch` 可通过 ISATAP IPv6 嵌入的私有 IPv4 绕过
8. **[#3070](https://github.com/sipeed/picoclaw/issues/3070)** - OneBot 媒体 URL 处理允许任意主机端获取

#### 命令执行与权限（3 项）
9. **[#3081](https://github.com/sipeed/picoclaw/issues/3081)** - Approval hook `cwd` symlink race 允许 `exec` 在未审核目录运行
10. **[#3079](https://github.com/sipeed/picoclaw/issues/3079)** - `exec` 命令白名单通过 jq 环境泄露绕过拒绝模式

#### 通讯渠道安全（4 项）
11. **[#3082](https://github.com/sipeed/picoclaw/issues/3082)** - Feishu 回复上下文扩展绕过 `allow_from` 验证
12. **[#3076](https://github.com/sipeed/picoclaw/issues/3076)** - WeCom 群组触发策略可被绕过
13. **[#3075](https://github.com/sipeed/picoclaw/issues/3075)** - 当前工作目录的 `skills/` 元数据被无条件加载
14. **[#3073](https://github.com/sipeed/picoclaw/issues/3073)** - LINE webhook 签名可被重放
15. **[#3068](https://github.com/sipeed/picoclaw/issues/3068)** - MQTT `allow_from` 通过 topic `client_id` 欺骗绕过

**分析**: 这是一次**全面的安全审计反馈**，覆盖认证、授权、网络隔离、沙箱逃逸、渠道隔离等多维度。问题范围从本地权限提升到远程数据获取，**严重程度普遍较高**。建议：
- 优先处理 Web 认证与 SSRF 漏洞（#3072, #3078, #3077）
- 制定 CVE 公告与补丁发布计划
- 考虑增加安全测试 CI 流程

---

### 二级热点：功能需求与协议完善

**[#2984](https://github.com/sipeed/picoclaw/issues/2984)** - Add explicit turn completion signal for WebSocket clients
- 作者: @Brook-sys | 评论: 1 | 👍: 1 | 创建: 2026-06-02
- **痛点**: 外部 WebSocket 客户端无法确定代理何时完全处理完用户消息
- **诉求**: 明确的回合完成信号（turn completion）
- **进度**: 已有 Issue，等待实现

**[#2404](https://github.com/sipeed/picoclaw/issues/2404)** - Add streaming HTTP request support in config
- 作者: @OuSatoru | 评论: 11 | 👍: 1 | 创建: 2026-04-07 | 更新: 2026-06-09
- **需求**: 在配置中增加 `"streaming": true` 支持流式 HTTP 请求
- **背景**: 与 Python OpenAI 客户端对齐，便于接入流式 LLM 后端
- **进度**: Issue 长期开放，未见相关 PR

---

## 🐛 Bug 与稳定性

### 已修复的重点缺陷

| Issue | 标题 | 严重度 | 修复 PR | 状态 |
|-------|------|--------|--------|------|
| #2796 | 历史记录中多次用户消息只显示最后一条 | 🔴 高 | [#2990](https://github.com/sipeed/picoclaw/pull/2990) | ✅ PR 开放中 |
| #2939 | claude-opus-4-7 拒绝 temperature 参数 | 🔴 高 | [#2940](https://github.com/sipeed/picoclaw/pull/2940) | ✅ 已合并 |
| #2968 | `/context` 命令忽视 `summarize_token_percent` 配置 | 🟡 中 | [#2988](https://github.com/sipeed/picoclaw/pull/2988) | ✅ PR 开放中 |
| #2958 | tool_calls 消息在流式传输时被错误过滤 | 🟡 中 | [#2987](https://github.com/sipeed/picoclaw/pull/2987) | ✅ PR 开放中 |
| 配置崩溃 | 模型名称类型断言无保护 | 🔴 高 | [#3064](https://github.com/sipeed/picoclaw/pull/3064) | ✅ 已合并 |

### 待合并的 Bug Fix PR

- **[#3087](https://github.com/sipeed/picoclaw/pull/3087)** - `exec` 安全卫士对相对路径的误判
- **[#2983](https://github.com/sipeed/picoclaw/pull/2983)** - LLM 空响应重试缝隙（语义空内容）
- **[#3067](https://github.com/sipeed/picoclaw/pull/3067)** - Session 隔离范围配置无法持久化
- **[#3061](https://github.com/sipeed/picoclaw/pull/3061)** - Windows 子进程控制台闪烁问题

### 稳定性评估

**现状**: 发现的缺陷均有对应 fix PR，无明显"僵尸 Bug"。安全审计的 15 个问题目前仍需修复，建议：
- 跟进 #2990, #2987, #2988 的合并时间表
- 为安全问题建立 fix PR 并加急审核

---

## 💡 功能请求与路线图信号

### 近期可能纳入版本的功能

| 功能 | Issue/PR | 状态 | 评估 |
|------|---------|------|------|
| **Agent 多智能体协作** | #2937 | ✅ 已合并 | **v0.3.0 候选** |
| **NEAR AI Cloud 提供商** | [#2917](https://github.com/sipeed/picoclaw/pull/2917) | 🔄 待合并 | 新的 LLM 生态接入 |
| **DeltaChat 网关** | [#3063](https://github.com/sipeed/picoclaw/pull/3063) | 🔄 待合并 | 通讯渠道扩展 |
| **Launcher 访问控制强化** | [#3083](https://github.com/sipeed/picoclaw/pull/3083) | 🔄 待合并 | 安全加固 |
| **流式 HTTP 请求** | #2404 | ⏳ 需求 | v0.4.0+ 考虑 |
| **WebSocket 回合信号** | #2984 | ⏳ 需求 | 协议完善方向 |

### 用户新增需求归类

```
基础设施 (6):
├─ 流式请求配置 (Python SDK 对齐) → 中优先级
├─ WebSocket 回合信号 (DX 完善) → 中优先级
├─ Agent

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报
**日期**: 2026-06-10 | **统计周期**: 过去24小时  
**项目**: [github.com/qwibitai/nanoclaw](https://github.com/qwibitai/nanoclaw)

---

## 1. 📊 今日速览

NanoClaw 在过去24小时内维持稳定的开发节奏，共产生 **4 条 PR 活动**，其中 2 条已关闭/合并、2 条待审核。值得注意的是**零新增 Issue**，表明项目在当前功能集上的稳定性较好，或社区反馈暂时平稳。整体活跃度适中，聚焦于功能完善（uninstall 工具、生态文档）和生产 bug 修复（Feishu 僵尸卡片），未发布新版本。

---

## 2. 🚀 版本发布

**无新版本发布**

---

## 3. ✅ 项目进展

### 已关闭/合并的关键 PR（2 条）

| PR | 标题 | 作者 | 状态 | 影响 |
|:---|:-----|:-----|:-----|:-----|
| [#2718](https://github.com/nanocoai/nanoclaw/pull/2718) | **fix(feishu): cleanup zombie active_cards when agent-runner exits abnormally** | @brookgao | ✅ CLOSED | **生产 bug 修复** - 解决 Feishu 交互卡片在 agent-runner 异常退出后长期卡在"运行中"状态（>50分钟）的问题。根本原因：`deleteActiveCard(jid)` 仅在 SDK `final` 事件触发时执行，但异常退出时该事件未被正确触发。 |
| [#2716](https://github.com/nanocoai/nanoclaw/pull/2716) | **resolve check test 0609 once** | @zybChaitin | ✅ CLOSED | 测试检查修复 - 解决 0609 版本测试套件问题 |

### 待审核的功能 PR（2 条）

| PR | 标题 | 作者 | 创建时间 | 优先级 |
|:---|:-----|:-----|:--------|:------|
| [#2719](https://github.com/nanocoai/nanoclaw/pull/2719) | **feat: add uninstall.sh — per-copy uninstaller with confirmation, dry-run, and OneCLI agent cleanup** | @amit-shafnir | 2026-06-09 | 🟡 工具完整性 |
| [#2717](https://github.com/nanocoai/nanoclaw/pull/2717) | **docs: add Atlas Cloud as OpenAI-compatible LLM backend option** | @lucaszhu-hue | 2026-06-09 | 🟡 生态扩展 |

**进展评估**: 项目在微服务可靠性（Feishu 卡片管理）和部署工具链（uninstall.sh）上持续演进，同时积极拓展 LLM 后端生态支持。

---

## 4. 💬 社区热点

**数据限制**: 当前数据未提供评论计数（comment count 为 undefined），无法准确识别最活跃的讨论。

**观察**: 所有 4 条 PR 均在 24 小时内创建并有快速响应（#2718、#2716 已关闭），表明维护团队的**响应效率较高**，但缺乏大规模社区讨论的迹象（可能反映项目使用场景相对垂直或社区规模)。

---

## 5. 🐛 Bug 与稳定性

### 已修复的生产 Bug

**[#2718] Feishu 僵尸卡片问题 — 严重程度: 🔴 高**
- **现象**: Interactive card 卡在"运行中"状态 50+ 分钟不更新
- **根本原因**: `agent-runner` 因 `PROCESS_TIMEOUT` 被强制杀死时，`deleteActiveCard(jid)` 的 cleanup 逻辑未正确执行（依赖 SDK 的 `final` 事件）
- **状态**: ✅ 已修复并合并 ([@brookgao](https://github.com/brookgao))
- **影响范围**: Feishu 集成用户在异常超时场景

### 待修复的已知问题

**无** - 当前无 Issue 队列中的开放 bug 报告

---

## 6. 💡 功能请求与路线图信号

### 近期 Approved Features（基于待合并 PR）

| 功能 | PR | 类别 | 推进阶段 |
|:-----|:---|:-----|:--------|
| **统一卸载工具** (uninstall.sh) | [#2719](https://github.com/nanocoai/nanoclaw/pull/2719) | 部署工具 | 审核中 |
| **Atlas Cloud LLM 后端** | [#2717](https://github.com/nanocoai/nanoclaw/pull/2717) | LLM 生态 | 审核中 |

**路线图信号**:
1. **部署与卸载流程优化** - 引入 per-copy uninstaller 和 dry-run 支持，改进 OneCLI agent 的生命周期管理
2. **LLM 后端多样化** - 继 Feishu 之后，重点支持 OpenAI-compatible 协议的云端推理服务（Atlas Cloud 提供 59+ 模型），降低商业化部署成本
3. **稳定性优先** - Bug fix（#2718）显示团队在生产问题响应上的重视

---

## 7. 👥 用户反馈摘要

**数据限制**: 当前 Issue 队列为空（0 开放 Issue），无法提取用户反馈。

**可推断的需求信号**:
- 从 [#2719](https://github.com/nanocoai/nanoclaw/pull/2719) uninstall.sh 的存在，推断部分用户面临**卸载/清理复杂度**问题
- 从 [#2717](https://github.com/nanocoai/nanoclaw/pull/2717) Atlas Cloud 文档补充，推断用户需要**更多 LLM 后端选项**（尤其是成本优化的云服务）
- Feishu 僵尸卡片的出现，反映**多渠道集成的可靠性诉求**

---

## 8. ⏳ 待处理积压

**当前状态**: 
- ✅ **无长期未响应的 Issue** — 0 开放 Issue 队列
- ⏳ **2 条 PR 待审核** — [#2719](https://github.com/nanocoai/nanoclaw/pull/2719)、[#2717](https://github.com/nanocoai/nanoclaw/pull/2717) 均创建于 2026-06-09，建议在 48 小时内完成审核
- 💭 **建议**: 监控 #2719 uninstall.sh 的审核周期，确保部署工具链的完整性及时交付

---

## 📈 项目健康度评分

| 维度 | 评分 | 说明 |
|:-----|:-----|:-----|
| **响应速度** | ⭐⭐⭐⭐⭐ | 4 条 PR 均在 24h 内处理，团队效率高 |
| **稳定性** | ⭐⭐⭐⭐ | 生产 bug（Feishu）快速修复，无积压问题 |
| **社区活跃度** | ⭐⭐⭐ | 0 新增 Issue，社区讨论暂时平稳，可能反映使用场景垂直或社区规模较小 |
| **功能迭代** | ⭐⭐⭐⭐ | 在部署工具和 LLM 生态两条线上均有进展 |
| **整体** | ⭐⭐⭐⭐ | 稳定推进中，聚焦生产质量和生态拓展 |

---

**下一步关注**:
1. 🔔 [#2719](https://github.com/nanocoai/nanoclaw/pull/2719) uninstall.sh 审核进展
2. 📦 [#2717](https://github.com/nanocoai/nanoclaw/pull/2717) 文档合并后的用户反馈
3. 🛡️ Feishu 僵尸卡片修复在下一版本的发布时间

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报
**日期：2026-06-10** | **数据时间段：过去24小时**

---

## 1. 📊 今日速览

IronClaw 项目呈现 **高度活跃状态**，单日处理 48 个 Issue 和 50 个 PR，其中已关闭/合并 36 个，**待合并 21 个**。项目焦点明显聚集在 **Reborn 生产化就绪和 WebUI v2 端到端测试覆盖**，同时持续修复工具调用、LLM 提供商兼容性等关键缺陷。虽未发布新版本，但大量基础设施和兼容性工作已就绪，预示近期可能有重要版本推送。整体健康度良好，但 **待合并 PR 积压较多**，建议加速评审。

---

## 2. 📦 版本发布

**本日无新版本发布**

*备注：PR #3708（chore: release）正在开放状态，涉及多包的破坏性变更：*
- `ironclaw_common`: 0.4.2 → 0.5.0 ⚠️ API breaking
- `ironclaw_skills`: 0.3.0 → 0.4.0 ⚠️ API breaking
- `ironclaw`: 0.24.0 → 0.29.1

---

## 3. 🚀 项目进展

### 已合并/关闭的关键 PR（共 7 个已关闭）

| PR | 标题 | 类型 | 影响 |
|---|---|---|---|
| [#4651](https://github.com/nearai/ironclaw/pull/4651) | [codex] Handle Reborn Railway start command placeholders | Bug Fix | 修复 Railway 部署时环境变量占位符失效问题 |
| [#4631](https://github.com/nearai/ironclaw/pull/4631) | Reborn: wire production Postgres storage config | Infra | **XL** 范围，完成生产 Postgres 存储配置接线 |
| [#4605](https://github.com/nearai/ironclaw/pull/4605) | Setup reborn webui v2 playwright E2E smoke test | Test | 建立 Reborn WebUI v2 浏览器端到端测试基础 |
| [#4614](https://github.com/nearai/ironclaw/pull/4614) | Add webchat v2 authentication parity audit and route tests | Test | 验证 v1→v2 认证路径兼容性（Bearer/DB/OIDC/Query Token） |
| [#4599](https://github.com/nearai/ironclaw/pull/4599) | [codex] Add Reborn operator command-plane route shells | Infra | **XL** 范围，建立操作员命令平面基础（Setup/Config/Logs/Lifecycle） |

**核心成就**：
- ✅ 生产 Postgres 后端已接线（#4631）
- ✅ 操作员命令平面骨架就绪（#4599）
- ✅ WebUI v2 浏览器测试基础建成（#4605）
- ✅ 认证兼容性审计完成（#4614）

---

## 4. 🔥 社区热点

### 评论最活跃的 Issues（Top 5）

| Issue | 标题 | 评论数 | 发布日期 | 热度信号 |
|---|---|---|---|---|
| [#3026](https://github.com/nearai/ironclaw/issues/3026) | Epic: Reborn production wiring and cutover readiness | **3** | 2026-04-28 | 🔴 **P0 Epic**，贯穿生产化全流程 |
| [#3957](https://github.com/nearai/ironclaw/issues/3957) | [hooks] Third-party activation hardening follow-ups | **2** | 2026-05-23 | 🔴 安全审查必需，Hook 第三方启用前置条件 |
| [#4642](https://github.com/nearai/ironclaw/issues/4642) | Strict-mode providers' null-for-unset-optionals rejected | **1** | 2026-06-09 | 🟠 工具调用关键缺陷，影响大多数内置工具 |

### 最新创建的高优先级 Issues（今日 P0-P1）

| Issue | 标题 | 优先级 | 所有者 |
|---|---|---|---|
| [#4647](https://github.com/nearai/ironclaw/issues/4647) | Unified (omni) search across threads, skills, extensions, and memory | P1 | @ilblackdragon |
| [#4644](https://github.com/nearai/ironclaw/issues/4644) | Universal attachments across all channels | P1 | @ilblackdragon |
| [#4625](https://github.com/nearai/ironclaw/issues/4625) | Slack channel-routed personal and team agents | P1 | @serrrfirat |
| [#4628](https://github.com/nearai/ironclaw/issues/4628) | Admin-shared tools and skills with per-user auth | P1 | @serrrfirat |

**热点解读**：
- **Reborn 生产化** 仍是团队 Top 1 焦点（#3026 Epic 及其 5 个子任务 #4619-4621 均已开启）
- **多租户/企业功能** 浮现（#4628 Shared tools、#4625 Slack routing、#4647 Omni search）
- **安全加固** 序列跟进（#3957 Hook 安全、#4611/4614 认证审计）

---

## 5. 🐛 Bug 与稳定性

### 今日报告的 Bugs（共 4 个，按严重程度排序）

| Issue | 标题 | 严重性 | 影响范围 | Fix PR | 状态 |
|---|---|---|---|---|---|
| [#4642](https://github.com/nearai/ironclaw/issues/4642) | Strict-mode providers' null-for-unset-optionals rejected by capability validation | 🔴 **Critical** | 影响 OpenAI/Codex/Claude 等 strict-mode 提供商的**所有工具调用** | [#4643](https://github.com/nearai/ironclaw/pull/4643) | ✅ 已有 PR，待合并 |
| [#4548](https://github.com/nearai/ironclaw/issues/4548) | Chat completion request serializes duplicate top-level `model` field when tools are included | 🟠 **High** | DeepSeek 提供商收到 HTTP 400 | — | ❌ 无 Fix PR |
| [#4587](https://github.com/nearai/ironclaw/issues/4587) | Cannot configure Minimax provider | 🟠 **High** | Minimax 提供商配置失败 | — | ❌ 无 Fix PR |
| [#4640](https://github.com/nearai/ironclaw/issues/4640) | Reborn gsuite google-calendar list_events returns oldest/unordered events | 🟡 **Medium** | 日历查询返回历史数据（缺 timeMin/orderBy） | — | ❌ 无 Fix PR |

### 稳定性评估
- ✅ 关键工具调用缺陷（#4642）**已有修复 PR #4643**，但仍待合并
- ⚠️ **DeepSeek、Minimax 提供商缺陷无人认领**，可能影响用户
- ⚠️ Calendar 集成返回错误数据，用户体验差

**建议**：加速 #4643 评审合并，并分配 #4548 和 #4587 的所有者。

---

## 6. 🎯 功能请求与路线图信号

### 新增高优先级 Feature Issues（共 6 个）

#### 第一梯队：多租户与企业协作（P1）
- **[#4628](https://github.com/nearai/ironclaw/issues/4628)** — Admin-shared tools and skills with per-user auth  
  *问题*：无法在多租户实例中共享预配置的工具，每个用户都要重复配置  
  *诉求*：管理员一次配置，所有成员可用，支持基于用户的认证权限隔离  
  *信号*：企业客户强需求

- **[#4625](https://github.com/nearai/ironclaw/issues/4625)** — Slack channel-routed personal and team agents  
  *问题*：Slack 无法成为第一类渠道，无法区分个人 Agent 和团队 Agent  
  *诉求*：一个 Slack App 支持 DM（个人 Agent）和频道（团队 Agent）的双重路由  
  *信号*：团队协作场景破局

#### 第二梯队：搜索与内容聚合（P1）
- **[#4647](https://github.com/nearai/ironclaw/issues/4647)** — Unified (omni) search  
  *现状*：搜索分散在前端命令面板、不完整、部分不真实  
  *诉求*：跨 Thread/Message/文件/Extensions/Skills/Memory 的统一搜索入口  

- **[#4644](https://github.com/nearai/ironclaw/pull/4644)** — Universal attachments across all channels  
  *现状*：Reborn 无声地丢弃附件；v1 有 4+ 个重复的格式支持逻辑  
  *诉求*：统一附件管道，可扩展格式注册表，Web UX 完善  

#### 第三梯队：安全与诊断（P1-P2）
- **[#4533](https://github.com/nearai/ironclaw/issues/4533)** — Reborn operator setup, config, diagnostics, and service lifecycle (Epic)  
  *问题*：Reborn 还不能替代 V1，因为无法自助部署、配置检查、调试、生命周期管理  
  *诉求*：完整的操作员工作流，无需手动编辑内部文件  
  *信号*：生产化前置条件，已有多个子 Issue 和 PR 在推进

### 已在开发的功能（Next Release 信号）

| PR | 功能 | 范围 | 预期影响 |
|---|---|---|---|
| [#4645](https://github.com/nearai/ironclaw/pull/4645) | Make Reborn production runtime launchable | **XL**，基础设施 | 生产环境首次完整可启动 |
| [#4652](https://github.com/nearai/ironclaw/pull/4652) | Document Reborn serve/WebUI testing flow + launcher | 开发者体验 | 降低本地开发门槛 |
| [#4653](https://github.com/nearai/ironclaw/pull/4653) | feat(cli): non-interactive tool setup with --secret flag | DevOps/CI-CD | 启用自动化部署流程 |
| [#4649](https://github.com/nearai/ironclaw/pull/4649) | fix(embeddings): honor config precedence, validate provider, enforce batch limits | 嵌入模型 | 修复 Bedrock 等提供商的配置优先级错误 |

**路线图信号**：
- 🟢 **Reborn 生产化** 即将突破（多个 PR 同步推进，基础设施已成型）
- 🟡 **多租户和企业功能** 开始浮现，预期下一个季度的重点

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# 📊 LobsterAI 项目动态日报
**日期**: 2026-06-10 | **数据周期**: 过去24小时

---

## 🎯 今日速览

LobsterAI 项目今日保持中等活跃度，共更新 **5 个 PR**（4个已合并）和 **2 个新 Issue**。项目核心聚焦于**协作功能完善**（任务完成通知）和**数据安全**（备份迁移），同时收到用户关于**跨模型多智能体协作**的架构级问题反馈。无新版本发布，但已合并的功能涉及系统通知、导出修复等，表明项目持续推进稳定性改进。

---

## 📦 版本发布

无新版本发布。

---

## 🚀 项目进展

**本日已合并 PR**（4个）

| PR | 作者 | 功能模块 | 描述 | 状态 |
|---|---|---|---|---|
| [#2130](https://github.com/netease-youdao/LobsterAI/pull/2130) | @liuzhq1986 | Cowork、通知 | **任务完成通知系统** - 为后台 Cowork 会话添加隐私安全的任务完成提醒，包括通知控制开关、macOS Dock 徽章和 Windows 任务栏支持 | ✅ 已合并 |
| [#2134](https://github.com/netease-youdao/LobsterAI/pull/2134) | @liuzhq1986 | Renderer、通知 | **任务完成通知恢复机制** - 修复主窗口关闭后的通知恢复、renderer 就绪等待、系统通知参考管理 | ✅ 已合并 |
| [#2135](https://github.com/netease-youdao/LobsterAI/pull/2135) | @fisherdaddy | Renderer | **临时关闭数据备份功能** - 可能与 #2136 的备份迁移重构有关 | ✅ 已合并 |
| [#2136](https://github.com/netease-youdao/LobsterAI/pull/2136) | @fisherdaddy | Renderer、核心、文档 | **数据备份和迁移功能** - 新增用户数据安全保护能力 | ✅ 已合并 |

**待合并 PR**（1个）

| PR | 作者 | 描述 | 优先级信号 |
|---|---|---|---|
| [#2133](https://github.com/netease-youdao/LobsterAI/pull/2133) | @fisherdaddy | **修复导出和代码复制 Bug** - 解决 Cowork 协作场景中的功能缺陷 | 🔧 Bug 修复，需尽快合并 |

---

## 💬 社区热点

**新提议 Issue**（2个）

1. **[#2131](https://github.com/netease-youdao/LobsterAI/issues/2131) - LobsterAI 支持 Hermes agent 有计划吗？**
   - 提问者: @wtgoku-create | 反应: 0 | 评论: 1
   - **信号**: 用户询问是否支持 Hermes 智能体框架，反映社区对**多智能体框架生态适配**的兴趣

2. **[#2132](https://github.com/netease-youdao/LobsterAI/issues/2132) - 跨模型子任务调用的问题**
   - 提问者: @woxinsj | 反应: 0 | 评论: 0
   - **信号**: 高质量架构级问题，涉及**跨模型协作**（如主任务用 M3 规划、子任务用 DeepSeek 执行）
   - **用户诉求**: 
     - 实现跨模型子任务的同步通知机制（参考同模型实现）
     - 子任务卡点/完成时主动反馈给主任务
     - 制定明确的跨模型任务调用规范
   - **技术深度**: 已进行根因检查（网关函数调用问题分析），说明社区具备较高的技术参与度

---

## 🐛 Bug 与稳定性

**已识别并处理的问题**

| 问题 | 位置 | 修复状态 | 严重程度 |
|---|---|---|---|
| 导出和代码复制功能缺陷 | Cowork 模块 | [#2133 待合并](https://github.com/netease-youdao/LobsterAI/pull/2133) | 🟡 中 |
| 任务完成通知恢复失败 | 系统通知系统 | [#2134 已合并](https://github.com/netease-youdao/LobsterAI/pull/2134) | 🟡 中 |
| 跨模型子任务调用失败 | 多智能体架构 | [#2132 需分析](https://github.com/netease-youdao/LobsterAI/issues/2132) | 🔴 高（架构缺陷） |

**稳定性评估**: 主要问题聚焦于新功能的边界场景（后台通知、跨模型调用），核心功能未见重大回归。

---

## 🎁 功能请求与路线图信号

**新功能诉求优先级**

| 优先级 | 功能 | 来源 | 预期影响 | 备注 |
|---|---|---|---|---|
| 🟥 高 | 跨模型子任务协作机制完善 | [#2132](https://github.com/netease-youdao/LobsterAI/issues/2132) | 核心竞争力提升 | 用户已规划实现方案，团队应跟进 |
| 🟨 中 | Hermes agent 框架支持 | [#2131](https://github.com/netease-youdao/LobsterAI/issues/2131) | 生态适配 | 需评估研发成本 |
| ✅ 进行中 | 数据备份和迁移 | [#2136 已合并](https://github.com/netease-youdao/LobsterAI/pull/2136) | 用户数据安全 | 刚完成实现 |
| ✅ 进行中 | 任务完成系统通知 | [#2130/2134 已合并](https://github.com/netease-youdao/LobsterAI/pull/2130) | 用户体验增强 | 已全量合并 |

---

## 👥 用户反馈摘要

**核心用户痛点**

1. **多模型协作能力欠缺** (Issue #2132)
   - 场景: 用户希望利用不同模型的特长（M3 擅长规划、DeepSeek 擅长快速执行）
   - 现状: 跨模型子任务调用机制不完善，子任务完成通知、卡点反馈缺失
   - 建议: 社区提出了具体的实现路径参考

2. **智能体框架兼容性** (Issue #2131)
   - 用户关注: Hermes 等第三方智能体框架是否得到支持
   - 暗示: 部分用户已有其他框架的使用基础，希望与 LobsterAI 整合

3. **隐私与安全** (PR #2130, #2136)
   - 满意点: 用户重视数据备份和隐私保护功能的实现（已合并）
   - 改进: 后台通知需要不暴露任务内容，体现对隐私的重视

---

## ⏳ 待处理积压

**当日暂无长期未响应的 Issue 或 PR**。所有新增 Issue (#2131, #2132) 创建于 24 小时内，待响应时间均在合理范围。建议优先关注 **#2132** 的架构级反馈，该 Issue 涉及核心多智能体能力，社区参与度高。

---

## 📈 数据汇总

| 指标 | 数值 | 环比 |
|---|---|---|
| 活跃 PR 数 | 5 | ↑ 中等 |
| 合并 PR 数 | 4 | ✅ 合并能力强 |
| 新 Issue 数 | 2 | ↑ 有社区参与 |
| 关闭 Issue 数 | 0 | → 需加速处理 |
| 版本发布 | 0 | → 无新发布 |

**项目健康度评估**: **6.5/10** - 功能迭代活跃，但跨模型等核心架构问题需尽快推进，建议下周优先合并 #2133 并启动 #2132 的设计评审。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报
**日期：2026-06-10 | 数据周期：过去24小时**

---

## 📊 今日速览

CoPaw 今日活跃度**极高**，24小时内处理 **34 个 Issue、35 个 PR**，其中 18 个 Issue 已关闭、15 个 PR 已合并，处理效率约 70%。发布了 **1.1.11-beta.2 版本**，包含浏览器控制增强和跨浏览器隔离修复。当前项目处于**快速迭代周期**，既有 Bug 修复（Windows 路径溢出、会话文件重复），也有大型架构升级（AgentScope 2.0 迁移、插件系统重构）并行推进，社区热情高涨。

---

## 🚀 版本发布

### **v1.1.11-beta.2** 
**发布时间：** 2026-06-09  
**PR：** [#5055](https://github.com/agentscope-ai/QwenPaw/pull/5055)

#### 更新内容
| 功能 | 描述 | PR |
|------|------|-----|
| **浏览器控制增强** | 新增页面坐标点击支持，提升自动化交互精度 | [#4905](https://github.com/agentscope-ai/QwenPaw/pull/4905) |
| **跨浏览器隔离** | 添加 CDP 超时参数和浏览器配置隔离机制，解决多浏览器切换冲突 | [#4905](https://github.com/agentscope-ai/QwenPaw/pull/4905) |

#### 迁移注意事项
- **无破坏性变更**，Beta 版本，建议灰度升级
- 浏览器配置隔离可能改变现有自动化脚本的会话管理行为，建议测试

---

## ✅ 项目进展

### 已合并关键 PR（共 15 个）

| 优先级 | PR | 主题 | 影响范围 | 状态 |
|--------|-----|------|--------|------|
| 🔴 **P0** | [#5021](https://github.com/agentscope-ai/QwenPaw/pull/5021) | 修复 `/compact` 命令忽略模型 `max_input_length` | 核心功能 | ✅ 已合并 |
| 🔴 **P0** | [#5036](https://github.com/agentscope-ai/QwenPaw/pull/5036) | 解决 Windows 会话文件名重复导致路径溢出 + Desktop Agent 间调用失败 | 稳定性 | ✅ 已合并 |
| 🟠 **P1** | [#5049](https://github.com/agentscope-ai/QwenPaw/pull/5049) | 免费模型零配置 + Provider OAuth 一键认证 | UX | ✅ 已合并 |
| 🟠 **P1** | [#5048](https://github.com/agentscope-ai/QwenPaw/pull/5048) | 修复 Agent 订阅广播中未 await 协程 | 并发安全 | ✅ 已合并 |
| 🟠 **P1** | [#5043](https://github.com/agentscope-ai/QwenPaw/pull/5043) | 集成 OpenSandbox MCP 插件，增强代码沙箱安全 | 安全 | ✅ 已合并 |
| 🟡 **P2** | [#5050](https://github.com/agentscope-ai/QwenPaw/pull/5050) | 主题切换图标优化（Computer → Sun） | UI 细节 | ✅ 已合并 |
| 🟡 **P2** | [#5054](https://github.com/agentscope-ai/QwenPaw/pull/5054) | 完整化 E2E 集成 CI 管道（后端启动、覆盖率、测试修复） | CI/CD | ✅ 已合并 |
| 🟡 **P2** | [#5012](https://github.com/agentscope-ai/QwenPaw/pull/5012) | M1 里程碑：Agent 页面 + API 模块单元测试（76 个新测试） | 测试覆盖 | ✅ 已合并 |
| 🟡 **P2** | [#5056](https://github.com/agentscope-ai/QwenPaw/pull/5056) | 移除冗余的 channel-tests workflow | CI 优化 | ✅ 已合并 |

### 本轮推进总结
- **稳定性突破**：修复了 Windows 路径溢出的关键 Bug（#5036），这是多位用户反复报告的痛点
- **功能体验**：零配置免费模型 + OAuth 认证大幅降低新用户入门门槛
- **测试基建**：E2E CI 管道全面落地 + 单元测试补齐，为后续大版本升级奠定基础
- **安全增强**：OpenSandbox MCP 集成、文件预览路径限制（#4981 待合并）

---

## 🔥 社区热点

### 讨论最活跃的 Issue

| Issue | 评论 | 👍 | 核心诉求 | 链接 |
|-------|------|-----|---------|------|
| **#5017** | 10 | 3 | 建议借鉴 Hermes Agent 的"学习循环"，实现 Agent 自动从行为中迭代技能 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/5017) |
| **#5003** | 8 | 0 | 使用阿里 Coding Plan（qwen3.7-plus）长期卡住，无法完成任务 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/5003) |
| **#4727** | 7 | 2 | **[Breaking Change]** AgentScope 1.x → 2.0 升级，涉及 API 和运行时架构大改 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/4727) |

### 背后的用户诉求
1. **学习循环** (#5017)：用户期待 Agent 具备自我完善能力，自动优化技能，对标业界先进（Hermes、小龙虾等）
2. **模型可靠性** (#5003)：阿里模型在某些场景下可能超时，需要更好的错误处理和重试机制
3. **架构升级** (#4727)：AgentScope 2.0 带来新机遇，但迁移工作量大，社区关注升级时间表

---

## 🐛 Bug 与稳定性

### 严重程度分级

#### 🔴 **P0 - 关键（已有 Fix PR）**

| Bug | 报告日期 | 现象 | Fix 状态 | PR |
|-----|---------|------|---------|-----|
| Windows 会话文件路径溢出 | 2026-06-06 | 会话文件名重复拼接，Windows 路径超限 (MAX_PATH 260) | ✅ 已合并 | [#5036](https://github.com/agentscope-ai/QwenPaw/pull/5036) |
| /compact 命令忽略模型上下文长度 | 2026-06-03 | MiniMax M3（512K）配置后仍使用 128K 默认值 | ✅ 已合并 | [#5021](https://github.com/agentscope-ai/QwenPaw/pull/5021) |
| OneBot 监听端口未释放 | 2026-06-03 | 热更新时旧服务器端口占用，新实例绑定失败（OSError: [Errno 98] address already in use） | ⏳ 待响应 | [#4926](https://github.com/agentscope-ai/QwenPaw/issues/4926) |

#### 🟠 **P1 - 高优（部分有 Fix）**

| Bug | 报告日期 | 现象 | Fix 状态 | 相关 Issue |
|-----|---------|------|---------|-----------|
| 本地部署模型无响应 | 2026-06-06 | 千问 3.6-27B（vLLM）在 1.1.9/1.1.10 无法回复，旧版本正常 | ⏳ 调查中 | [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) |
| 前端流式输出导致客户端卡顿 | 2026-05-29 | 长内容流式输出时，本地浏览器卡顿至鼠标无法拖动 | ⏳ 调查中 | [#4792](https://github.com/agentscope-ai/QwenPaw/issues/4792) |
| 思考内容显示问题 | 2026-06-04~06-08 | DeepSeek、KimiCode API 的 reasoning/thinking 内容无法展开显示 | ⏳ 调查中 | [#4962](https://github.com/agentscope-ai/QwenPaw/issues/4962), [#5013](https://github.com/agentscope-ai/QwenPaw/issues/5013) |
| MCP 工具名包含点号导致 API 校验失败 | 2026-06-02~09 | 钉钉 PAT（`pat.batch_plan`）因名字包含 `.` 被 OpenAI/DeepSeek 拒绝 | ✅ 已修复 | [#4918](https://github.com/agentscope-ai/QwenPaw/issues/4918), [#5034](https://github.com/agentscope-ai/QwenPaw/issues/5034), [#5045](https://github.com/agentscope-ai/QwenPaw/issues/5045) |

#### 🟡 **P2 - 中优（产品体验）**

| Bug | 报告日期 | 现象 | Fix 状态 |
|-----|---------|------|---------|
| Windows Desktop 前端加载不流畅 | 2026-06-08 | 任务执行时会话切换卡顿，CPU 激增 | ⏳ 调查中 |
| Tauri 桌面版外链无法打开 & 文件下载被阻止 | 2026-06-09 | GitHub 链接、文档菜单无反应；导出/下载附件被静默忽略 | ⏳ 待处理 |
| Windows 打开非 C 盘目录失败 | 2026-06-09 | Code-Open Directory 只能访问 C 盘 | ⏳ 待处理 |
| 钉钉 AI Card 空内容仍发送 | 2026-06-09 | Agent 输出为空字符串时，仍发送"处理中..."卡片 | ⏳ 待处理 |

### 新兴问题
- **多回复问题** (#5030)：开启主动模式后，微信频道对一个问题回复两次（内容相似但不同）
- **工具调用合并问题** (#5039)：OpenAI 兼容流解析器中，多个思考块的工具调用互相覆盖

---

## 💡 功能请求与路线图信号

### 用户呼声最高的新功能

| 优先级 | 功能需求 | 反应数 | 对标

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [Big Model Radar](https://github.com/hehongtao88/big_model_radar) 自动生成。*