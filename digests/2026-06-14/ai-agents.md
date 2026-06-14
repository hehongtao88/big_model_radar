# OpenClaw 生态日报 2026-06-14

> Issues: 500 | PRs: 500 | 覆盖项目: 12 个 | 生成时间: 2026-06-14 03:47 UTC

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
**日期：2026-06-14** | **数据周期：过去24小时**

---

## 📊 今日速览

OpenClaw 项目今日活跃度**极高**，24小时内处理 **500 条 Issues**（新开/活跃 405 条）和 **500 条 PR**（待合并 293 条），发布 **2 个新版本**。项目正处于密集迭代阶段，聚焦于**频道交付稳定性**（Telegram/WhatsApp 富文本、Feishu 线程路由）和**网关内存泄漏**等 P0/P1 级生产问题。社区反馈集中在**会话状态管理**、**消息丢失**和**安全隔离**三大痛点。

---

## 🚀 版本发布

### **v2026.6.8-beta.1** 与 **v2026.6.7-beta.1**

#### 核心改进

| 版本 | 主要特性 | 影响范围 |
|------|--------|--------|
| **2026.6.8** | • Telegram 富文本支持（表格、列表、可展开引用块）<br>• WhatsApp 频道交付增强<br>• CLI 后端交付改进 | 频道交付、用户体验 |
| **2026.6.7** | • Slack/Telegram 同频道转录持久化<br>• 顶层 `image` 消息工具媒体附件<br>• 可展开 Telegram 引用块<br>• 分页操作结果 | 消息交付、媒体处理 |

#### 破坏性变更
- **无明确标注**，但涉及消息工具 schema 变更（见 #43015），建议升级前测试自定义消息模板

#### 迁移注意
- Telegram 用户应验证富文本渲染（特别是 `<think>` 等角括号标签，见 #49104）
- WhatsApp 用户检查媒体边界处理

---

## 🔧 项目进展

### 今日合并/关闭的关键 PR

| PR | 状态 | 内容 | 影响 |
|----|------|------|------|
| **#92850** | ✅ CLOSED | 修复 memory-core 重索引后 `__meta` 未写入 | 内存搜索可用性 |
| **#92855** | ✅ CLOSED | 修复 iOS Safari 聊天视口处理 | 移动端 UX |
| **#92854** | ✅ CLOSED | 拒绝 slug 生成器错误负载 | 内存文件名稳定性 |
| **#92853** | ✅ CLOSED | ACP 服务器接受 MCP 日期格式 protocolVersion | 工具集成兼容性 |
| **#63644** | ✅ CLOSED | iPhone Safari 聊天布局和输入缩放修复 | 移动端布局 |

### 待合并的高优先级 PR

| PR | 优先级 | 内容 | 风险等级 |
|----|--------|------|--------|
| **#92857** | P1 | 修复 OpenAI Responses API 加密推理历史重放 | 🟡 中 |
| **#92852** | P2 | 配置监视器 inotify 耗尽时降级为轮询 | 🟡 中 |
| **#92775** | P2 | 启动时预热上下文窗口缓存，修复首次 /status | 🟡 中 |
| **#92824** | P2 | 修复 OpenAI OAuth 媒体路由 | 🟡 中 |
| **#92782** | P2 | 修复 Qwen 视觉模型 DashScope 400 错误 | 🟡 中 |

**项目向前推进**：今日共 **7 个 PR 合并/关闭**，主要聚焦**移动端 UX**、**内存搜索稳定性**和**API 兼容性**。待合并队列中 **293 条 PR** 显示项目开发节奏快速，但合并速度可能跟不上提交速度。

---

## 💬 社区热点

### 评论最多的 Issues（Top 5）

| Issue | 评论数 | 标签 | 核心诉求 |
|-------|--------|------|--------|
| **#48183** | 19 | P2, 内存泄漏 | [Feishu 监视器状态清理不完整](https://github.com/openclaw/openclaw/issues/48183) — httpServers Map 未正确释放 |
| **#44925** | 19 | P1, 消息丢失 | [子代理完成结果无声丢失](https://github.com/openclaw/openclaw/issues/44925) — 无重试、无通知、超时无自动重启 |
| **#48788** | 18 | P2, 数据丢失 | [多编码 Content-Disposition 处理](https://github.com/openclaw/openclaw/issues/48788) — Feishu 中文文件名编码问题 |
| **#45740** | 13 | P2, 安全 | [gh-issues 技能注入不受信任的 issue body](https://github.com/openclaw/openclaw/issues/45740) — 提示注入漏洞 |
| **#90991** | 13 | P1, 系统过载 | [Cron 触发器污染全局运行时状态](https://github.com/openclaw/openclaw/issues/90991) — 已关闭，但反映调度隔离问题 |

### 反应最多的 Issues（Top 3）

| Issue | 👍 数 | 标签 | 意义 |
|-------|-------|------|------|
| **#45608** | 4 | P2, 功能请求 | [重置前内存刷新](https://github.com/openclaw/openclaw/issues/45608) — 用户强烈支持 `/new` 时的内存保留 |
| **#42840** | 6 | P2, 功能请求 | [Control UI 支持 MathJax/LaTeX](https://github.com/openclaw/openclaw/issues/42840) — 科学计算用户需求 |
| **#90093** | 2 | 无标签 | [OpenAI ChatGPT Responses 加密推理重放失败](https://github.com/openclaw/openclaw/issues/90093) — 已有 fix PR #92857 |

### 背后的诉求分析

1. **消息可靠性危机**：#44925、#48183 反映子代理编排、Feishu 监视器等关键路径存在**无声失败**，用户无法感知任务丢失
2. **编码/国际化**：#48788 暴露多语言文件名处理的架构缺陷，需要集中式编码工具
3. **安全隔离**：#45740 提示注入漏洞表明技能集成缺乏输入清理，威胁子代理安全
4. **用户体验**：#42840 的 6 个赞显示科学计算社区对 LaTeX 渲染的迫切需求

---

## 🐛 Bug 与稳定性

### P0/P1 级生产问题（按严重程度）

| Issue | 优先级 | 症状 | 状态 | Fix PR |
|-------|--------|------|------|--------|
| **#91588** | P0 | 网关内存泄漏：RSS 350MB → 15.5GB，OOM 崩溃 | 🔴 OPEN | ❌ 无 |
| **#44925** | P1 | 子代理完成结果无声丢失，无重试 | 🔴 OPEN | ❌ 无 |
| **#48003** | P1 | Steer 模式不在主会话中注入消息 | 🔴 OPEN | ❌ 无 |
| **#43367** | P1 | 多代理编排不稳定：并发覆写、会话锁失败 | 🔴 OPEN | ❌ 无 |
| **#40001** | P1 | Write 工具缺少追加模式，孤立 cron 会话覆写共享文件 | 🔴 OPEN | ❌ 无 |
| **#44905** | P1 | Discord 泄露内部工具调用痕迹到频道 | 🔴 OPEN | ❌ 无 |
| **#90093** | P1 | OpenAI ChatGPT Responses 加密推理重放失败 | 🔴 OPEN | ✅ #92857 |
| **#85251** | P1 | Codex app-server 发出 turn/started 后沉默 | 🔴 OPEN | ❌ 无 |
| **#86996** | P1 | Active Memory + Codex 导致长延迟、超时、启动中止 | 🔴 OPEN | ❌ 无 |

### P2 级回归与行为问题（样本）

| Issue | 症状 | 根本原因 | 状态 |
|-------|------|--------|------|
| **#44993** | Heartbeat/Cron 时间戳陈旧 | 时间未在运行间刷新 | 🔴 OPEN |
| **#45765** | OPENCLAW_HOME 产生嵌套目录 | 路径处理逻辑错误 | 🔴 OPEN |
| **#41744** | Feishu 读取图像工具丢失媒体 | 最终负载前媒体未保留 | 🔴 OPEN |
| **#48573** | 嵌入式运行会话泄漏 | 子代理状态未清理 | ✅ CLOSED |

### 稳定性评估

- **网关层**：**严重** — #91588 内存泄漏是生产杀手，影响长期运行部署
- **消息交付**：**严重** — 多个 P1 问题导致消息无声丢失（#44925、#48003、#44905）
- **会话管理**：**严重** — 并发覆写、锁超时、子代理泄漏（#43367、#86538、#48573）
- **频道适配器**：**中等** — Feishu/Discord 特定问题，但影响特定用户群体

---

## ✨ 功能请求与路线图信号

### 用户强烈支持的功能（👍 ≥ 2）

| Issue | 👍 | 内容 | 可能性 |
|-------|----|----|--------|
| **#42840** | 6 | Control UI MathJax/LaTeX 支持 | 🟢 高（UI 增强，无后端改动） |
| **#45608** | 4 | `/new` 前内存刷新 | 🟢 高（已有 compaction 机制可复用） |
| **#45758** | 2 | YAML 配置格式支持 | 🟡 中（需要配置解析器扩展） |
| **#40540** | 2 | Windows `openclaw update` EBUSY 修复 | 🟢 高（已有 #81443 相关工作） |

### 架构级功能提案

| Issue | 类型 | 内容 | 复杂度 |
|-------|------|------|--------|
| **#48874** | RFC | 多会话架构：共享 LLM + 隔离会话 + 公共知识库 | 🔴 极高 |
| **#42475** | Feature | 网关级每代理成本预算强制 | 🟡 中 |
| **#7707** | Feature | 按来源标记内存信任级别 | 🟡 中 |
| **#39979** | Feature | 路径作用域 RWX 权限（替代二进制白名单） | 🟡 中 |

### 路线图信号

- **短期（2-4 周）**：MathJax 支持、内存刷新、Windows 更新修复
- **中期（1-2 月）**：多编码处理、权限系统重构、成本预算
- **长期（3+ 月）**：多会话架构、内存信任标记、自然语言规则学习

---

## 👥 用户反馈摘要

### 真实用户痛点（按频率）

#### 1. **消息可靠性** — 最高频
- **场景**：子代理编排、Feishu 监视器、Discord 频道
- **问题**：结果无声丢失，无重试机制，用户无法感知失败
- **引用**：#44925（19 评论）、#48183（19 评论）、#44905（10 评论）
- **用户声音**：*"Subagent task orchestration has multiple failure modes where results are silently lost"*

#### 2. **会话状态混乱** — 高频
- **场景**：多代理并发、cron 隔离、子代理生命周期
- **问题**：并发覆写配置、会话锁超时、僵尸代理持久化
- **引用**：#43367（10 评论）、#47975（9 评论）、#48573（12 评论）
- **用户声音**：*"Multi-agent orchestration is unstable: concurrent agents add/config overwrites, session-lock failures"*

#### 3. **国际化与编码** — 中频
- **场景**：Feishu 中文文件名、多语言内容
- **问题**：UTF-8 误读为 Latin-1，需要集中式编码工具
- **引用**：#48788（18 评论）
- **用户声音**：*"A proper architectural solution should handle multiple encodings (Shift-JIS, EUC-KR, GB18030, etc.)"*

#### 4. **安全隔离** — 中频
- **场景**：技能集成、子代理提示注入
- **问题**：不受信任的 GitHub issue body 直接注入提

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向分析报告
**日期：2026-06-14** | **覆盖项目：11 个核心开源项目**

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**快速迭代与功能完善的关键阶段**。从数据看，核心项目日均处理 **50+ 条 Issue/PR**，呈现"多点突破、各具特色"的发展态势：**OpenClaw 聚焦频道交付稳定性与会话管理**，**NanoBot/Zeroclaw 强化内存系统与多代理编排**，**IronClaw 完善附件端到端流程**，**CoPaw 驱动国际化与社区贡献**。整体而言，生态已从"功能堆砌"转向"系统可靠性"和"用户体验"，国际化需求（越南语、中文编码）和企业级部署（容器化、权限隔离）成为新的增长点。

---

## 2. 各项目活跃度对比

| 项目 | 24h Issues | 24h PRs | 待合并 PR | 新版本 | 健康度评分 | 活跃度等级 |
|------|-----------|---------|----------|--------|-----------|----------|
| **OpenClaw** | 405 | 500 | 293 | ✅ 2 个 | ⭐⭐⭐⭐ | 🔴 极高 |
| **Zeroclaw** | 26 | 50 | 45 | ❌ | ⭐⭐⭐⭐ | 🔴 极高 |
| **NanoBot** | 2 | 23 | 13 | ❌ | ⭐⭐⭐⭐ | 🟠 高 |
| **IronClaw** | 2 | 24 | 17 | ❌ | ⭐⭐⭐⭐ | 🟠 高 |
| **PicoClaw** | 1 | 7 | 3 | ✅ nightly | ⭐⭐⭐⭐ | 🟡 中高 |
| **NanoClaw** | 1 | 6 | 2 | ❌ | ⭐⭐⭐⭐ | 🟡 中高 |
| **Moltis** | 1 | 3 | 3 | ❌ | ⭐⭐⭐⭐ | 🟡 中 |
| **CoPaw** | 8 | 8 | 7 | ❌ | ⭐⭐⭐⭐ | 🟡 中 |
| **LobsterAI** | 4 | 5 | 3 | ❌ | ⭐⭐⭐ | 🟡 中 |
| **TinyClaw** | 0 | 0 | 0 | ❌ | ⭐⭐ | ⚪ 无活动 |
| **ZeptoClaw** | 0 | 0 | 0 | ❌ | ⭐⭐ | ⚪ 无活动 |

**关键观察**：
- **第一梯队**（OpenClaw、Zeroclaw）：日均 400+ 更新，处于密集迭代期，问题驱动修复机制高效
- **第二梯队**（NanoBot、IronClaw、PicoClaw）：日均 20-30 更新，功能完善与稳定性并行
- **第三梯队**（NanoClaw、Moltis、CoPaw、LobsterAI）：日均 5-10 更新，稳定维护阶段
- **无活动项目**（TinyClaw、ZeptoClaw）：可能处于孵化或维护暂停状态

---

## 3. OpenClaw 在生态中的定位

### 3.1 技术路线对比

| 维度 | OpenClaw | Zeroclaw | NanoBot | IronClaw |
|------|----------|----------|---------|----------|
| **核心定位** | 频道交付 + 会话管理 | 多代理编排 + 梦幻模式 | 轻量级 Agent + WebUI | 附件处理 + Slack 集成 |
| **会话架构** | 单会话 + 子代理 | 多会话共享 + 隔离 | 单会话 + 内存压缩 | 单会话 + 附件引用 |
| **内存系统** | 活跃内存 + 搜索 | 梦幻模式（周期巩固） | 空闲压缩 + 总结 | 附件转录持久化 |
| **多代理支持** | 子代理编排 | 原生多代理 + 委托 | 子代理预设 | 运行时上下文共享 |
| **频道适配** | Telegram/WhatsApp/Feishu/Discord | QQ/DingTalk/WeChat | 内置 WebUI | Slack 原生集成 |
| **部署模式** | 网关 + CLI | 网关 + Desktop | 网关 + WebUI | 网关 + MCP |
| **代码成熟度** | 🔴 高迭代（500 PR/天） | 🟠 快速迭代（50 PR/天） | 🟡 稳定迭代（23 PR/天） | 🟡 稳定迭代（24 PR/天） |

### 3.2 优势与差异

**OpenClaw 的核心优势**：
1. **频道交付完整性**：支持 4+ 主流频道（Telegram/WhatsApp/Feishu/Discord），富文本、媒体、线程路由等细节完善
2. **会话状态管理**：内存搜索、活跃内存、消息持久化等机制成熟，但存在并发覆写、锁超时等 P1 问题
3. **社区规模**：日均 500 条 PR，维护者响应快速，但问题积压（293 条待合并 PR）

**与 Zeroclaw 的差异**：
- Zeroclaw 强调**多代理编排与梦幻模式**（周期性内存巩固），适合长期对话和知识积累
- OpenClaw 强调**频道交付与会话隔离**，适合多渠道、多用户场景
- Zeroclaw 的多数据库后端支持（PostgreSQL/Oracle）面向企业级部署，OpenClaw 仍以单机为主

**与 NanoBot 的差异**：
- NanoBot 更轻量级，WebUI 自动化管理完善，TUI 交互现代化
- OpenClaw 功能更全面但复杂度更高，学习曲线陡峭

**与 IronClaw 的差异**：
- IronClaw 专注**附件端到端流程**（摄入→存储→提取→模型可见），Slack 集成深度高
- OpenClaw 附件支持较弱，但频道多样性更强

### 3.3 社区规模对比

| 指标 | OpenClaw | Zeroclaw | NanoBot | IronClaw |
|------|----------|----------|---------|----------|
| 24h Issue 评论数 | 19-19 条（Top 2） | 18 条（Top 1） | 15 条（#193） | 无统计 |
| 用户反馈集中度 | 消息可靠性、会话管理 | 梦幻模式、Docker 部署 | 本地推理、自动化 | Slack 重审批、附件可见 |
| 首次贡献者活跃度 | 低（维护者主导） | 低（维护者主导） | 中（#4098 等） | 中（@henrypark133 等） |

**结论**：OpenClaw 社区规模最大但维护者主导，Zeroclaw 用户需求更聚焦，NanoBot/IronClaw 首次贡献者更活跃。

---

## 4. 共同关注的技术方向

### 4.1 消息可靠性与会话管理

| 项目 | 具体诉求 | 严重程度 | 状态 |
|------|---------|--------|------|
| **OpenClaw** | 子代理完成结果无声丢失、Feishu 监视器状态清理不完整 | 🔴 P1 | 无 fix PR |
| **Zeroclaw** | ask_user 工具即时失败、Canvas 存储回归 | 🔴 P1 | 有 fix PR |
| **IronClaw** | Slack 重新审批循环、忙碌线程无反馈 | 🔴 P1 | 有 fix PR (#4839) |
| **NanoBot** | 会话历史压缩逻辑错误 | 🟡 P2 | 已修复 (#4326) |

**共同根因**：多代理编排、频道适配、会话隔离等复杂场景下的**状态同步与错误恢复机制不完善**。

**行业启示**：AI 智能体框架需要内置**可观测性与自动重试机制**，而非依赖上层应用处理。

---

### 4.2 国际化与编码支持

| 项目 | 具体诉求 | 涉及范围 |
|------|---------|--------|
| **OpenClaw** | Feishu 中文文件名编码（UTF-8 vs Latin-1）、多语言内容处理 | #48788 |
| **Zeroclaw** | QQ/DingTalk/WeChat 流式卡片、llama.cpp 模型路由 | #7531, #7539 |
| **CoPaw** | 越南语界面、Zalo Bot 频道、Kimi Coding 接入 | #5169, #5168, #5156 |
| **PicoClaw** | 多语言文件名处理 | #7521 |

**共同需求**：**集中式编码工具库** + **多语言 UI 框架** + **区域化 LLM 提供商集成**。

**行业启示**：东南亚市场（越南、印尼）正成为新增长点，项目应优先支持越南语、泰语等。

---

### 4.3 多代理编排与权限隔离

| 项目 | 具体诉求 | 状态 |
|------|---------|------|
| **OpenClaw** | 多代理并发覆写、会话锁失败、子代理泄漏 | 🔴 P1，无 fix |
| **Zeroclaw** | 按代理配置委托花名册、多数据库后端 | 🟠 有 PR (#7590, #6893) |
| **NanoClaw** | 提供商能力声明、持久化内存支持 | ✅ 已合并 (#2746, #2745) |
| **IronClaw** | 运行时上下文增强、出站交付目标指导 | 🟠 有 PR (#4836, #4780) |

**共同需求**：**细粒度权限控制** + **代理间通信隔离** + **状态持久化与恢复**。

**行业启示**：多代理系统的关键是**隔离与协调的平衡**，需要明确的能力声明框架。

---

### 4.4 内存系统与上下文管理

| 项目 | 具体诉求 | 技术方向 |
|------|---------|--------|
| **OpenClaw** | 内存搜索稳定性、消息丢失 | 活跃内存 + 搜索索引 |
| **Zeroclaw** | 梦幻模式（周期巩固）、内存反思学习 | 周期性压缩 + 反思引擎 |
| **NanoBot** | 会话历史压缩、空闲压缩总结 | 增量压缩 + 总结 |
| **CoPaw** | 上下文压缩导致数据丢失 | 容错压缩 |

**共同需求**：**可靠的上下文压缩算法** + **防丢失机制** + **反思学习能力**。

**行业启示**：长对话场景下，内存管理是**质量与成本的关键权衡点**，需要更智能的压缩策略。

---

### 4.5 容器化部署与企业级支持

| 项目 | 具体诉求 | 状态 |
|------|---------|------|
| **Zeroclaw** | Docker 文档完善、Rootless 容器配置 | 🟠 有 PR (#6760) |
| **NanoClaw** | 容器 SIGKILL 后日志恢复、Docker Desktop 兼容性 | 🟠 有 PR (#2750, #2732) |
| **Moltis** | Docker 部署路径冲突 | ✅ 有 fix PR (#1122) |
| **CoPaw** | Tauri 启动性能优化 | 🔴 无 fix，用户反馈严重 |

**共同需求**：**可靠的容器生命周期管理** + **跨平台兼容性** + **启动性能优化**。

**行业启示**：云原生部署已成为**企业用户的基本诉求**，项目应优先投入容器化支持。

---

## 5. 差异化定位分析

### 5.1 功能侧重维度

```
┌─────────────────────────────────────────────────────────────┐
│                    功能侧重矩阵                              │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  频道交付完整性 ↑                                             │
│  │                                                            │
│  │  OpenClaw ★★★★★                                          │
│  │  Zeroclaw ★★★★☆                                          │
│  │  IronClaw ★★★★☆                                          │
│  │  NanoBot

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报
**日期：2026-06-14** | **项目：github.com/HKUDS/nanobot**

---

## 📊 今日速览

NanoBot 项目今日保持**高度活跃**的开发节奏，24小时内处理 23 条 Issues/PRs（新增 2 个 Issue，合并/关闭 5 个 PR，待合并 13 个）。项目聚焦于**稳定性修复**（环境变量解析、MCP 服务器崩溃、Anthropic API 兼容性）和**功能完善**（WebUI 自动化管理、TUI 交互界面、子代理模型预设），同时推进**架构优化**（配置循环依赖解耦、会话历史压缩改进）。整体呈现**功能迭代与质量修复并行**的健康状态。

---

## 🔄 项目进展

### 已合并/关闭的关键 PR（5 条）

| PR | 标题 | 影响范围 |
|---|---|---|
| **#4326** | [fix(memory): 空闲压缩时使用完整会话尾部进行总结](https://github.com/HKUDS/nanobot/pull/4326) | 修复会话历史压缩逻辑，确保最后 8 条消息的纠正信息被纳入总结范围，解决 #4264 |
| **#4327** | [Fix WebUI 启动阻塞问题](https://github.com/HKUDS/nanobot/pull/4327) | 将慢速 HTTP 处理器移出网关事件循环，优化 WebUI 启动性能 |
| **#4314** | [Break tool config schema import cycle](https://github.com/HKUDS/nanobot/pull/4314) | 架构重构：将共享 Pydantic 配置提取到独立模块，消除循环依赖 |
| **#4313** | [feat(settings): WebUI/config.json 设置对等性](https://github.com/HKUDS/nanobot/pull/4313) | 新增温度、工具限制、梦想、频道、内存字段的写入端点，扩展 WebUI 设置覆盖范围 |
| **#4098** | [Fix exec workspace symlink 防护与路径优先级](https://github.com/HKUDS/nanobot/pull/4098) | 安全修复：阻止相对符号链接逃逸工作区，修复 #4083 |

**进展评估**：项目在**内存管理、性能优化、架构清理、安全加固**四个维度同步推进，展现成熟的工程实践。

---

## 🔥 社区热点

### 最活跃讨论

| Issue/PR | 标题 | 活跃度 | 核心诉求 |
|---|---|---|---|
| **#193** | [Ollama API 支持？](https://github.com/HKUDS/nanobot/issues/193) | 15 条评论 | 用户期望支持 Ollama 本地 LLM 推理服务，目前仅支持 vLLM |
| **#4329** | [Nanobot TUI](https://github.com/HKUDS/nanobot/pull/4329) | 新增大型功能 | 为 CLI 代理新增内联交互式 TUI，支持斜杠命令、多模态输入（图片+音频转写） |
| **#4330** | [feat(webui): 自动化管理视图](https://github.com/HKUDS/nanobot/pull/4330) | 新增 WebUI 功能 | 列表、过滤、运行、暂停/恢复、删除用户自动化，完善自动化工作流管理 |

**背后诉求分析**：
- **本地推理生态**：用户希望支持更多开源 LLM 推理框架（Ollama），降低云 API 依赖
- **交互体验升级**：CLI 用户期望更现代的 TUI 界面，而非传统 Rich-Live 循环
- **自动化工作流**：WebUI 用户需要完整的自动化管理能力（CRUD + 执行控制）

---

## 🐛 Bug 与稳定性

### 严重程度排序

#### 🔴 **P0 - 阻断性崩溃**

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| **#4322** | [NameError: 'session_key' 未定义](https://github.com/HKUDS/nanobot/issues/4322) | 🔴 OPEN | 待修复 |
| **#4303** | [MCP 服务器关闭时 GC 崩溃](https://github.com/HKUDS/nanobot/pull/4303) | 🟡 OPEN | 自身为 fix PR |

**根因**：#4322 由合并 `origin/main` 到 `fix/prompt-caching` 分支引入，`_build_memory_context` 方法提取时遗漏 `session_key` 变量定义。

#### 🟠 **P1 - 功能性故障**

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| **#4333** | [Anthropic provider 向 opus-4-8/Fable 发送已弃用的 `temperature` 参数](https://github.com/HKUDS/nanobot/issues/4333) | 🔴 OPEN | **#4334** ✅ |
| **#4264** | [idleCompact 应使用完整会话历史而非删除最后 8 条消息的历史](https://github.com/HKUDS/nanobot/issues/4264) | 🟢 CLOSED | **#4326** ✅ |

**#4333 详情**：Anthropic API 仅对 `opus-4-7` 豁免 `temperature` 参数，新模型 `opus-4-8` 和 `Fable` 仍会收到该参数，导致 400 错误。Fix PR #4334 已提交，扩大 `omit_temperature` 检查范围。

#### 🟡 **P2 - 配置/环保问题**

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| **#4083** | [pathAppend 不遵循可执行文件查找优先级](https://github.com/HKUDS/nanobot/issues/4083) | 🟢 CLOSED | **#4098** ✅ |

---

## 💡 功能请求与路线图信号

### 已有 PR 支持的新功能（预期下一版本）

| 功能 | PR | 状态 | 预期影响 |
|---|---|---|---|
| **TUI 交互界面** | [#4329](https://github.com/HKUDS/nanobot/pull/4329) | 🟡 OPEN | 提升 CLI 用户体验，支持斜杠命令、多模态输入 |
| **WebUI 自动化管理** | [#4330](https://github.com/HKUDS/nanobot/pull/4330) | 🟡 OPEN | 完善自动化工作流，支持 CRUD + 执行控制 |
| **子代理模型预设** | [#4291](https://github.com/HKUDS/nanobot/pull/4291) | 🟡 OPEN | 允许子代理使用不同模型，灵活的多模型编排 |
| **文件工具开关** | [#4138](https://github.com/HKUDS/nanobot/pull/4138) | 🟡 OPEN | 与 `exec`/`web` 工具组对等，支持禁用内置文件系统工具 |
| **反向代理/子路径支持** | [#4328](https://github.com/HKUDS/nanobot/pull/4328) | 🟡 OPEN | WebUI 可在 `/nanobot/` 等子路径下正确运行 |

### 用户期望但未有 PR 的功能

- **Ollama API 支持** (#193)：15 条评论，用户强烈期望支持本地推理框架

---

## 👥 用户反馈摘要

### 核心痛点

1. **本地推理生态缺失**（#193）
   - 用户期望支持 Ollama，降低云 API 成本和隐私风险
   - 当前仅支持 vLLM，生态不够开放

2. **会话历史管理不当**（#4264）
   - 用户在纠正模型错误后，最终正确结果未被纳入压缩总结
   - 导致 history.jsonl 记录错误的结论

3. **API 兼容性脆弱**（#4333）
   - Anthropic 新模型参数变化，项目跟进不及时
   - 用户升级模型后直接遇到 400 错误

4. **部署灵活性不足**（#4328）
   - WebUI 假设部署在根路径，反向代理场景下资源加载失败
   - 企业用户无法在子路径下部署

### 满意度信号

- 自动化管理、TUI 界面、多模型编排等新功能获得积极响应
- 项目对 bug 修复的响应速度快（#4333 当日修复）

---

## ⏳ 待处理积压

### 长期未响应的重要 Issue

| Issue | 创建时间 | 天数 | 状态 | 优先级 |
|---|---|---|---|---|
| **#193** | 2026-02-06 | **128 天** | 🔴 CLOSED（无解决方案） | 🟠 P1 |
| **#4083** | 2026-05-29 | **16 天** | 🟢 CLOSED（已修复） | ✅ |

### 待合并 PR 堆积

**13 个待合并 PR**，其中关键项：

| PR | 创建时间 | 天数 | 阻塞原因 |
|---|---|---|---|
| **#4329** (TUI) | 2026-06-13 | 1 天 | 大型功能，可能需要设计评审 |
| **#4330** (WebUI 自动化) | 2026-06-13 | 1 天 | 新 WebUI 功能，需要集成测试 |
| **#4291** (子代理预设) | 2026-06-11 | 3 天 | 多模型编排，需要文档更新 |
| **#4328** (反向代理支持) | 2026-06-13 | 1 天 | 部署场景修复，优先级应提高 |
| **#4303** (MCP GC 崩溃) | 2026-06-11 | 3 天 | 阻断性 bug，应优先合并 |

**建议**：
- 🔴 **立即处理**：#4303（MCP 崩溃）、#4322（session_key 错误）
- 🟠 **本周合并**：#4334（Anthropic 兼容性）、#4328（反向代理）
- 🟡 **评审中**：#4329、#4330、#4291（大型功能，需设计评审）

---

## 📈 项目健康度评分

| 维度 | 评分 | 备注 |
|---|---|---|
| **活跃度** | ⭐⭐⭐⭐⭐ | 24h 内 23 条更新，高频迭代 |
| **稳定性** | ⭐⭐⭐⭐ | 3 个 P0/P1 bug，但修复 PR 已就位 |
| **功能完善度** | ⭐⭐⭐⭐ | TUI、自动化、多模型编排等新功能完善 |
| **社区响应** | ⭐⭐⭐⭐ | 用户反馈及时，但 Ollama 需求长期未响应 |
| **代码质量** | ⭐⭐⭐⭐ | 架构优化（循环依赖解耦）、安全加固（symlink 防护） |

**总体评估**：项目处于**快速迭代期**，功能完善与质量修复并行，但需关注 MCP 崩溃、session_key 错误等阻断性 bug 的及时修复。

---

**报告生成时间**：2026-06-14 | **数据来源**：GitHub API | **下次更新**：2026-06-15

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目日报 | 2026-06-14

## 📊 今日速览

Zeroclaw 项目今日呈现极高活跃度：24 小时内新增/活跃 Issue 26 条，关闭 16 条，共计 42 条 Issue 更新；PR 方面待合并 45 条、已合并/关闭 5 条，合计 50 条。虽未发布新版本，但大量功能特性和缺陷修复正在并行推进。项目整体处于快速迭代阶段，维护团队响应积极，社区参与度高。

---

## 🔧 项目进展

### 重点合并方向（待合并 45 条 PR 中最关键的几条）

| PR | 类型 | 内容摘要 |
|---|---|---|
| [#7558](https://github.com/zeroclaw-labs/zeroclaw/pull/7558) | 基础设施 | 规范化安装器规格，消除9个交付面的特性漂移，单一真实来源策略 |
| [#7590](https://github.com/zeroclaw-labs/zeroclaw/pull/7590) | 功能 | **按代理配置委托花名册**，打破跨profile到达限制，支持不同风险配置的代理间委托 |
| [#6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893) | 基础设施 | **多数据库后端**（PostgreSQL/Oracle/MySQL/Db2），为多代理舰队支持会话状态共享 |
| [#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693) | 核心特性 | **梦幻模式**：周期性内存巩固引擎（5阶段：收集→反思→巩固→修剪→报告），本地优先 |
| [#7570](https://github.com/zeroclaw-labs/zeroclaw/pull/7570) | 可观测性 | OTel GenAI 跨度仪表化，运行时内存操作全覆盖（超大PR，需维护者关注） |

**进展信号**：基础设施稳定性、代理灵活性、企业级部署支持是当前优先级，这些 PR 合并后将显著提升项目成熟度。

---

## 🔥 社区热点

### 评论最多的讨论（反映用户关注度）

| Issue | 讨论焦点 | 评论数 | 状态 |
|---|---|---|---|
| [#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) | **梦幻模式**：空闲期内存巩固 & 反思学习 | 18 | 🟢 OPEN / Accepted |
| [#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) | RFC：统一三个代理引擎（RFC已执行，改为单一合并PR#7540） | 5 | 🔴 CLOSED |
| [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470) | Bug：安全模式下多项问题（Telegram重复保存、高推理成本） | 5 | 🔴 CLOSED / Stale |
| [#5570](https://github.com/zeroclaw-labs/zeroclaw/issues/5570) | 优化：SQLite向量搜索O(n)→ANN加速 | 5 | 🔴 CLOSED / Stale |
| [#6760](https://github.com/zeroclaw-labs/zeroclaw/issues/6760) | Feature：Docker文档更新（v0.7.5-debian实测） | 4 | 🟢 OPEN / Accepted |

**用户需求洞察**：高级用户关注内存系统升级（梦幻模式），部署用户需要Docker文档，性能优化（向量搜索）也有市场。

---

## 🐛 Bug 与稳定性

### 严重程度排序

#### 🔴 **P1 - Workflow Blocked**（需立即修复）

| Issue | 描述 | 影响范围 | Fix 状态 |
|---|---|---|---|
| [#7563](https://github.com/zeroclaw-labs/zeroclaw/issues/7563) | Canvas 存储回归（#6986 后 WS 会话 /canvas 页面空白） | 网关 WS/ACP | 🟡 In-Progress |
| [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | ask_user 工具即时失败："Channel closed before receiving response" | 网关仪表板 | ✅ Fix PR [#7588](https://github.com/zeroclaw-labs/zeroclaw/pull/7588) |
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | macOS 应用启动失败（权限检测&空白页，15.7.7） | Desktop/Tauri | 🔴 Blocked（需调查） |
| [#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523) | 仪表板无法访问（Web 前端构建缺失） | 网关 Web | 🟡 In-Progress |

#### 🟡 **P2 - Degraded Behavior**（影响体验）

| Issue | 描述 | Fix 状态 |
|---|---|---|
| [#7591](https://github.com/zeroclaw-labs/zeroclaw/issues/7591) | 快速启动中大写代理别名验证缺失（失败后丢失所有输入） | 🔴 New（未处理） |
| [#7378](https://github.com/zeroclaw-labs/zeroclaw/issues/7378) | Zerocode Cmd-C 复制被误认为退出信号 (macOS) | ✅ [#7378](https://github.com/zeroclaw-labs/zeroclaw/issues/7378) CLOSED |
| [#7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377) | Zerocode 深色主题继承不可读前景色（亮色终端） | ✅ CLOSED |

#### 🟢 **P3 - Minor Issues**

| Issue | 描述 |
|---|---|
| [#7509](https://github.com/zeroclaw-labs/zeroclaw/issues/7509) | 自测试在 Windows 主机上失败（ZIP 资产被拒） |

**稳定性评估**：网关/Web 前端存在聚焦问题（3个P1），macOS 构建有隐患，但修复 PR 已上线或在进行中。

---

## 💡 功能请求与路线图信号

### 高优先级特性（P2 Accepted）

| Issue | 需求 | 相关 PR | 预期影响 |
|---|---|---|---|
| [#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) | **梦幻模式**：周期性内存巩固 & 反思 | [#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693) | 高级用户留存，长期对话质量提升 |
| [#6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289) | 快速安装建议（提示缺失的 Skills/Plugins） | 无 | 降低新用户学习曲线 |
| [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) | RFC：原生动态库插件系统 | 无 | 插件生态成熟度 |
| [#7514](https://github.com/zeroclaw-labs/zeroclaw/issues/7514) | Delegate 工具支持跨风险配置 | [#7590](https://github.com/zeroclaw-labs/zeroclaw/pull/7590) | 多代理编排灵活性 |
| [#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531) | QQ/DingTalk/WeChat 流式卡片消息 | 无 | 中文市场用户体验 |
| [#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539) | llama.cpp 模型路由器 | 无 | 本地模型用户快速模型切换 |
| [#7521](https://github.com/zeroclaw-labs/zeroclaw/issues/7521) | file_read 字符编码检测（CP1251/Latin-1） | 无 | 国际化文件支持 |

**v0.8.1 方向**：企业级会话共享、内存系统升级、多语言渠道体验优化是关键。

---

## 👥 用户反馈摘要

### 真实痛点与使用场景

| 用户群体 | 反馈内容 | Issue |
|---|---|---|
| **Docker/K8s 部署者** | 官方 YAML 示例不完整或有缩进错误，需要可靠的 Rootless 容器配置 | [#6760](https://github.com/zeroclaw-labs/zeroclaw/issues/6760) |
| **macOS 用户** | 应用启动权限检测失败、空白页、窗口消失，严重影响桌面体验 | [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) |
| **本地模型爱好者** | GPT 5.4 + 高推理模式下 Telegram 消息重复保存；llama.cpp 缺少便捷的模型切换 | [#5470](https://github.com/zeroclaw-labs/zeroclaw/issues/5470), [#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539) |
| **中文市场用户** | WhatsApp/QQ/DingTalk 等需要流式卡片支持，减少等待焦虑 | [#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531), [#7518](https://github.com/zeroclaw-labs/zeroclaw/issues/7518) |
| **国际化用户** | 非 UTF-8 文件（Cyrillic/Latin-1/Shift-JIS）无法正确读取 | [#7521](https://github.com/zeroclaw-labs/zeroclaw/issues/7521) |
| **Web UI 用户** | 仪表板频繁崩溃（canvas 回归、ask_user 失败） | [#7563](https

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报
**日期**: 2026-06-14 | **数据周期**: 过去24小时

---

## 📊 今日速览

PicoClaw 项目保持高活跃度，过去24小时内合并/关闭 5 条 PR，新增 1 条 Issue，发布 nightly 构建版本。项目重点聚焦于**视觉模型路由修复**、**TTS 参数扩展**和**代码质量改进**，同时有新功能（远程 WebSocket 模式）正在审核中。整体呈现**稳定迭代、问题驱动修复**的健康开发节奏。

---

## 🚀 版本发布

**Nightly Build: v0.2.9-nightly.20260614.cf67dd38**
- **类型**: 自动化夜间构建（可能不稳定）
- **变更范围**: 相比 v0.2.9 的增量更新
- **完整日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **建议**: 用于测试新特性，生产环境建议等待正式版本

---

## ✅ 项目进展

**今日合并/关闭 PR 统计**: 5 条

| PR | 标题 | 影响范围 | 状态 |
|---|---|---|---|
| [#3119](https://github.com/sipeed/picoclaw/pull/3119) | fix(tts): support OpenRouter voice overrides and fallback | TTS 模块 | ✅ 已合并 |
| [#3117](https://github.com/sipeed/picoclaw/pull/3117) | fix(agent): route media turns to image models | Agent 核心逻辑 | ✅ 已合并 |
| [#3065](https://github.com/sipeed/picoclaw/pull/3065) | fix(seahorse): explicitly ignore Close() errors | 数据库层 | ✅ 已合并 |
| [#3066](https://github.com/sipeed/picoclaw/pull/3066) | fix: explicitly ignore Close() errors on temp file paths | 文件系统层 | ✅ 已合并 |
| [#2935](https://github.com/sipeed/picoclaw/pull/2935) | docs(i18n): add Traditional Chinese (zh-TW) locale | 文档国际化 | ✅ 已关闭 |

**核心进展**:
- **视觉能力修复**: #3117 解决了图像描述幻觉问题，确保媒体请求正确路由到支持视觉的模型
- **TTS 增强**: #3119 扩展 OpenRouter TTS 参数灵活性，支持模型级别的 voice/format 覆盖
- **代码质量**: #3065、#3066 消除 linter 警告，提升代码规范性

---

## 💬 社区热点

**最活跃讨论**:

1. **[#3012 - 进化模式下持续消耗 Token](https://github.com/sipeed/picoclaw/issues/3012)** 
   - 状态: 🔴 OPEN（8天未解决）
   - 评论: 3 条 | 创建: 2026-06-05 | 最后更新: 2026-06-13
   - **问题**: 启用 Evolution 功能时，系统每分钟持续消耗 Token，即使无实际请求
   - **环境**: PicoClaw v0.2.9 + MiniMax + FreeBSD
   - **严重程度**: 🔴 高（直接影响成本）

2. **[#3108 - 图像描述幻觉（已修复）](https://github.com/sipeed/picoclaw/issues/3108)**
   - 状态: ✅ CLOSED（2天内修复）
   - 创建: 2026-06-11 | 关闭: 2026-06-13
   - **问题**: 使用不支持视觉的模型（deepseek-v4-flash）时，图像描述与实际内容无关
   - **修复**: PR #3117 已合并，通过模型路由解决

---

## 🐛 Bug 与稳定性

| 优先级 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| 🔴 高 | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | Evolution 模式 Token 泄漏 | ⏳ 待修复 |
| 🟡 中 | [#3108](https://github.com/sipeed/picoclaw/issues/3108) | 图像描述幻觉 | ✅ [#3117](https://github.com/sipeed/picoclaw/pull/3117) 已修复 |

**稳定性评估**:
- 代码质量持续改进（linter 警告消除）
- 关键路径修复及时（图像模型路由问题 2 天内修复）
- **风险点**: Evolution 功能的 Token 消耗问题需要优先关注

---

## 🎯 功能请求与路线图信号

**进行中的新功能**:

1. **[#2964 - 图像输入压缩](https://github.com/sipeed/picoclaw/pull/2964)** (OPEN)
   - 添加可配置的多级图像压缩策略
   - 目的: 优化媒体处理，减少 API 成本
   - 状态: 待审核（创建于 2026-05-28，已 16 天）

2. **[#3118 - 远程 Pico WebSocket 模式](https://github.com/sipeed/picoclaw/pull/3118)** (OPEN)
   - 为 `picoclaw agent` 命令添加远程模式支持
   - 用途: 支持分布式部署、远程 Agent 调用
   - 状态: 待审核（创建于 2026-06-12，刚提交）

**路线图信号**:
- 视觉能力完善（图像压缩、模型路由）
- 部署灵活性提升（远程 WebSocket）
- 成本优化（TTS 参数灵活性、图像压缩）

---

## 👥 用户反馈摘要

**真实痛点**:

1. **成本控制** (#3012)
   - 用户痛点: Evolution 功能在启用后持续消耗 Token，即使系统空闲
   - 使用场景: 长期运行的 Agent 服务
   - 建议: 需要更精细的 Token 消耗控制机制

2. **多模态能力** (#3108)
   - 用户痛点: 模型选择不当导致图像处理失败（幻觉）
   - 使用场景: 跨模型的图像描述任务
   - 满意度: 快速修复提升了信任度

3. **部署灵活性** (#3118)
   - 用户需求: 支持远程 Agent 调用，而非仅本地模式
   - 使用场景: 微服务架构、分布式部署

---

## ⚠️ 待处理积压

| 优先级 | 项目 | 创建时间 | 未响应天数 | 建议 |
|---|---|---|---|---|
| 🔴 高 | [#3012](https://github.com/sipeed/picoclaw/issues/3012) | 2026-06-05 | 8 天 | **需要立即分配** - Token 泄漏影响用户成本 |
| 🟡 中 | [#2964](https://github.com/sipeed/picoclaw/pull/2964) | 2026-05-28 | 16 天 | **需要审核** - 图像压缩功能已就绪，建议合并或反馈 |
| 🟡 中 | [#3118](https://github.com/sipeed/picoclaw/pull/3118) | 2026-06-12 | 1 天 | **新提交** - 远程模式功能，需要审核 |

---

## 📈 项目健康度评分

| 维度 | 评分 | 说明 |
|---|---|---|
| **活跃度** | ⭐⭐⭐⭐⭐ | 24h 内 7 条 PR、2 条 Issue，持续迭代 |
| **响应速度** | ⭐⭐⭐⭐ | 关键 Bug 2 天内修复，但 #3012 待处理 |
| **代码质量** | ⭐⭐⭐⭐ | linter 警告消除，规范性提升 |
| **功能完善度** | ⭐⭐⭐⭐ | 视觉、TTS、部署等多维度优化 |
| **社区沟通** | ⭐⭐⭐ | 需要加强对长期 Issue 的反馈 |

**总体评价**: 项目处于**健康活跃期**，问题驱动修复机制有效，但需要关注 Evolution 功能的成本控制问题。

---

*报告生成时间: 2026-06-14 | 数据来源: GitHub API*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报
**日期：2026-06-14** | **项目：github.com/qwibitai/nanoclaw**

---

## 📊 今日速览

NanoClaw 项目今日保持**中等活跃度**，过去24小时内处理了6条 PR（4条已合并/关闭，2条待合并）和1条 Issue（已关闭）。核心开发团队聚焦于**稳定性加固**和**提供商能力扩展**，连续合并了5个功能性 PR，表明项目正在快速迭代核心架构。未发布新版本，但合并内容涉及关键的容器生命周期修复和 SDK 依赖升级。

---

## 🔧 项目进展

### 已合并/关闭的关键 PR（4条）

| PR | 作者 | 状态 | 核心内容 |
|---|---|---|---|
| [#2747](https://github.com/nanocoai/nanoclaw/pull/2747) | @omri-maya | ✅ CLOSED | **SDK 升级 2.2.1** — 集成凭证存根挂载 + 机器可检查的 pins，增强提供商凭证管理能力 |
| [#2746](https://github.com/nanocoai/nanoclaw/pull/2746) | @omri-maya | ✅ CLOSED | **Agent-surfaces 能力接缝** — 主机侧提供商能力注册表，支持按能力声明的提供商发现 |
| [#2745](https://github.com/nanocoai/nanoclaw/pull/2745) | @omri-maya | ✅ CLOSED | **持久化内存脚手架** — 为提供商添加可选的持久化内存支持（`usesMemoryScaffold` 能力） |
| [#2754](https://github.com/nanocoai/nanoclaw/pull/2754) | @omri-maya | ✅ CLOSED | **onExchangeComplete 钩子 + 斜杠命令中断** — 核心运行器扩展，支持交换完成事件和命令中断机制 |

**进展评估**：4条 PR 全部来自 @omri-maya，聚焦于**提供商生态系统强化**，包括内存管理、能力声明、事件钩子等核心扩展点。这些合并表明项目正在建立更灵活的提供商接口层。

### 待合并的重要 PR（2条）

| PR | 作者 | 优先级 | 核心内容 |
|---|---|---|---|
| [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) | @sturdy4days | 🔴 高 | **修复容器 SIGKILL 后的陈旧日志恢复** — 解决 #2516、#2640 两个相关故障模式，涉及 `outbound.db` 只读句柄的稳定性 |
| [#2732](https://github.com/nanocoai/nanoclaw/pull/2732) | @caburi00 | 🔴 高 | **健康审计加固** — 容器生命周期、Agent-runner 多项安全加固，包括 realpath 绑定挂载、并发容器限制、Docker Desktop drvfs 崩溃修复 |

**待合并分析**：两条 PR 均涉及**生产稳定性**，#2750 针对数据库日志恢复，#2732 针对容器生命周期和安全边界。建议优先合并。

---

## 🐛 Bug 与稳定性

### 已识别的关键问题（均有修复 PR）

| 问题 | 严重程度 | 症状 | 修复 PR | 状态 |
|---|---|---|---|---|
| **#2516** | 🔴 严重 | 容器 SIGKILL 后 `outbound.db` 日志陈旧，导致只读句柄故障 | [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) | ⏳ 待合并 |
| **#2640** | 🔴 严重 | 热日志轮询竞态条件，与 #2516 相关 | [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) | ⏳ 待合并 |
| **Docker Desktop drvfs 崩溃** | 🟠 中等 | 容器启动时 exit 127，与绑定挂载源路径解析相关 | [#2732](https://github.com/nanocoai/nanoclaw/pull/2732) | ⏳ 待合并 |
| **并发容器溢出** | 🟠 中等 | 未强制 `MAX_CONCURRENT_CONTAINERS` 限制，导致资源耗尽 | [#2732](https://github.com/nanocoai/nanoclaw/pull/2732) | ⏳ 待合并 |

**稳定性评估**：4个已识别的生产问题均有修复方案，但尚未合并。建议加快 #2750 和 #2732 的审查流程。

---

## 🎯 功能请求与路线图信号

### 近期功能扩展方向（基于已合并 PR）

1. **提供商能力声明框架** (#2746)
   - 支持提供商按能力自注册（如 `usesMemoryScaffold`）
   - 启用主机侧能力发现和路由

2. **持久化内存支持** (#2745)
   - 提供商可选的跨会话状态保留
   - 信号：用户需要有状态的提供商实例

3. **事件驱动的运行器扩展** (#2754)
   - `onExchangeComplete` 钩子支持交换完成事件
   - 斜杠命令中断机制
   - 信号：用户需要更细粒度的运行器生命周期控制

4. **凭证管理增强** (#2747)
   - SDK 2.2.1 集成凭证存根挂载
   - 机器可检查的 pins
   - 信号：安全凭证隔离需求上升

**路线图推断**：项目正在构建**模块化提供商生态**，重点是能力声明、状态管理和事件驱动架构。

---

## 💬 社区热点

### 今日讨论活跃度

| 项目 | 类型 | 热度 | 分析 |
|---|---|---|---|
| [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) | PR | 🔥 高 | 最新更新（2026-06-14），涉及两个关键 Issue 的修复，预期引发审查讨论 |
| [#2732](https://github.com/nanocoai/nanoclaw/pull/2732) | PR | 🔥 高 | 多层次安全加固，涉及容器生命周期和 Docker Desktop 兼容性，用户关注度高 |
| [#2755](https://github.com/nanocoai/nanoclaw/issues/2755) | Issue | ❄️ 低 | 误发 Issue，已关闭，无实质讨论 |

**社区信号**：核心维护者（@omri-maya、@sturdy4days、@caburi00）活跃度高，聚焦于稳定性和功能扩展。无用户投诉或争议性讨论。

---

## 📋 用户反馈摘要

### 隐含的用户痛点（基于 PR 内容推断）

| 痛点 | 来源 | 影响范围 |
|---|---|---|
| **容器崩溃后数据库不可用** | #2516、#2640 | 生产环境数据持久化 |
| **Docker Desktop 兼容性问题** | #2732 | 开发环境启动失败 |
| **提供商状态管理困难** | #2745 | 有状态应用集成 |
| **凭证隔离不足** | #2747 | 安全敏感场景 |
| **运行器生命周期不可控** | #2754 | 高级工作流定制 |

**用户满意度信号**：无负面反馈，问题均被主动识别和修复，表明项目对用户需求的响应能力强。

---

## ⏳ 待处理积压

### 关键待合并 PR（需加快审查）

| PR | 创建时间 | 待合并天数 | 优先级 | 建议 |
|---|---|---|---|---|
| [#2750](https://github.com/nanocoai/nanoclaw/pull/2750) | 2026-06-12 | 2 天 | 🔴 高 | 涉及两个生产 Bug，建议 24h 内合并 |
| [#2732](https://github.com/nanocoai/nanoclaw/pull/2732) | 2026-06-11 | 3 天 | 🔴 高 | 多项安全加固，建议优先审查 |

### 长期未响应的 Issue

- **无**：今日仅 1 条 Issue，已关闭；项目整体响应及时。

---

## 📈 项目健康度评分

| 维度 | 评分 | 备注 |
|---|---|---|
| **活跃度** | ⭐⭐⭐⭐ | 6 条 PR/天，核心团队持续迭代 |
| **稳定性** | ⭐⭐⭐ | 4 个已识别 Bug，修复方案就绪但未合并 |
| **功能完整性** | ⭐⭐⭐⭐ | 提供商生态快速扩展，能力框架成熟 |
| **社区响应** | ⭐⭐⭐⭐⭐ | 无积压 Issue，问题快速闭环 |
| **文档/通信** | ⭐⭐⭐ | PR 描述详细，但无发布说明 |

**总体评估**：**健康且高速发展**。项目正处于功能扩展期，稳定性修复已就绪，建议加快合并关键 PR 以确保生产环境可靠性。

---

**下一步建议**：
1. ✅ 优先合并 #2750 和 #2732（生产稳定性）
2. 📝 为下一版本准备发布说明（包含 SDK 升级、能力框架变更）
3. 📊 监控 #2750 合并后的 outbound.db 故障率

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报
**日期：2026-06-14** | **项目：nearai/ironclaw**

---

## 📊 今日速览

IronClaw 项目今日保持**高度活跃**的开发节奏，24小时内新增 2 条 Issue、24 条 PR 更新（17 条待合并），其中 7 条已合并/关闭。虽未发布新版本，但核心功能迭代密集，特别是围绕**附件处理端到端流程**和 **Slack 集成稳定性**的多个关键 PR 正在推进中。项目整体呈现"功能完善期"的特征，重点从新增功能转向系统可靠性和用户体验优化。

---

## 🔄 项目进展

### 已合并/关闭的关键 PR（过去24小时）

| PR | 状态 | 核心贡献 |
|---|---|---|
| [#4675](https://github.com/nearai/ironclaw/pull/4675) | ✅ 合并 | **重构：文本提取模块独立化** - 将 `document_extraction/extractors.rs` 的字节→文本转换逻辑提取为独立叶子 crate `ironclaw_extractors`，提升代码复用性和可维护性 |
| [#4672](https://github.com/nearai/ironclaw/pull/4672) | ✅ 合并 | **功能：WebChat v2 内联附件上传** - 完成端到端接入，用户可在 WebChat 中直接上传文件，字节通过文件系统权限落地到项目存储 |
| [#4670](https://github.com/nearai/ironclaw/pull/4670) | ✅ 合并 | **功能：入站附件字节→转录引用桥接** - 连接字节落地与转录 `AttachmentRef` 持久化，为后续模型可见性奠基 |
| [#4668](https://github.com/nearai/ironclaw/pull/4668) | ✅ 合并 | **功能：MountView 附件落地 crate** - Track 6 字节存储基础设施，支持模型访问附件内容 |
| [#4655](https://github.com/nearai/ironclaw/pull/4655) | ✅ 合并 | **功能：转录合约扩展** - Reborn 转录从纯文本扩展为支持附件引用，确保上传内容不丢失 |
| [#4242](https://github.com/nearai/ironclaw/pull/4242) | ✅ 合并 | **依赖更新：tar 0.4.45→0.4.46** - 安全补丁（修复 PAX 存档漏洞） |

**进展评估**：#4644 相关的附件功能栈（6 个 PR）已有 5 个合并，形成了从字节摄入→存储→转录持久化→模型可见性的完整链路。这是本周期最重要的功能交付。

---

## 🔥 社区热点

### 高活跃度 PR（待合并，核心功能）

| PR | 作者 | 规模 | 热度信号 | 核心诉求 |
|---|---|---|---|---|
| [#4839](https://github.com/nearai/ironclaw/pull/4839) | @henrypark133 | XL | 🔴 关键修复 | **Slack 重新审批循环修复** - 修复需要一次性审批+凭证的能力调用（如 Gmail OAuth）在每个恢复周期都要求新审批的问题。根因：未保留调用身份跨认证网关重新分发 |
| [#4838](https://github.com/nearai/ironclaw/pull/4838) | @henrypark133 | XL | 🔴 关键修复 | **忙碌线程显式网关反馈** - 替换延迟-排空方案，改为直接拒绝+显式通知，用户成为重试主体，提升交互透明度 |
| [#4836](https://github.com/nearai/ironclaw/pull/4836) | @henrypark133 | XL | 🟠 重要功能 | **运行时上下文增强** - 模型可见已连接的频道、出站交付状态、运行来源，支持更智能的路由决策 |
| [#4841](https://github.com/nearai/ironclaw/pull/4841) | @serrrfirat | XL | 🟠 重要功能 | **消除运行崩溃失败** - 将终端错误（HostUnavailable、模型失败、协议错误）转为可恢复或有解释的状态，提升稳定性 |
| [#4677](https://github.com/nearai/ironclaw/pull/4677) | @ilblackdragon | L | 🟠 重要功能 | **附件文本折叠入模型上下文** - 将提取的文档文本和音频转录作为 `<attachments>` 块注入模型可见的 ContextMessage，实现"附件对模型可见" |
| [#4676](https://github.com/nearai/ironclaw/pull/4676) | @ilblackdragon | M | 🟠 重要功能 | **入站路径文档文本提取** - `land_inbound_attachments` 调用 `ironclaw_extractors` 填充 `AttachmentRef.extracted_text`，转录携带文档内容而非仅元数据 |

**热点分析**：
- **Slack 集成稳定性** 是当前最紧迫的问题（#4839, #4843, #4844 三个相关 PR），反映 QA 测试中发现的重复审批循环、网关分发重复等生产级缺陷
- **附件端到端流程** 是本周期的核心功能交付，从摄入→存储→提取→模型可见形成闭环
- **运行时透明度** (#4836, #4838) 反映用户对"为什么失败、现在什么状态"的诉求

---

## 🐛 Bug 与稳定性

### 今日新增 Issue

| Issue | 优先级 | 状态 | 描述 |
|---|---|---|---|
| [#4845](https://github.com/nearai/ironclaw/issues/4845) | 🟠 中 | OPEN | **代码重构需求** - 提议提取 `resume_json` / `auth_resume_json` 的共享 resume-authority head，消除重复逻辑（类似 #4839 已做的尾部提取）。背景：#4839 已提取共享尾部，现需处理头部 |
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | 🔴 高 | OPEN | **夜间 E2E 测试失败** - 自动化报告，创建于 2026-05-27，最后更新 2026-06-13。失败工作流：Nightly E2E，涉及 v2-engine，已 17 天未解决 |

### 相关修复 PR（进行中）

| 修复 PR | 关联 Issue | 状态 | 修复内容 |
|---|---|---|---|
| [#4843](https://github.com/nearai/ironclaw/pull/4843) | #4839 系列 | OPEN | **单飞网关交付** - 修复网关分发重复问题（Bug 3），确保同一 run_id 的审批分辨率 ack 不会触发多次交付 |
| [#4844](https://github.com/nearai/ironclaw/pull/4844) | #4839 系列 | OPEN | **网关路由过滤修复** - 用原始网关字符串替换 `fn(&GateRef)->bool`，修复每路由分配和网关类型判断错误 |
| [#4846](https://github.com/nearai/ironclaw/pull/4846) | 新增 | OPEN | **工作区工具路径规范化** - 修复裸 `workspace/...` 路径被嵌套为 `/workspace/workspace/...` 的问题，添加回归测试覆盖 |

**稳定性评估**：
- ✅ **Slack 集成**：已识别 3 个根因（#4839, #4843, #4844），对应 PR 均在审查中，预期本周合并
- ⚠️ **E2E 测试**：#4108 长期未解决（17 天），需要维护者关注，可能涉及 v2-engine 的深层问题
- ✅ **附件流程**：5 个 PR 已合并，基础设施稳定

---

## 🎯 功能请求与路线图信号

### 正在推进的功能栈

| 功能 | 相关 PR | 预期影响 | 路线图信号 |
|---|---|---|---|
| **附件模型可见性** | #4676, #4677, #4675 | 用户可上传文档，模型直接访问内容，无需手动复制粘贴 | ✅ 本周期交付（5/6 PR 已合并） |
| **Slack 连接状态持久化** | [#4777](https://github.com/nearai/ironclaw/pull/4777) | 修复 Use Case 3 的 Slack 重连循环，WebUI 反映真实连接状态 | 🟠 XL PR，待合并 |
| **运行时上下文透明度** | #4836 | 模型可见频道连接、交付目标、运行来源，支持智能路由 | 🟠 XL PR，待合并 |
| **出站交付目标指导** | [#4780](https://github.com/nearai/ironclaw/pull/4780) | 模型在创建例程前选择交付目标，避免"Slack 不可用"的假警告 | 🟠 L PR，待合并 |
| **运行失败恢复** | #4841 | 消除"运行崩溃"终端错误，所有失败都可恢复或有解释 | 🟠 XL PR，待合并 |
| **网关 API 端点** | [#4264](https://github.com/nearai/ironclaw/pull/4264) | 添加 `POST /api/routines` 端点，支持外部系统创建例程 | 🟠 M PR，待合并 |

**路线图推断**：
- **Q2 2026 重点**：附件端到端 + Slack 稳定性 + 运行时透明度
- **下一阶段**：API 完善（网关端点）、外部集成增强

---

## 💬 用户反馈摘要

### 从 Issue/PR 描述提炼的用户痛点

| 痛点 | 来源 | 用户影响 | 优先级 |
|---|---|---|---|
| **重复审批循环** | #4839 QA 测试 | 一个逻辑调用（Gmail 获取邮件）需要 4 次连续审批，严重影响工作流体验 | 🔴 高 |
| **Slack 连接状态不同步** | #4777 | WebUI 总是显示 Slack 未连接，即使已连接，导致用户困惑 | 🟠 中 |
| **运行失败无解释** | #4841 | HostUnavailable、模型失败等错误显示为不透明代码，用户无法判断是否可重试 | 🟠 中 |
| **附件内容不可见** | #4676, #4677 | 用户上传文档，模型看不到内容，只能看到文件名，需手动复制粘贴 | 🟠 中 |
| **线程阻塞无反馈** | #4838 | 消息在忙碌线程上被静默停泊，用户不知道为什么没有响应 | 🟠 中 |
| **模型无法智能路由** | #4836 | 模型不知道哪些频道已连接、当前交付目标是什么，导致路由决策不当 | 🟡 低 |

**用户满意度信号**：
- ✅ 核心功能（附件、Slack）正在快速迭代修复
- ⚠️ 交互透明度（失败原因、状态反馈）仍需改进
- ⚠️ E2E 测试长期失败，可能影响用户对稳定性的信心

---

## 📋 待处理积压

### 长期未解决的关键 Issue

| Issue | 创建时间 | 天数 | 状态 | 建议 |
|---|---|---|---|---|
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | 2026-05-27 | 17 天 | OPEN，自动化报告 | 🔴 **需立即关注** - 夜间 E2E 测试持续失败，可能掩盖回归问题。建议：(1) 分配所有者调查 v2-engine 问题，(2) 临时禁用或标记为已知问题，(3) 添加 root-cause 标签 |

### 待合并的关键 PR（>24小时）

| PR | 创建时间 | 等待天数 | 规模 | 建议 |
|---|---|---|---|---|
| [#3708](https://github.com/nearai/ironclaw/pull/3708) | 2026-05-16 | 29 天 | M | 🔴 **发布 PR 长期待合并** - 包含破坏性变更（ironclaw_common 0.4.2→0.5.0, ironclaw_skills 0.3.0→0.4.0），需加速审查和发布流程 |
| [#4777](https://github.com/nearai/ironclaw/pull/4777) | 2026-06-11 | 3 天 | XL | 🟠

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报
**日期：2026-06-14** | **数据周期：过去24小时**

---

## 📊 今日速览

LobsterAI 项目今日保持稳定的开发节奏，共新增 4 条 Issue 和 5 条 PR。其中 2 条 PR 已合并/关闭，3 条待审核。项目活跃度中等，主要聚焦于**技能管理系统的完善**和**UI/UX 优化**，反映出团队在提升产品稳定性和用户体验方面的持续投入。值得注意的是，所有新增 Issue 均标记为 `[stale]`，暗示这些问题可能已存在一段时间，需要优先处理。

---

## 🔧 项目进展

### ✅ 已合并/关闭 PR（2 条）

| PR | 作者 | 内容 | 影响 |
|---|---|---|---|
| [#1466](https://github.com/netease-youdao/LobsterAI/pull/1466) | @linlihua | **fix(mcp)**: MCP 服务器表单模态框关闭按钮在内容过长时不可达 | 修复了模态框滚动布局问题，提升用户交互体验 |
| [#1467](https://github.com/netease-youdao/LobsterAI/pull/1467) | @linlihua | **fix(shortcuts)**: macOS 快捷键显示优化（Cmd ⌘ 替代 Ctrl） | 增强跨平台一致性，改善 macOS 用户体验 |

**进展评估**：两条 PR 均为 UX 细节优化，反映团队对用户体验的关注。@linlihua 在平台适配方面表现活跃。

### ⏳ 待审核 PR（3 条）

| PR | 作者 | 优先级 | 关键改动 |
|---|---|---|---|
| [#1440](https://github.com/netease-youdao/LobsterAI/pull/1440) | @gongzhi-netease | 🔴 高 | **feat(cowork)**: 将已选技能标签从底部工具栏移至输入框顶部，优化布局层级 |
| [#1441](https://github.com/netease-youdao/LobsterAI/pull/1441) | @febugcoder | 🔴 高 | **feat(artifacts)**: 为 HTML、React、Mermaid 添加可扩展预览管道（冲突解决版本） |
| [#1445](https://github.com/netease-youdao/LobsterAI/pull/1445) | @gongzhi-netease | 🔴 高 | **fix(skills)**: 修复技能重复导入无校验 + zip 导入目录名异常问题 |

**建议**：#1445 涉及数据完整性和系统稳定性，应优先合并；#1441 为功能增强，可跟进审核。

---

## 🐛 Bug 与稳定性

### 严重级别问题（按影响范围排序）

| Issue | 严重度 | 问题描述 | 状态 |
|---|---|---|---|
| [#1439](https://github.com/netease-youdao/LobsterAI/issues/1439) | 🔴 **高** | 已停用的技能在对话中仍可被调用 | 🔴 无对应 fix PR |
| [#1442](https://github.com/netease-youdao/LobsterAI/issues/1442) | 🟡 **中** | Agent 添加技能后，对话中技能标签消失，重新切换才重现 | 🔴 无对应 fix PR |
| [#1437](https://github.com/netease-youdao/LobsterAI/issues/1437) | 🟡 **中** | 创建定时任务时，选择"不重复"后点击创建无反应，无错误提示 | 🔴 无对应 fix PR |
| [#1443](https://github.com/netease-youdao/LobsterAI/issues/1443) | 🟡 **中** | OpenClaw v2026.3.24 版本兼容性问题（breaking change） | 🔴 无对应 fix PR |

**稳定性评估**：
- **#1439** 最为严重，涉及权限控制和系统安全，已停用的技能不应被调用
- **#1437** 反映表单验证缺失，用户无法获得反馈
- **#1443** 为依赖版本升级问题，需制定升级计划

---

## 💡 社区热点

### 讨论最活跃的 Issue

**[#1443](https://github.com/netease-youdao/LobsterAI/issues/1443) - OpenClaw 新版本适配**
- **创建时间**：2026-04-03 | **最后更新**：2026-06-13（74 天未解决）
- **评论数**：2 | **用户诉求**：明确的版本升级计划和兼容性支持
- **背景**：OpenClaw v2026.3.24 引入 breaking change，用户本地升级失败
- **隐含信号**：用户期望项目主动跟进上游依赖更新，而非被动等待

### 技能系统相关问题集中爆发

三条 Issue（#1439、#1442、#1445）均指向**技能管理系统**的问题：
- 权限控制不完善（已停用仍可调用）
- UI 状态管理混乱（标签消失/重现）
- 导入流程缺乏校验（重复导入、目录名异常）

**结论**：技能系统是当前用户反馈最集中的模块，需要系统性的重构或加固。

---

## 🎯 功能请求与路线图信号

### 已有 PR 支持的功能方向

| 功能方向 | 相关 PR | 预期收益 |
|---|---|---|
| **技能管理优化** | #1440、#1445 | 改善技能选择 UX，提升数据完整性 |
| **内容预览增强** | #1441 | 支持 HTML/React/Mermaid 原生渲染，提升协作体验 |
| **跨平台适配** | #1467 | 改善 macOS 用户体验 |
| **表单交互完善** | #1466 | 修复模态框可用性问题 |

### 用户期望的新功能

- **版本管理**：OpenClaw 等关键依赖的升级计划透明化
- **技能权限**：更细粒度的技能启用/禁用控制
- **表单反馈**：定时任务等复杂表单的实时验证提示

---

## 👥 用户反馈摘要

### 核心痛点

1. **技能系统不可靠**（#1439、#1442）
   - 用户期望：已停用的技能应完全隔离，不出现在任何调用链路
   - 现状：权限控制存在漏洞，UI 状态管理不稳定

2. **表单交互缺乏反馈**（#1437）
   - 用户期望：操作失败时有明确的错误提示
   - 现状：静默失败，用户无法判断问题原因

3. **依赖版本跟进滞后**（#1443）
   - 用户期望：项目主动适配上游更新，提供升级指南
   - 现状：用户自行升级遇到 breaking change，无官方支持

### 用户满意度信号

- 用户积极报告问题，提供截图和复现步骤，说明项目有一定用户基础
- 问题标记为 `[stale]` 表示长期未解决，可能导致用户流失

---

## ⚠️ 待处理积压

### 长期未响应的关键 Issue（74 天）

| Issue | 创建时间 | 最后更新 | 天数 | 优先级 |
|---|---|---|---|---|
| [#1443](https://github.com/netease-youdao/LobsterAI/issues/1443) | 2026-04-03 | 2026-06-13 | 71 | 🔴 高 |
| [#1437](https://github.com/netease-youdao/LobsterAI/issues/1437) | 2026-04-03 | 2026-06-13 | 71 | 🟡 中 |
| [#1439](https://github.com/netease-youdao/LobsterAI/issues/1439) | 2026-04-03 | 2026-06-13 | 71 | 🔴 高 |
| [#1442](https://github.com/netease-youdao/LobsterAI/issues/1442) | 2026-04-03 | 2026-06-13 | 71 | 🟡 中 |

### 建议行动

1. **立即处理 #1439**：权限控制漏洞，可能影响系统安全
2. **制定 #1443 的版本升级计划**：发布官方升级指南或新版本支持
3. **批量修复技能系统**：将 #1440、#1445 与 #1439、#1442 关联，作为一个整体改进周期
4. **补充表单验证**：#1437 涉及的定时任务模块需要完整的输入校验和错误提示

---

## 📈 项目健康度评分

| 维度 | 评分 | 备注 |
|---|---|---|
| **开发活跃度** | 7/10 | 日均 4.5 条 Issue + PR，保持稳定 |
| **问题响应速度** | 3/10 | 71 天未解决的问题过多，需改进 |
| **代码质量** | 7/10 | PR 涉及细节优化和 bug 修复，质量可控 |
| **用户满意度** | 5/10 | 技能系统问题集中，用户反馈积极但问题积压 |
| **版本管理** | 4/10 | 无新版本发布，依赖升级计划不明确 |

**总体评估**：项目处于**稳定维护阶段**，但存在**问题积压和响应延迟**的风险。建议优先处理技能系统的系统性改进，并建立更透明的版本升级计划。

---

*报告生成时间：2026-06-14 | 数据来源：GitHub API*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报
**日期：2026-06-14**

---

## 📊 今日速览

Moltis 项目今日保持稳定的开发节奏，共新增 1 个 Bug 报告和 3 个待合并 PR。项目聚焦于 **MCP OAuth 集成的稳定性修复**和**容器化部署的完善**，同时依赖项也在持续更新。虽然暂无版本发布，但已有针对关键 Bug 的修复 PR 在审核中，表明维护团队响应迅速。整体活跃度中等偏高，问题发现与修复的闭环效率较好。

---

## 🐛 Bug 与稳定性

### 🔴 **高优先级**

**#1119 - MCP OAuth 失败：`invalid_target` 错误（Notion、Linear 等服务）**
- **报告者**: @xzavrel | **创建**: 2026-06-13 | **更新**: 2026-06-14
- **影响范围**: 所有使用 `resource_metadata` 参数的 OAuth MCP 服务器（Notion、Linear 等）
- **问题描述**: 在 OAuth 授权流程中，浏览器返回 `invalid_target` 错误，导致远程 MCP 服务器无法添加
- **修复状态**: ✅ **已有 Fix PR** → [#1120](https://github.com/moltis-org/moltis/pull/1120)
- **根本原因**: `discover_and_register()` 错误地将 `WWW-Authenticate` 头中的 `resource_metadata` URL 传递给 `fetch_resource_metadata()`，应改用直接 fetch
- **链接**: [Issue #1119](https://github.com/moltis-org/moltis/issues/1119)

---

## 🚀 项目进展

### 待合并 PR（3 条）

| PR | 类型 | 作者 | 创建时间 | 说明 |
|---|---|---|---|---|
| [#1120](https://github.com/moltis-org/moltis/pull/1120) | **Bug Fix** | @xzavrel | 2026-06-13 | **MCP OAuth 修复**：修正 `resource_metadata` URL 的处理逻辑，改用直接 fetch 而非通过 `fetch_resource_metadata()` |
| [#1122](https://github.com/moltis-org/moltis/pull/1122) | **Bug Fix** | @sayotte | 2026-06-14 | **Docker 部署修复**：移除 Dockerfile 中与主目录绑定挂载冲突的 VOLUME 声明，解决路径覆盖问题 |
| [#1121](https://github.com/moltis-org/moltis/pull/1121) | **依赖更新** | @dependabot[bot] | 2026-06-14 | **esbuild 升级**：从 0.25.12 → 0.28.1（npm_and_yarn 组），涉及 `/crates/web/ui` |

**进展评估**: 
- 两个关键 Bug 修复（OAuth 和 Docker 部署）直指用户痛点
- 依赖项主动更新，保持工具链现代化
- **预期影响**: 这些 PR 合并后将显著改善 MCP 服务器集成体验和容器化部署稳定性

---

## 💬 社区热点

### 最活跃讨论

**#1119 - MCP OAuth `invalid_target` 错误** 
- **评论数**: 1 | **反应数**: 0
- **热度指标**: 🟡 中等（新报告，已有快速响应）
- **讨论焦点**: 
  - 用户遇到的具体错误场景（Notion、Linear 等主流服务）
  - 维护者快速定位根本原因并提交修复
- **用户诉求**: 支持更多 OAuth 标准变体，提高与第三方服务的兼容性

---

## 🔧 功能请求与路线图信号

**暂无新功能请求**，但从 PR 活动可推断项目优先级：

1. **MCP 生态兼容性** ⬆️ 优先级提升
   - 修复 OAuth 标准差异问题
   - 信号：与 Notion、Linear 等主流工具的集成是核心诉求

2. **容器化部署完善** ⬆️ 优先级提升
   - 解决 Docker 部署中的路径管理问题
   - 信号：云原生部署场景日益重要

3. **工具链现代化** 持续进行
   - esbuild 等构建工具定期更新

---

## 👥 用户反馈摘要

### 核心痛点

| 痛点 | 来源 | 影响用户 | 状态 |
|---|---|---|---|
| **OAuth 集成失败** | #1119 | 使用 Notion、Linear 等服务的用户 | 🔧 修复中 |
| **Docker 部署路径冲突** | #1122 | 容器化部署用户 | 🔧 修复中 |

### 使用场景洞察

- **企业工具集成**: 用户希望将 Moltis 与 Notion、Linear 等企业级工具无缝连接
- **容器化部署**: 用户采用 Docker 部署，需要可靠的卷挂载管理

---

## 📋 待处理积压

**当前无长期未响应的重要 Issue**。项目维护状态良好：
- ✅ 新 Issue 在 24 小时内获得响应（#1119 → #1120 快速修复）
- ✅ PR 审核周期短，无陈旧 PR 堆积

---

## 📌 维护者提示

1. **优先合并** [#1120](https://github.com/moltis-org/moltis/pull/1120) 和 [#1122](https://github.com/moltis-org/moltis/pull/1122)，这两个修复直指用户关键路径
2. **考虑发布补丁版本**，修复 OAuth 问题后建议发布 patch release，通知用户升级
3. **测试覆盖**: 为 OAuth `resource_metadata` 场景补充集成测试，防止回归

---

**报告生成时间**: 2026-06-14 | **数据来源**: GitHub API | **下次更新**: 2026-06-15

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报
**日期：2026-06-14** | **项目：CoPaw (AgentScope AI)**

---

## 📊 今日速览

CoPaw 项目今日保持高活跃度，过去24小时新增 **8 条 Issues** 和 **8 条 PRs**，其中 7 条 PR 待合并、1 条已关闭。虽未发布新版本，但社区贡献热情高涨，特别是来自越南用户的国际化需求和首次贡献者的质量修复。项目呈现**功能迭代与稳定性改进并行**的健康发展态势，但存在若干**关键 Bug 需要优先处理**。

---

## 🔄 项目进展

### 已合并/关闭
- **#2498** [已关闭] `fix(agents)`: 修复新建 Agent 时的语言选择问题，确保使用控制台语言而非硬编码英文/中文 — 解决了多语言用户体验的长期痛点

### 待合并的关键 PR（7 条）

| PR | 类型 | 优先级 | 说明 |
|---|---|---|---|
| **#5175** | feat | 🟢 高 | [越南语支持] 首次贡献者快速响应 #5169 需求，已实现 Console 越南语界面 |
| **#5170** | perf | 🟡 中 | [性能优化] 缓存 PROFILE.md 读取，解决 Agent 列表端点的 O(n²) 性能问题 |
| **#5035** | fix | 🟡 中 | [llama.cpp 兼容性] 修复版本号解析的固定宽度切片 Bug，支持 5 位数 build 号 |
| **#5040** | fix | 🟡 中 | [Cron 容错] 允许 jobs.json 包含无效任务，而非全部失败 |
| **#5037** | fix | 🟡 中 | [Linux 浏览器检测] 修复空 Exec= 行导致的 IndexError |
| **#5041** | fix | 🟡 中 | [备份容错] 跳过不可读文件，防止整个备份失败 |
| **#5038** | fix | 🟡 中 | [上下文管理] 防护空消息列表导致的 IndexError |

**评估**：7 条待合并 PR 中，**1 条新功能 + 6 条稳定性修复**，体现了项目对健壮性的重视。首次贡献者 @ly-wang19 贡献了 5 条高质量修复。

---

## 🌟 社区热点

### 最活跃讨论
1. **#5156** [建议支持 kimi-for-coding / 加入 uv 白名单](https://github.com/agentscope-ai/QwenPaw/issues/5156)
   - 👤 作者：@wjt0321 | 💬 评论：4 | 📅 更新：2026-06-13
   - **诉求**：支持 Kimi Coding 订阅用户直接接入（而非仅限官方 API），降低已付费用户的使用门槛
   - **背景**：反映出 LLM 提供商生态多元化，用户期望灵活的接入方式

2. **#5047** [Windows Tauri 桌面端启动特别慢](https://github.com/agentscope-ai/QwenPaw/issues/5047)
   - 👤 作者：@moolawooda | 💬 评论：3 | 📅 创建：2026-06-09
   - **痛点**：从 Python 打包迁移到 Tauri 后，启动时间从 1-2 分钟恶化至 10+ 分钟，频繁无响应
   - **影响**：Windows 用户体验严重下降，可能导致用户流失

3. **#5169** [请求添加越南语界面](https://github.com/agentscope-ai/QwenPaw/issues/5169)
   - 👤 作者：@biencuong | 💬 评论：2 | 📅 创建：2026-06-13
   - **进展**：社区快速响应，@nguyenthanhthe 已提交 PR #5175 实现
   - **信号**：东南亚市场需求明确，国际化路线图正在执行

---

## 🐛 Bug 与稳定性

### 严重级 Bug（需立即处理）

| Issue | 严重度 | 描述 | 状态 |
|---|---|---|---|
| **#5172** | 🔴 严重 | [聊天无响应] 对话中断后再次提问会永久等待，需点击停止才能恢复；QQ/微信接入时无法停止 | ✅ 已关闭（可能为用户误操作） |
| **#5171** | 🔴 严重 | [上下文压缩缺陷] 人设文件 Token 超过阈值时，压缩会导致上下文完全丢失（保留为0），任务中断 | ❌ 开放，无 fix PR |
| **#5174** | 🟠 高 | [Cron/心跳机制限制] Cron Agent 无法执行 write_file、spawn_subagent；心跳 Agent 理论可行但实际不执行 | ❌ 开放，需设计评审 |

### 中等级 Bug（已有 fix PR）
- **#5035**: llama.cpp 版本解析 → **PR #5035 待合并**
- **#5040**: Cron jobs.json 容错 → **PR #5040 待合并**
- **#5037**: Linux 浏览器检测 → **PR #5037 待合并**
- **#5041**: 备份文件读取 → **PR #5041 待合并**
- **#5038**: 空消息列表处理 → **PR #5038 待合并**

**建议**：优先合并 6 条待审 fix PR，然后集中处理 #5171（上下文压缩）和 #5174（Agent 机制）。

---

## 💡 功能请求与路线图信号

### 新功能需求（优先级排序）

| 需求 | 来源 | 状态 | 预期影响 |
|---|---|---|---|
| **越南语界面** | #5169 | ✅ PR #5175 已提交 | 🟢 可纳入下一版本 |
| **Zalo Bot 频道** | #5168 | ❌ 开放 | 🟡 需评估东南亚市场优先级 |
| **Kimi Coding 接入** | #5156 | ❌ 开放 | 🟡 涉及 LLM 提供商集成架构 |
| **Tauri 启动性能优化** | #5047 | ❌ 开放 | 🔴 高优先级（用户体验关键） |

### 国际化趋势
- 越南用户活跃度上升（#5169, #5168, #5175）
- 建议后续考虑 **东南亚本地化** 专项（语言 + 频道 + LLM 提供商）

---

## 👥 用户反馈摘要

### 核心痛点
1. **性能问题**（#5047）
   - Tauri 迁移后桌面端启动速度严重下降
   - 用户期望：快速启动、稳定运行

2. **功能完整性**（#5156, #5174）
   - 已付费 LLM 订阅用户无法直接接入
   - Agent 自动化能力受限（Cron/心跳机制）

3. **稳定性与容错**（#5171, #5172）
   - 上下文压缩导致数据丢失
   - 对话中断后恢复困难

4. **国际化需求**（#5169, #5168）
   - 越南用户明确要求本地化支持
   - 东南亚市场潜力大

### 用户满意度信号
- 社区贡献热情高（首次贡献者积极参与）
- 问题反馈详细（附截图、版本号、硬件配置）
- 跨地域用户活跃（中国、越南、印尼等）

---

## ⏳ 待处理积压

### 长期未响应的关键 Issue
- **#5047**（Tauri 性能）：创建于 2026-06-09，已 5 天未有官方回应 → **建议立即跟进**
- **#5171**（上下文压缩）：创建于 2026-06-13，严重程度高 → **需分配负责人**
- **#5174**（Agent 机制）：创建于 2026-06-13，涉及架构设计 → **需技术评审**

### PR 审核积压
- **6 条 fix PR**（#5035, #5037, #5038, #5040, #5041, #5170）已待审 → **建议批量审核**
- **1 条新功能 PR**（#5175）首次贡献 → **优先合并以鼓励社区**

---

## 📈 项目健康度评分

| 维度 | 评分 | 备注 |
|---|---|---|
| **社区活跃度** | ⭐⭐⭐⭐⭐ | 24h 新增 16 条 Issue/PR，首次贡献者活跃 |
| **代码质量** | ⭐⭐⭐⭐ | 6 条稳定性修复 PR，覆盖容错、性能、兼容性 |
| **问题响应速度** | ⭐⭐⭐ | 部分关键 Issue（#5047）未及时回应 |
| **版本迭代** | ⭐⭐⭐ | 无新版本发布，但 PR 积累充足 |
| **国际化进展** | ⭐⭐⭐⭐ | 越南语支持快速推进，东南亚市场开拓中 |

**总体评估**：项目处于**健康的高速迭代阶段**，社区贡献质量高，但需加强关键 Bug 的优先级管理和性能问题的及时响应。

---

## 🎯 建议行动项

1. **本周优先**
   - [ ] 合并 6 条待审 fix PR（#5035, #5037, #5038, #5040, #5041, #5170）
   - [ ] 合并越南语 PR #5175，发布小版本
   - [ ] 指派负责人处理 #5171（上下文压缩）和 #5047（Tauri 性能）

2. **下周规划**
   - [ ] 技术评审 #5174（Agent 机制限制）
   - [ ] 评估 #5156（Kimi 接入）和 #5168（Zalo Bot）的可行性
   - [ ] 发布包含 fix 和越南语的新版本

3. **长期建议**
   - [ ] 建立 Bug 优先级 SLA（严重 Bug 24h 内回应）
   - [ ] 启动东南亚本地化专项（语言 + 频道 + LLM）
   - [ ] 性能基准测试（特别是 Tauri 启动时间）

---

**报告生成时间**：2026-06-14 | **数据来源**：GitHub API | **下次更新**：2026-06-15

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