# OpenClaw 生态日报 2026-06-12

> Issues: 500 | PRs: 500 | 覆盖项目: 12 个 | 生成时间: 2026-06-12 03:41 UTC

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

# OpenClaw 项目动态日报 | 2026-06-12

## 📊 今日速览

OpenClaw 项目表现出**极高的活跃度与紧张的修复节奏**。过去24小时新增/活跃 Issues 472 条、待合并 PR 378 条，同时发布了安全加固版本 v2026.6.6-beta.2。项目正处于**多维度的质量改进阶段**：安全边界收紧、多代理编排稳定性提升、工具链完善，但同时暴露了大量 session 状态一致性、消息投递、沙箱隔离等深层次问题。评论最热的 50 个 Issue 反映出社区对**跨平台支持（Linux/Windows）、权限隔离、多代理协调**的强烈诉求。

---

## 🚀 版本发布

### **v2026.6.6-beta.2** 安全加固版本
**发布时间**：2026-06-12  
**核心方向**：安全边界大幅收紧

#### 关键改进
- **转录记录安全性**：加强对话数据隐私保护
- **沙箱绑定隔离**：强化容器化执行隔离
- **主机环境继承**：限制环境变量渗透
- **MCP 标准输入输出安全**：协议边界加固
- **Codex HTTP 访问控制**：限制第三方模型的网络权限
- **原生搜索策略**：Web 搜索请求过滤
- **发送方检查**：强化消息来源校验
- **已删除代理 ACP 绕过**：补全权限审计漏洞
- **回环工具攻击**：防止工具链自指
- **Discord 审核**：群组操作安全加固
- **Teams 群组操作**：多租户隔离增强

#### ⚠️ 迁移提示
此版本为 **beta**，建议在**非生产环境先行验证**。安全边界收紧可能影响现有的以下配置：
- 自定义脚本中依赖环境变量注入的工作流
- 通过工具链执行的第三方工具集成
- 多租户共享沙箱配置

---

## 📈 项目进展

### 今日合并/关闭的关键 PR

#### 🔧 重要修复（5 条）

1. **#92304** [CLOSED] - `fix(cron): preserve tz and staggerMs when editing cron expression`
   - **影响**：修复定时任务编辑时时区和错开时间被清空的回归问题
   - **状态**：已关闭/合并 ✅

2. **#92295** [CLOSED] - `fix(cron): preserve tz and staggerMs when --cron replaces expression`
   - **影响**：修复 `openclaw cron edit` 命令的参数保留逻辑
   - **状态**：已关闭/合并 ✅

3. **#92312** [CLOSED] - `Fix dashboard history projection and approval followups`
   - **影响**：修复 Web UI 仪表板历史展示，隐藏工具调用的纯文本消息，改进审批流程
   - **状态**：已关闭，被 #92328 替代

4. **#68936** [CLOSED] - `Autofix: add PR review autofix pipeline + Windows daemon`
   - **规模**：XL (~785 行)
   - **影响**：添加自动化 PR 审查修复管道和 Windows 后台守护进程，提升开发效率
   - **状态**：已合并 ✅

5. **#56263** [CLOSED] - `Allow configurable file permissions (chmod 0o640/0o750) for multi-user setups`
   - **影响**：解决多用户容器环境下文件权限被硬编码为 600 导致组成员无法读取的问题
   - **状态**：已合并 ✅

#### 📋 待合并的高优先级 PR（评论最多）

| PR | 标题 | 优先级 | 风险评估 | 进度 |
|---|---|---|---|---|
| #78441 | feat(subagents): forward toolsAllow from sessions_spawn | P2 | 🚨 兼容性 | 待审核 |
| #92300 | fix(openai-responses): collapse cumulative message snapshots | P1 | 🚨 消息投递 | 待审核 |
| #92318 | fix(cron): require explicit message target proof | P1 | 🚨 消息投递 | 待审核 |
| #87504 | fix(skill-workshop): align agent_end hook timeout | P2 | 🚨 兼容性 | 等待审核 |
| #84758 | feat(subagents): add execution backend placement contract | P2 | 🚨 兼容性 | 待审核 |

**项目推进指标**：378 条待合并 PR、122 条已合并/关闭，说明**合并速度与问题增长速度维持在 1:3 的压力比**，maintenance 容量接近饱和。

---

## 🔥 社区热点

### Top 10 最活跃 Issues（按评论数）

| 排名 | Issue | 评论数 | 关键词 | 用户诉求 |
|---|---|---|---|---|
| 1 | #75 | 109 👍79 | Linux/Windows 应用 | **跨平台支持**：macOS 有完整应用，Windows/Linux 用户被迫使用 API 或浏览器 |
| 2 | #9443 | 25 | Android APK 预编译 | **分发简化**：源码编译门槛高，需官方预编译版本 |
| 3 | #32473 | 17 | HTTPS/localhost 安全上下文 | **Docker 部署问题**：VPS 上自签证书导致控制 UI 无法加载 |
| 4 | #22438 | 17 | 分层启动文件加载 | **Token 优化**：每次 session 加载全量 bootstrap 文件浪费 token |
| 5 | #32296 | 15 | Agent 回复错误消息 | **会话混乱**：session context 管理缺陷导致回复不对应 |
| 6 | #10659 | 13 | 隐蔽密钥系统 | **安全隔离**：Agent 可见原始 API Key，易泄露或被注入攻击 |
| 7 | #39604 | 13 | 私网访问配置 | **网络控制**：web_fetch 无法访问内网服务，限制了内部工具集成 |
| 8 | #85888 | 12 | Cron 定时失败（MiniMax 503） | **稳定性**：特定时段 cron 持续失败，manual trigger 正常，调度策略有问题 |
| 9 | #6731 | 12 | safe/unsafe ClawdBot 模式 | **安全策略**：呼吁用 Rust 重写以获得内存安全和沙箱隔离 |
| 10 | #57326 | 12 | CLI 后端绕过 CLI dispatch | **权限边界**：某些路径仍绕过 CLI provider，安全回归 |

### 🌟 今日新热话题

**#39476** [新增] - A2A sessions_send 往返调用导致重复消息
- **问题**：Agent A 通过 `sessions_send` 调用 Agent B，B 可回调 A，导致消息重复
- **影响**：多代理编排的关键缺陷，会造成消息风暴
- **评论**：10 条，已识别需要在工具层加入环路检测

**#91363** [新增] - 隔离 cron 在 model-call-started 阶段持续失败
- **问题**：isolated cron 无法启动 LLM 调用，usage.input=0 说明请求未送达
- **影响**：定时任务完全不可用（isolation mode）
- **预期修复**：涉及 session 初始化和隔离容器通信路径

---

## 🐛 Bug 与稳定性

### 严重程度分级

#### 🔴 **Critical / P1**（8 个，其中 3 个有 fix PR）

| Issue | 标题 | 根因 | Fix PR 状态 |
|---|---|---|---|
| #32296 | Agent 回复前一条消息 | Session context 混乱 | 无 |
| #29387 | agentDir bootstrap 文件被忽略 | 路径优先级逻辑错误 | 无 |
| #10659 | Agent 可见原始 API Key | 缺少密钥隐蔽层 | 无（架构改进） |
| #40001 | write 工具缺少 append 模式 | 工具功能不完整 | 无 |
| #39476 | sessions_send 往返导致重复消息 | 缺乏环路检测 | 无 |
| #40540 | Windows update 命令 EBUSY 错误 | 文件锁定问题 | 无 |
| #31331 | Docker + 沙箱 workspaceAccess 失败 | 容器内外路径映射错误 | 无 |
| #91363 | 隔离 cron LLM 请求失败 | 初始化/通信路径缺陷 | **#92294** ⏳ |

#### 🟠 **High / P2**（35+ 个，其中 8 个有 fix PR）

**已修复或待审**：
- #57901 - Safeguard compaction 忽视 model config → 无 fix
- #31583 - exec 工具不继承环境变量 → 无 fix  
- #37634 - workspaceAccess none 仍挂载为只读 → 无 fix
- #38327 - Gemini 3.1 Pro "Cannot convert undefined" → 无 fix
- #92178 - 仪表板 formatAuditList crash → **#92178** ✅ 待合并

#### 🟡 **Medium / P3**（基础设施、可用性、非关键路径）

- 定时任务参数清空 → **#92304 #92295** ✅ 已合并
- 网络 avatar 端点 404 → #38439 未见修复
- Telegram DM 路由污染 → #41165 未见修复
- CLI 无法自更新 → #40540 涉及跨平台文件锁

### 回归问题（Regression）统计
- 本次报告期识别回归 **12 条**（标记 `regression` 标签）
- 最常见：session 状态漂移、权限隐式提升、工具功能丢失
- **趋势**：与最近的安全加固和多代理功能膨胀相关

---

## ✨ 功能请求与路线图信号

### 高热度功能需求（反馈者 3 人以上）

| 功能 | Issue | 赞 | 关键度 | 预期 |
|---|---|---|---|---|
| **跨平台应用（Linux/Windows）** | #75 | 79 | 🔴 Critical | v2026.7 |
| **隐蔽密钥系统** | #10659 | 4 | 🔴 Critical | 未排期 |
| **分层 bootstrap 加载** | #22438 | 0 | 🟠 High | 未排期 |
| **私网 fetch 访问** | #39604 | 9 | 🟠 High | 可能 v2026.7 |
| **多代理能力画像** | #35203 | 0 | 🟠 High | 未排期 |
| **会话内存自动保留** | #40418 | 1 | 🟡 Medium | 未排期 |
| **Android APK 预编译** | #9443 | 2 | 🟡 Medium | 可能 v2026.6.7 |
| **路径级权限（RWX）** | #39979 | 0 | 🟠 High | 与 ACP 重构关联 |
| **native secrets 管理** | #13610 | 1 | 🟠 High | 未排期 |

### 已有对应 PR 的功能（将进入下一版本）

1. **#84758** - 子代理执行后端放置契约 → `sessions_spawn` 支持 backend 选择
2. **#78441** - 子代理工具权限转发 → 精细化工具隔离
3. **#86655** - Claude 应用服务器集成 → Anthropic 原生支持（对标 OpenAI bridge）
4. **#85664** - read 工具直接调用 HTTP → 减少网络往返
5. **#12581** - Session 剪枝生命周期钩子 → 可观测性提升

---

## 👥 用户反馈摘要

### 核心痛点

#### 1️⃣ **跨平台可用性（最广泛诉求）**
- **现状**：仅有 macOS/iOS/Android；Windows/Linux 用户无官方应用
- **诉求**：与 native 应用同功能的 Linux/Windows 应用或便携编译包
- **用户角色**：企业部署（VPS 用户）、开发工具链集成者

#### 2️⃣ **安全隔离与权限模型（深层诉求）**
- **现状**：密钥明文存储、工具权限二元化、沙箱绑定不完整
- **诉求**：
  - 密钥隐蔽层（Agent 使用但看不到）
  - 路径级 RWX 权限（如 Unix DAC）
  - 能力画像（Agent 能做什么自动生成）
- **用户角色**：安全敏感型企业、金融/医疗行业

#### 3️⃣ **多代理编排稳定性（新场景痛点）**
- **

---

## 横向生态对比

# AI 智能体开源生态全景分析报告 | 2026-06-12

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**快速分化与专业化的阶段**。一方面，多代理协作、工具隔离、消息可靠性等**生产级基础设施**成为所有项目的共同关切，表明生态已走出"单Agent demo"阶段；另一方面，各项目在多渠道集成、实时交互、安全隔离等方向探索出显著的差异化路线，反映出不同应用场景对"智能体平台"的多元诉求。整体呈现**高活跃度、高问题密度、快速迭代**的特征，社区用户从功能尝鲜向生产部署逐步转向，暴露出的Bug与需求质量都显著提升。

---

## 2. 各项目活跃度对比

| 项目 | 新增 Issue | 活跃 PR | 已合并 | 待审 | 版本发布 | 周期健康度 | 稳定性评分 |
|------|-----------|---------|--------|------|---------|----------|-----------|
| **OpenClaw** | 472 | 378 | 122 | 378 | v2026.6.6-beta.2 | ⚠️ 压力饱和 | ⭐⭐⭐⭐ |
| **NanoBot** | 3 | 18 | 6 | 12 | — | ✅ 健康 | ⭐⭐⭐⭐ |
| **ZeroClaw** | 50 | 50 | 3 | 47 | v0.8.0 | 🔴 质量滞后 | ⭐⭐⭐ |
| **PicoClaw** | 7 | 31 | 18 | 13 | v0.2.9-nightly | ✅ 高效 | ⭐⭐⭐⭐ |
| **NanoClaw** | 5 | 14 | 9 | 5 | — | ✅ 健康 | ⭐⭐⭐⭐ |
| **IronClaw** | 31 | 47 | 4 | 43 | — | 🟡 功能驱动 | ⭐⭐⭐⭐ |
| **LobsterAI** | 2 | 15 | 14 | 1 | — | ✅ 最优 | ⭐⭐⭐⭐⭐ |
| **Moltis** | 1 | 1 | 0 | 1 | — | ✅ 稳定 | ⭐⭐⭐⭐ |
| **CoPaw** | 34 | 41 | 8 | 23 | v1.1.11.post2 | 🔴 补丁频繁 | ⭐⭐ |

**关键指标解读**：
- **Issue 密度与 PR 合并比**：OpenClaw（1:3.1 压力比）> ZeroClaw（1:1 功能超前）> IronClaw（1:1.5 架构迭代）
- **最高效项目**：LobsterAI（93% 合并率，14/15 PR）与 NanoClaw（86% 合并率）
- **最大挑战**：OpenClaw（maintenance 容量接近饱和）与 CoPaw（质量缺陷频繁）

---

## 3. OpenClaw 在生态中的定位

### 技术路线对比

| 维度 | OpenClaw | NanoBot | ZeroClaw | 其他 |
|------|----------|---------|----------|------|
| **架构** | 多Agent编排 + 沙箱隔离 | 轻量级 SDK | 多命名代理 | 单或双代理为主 |
| **核心能力** | 工具权限模型 + MCP 标准 | Python SDK 完整性 | 多代理生命周期 | UI/UX 优先 |
| **安全模型** | 密钥隐蔽、权限 ACL | 基础隔离 | 工具过滤、权限策略 | 默认信任 |
| **多渠道支持** | Discord、Teams、Slack 完整 | 通用 SDK | 多种（包括 Twitch）| 差异化（邮件、DingTalk） |
| **成熟度** | 生产级（Beta 安全加固） | 开发级 SDK | RC 阶段（v0.8.0） | 早期-中期混合 |

### 社区规模与影响力

```
Issue 反馈热度（评论数排名）：
OpenClaw      #75 (跨平台支持) — 109评论、79赞  🏆
IronClaw      #3036 (配置即代码) — 7评论，core驱动
LobsterAI     #1462 (多Agent协作) — 2评论，69天活跃
ZeroClaw      #6699 (工具过滤) — 7评论
```

**优势总结**：
- ✅ 社区关注度最高（Issue 反馈量 472 条，其他项目 1-50 条）
- ✅ 功能完整度最强（多渠道、工具链、Automation 最全）
- ✅ 安全架构最成熟（v2026.6.6 安全加固版发布）
- ⚠️ 维护压力最大（待合并 PR 378 条，合并速度跟不上问题增速）

**差异化定位**：
- OpenClaw = "企业级多Agent平台" + "高度开放的工具生态"
- NanoBot = "最轻量级 Python SDK"，适合嵌入式集成
- ZeroClaw = "本地部署的多代理容器"，强调自主性与隐私
- LobsterAI = "最佳用户体验"，注重交互设计与多渠道现成方案

---

## 4. 共同关注的技术方向

### 4.1 多代理协作与编排
**涉及项目**：OpenClaw、ZeroClaw、NanoBot、LobsterAI、PicoClaw、NanoClaw

| 项目 | 具体诉求 | 实现状态 | 优先级信号 |
|------|---------|---------|----------|
| **LobsterAI** | 单 Agent 绑定不同模型 + Manager 调度 | PR 进行中（#1462） | ⭐⭐⭐⭐ 用户强烈呼吁 |
| **OpenClaw** | `sessions_send` A2A 调用去重 + 环路检测 | Issue 已识别（#39476） | ⭐⭐⭐⭐ P1 阻塞 |
| **ZeroClaw** | 多命名代理独立配置 + 工具访问控制 | v0.8.0 已交付，但 Bug 未修 | ⭐⭐⭐ 架构级需求 |
| **NanoBot** | Cron 自动化会话绑定 + 子代理完成等待 | 待合并 PR 存在（#4299, #4304） | ⭐⭐⭐ 异步任务可靠性 |
| **PicoClaw** | Agent Collaboration Bus（邮箱、协作线程） | 待审 PR（#2937） | ⭐⭐⭐ 架构研究中 |

**跨项目共识**：多代理需求已成"刚需"，从协议设计（A2A 消息投递）、到任务协调（Cron 绑定）、再到权限隔离（工具访问控制），都需要**统一的编排模型**。

### 4.2 安全隔离与权限模型
**涉及项目**：OpenClaw、ZeroClaw、NanoBot、PicoClaw、NanoClaw

| 项目 | 具体诉求 | 实现状态 | 问题根源 |
|------|---------|---------|---------|
| **OpenClaw** | 隐蔽密钥系统（Agent 使用但看不到 Key） | 未排期，架构改进 | ⭐⭐⭐⭐ P0 安全缺陷 |
| **ZeroClaw** | 工具过滤失效（`tool_filter_groups` 前缀 Bug） | Issue #6699（7评论） | ⭐⭐⭐⭐ 权限绕过风险 |
| **ZeroClaw** | 代理委派模式权限冲突（空工具列表拒绝） | Issue #7470（7评论） | ⭐⭐⭐⭐ S1 策略矛盾 |
| **PicoClaw** | CIDR 限制绕过（本机环回代理） | Issue #3080（已关闭，#2955 修复） | ⭐⭐⭐ 初始化漏洞 |
| **NanoClaw** | writeOutboundDirect 只读模式导致消息丢弃 | PR #2738 已合并 | ⭐⭐⭐⭐ 数据库访问模式 |

**跨项目共识**：权限隔离从"二元信任模型"升级到"细粒度访问控制"的转变正在全面进行。隐蔽密钥、工具白名单、操作审计成为**生产部署的标配**。

### 4.3 消息投递可靠性
**涉及项目**：OpenClaw、ZeroClaw、NanoBot、PicoClaw、NanoClaw、Moltis

| 项目 | 具体问题 | 问题类型 | 修复进度 |
|------|---------|---------|---------|
| **OpenClaw** | `sessions_send` 往返调用消息重复（#39476） | 环路检测缺失 | ❌ Issue 阶段 |
| **OpenClaw** | 消息投递到期（#92300 collapse snapshots） | 状态管理 | ⏳ PR 待审 |
| **NanoBot** | 孤立工具结果持久化破坏 API 兼容性（#4306） | 消息类型不匹配 | ✅ PR 待合并 |
| **NanoClaw** | wiring create 跳过 agent_destinations 副作用（#2743） | ORM 隐含行为 | ⏳ PR 待审 |
| **Moltis** | WhatsApp @lid 聊天回复投递失败（#1116） | JID 重写机制 | ⏳ PR 待合并 |
| **PicoClaw** | Spawn 子代理消息重复（#3094） | ForUser 字段重复投递 | ❌ 未解决 |

**跨项目共识**：**消息投递已成为最高频的 P0/P1 缺陷类型**，涉及数据库访问模式、状态机设计、多渠道适配等多层系统。单个项目难以独自解决，急需**统一的消息协议与投递可靠性框架**。

### 4.4 跨平台与部署易用性
**涉及项目**：OpenClaw、PicoClaw、CoPaw、LobsterAI

| 项目 | 诉求 | 用户规模 | 当前方案 |
|------|------|---------|---------|
| **OpenClaw** | Linux/Windows 应用（仅 macOS/iOS） | ⭐⭐⭐⭐⭐ 79赞、109评论 | 无，仅浏览器+API |
| **PicoClaw** | Windows 路径分隔符兼容性（63天积压） | ⭐⭐⭐⭐ 文件操作全失效 | 无，仍 OPEN |
| **PicoClaw** | 32 位 Android 支持 | ⭐⭐⭐ | 已标记 wontfix |
| **CoPaw** | Tauri Windows SSL 证书 + 内存泄漏 | ⭐⭐⭐⭐ 客户端无法启动 | PR #5125 CI 加固，非根因 |
| **CoPaw** | OpenSSL 3.5 DER 证书解析失败 | ⭐⭐⭐ Windows 用户 | 需升级 Python/SSL workaround |

**跨项目共识**：**Windows 与 Linux 桌面端仍是开源 AI 助手的显著短板**，WebUI 可用但原生应用缺失导致大量企业用户被迫接受第三方包装方案。

---

## 5. 差异化定位分析

### 5.1 功能侧重矩阵

```
                    安全隐私优先          交互体验优先
高度开放工具    OpenClaw               LobsterAI
(多渠道/扩展)        ✓                      ✓ ✓
                 (MCP标准)             (多渠道完整)

本地轻量部署    ZeroClaw               PicoClaw/NanoBot
(SDK/容器)           ✓                      ✓
                 (配置编码)            (嵌入式友好)

企业多租户      IronClaw               CoPaw
(可观测性)           ✓                      ✓
                 (OTel基础设施)        (云原生UI)
```

### 5.2 架构路线清单

| 项目 | 核心架构 | 依赖关系 | 扩展模式 | 最佳应用场景 |
|------|---------|---------|---------|------------|
| **OpenClaw** | 多Agent编排 + 工具沙箱 | 轻依赖（纯 Node.js） | MCP 标准、A2A 协议 | 企业 AI 助手平台、工具链自动化 |
| **NanoBot** | Python SDK + Provider 抽象 | 高依赖（LLM SDK） | 自定义提供商、技能插件 | AI 应用嵌入、研究原

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报
**日期：2026-06-12**

---

## 📊 今日速览

NanoBot 项目今日保持高活跃度，过去 24 小时新增 3 条 Issue、合并/推进 18 条 PR，其中 12 条待合并。项目呈现**功能开发与稳定性修复并行**的态势：一方面推进 Python SDK 扩展、Cron 自动化会话绑定、技能缓存等核心功能升级，另一方面积极应对 MCP 重连崩溃、孤立工具结果持久化等生产级问题。整体来看，项目维护活跃、社区贡献热度高，但出现了多个新 Bug 需要优先处理。

---

## 🎯 项目进展

### 今日合并/关闭（6 条）

| PR | 内容 | 意义 |
|---|---|---|
| [#4020](https://github.com/HKUDS/nanobot/pull/4020) | `feat(providers)`: 支持按提供商配置流空闲超时 | 解决本地 LLM（LM Studio、Ollama）在复杂 prompt 上的超时问题，提升开发者体验 |
| [#4289](https://github.com/HKUDS/nanobot/pull/4289) | `feat(slack)`: 增加频道 @mention 限制选项 | Slack 集成功能完善，允许更灵活的权限控制 |
| [#4281](https://github.com/HKUDS/nanobot/pull/4281) | `feat(transcription)`: 新增 SiliconFlow 转录提供商 | 扩展转录能力，支持国产开源模型 FunAudioLLM |
| [#4257](https://github.com/HKUDS/nanobot/pull/4257) | `fix(utils)`: 修复消息分割对代码块的破坏 | 修复 Markdown 渲染缺陷 |
| [#4298、#4297](https://github.com/HKUDS/nanobot/pull/4298) | Worktree 功能 + Hermes 研究文档 | 文档和工具链优化 |
| [#4294](https://github.com/HKUDS/nanobot/pull/4294) | `chore(repo)`: 移除桌面应用，精简核心仓库 | 项目结构调整，专注核心 AI 智能体功能 |

### 待合并重点 PR（12 条）

**核心功能** (预期对整体架构的提升)：
- [#4306](https://github.com/HKUDS/nanobot/pull/4306) `fix(session)`: 防止孤立工具结果持久化 — 解决 OpenAI/Anthropic API 兼容性问题
- [#4299](https://github.com/HKUDS/nanobot/pull/4299) `feat(cron)`: Cron 自动化绑定到会话 — 改进会话级调度机制
- [#4296](https://github.com/HKUDS/nanobot/pull/4296) `feat(sdk)`: 扩展 Python SDK 运行时控制 — 提升 SDK 易用性和功能完整性
- [#4301](https://github.com/HKUDS/nanobot/pull/4301) `feat(skills)`: 缓存技能加载器元数据 — 性能优化，减少重复扫描和解析

**问题修复**：
- [#4303](https://github.com/HKUDS/nanobot/pull/4303) `fix(mcp)`: 关闭 MCP 追踪生成器防止 GC 崩溃 — 直接解决 [#4302](https://github.com/HKUDS/nanobot/issues/4302)
- [#4304](https://github.com/HKUDS/nanobot/pull/4304) `fix(cron)`: 等待子智能体完成再标记 Cron 完成 — 解决异步任务未等待问题

**功能增强**：
- [#3239](https://github.com/HKUDS/nanobot/pull/3239) `feat`: 支持多个自定义 OpenAI 兼容提供商 — 长期 issue，已有 PR 实现
- [#4300](https://github.com/HKUDS/nanobot/pull/4300) `feat(skills)`: 检查技能类型要求 — 技能系统完善
- [#4021](https://github.com/HKUDS/nanobot/pull/4021) `fix(codex)`: Codex 去重和重试机制 — 修复 Responses API 重复项问题
- [#3538](https://github.com/HKUDS/nanobot/pull/3538) `feat`: Gateway 启动/停止/重启命令 — 运维工具完善

---

## 🔥 社区热点

### 高热度 Issue

**[#4305 Multiple custom providers](https://github.com/HKUDS/nanobot/issues/4305)** 👤 @smurfix
- **创建时间**：2026-06-11
- **诉求**：需要多个自定义提供商而非仅一个，建议在提供商配置中加入 `template` 参数选择内置提供商
- **背景**：与已有 PR [#3239](https://github.com/HKUDS/nanobot/pull/3239) 功能诉求**完全一致**，说明该需求确实是用户痛点
- **信号**：该 PR 应该优先合并，解决用户多云/多端点接入的需求

**[#4302 nanobot gateway crashes after mcp reconnect](https://github.com/HKUDS/nanobot/issues/4302)** 👤 @tjc0726
- **创建时间**：2026-06-11
- **严重程度**：⚠️ 高（Gateway 级别崩溃）
- **状态**：已有对应 PR [#4303](https://github.com/HKUDS/nanobot/pull/4303) 待合并
- **影响范围**：MCP 服务器重连场景

---

## 🐛 Bug 与稳定性

### 今日报告的 Bug（按严重程度排序）

| Issue | 严重度 | 描述 | 已有 Fix | 状态 |
|-------|--------|------|---------|------|
| [#4302](https://github.com/HKUDS/nanobot/issues/4302) | 🔴 **Critical** | Gateway MCP 重连后崩溃，`RuntimeError: cancel scope` | ✅ [#4303](https://github.com/HKUDS/nanobot/pull/4303) | 待合并 |
| [#4236](https://github.com/HKUDS/nanobot/issues/4236) | 🟠 **High** | Ubuntu 24.04 用户命名空间限制导致 bwrap sandbox 失效 | ❌ 无 | 已关闭，可能标记为 wontfix |
| [#4306](https://github.com/HKUDS/nanobot/pull/4306) | 🟠 **High** | 孤立工具结果（`role:"tool"` 无匹配 `tool_call_id`）被持久化，严格 API 拒绝 | ✅ PR 本身即 Fix | 待合并 |

### 潜在稳定性风险

- **[#4021](https://github.com/HKUDS/nanobot/pull/4021)**：Codex provider 重复项 400 错误，影响多轮对话
- **[#4304](https://github.com/HKUDS/nanobot/pull/4304)**：Cron 子智能体异步任务未等待，可能导致数据不一致

---

## 💡 功能请求与路线图信号

### 高优先级功能需求

| 需求 | Issue | 相关 PR | 预期方向 |
|------|-------|--------|---------|
| **多自定义提供商支持** | [#4305](https://github.com/HKUDS/nanobot/issues/4305) | [#3239](https://github.com/HKUDS/nanobot/pull/3239) | ✅ **即将合并** — 解决多云/多端点接入 |
| **Python SDK 完整度** | — | [#4296](https://github.com/HKUDS/nanobot/pull/4296) | ✅ **待合并** — 提升开发者体验 |
| **会话级自动化调度** | — | [#4299](https://github.com/HKUDS/nanobot/pull/4299) | ✅ **待合并** — Cron 功能现代化 |
| **技能类型检查** | — | [#4300](https://github.com/HKUDS/nanobot/pull/4300) | ✅ **待合并** — 技能兼容性保障 |

### 项目演进信号

- **核心架构优化**：Session 历史清理、MCP 生命周期管理、Cron 异步任务等
- **开发者体验**：SDK 完善、本地 LLM 支持优化、多提供商灵活配置
- **提供商生态**：持续扩展（SiliconFlow 转录、Kimi 联盟链接）
- **项目调整**：移除桌面应用，专注核心智能体引擎

---

## 👥 用户反馈摘要

### 真实用户痛点

1. **多提供商需求** [#4305](https://github.com/HKUDS/nanobot/issues/4305)
   - **场景**：用户需在同一实例中接入多个自定义 OpenAI 兼容 API（内部 API、多云提供商）
   - **现状困境**：当前仅支持单个 `custom` 提供商

2. **本地 LLM 超时问题** [#4020](https://github.com/HKUDS/nanobot/pull/4020)
   - **场景**：LM Studio、Ollama 用户在复杂 prompt 上卡 90s 默认超时
   - **需求**：可配置的流空闲超时，环境变量太不易发现

3. **Linux 沙箱限制** [#4236](https://github.com/HKUDS/nanobot/issues/4236)
   - **场景**：Ubuntu 24.04 LTS 限制非特权用户命名空间，bwrap sandbox 无法工作
   - **当前状态**：问题已关闭（系统级问题，非应用问题）

4. **跨功能兼容性** [#4300](https://github.com/HKUDS/nanobot/pull/4300)
   - **场景**：用户构建基金管理技能，需复用股票数据/新闻技能，但兼容性不清
   - **需求**：技能类型要求检查，避免隐式失败

### 社区满意度信号

- 高 PR 活跃度（18 条/24h）表明维护者响应迅速
- Issue 快速关闭（#4236 仅耗时 4 天）
- 问题 fix PR 同步提交（#4303 与 #4302 同日发布）

---

## ⏳ 待处理积压

### 长期未合并的关键 PR

| PR | 创建日期 | 天数 | 状态 | 优先级 |
|----|---------|----|------|--------|
| [#3239](https://github.com/HKUDS/nanobot/pull/3239) | 2026-04-17 | **56 天** | OPEN | 🔴 **Critical** — 高频用户需求 |
| [#3538](https://github.com/HKUDS/nanobot/pull/3538) | 2026-04-29 | **44 天** | OPEN | 🟠 High — Gateway 运维工具 |
| [#4021](https://github.com/HKUDS/nanobot/pull/4021) | 2026-05-27 | **16 天** | OPEN | 🟠 High — 生产 Bug 修复 |

### 建议行动

1. **立即合并** [#3239](https://github.com/HKUDS/nanobot/pull/3239) 与 [#4303](https://github.com/HKUDS/nanobot/pull/4303) — 解决用户刚需和新崩溃
2. **加快审核** [#4296](https://github.com/HKUDS/nanobot/pull/4296)、[#4299](https://github.com/HKUDS/nanobot/pull/4299)、[#4301](https://github.com/HKUDS/nanobot/pull/4301) — 核心功能完善
3. **关注长期积压** — [#3538](https://github.com/HKUDS/nanobot/pull/3538) 超过 40 天未合并，可能因 scope 分歧，建议主动沟通

---

## 📈 项目健康度评分

| 维度 | 评分 | 备注 |
|------|------|------|
| **活跃度** | ⭐⭐⭐⭐⭐ | 18 PR/24h，维护者高响应 |
| **功能演进** | ⭐⭐⭐⭐⭐ | SDK、Cron、多提供商等多方向推进 |
| **稳定性** | ⭐⭐⭐⭐ | 新 Bug 及时发现和 Fix，MCP/Cron 风险待处理 |
| **社区参与** | ⭐⭐⭐⭐ | 多个贡献者，用户反馈精准 |
| **技术债** | ⭐⭐⭐⭐ | 长期 PR 积压需加快，但无明显代码异味 |

**总体评价：项目处于活跃发展阶段，功能迭代快速

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报
**2026-06-12**

---

## 📊 今日速览

ZeroClaw 项目保持高活跃度，过去24小时共处理 **100 条更新**（50 个 Issues + 50 个 PRs），其中包括重量级 **v0.8.0 正式版发布**。项目存在明显的"质量与扩展性张力"：一方面新版本带来多代理架构、配置重构等核心升级；另一方面高优先级 Bug（特别是安全类和工作流阻塞类）依然积压，表明发布节奏快但稳定性修复滞后。整体评估：**功能驱动型高速迭代，但需要加强基础设施和边界场景的可靠性**。

---

## 🚀 版本发布

### **v0.8.0 - 多代理架构重大升级**

**发布时间**：2026-06-11  
**核心变更**：
- **多命名代理架构**：单个守护进程现支持运行多个命名代理，每个代理独立的：
  - 工作区（workspace）
  - 内存存储（memory）
  - 模型提供商（model provider）
  - 安全策略（security policy）
  - 通道绑定（channels）
  - 个性化配置（personality）
- **配置模式重构**：新的自动迁移架构，已有配置可无缝升级
- 发布受 **[#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)** 版本阻塞追踪指导

**破坏性变更**：
- 配置文件格式变更（自动迁移支持）
- 可能涉及 `[[mcp.servers]]` 数组字段编辑的持久化路径变化 → **[#7519](https://github.com/zeroclaw-labs/zeroclaw/pull/7519)** 修复

**迁移注意**：
1. 首次启动 v0.8.0 时会自动执行配置迁移，建议备份旧配置文件
2. 多代理模式下各代理的 workspace 隔离，工作目录继承逻辑有变 → 参考 **[#7517](https://github.com/zeroclaw-labs/zeroclaw/pull/7517)** 的 ACP 会话 cwd 修复
3. Dashboard 构建方式变更 → 使用 `cargo web build` 作为标准入口 **[#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523)**

---

## 📈 项目进展

### 合并/关闭的关键 PR（过去24小时）

| PR | 状态 | 类型 | 影响 |
|-------|--------|--------|---------|
| **[#7517](https://github.com/zeroclaw-labs/zeroclaw/pull/7517)** | ✅ 已合并 | fix(runtime/subagent) | **修复 ACP 会话中子代理 cwd 继承失败** → 解决多代理协作的工作目录隔离问题 |
| **[#7519](https://github.com/zeroclaw-labs/zeroclaw/pull/7519)** | ✅ 已合并 | fix(config) | **修复 MCP 服务器配置的增量持久化** → 单字段编辑不再丢失数组元素 |
| **[#7520](https://github.com/zeroclaw-labs/zeroclaw/pull/7520)** | ✅ 已合并 | fix(ci) | **修复 ARM glibc 版本构建** → v0.8.0 发布流程关键修复 |
| **[#6443](https://github.com/zeroclaw-labs/zeroclaw/issues/6443)** | ✅ 已关闭 | feat(channel:twitch) | **Twitch 聊天频道支持** → IRC 适配器完成 |
| **[#7263](https://github.com/zeroclaw-labs/zeroclaw/issues/7263)** | ✅ 已关闭 | fix(agent) | **ACP 会话 cwd 继承修复** → 子代理开发模式解锁 |

**项目推进量**：v0.8.0 发布标志着多代理架构可用，但同步合并的是 3 个基础修复（配置、CI、运行时）。**稳定性追赶节奏相对较慢**——47 个待合并 PR 中仍有大量高优先级 Bug 待修复。

---

## 🔥 社区热点

### 评论最活跃的议题（前5）

1. **[#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699) - MCP 工具过滤失效** ⭐ 7 条评论
   - **症状**：`tool_filter_groups` 配置对真实 MCP 工具无效，前缀检查 Bug + 延迟加载未集成
   - **优先级**：P1（高）| **标签**：bug, runtime, tool, tool:mcp
   - **背后诉求**：多代理场景下的工具访问控制未生效，安全策略被绕过

2. **[#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470) - 代理委派模式安全策略冲突** ⭐ 7 条评论
   - **症状**：代理委派（delegate mode）拒绝空的 `risk_profile.allowed_tools`，且相同配置下位无法隔离不同权限代理
   - **优先级**：P1（S1）| **标签**：bug, security, tool:delegate
   - **背后诉求**：多代理评审/研究工作流被阻塞，安全隔离机制设计有漏洞

3. **[#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112) - v0.8.0 版本追踪器** ⭐ 3 条评论（已关闭）
   - **作用**：v0.8.0 发布的里程碑协调中心，配置 & 工具解析稳定化、运行时提供商正确性
   - **已关闭**：表示版本发布计划已完成交付

4. **[#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) - WSL2 连续 OOM** ⭐ 4 条评论
   - **症状**：WSL2 环境下守护进程频繁被内存不足杀死
   - **优先级**：P1（S0 数据丢失风险）| **标签**：bug, runtime, r:needs-repro
   - **背后诉求**：Windows 开发环境稳定性，内存管理优化

5. **[#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) - Gemini 400 对话历史序列化违规** ⭐ 4 条评论
   - **症状**：向 Gemini API 发送的对话历史在首个用户消息前含有助手工具调用，违反协议
   - **优先级**：P1 | **标签**：bug, provider:gemini, agent:loop
   - **背后诉求**：多提供商兼容性，历史序列化规则硬编码

### PR 焦点（新功能）

- **[#7490](https://github.com/zeroclaw-labs/zeroclaw/pull/7490) + [#7489](https://github.com/zeroclaw-labs/zeroclaw/pull/7489)** - Discord 斜杠命令动态生成
  - 基于技能自动生成 Discord `/command` 语法
  - 无需公开 HTTPS 端点，仅 WebSocket 通信
  - **体现趋势**：支持多频道、多格式的 UX 适配

---

## 🐛 Bug 与稳定性

### 按严重程度排列（P1 优先级）

| Issue | 严重性 | 状态 | Fix PR | 摘要 |
|-------|--------|--------|---------|--------|
| **[#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699)** | P1 | 进行中 | ❌ 无 | MCP 工具过滤器前缀匹配 Bug + 延迟加载未集成 |
| **[#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)** | P1/S1 | 已接受 | ❌ 无 | 代理委派的空工具列表拒绝 & 权限隔离失败 |
| **[#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)** | P1/S0 | 进行中 | ❌ 无 | WSL2 连续 OOM，数据丢失风险 |
| **[#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302)** | P1 | 进行中 | ❌ 无 | Gemini 对话历史违反协议（助手消息在用户前） |
| **[#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)** | P1 | 已接受 | ❌ 无 | 默认 32k 上下文预算在首轮就被系统提示 + 工具定义爆满 |
| **[#6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914)** | P1 | 已阻塞 | ❌ 无 | `allowed_tools` / `denied_tools` 未在代理循环执行时强制 |
| **[#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434)** | P1 | 进行中 | ❌ 无 | Shell 工具在 `autonomy.level=full` 被拒（从未到达运行时） |
| **[#6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350)** | P1 | 进行中 | ❌ 无 | WhatsApp Web LID 联系人绕过允许号码列表（静默丢弃） |
| **[#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361)** | P1 | 进行中 | ❌ 无 | 上下文压缩丢弃 OpenAI 兼容提供商的助手工具调用 & 工具结果 |
| **[#7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523)** | P1 | 新报告 | ❌ 无 | **v0.8.0 Dashboard 不可用** → macOS Homebrew 安装后无前端构建 |

### 关键数据
- **P1/高优先级 Bug 总数**：17 条（待合并 PR 中仅 3 条涉及 Bug 修复）
- **工作流阻塞类（S1）**：8 条
- **数据丢失风险（S0）**：1 条（WSL2 OOM）
- **未有 Fix PR 的 P1 Bug**：12 条（≈70%）

**稳定性评估**：v0.8.0 发布虽带来架构升级，但基础 Bug 积压严重。特别是安全相关（工具过滤、权限隔离）和多提供商兼容性的修复均未交付，存在较高的生产风险。

---

## ✨ 功能请求与路线图信号

### 新功能需求（过去24小时报告）

| Issue | 优先级 | 状态 | 关联 PR | 备注 |
|-------|--------|--------|---------|--------|
| **[#6312](https://github.com/zeroclaw-labs/zeroclaw/issues/6312)** | P2 | 进行中 | [#7297](https://github.com/zeroclaw-labs/zeroclaw/pull/7297) | Gateway 按别名的 Webhook 路由（已有按代理查询参数方案，本需求另辟蹊径） |
| **[#6391](https://github.com/zeroclaw-labs/zeroclaw/issues/6391)** | P2 | 阻塞 | ❌ | 守护进程节点真实心跳追踪（Online/Stale/Offline） |
| **[#6390](https://github.com/zeroclaw-labs/zeroclaw/issues/6390)** | P2 | 开放 | ❌ | `zeroclaw node add <url>` CLI 注册远程守护进程 |
| **[#6346](https://github.com/zeroclaw-labs/zeroclaw/issues/6346)** | P2 | 开放 | 部分实现 | CLI + Dashboard 节点健康 & 管理（与 #6391 关联） |
| **[#6365](https://github.com/zeroclaw-labs/zeroclaw/issues/6365)** | P2 | 进行中 | ❌ | Dashboard "更新 ZeroClaw" 按钮（暴露 CLI 更新流程） |
| **[#6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642)** | P2 | 进行中 | [#6190](https://github.com/zeroclaw-labs/zeroclaw/pull/6190) | OpenTelemetry 中捕获完整提示/补全（gen_ai.input.messages） |

### 路线图信号总结

1. **多代理基础设施**（v0.8.0 已交付）
   - ✅ 配置重构、多命名代理
   - ⏳ **下一阶段**：节点健康追踪、远程注册 CLI、Dashboard 管理界面

2. **安全 & 工具管理**（关键堵点）
   - 🔴 工具过滤、权限隔离 Bug 未修复
   - ⏳ 需要优先级调整，建议提升至 v0.8.1 紧急修复

3. **可观测性**（持续迭

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报
**日期：2026-06-12** | **数据周期：过去24小时**

---

## 📊 今日速览

PicoClaw 项目今日保持高活跃度，24小时内新增 **7 条 Issue（含4条新开/活跃）、31 条 PR（待合并13条，已合并/关闭18条）**，以及 **1 个 Nightly 版本发布**。PR 合并速度显著，说明核心维护团队处理效率高。Issue 中既有跨平台兼容性问题（Windows 路径分隔符）、视觉模型幻觉、消息去重等功能性缺陷，也有安全漏洞（CIDR 绕过），反映项目在稳定性和功能完整性方面仍有改进空间。整体活跃度评估：**优秀** ✅

---

## 🚀 版本发布

**v0.2.9-nightly.20260612.413d3749** 
- **类型**：Nightly Build（自动化构建，可能不稳定）
- **对比范围**：[v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **特征**：自动每日构建，包含最新主分支代码
- **建议**：仅供开发/测试环境使用，生产环境应等待正式 GA 版本

---

## ✅ 项目进展

### 已合并/关闭的关键 PR（18 条）

| PR # | 标题 | 作者 | 影响 |
|------|------|------|------|
| #2957 | fix(channels): prevent tool_calls from being dropped during streaming | @loafoe | 🔴 **HIGH**：修复流式传输中 tool_calls 消息被错误过滤的问题，恢复工具调用可靠性 |
| #2955 | fix: verify process identity in singleton PID check | @yuxuan-7814 | 🟡 **MEDIUM**：启动失败修复，PID 文件验证增强，防止进程重用冲突 |
| #2947 | fix: correct claude-sonnet-4.6 model ID to use hyphens | @yuxuan-7814 | 🟡 **MEDIUM**：Anthropic 模型 ID 正确性修复，消除 HTTP 404 错误 |
| #2934 | fix(channels): allow whatsapp native mode with use_native flag | @dtapps | 🟡 **MEDIUM**：WhatsApp 原生模式支持，扩展通道覆盖 |
| #2696 | feat(mcp): support per-request dynamic headers from channel context | @loafoe | 🟢 **FEATURE**：MCP 服务器动态请求头支持，增强集成灵活性 |
| #3060 | fix: use %w for error wrapping and handle json.MarshalIndent error | @chengzhichao-xydt | 🔵 **CODE QUALITY**：错误处理改进，增强可调试性 |
| #3067 | fix: add DmScope field to SessionConfig to persist dm_scope setting | @SiYue-ZO | 🟡 **MEDIUM**：会话隔离范围持久化修复，UI 配置不再丢失 |

**依赖更新（Automated Merge）**：8 条依赖更新 PR 已合并（AWS SDK v2、Go Sync、MCP SDK、ESLint、Vite 等），保持依赖树最新。

### 项目整体推进
- **聚焦方向**：流式处理稳定性（#2957）、进程管理（#2955）、模型兼容性（#2947）、配置持久化（#3067）
- **代码质量**：错误处理规范化（%w 包装、异常捕获）正在推进
- **生态扩展**：MCP 动态头支持为后续 AI 模型、外部服务集成铺路

---

## 💬 社区热点

### 高关注 Issue

**🌟 #2984** - [Feature] Add explicit turn completion signal for Pico WebSocket clients  
- **作者**：@Brook-sys | **反应**：2 👍 | **评论**：2 条
- **状态**：OPEN（刚提出 10 天，已更新）
- **核心诉求**：WebSocket 客户端需显式的"代理处理完成"信号，当前缺乏确定性判断时机
- **影响范围**：所有使用 Pico 协议的外部客户端（Web UI、移动应用等）
- **链接**：[Issue #2984](https://github.com/sipeed/picoclaw/issues/2984)

**⚠️ #3094** - [Bug] 异步子代理(spawn)任务完成时，ForUser字段导致重复消息  
- **作者**：@v2up-32mb | **反应**：0 👍 | **评论**：1 条
- **状态**：OPEN（刚提出 2 天）
- **关键问题**：Spawn 派发子代理任务完成后，飞书/Telegram 同时收到两条相同内容消息（原始 + 汇总）
- **根源**：ForUser 字段同时用于直接推送和主代理汇总
- **影响面**：多通道场景，严重影响用户体验
- **链接**：[Issue #3094](https://github.com/sipeed/picoclaw/issues/3094)

**🔍 #3108** - [BUG] Image description requests hallucinate when active model lacks vision support  
- **作者**：@afjcjsbx | **反应**：0 👍 | **评论**：0 条
- **状态**：OPEN（刚提出）
- **现象**：使用文本模型（如 deepseek-v4-flash）描述图像时，图像被加载但最终答案无关
- **根源**：模型选择未考虑视觉能力的约束
- **链接**：[Issue #3108](https://github.com/sipeed/picoclaw/issues/3108)

---

## 🐛 Bug 与稳定性

### 按严重程度排列

| 优先级 | Issue # | 标题 | 状态 | Fix PR | 影响 |
|--------|---------|------|------|--------|------|
| 🔴 **CRITICAL** | #2472 | Windows 路径分隔符不兼容导致 `list_dir` 返回"invalid argument" | OPEN | ❌ 无 | 文件操作在 Windows 上完全失效 |
| 🔴 **CRITICAL** | #3080 | PicoClaw launcher `allowed_cidrs` 可被本机环回代理绕过 | CLOSED | ✅ #2955 相关 | 安全漏洞：首次运行时 CIDR 限制可被绕过 |
| 🟠 **HIGH** | #3094 | Spawn 子代理消息重复 | OPEN | ❌ 无 | 多通道用户体验严重下降 |
| 🟠 **HIGH** | #3108 | 无视觉模型时图像描述幻觉 | OPEN | ❌ 无 | AI 能力约束不足 |
| 🟡 **MEDIUM** | #2958 | 连续请求中 tool_calls 消息丢失（Pico Channel） | CLOSED | ✅ #2957 | 工具调用可靠性缺陷 |
| 🟡 **MEDIUM** | #2954 | 不支持 32 位 Android 系统 | CLOSED | ❌ 无 | Android 客户端覆盖面受限 |

### 待修复的关键路径
1. **#2472**（Windows 路径）- 影响所有 Windows 用户的文件操作，**建议高优先级处理**
2. **#3094**（消息重复）- 生产环境直接影响用户信任度

---

## 🎯 功能请求与路线图信号

### 已有进行中的功能开发

| 特性 | PR # | 作者 | 状态 | ETA 信号 |
|------|------|------|------|---------|
| **Agent Collaboration Bus** | #2937 | @afjcjsbx | OPEN | 邮箱、协作线程、权限模型，架构设计完整 |
| **MCP 参数解析增强** | #3048 | @afjcjsbx | OPEN | 修复 `--no-color` 等根级标志泄露 |
| **Channel 配置合并** | #2956 | @yuxuan-7814 | OPEN | security.yml 与 config.json 合并逻辑修复 |

### 用户新需求
- **#2984**：Pico WebSocket 完成信号 - 用户希望更清晰的协议语义，便于客户端决策树设计
- **Implicit**：跨平台兼容性需求呼声高（Windows、Android 32bit），表明用户群体多样化

### 路线图推测
- **中期**（v0.3.x）：Agent Collaboration 完成、MCP 增强、跨平台修复
- **长期**：更完善的模型能力匹配（视觉模型自动选择）、协议标准化

---

## 👥 用户反馈摘要

### 真实痛点梳理

| 痛点类型 | Issue | 用户群体 | 满意度 |
|---------|-------|---------|--------|
| **跨平台兼容性** | #2472, #2954 | Windows/Android 用户 | ⭐⭐ 低 |
| **消息可靠性** | #2958, #3094 | 多通道集成用户 | ⭐⭐⭐ 中等 |
| **协议清晰度** | #2984 | WebSocket 客户端开发者 | ⭐⭐⭐⭐ 中高 |
| **AI 能力约束** | #3108 | 轻 RAG 应用用户 | ⭐⭐⭐ 中等 |
| **配置持久化** | #3067 | Web UI 用户 | ⭐⭐⭐⭐ 中高 |

### 使用场景洞察
1. **多通道集成方**：飞书、Telegram、WhatsApp 混用，对消息顺序和去重敏感
2. **跨平台部署方**：Windows Server、Android 终端部署，对兼容性要求高
3. **WebSocket 客户端开发**：需要明确的状态机和信号定义
4. **AI 能力组合**：文本+视觉模型混合场景，自动能力选择需求

### 社区情绪
- **维护者响应速度**：快速（多数 Issue 24h 内有反应或更新）✅
- **PR 审核效率**：高（18/31 已合并/关闭，待审 13）✅
- **透明度**：良好（Bug、Feature、Security 标签清晰）✅

---

## 📋 待处理积压

### 长期待响应的重要 Issue

| Issue # | 标题 | 创建日期 | 天数 | 状态 | 优先级 |
|---------|------|---------|------|------|--------|
| #2472 | Windows 路径分隔符 | 2026-04-10 | **63 天** | OPEN，有评论 | 🔴 CRITICAL |
| #2954 | 32 位 Android 支持 | 2026-05-27 | **16 天** | CLOSED（标记为 stale） | 🟡 MEDIUM |
| #2984 | WebSocket 完成信号 | 2026-06-02 | **10 天** | OPEN，社区关注 | 🟠 HIGH |

### 待合并的关键 PR（13 条）

最值得关注的：
- **#2937** (Agent Collaboration) - 架构复杂，可能需要多轮审查
- **#3107** (Copilot SDK v0.2→v1.0 bump) - 大版本升级，需验证兼容性
- **#3048** (MCP 参数解析) - 修复但可能涉及向后兼容性评估

### 维护者关注建议
1. ⏰ **#2472** 已积压 63 天，应列为 sprint 优先项（评估是否阻塞其他工作）
2. 📦 **大版本依赖更新**（#3107 Copilot SDK v1.0）应明确发布周期规划
3. 🔄 **Agent Collaboration** 的审查复杂度高，建议分阶段合并或进行架构同步会议

---

## 📈 数据看板

```
过去24小时统计：
├─ Issues: 7 条（新开4 + 已关4 = 8 处理）
├─ PRs: 31 条（合并/关闭18 + 待审13）
├─ 版本发布: 1 个 (Nightly)
├─ 平均 PR 合并时间: ~3-10 天
├─ 安全漏洞: 1 个 (已关闭)
└─ 功能中断: 2 个 (Windows + Spawn 消息)
```

---

**报告生成时间**：2026-06-12 | **数据来源**：GitHub API | **下次更新**：2026-06-13

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报
**日期：2026-06-12** | **数据统计周期：过去24小时**

---

## 📊 今日速览

NanoClaw 展现出**高度活跃的开发节奏**。过去24小时内合并/关闭 9 条 PR、新增 5 条待审 PR，代码改进覆盖核心系统架构（消息投递、会话管理、容器生命周期）、多渠道集成（Signal 反应系统）、以及运维工具链（设置流程、健康审计修复）。项目维护团队表现出**高效的问题响应和迭代速度**，同时也反映出系统在**规模化运维和多代理协调**方面仍在打磨。

---

## 🚀 项目进展

### 已合并/关闭的关键 PR（9 条）

#### 🔧 **核心稳定性修复（4 条）**

1. **[#2738] fix(session-manager): writeOutboundDirect 只读模式 Bug** 
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2738
   - **影响**：修复 `outbound.db` 被以只读模式打开，导致命令控制网关（command-gate）的拒绝响应无法投递的严重 Bug
   - **问题根源**：`writeOutboundDirect()` 调用 `openOutboundDb(readonly: true)`，后续 INSERT 操作必然失败，错误被 finally 块吞没
   - **关联 Issue**：[#2495](https://github.com/nanocoai/nanoclaw/issues/2495)（已关闭）

2. **[#2736] fix(host-sweep): 容器启动后的 stale processing claims 宽限期**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2736
   - **影响**：修复新唤醒容器的陈旧处理声明（processing claims）导致的任务丢失/重复问题

3. **[#2735] fix(chat-sdk-bridge): 记录批准卡片的执行用户**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2735
   - **影响**：完善审批流程的审计追踪

4. **[#2741] fix(setup): 自动将握手上下文作为首条用户消息提交给 Claude**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2741
   - **影响**：修复交互式设置流程中 Claude 无法激活的问题（之前通过 `--append-system-prompt` 传递，Claude 需要用户消息才会响应）

#### 🎯 **架构增强与新功能（5 条）**

5. **[#2733] feat(channels): 原生 channel-instance 维度 — 多机器人基础设施**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2733
   - **意义**：为多机器人部署铺平道路，引入 channel 多实例支持

6. **[#2734] feat(delivery): getDeliveryAction 读侧实现**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2734
   - **意义**：完善消息投递动作注册表的查询能力

7. **[#2737] feat(approvals): 批准解决回调注册表 — 模块式观察者模式**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2737
   - **意义**：提升批准流程的模块化度和可扩展性

8. **[#2739] feat(webhook-server): 原始路由注册表 — 非 Chat-SDK webhooks 成为可选项**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2739
   - **意义**：扩展 webhook 生态，支持自定义集成

9. **[#2740] feat(container): 每组空闲超时 — 临时会话的优雅退出**
   - 链接：https://github.com/nanocoai/nanoclaw/pull/2740
   - **意义**：优化资源利用，支持按组配置容器生命周期

---

## 🔴 Bug 与稳定性

### 严重级别问题

| Issue | 标题 | 状态 | Fix PR | 严重度 |
|-------|------|------|--------|--------|
| [#2495](https://github.com/nanocoai/nanoclaw/issues/2495) | writeOutboundDirect 只读模式，命令控制拒绝无法投递 | ✅ 已关闭 | [#2738](https://github.com/nanocoai/nanoclaw/pull/2738) | **P0** |
| [#2743](https://github.com/nanocoai/nanoclaw/pull/2743) | wirings create 跳过 agent_destinations 副作用，新聊天消息被丢弃 | 🟡 待审 | - | **P0** |

### 中等级别问题

| 类别 | 描述 | 链接 | 状态 |
|------|------|------|------|
| Signal 适配器 | 反应系统（add_reaction）被静默丢弃，代理和入站反应信封都无法处理 | [#2744](https://github.com/nanocoai/nanoclaw/pull/2744) | 🟡 待审 |
| 容器健康 | Docker Desktop drvfs 崩溃循环（exit 127）、并发容器限制缺失、daemon kill 降级 | [#2732](https://github.com/nanocoai/nanoclaw/pull/2732) | 🟡 待审 |

**总体评估**：今日修复聚焦于消息投递链路的关键节点（outbound.db 访问、wiring 创建副作用、Signal 反应处理），反映出**多代理消息系统的脆弱点正在被系统性强化**。

---

## 🎯 社区热点

### 最活跃讨论

**[#1356] Agent memory system redesign** 
- 作者：@Ordinath | 链接：https://github.com/nanocoai/nanoclaw/issues/1356
- **创建**：2026-03-23 | **最后活动**：2026-06-11
- **参与度**：2 条评论 | 👍 6 个赞
- **诉求分析**：
  - 当前内存系统（MEMORY.md 索引 + satellite markdown）在小规模（~54 文件、~83 KB）有效，但**缺乏垂直扩展能力**
  - 问题跟踪了研究发现和更全面、可扩展的代理内存系统的重新设计方案
  - 这是一个**架构级需求**，涉及长期知识管理和多轮对话的连贯性
  - **影响范围**：所有需要持久化学习的多代理部署

---

## 📋 功能请求与路线图信号

### 即将进入下一版本的功能（基于已合并 PR）

| 功能 | 来源 PR | 预期影响 | 优先级 |
|------|---------|---------|--------|
| 多机器人通道隔离 | [#2733](https://github.com/nanocoai/nanoclaw/pull/2733) | 支持单部署多租户 | P1 |
| 消息投递动作读侧 | [#2734](https://github.com/nanocoai/nanoclaw/pull/2734) | 增强可观测性 | P2 |
| Signal 反应系统完善 | [#2744](https://github.com/nanocoai/nanoclaw/pull/2744) | 多渠道集成深化 | P1 |
| 基于组的资源生命周期 | [#2740](https://github.com/nanocoai/nanoclaw/pull/2740) | 成本优化 | P2 |

### 未来方向信号

**PR Factory 配方** ([#2742](https://github.com/nanocoai/nanoclaw/pull/2742)) - 这是一份**发布配方**，展示了如何利用 NanoClaw 构建 PR 审查、分类、测试的自动化工作流。反映出项目正在从**代理框架**向**行业场景模板库**演进。

---

## 👥 用户反馈摘要

### 核心痛点（来自 Issues）

1. **大规模多代理部署中的消息投递可靠性**（Issue [#2495](https://github.com/nanocoai/nanoclaw/issues/2495)、PR [#2743](https://github.com/nanocoai/nanoclaw/pull/2743)）
   - 用户发现消息被无声地丢弃，难以调试
   - 根本原因跨越数据库访问模式和 ORM 层的隐含副作用

2. **代理长期记忆的扩展性**（Issue [#1356](https://github.com/nanocoai/nanoclaw/issues/1356)）
   - markdown 文件系统在代理知识库增长后面临性能和一致性问题
   - 用户需要一个更有结构化、可查询的内存层

3. **多渠道集成的完整性**（PR [#2744](https://github.com/nanocoai/nanoclaw/pull/2744)）
   - Signal 用户报告反应（reactions）无法工作
   - 适配器层与核心消息系统的消息类型不对齐

4. **容器级健康与恢复**（PR [#2732](https://github.com/nanocoai/nanoclaw/pull/2732)）
   - 关键的崩溃循环（Docker Desktop 兼容性）和资源泄漏问题
   - 对生产多代理部署构成风险

---

## ⏳ 待处理积压

### 长期未关闭但活跃的需求

| Issue | 标题 | 创建日期 | 天数 | 优先级信号 |
|-------|------|---------|------|----------|
| [#1356](https://github.com/nanocoai/nanoclaw/issues/1356) | Agent memory system redesign | 2026-03-23 | **81 天** | 🔴 高频讨论，涉及架构重构 |

**维护者提示**：
- **#1356** 虽未关闭但已获得 6 个赞且有 2 条评论，表明用户强烈关注。建议：
  - 在下个 milestone 中将其分解为具体子任务（如"内存层 KV 存储接口"、"向量化检索原型"）
  - 发起 RFC 或架构讨论（如果尚未进行），争取社区反馈
  - 考虑在 v2.0 之前交付 MVP 版本

### 待审 PR 积压（5 条）

所有 5 条待审 PR 均于 **2026-06-11 创建**，尚未超过 24 小时：
- [#2744](https://github.com/nanocoai/nanoclaw/pull/2744) - Signal 反应修复（阻塞用户功能）
- [#2743](https://github.com/nanocoai/nanoclaw/pull/2743) - wiring 创建 Bug 修复（P0 稳定性）
- [#2742](https://github.com/nanocoai/nanoclaw/pull/2742) - PR Factory 配方（新示例）
- [#2732](https://github.com/nanocoai/nanoclaw/pull/2732) - 容器健康加固（安全审计）
- [#2685](https://github.com/nanocoai/nanoclaw/pull/2685) - Signal 文档更新（待审 8 天）

**建议优先级**：#2743 和 #2744（消息投递关键路径）> #2732（安全）> #2742（文档） > #2685（文档）

---

## 📈 项目健康度评分

| 维度 | 评分 | 说明 |
|------|------|------|
| **开发活跃度** | ⭐⭐⭐⭐⭐ | 24h 内 14 条 PR，9 条已合并，高效迭代 |
| **Bug 响应速度** | ⭐⭐⭐⭐ | 核心问题（#2495）24h 内提出、修复、合并 |
| **架构演进** | ⭐⭐⭐⭐ | 多机器人、消息投递、生命周期管理同步推进 |
| **文档与通信** | ⭐⭐⭐ | 配方和 PR 总结清晰，但长期需求（#1356）缺乏明确里程碑 |
| **用户反馈纳入** | ⭐⭐⭐⭐ | 快速响应多渠道问题，但内存系统重构仍在研究阶段 |

**总体评估**：🟢 **健康且高速发展** | 建议关注多代理系统的复杂性增长与文档/测试的同步覆盖。

---

**日报生成时间**：2026-06-12 | **下次更新**：2026-06-13

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报
**日期：2026-06-12** | **数据周期：过去24小时**

---

## 📊 今日速览

IronClaw 项目保持高度活跃，过去24小时共更新 **78 条 Issue 和 PR**（Issues: 31条，PR: 47条）。其中 **Reborn WebUI v2** 相关工作成为焦点，15+ 个前端 Bug 密集报告和修复，反映出本地开发体验迭代已进入"稳定化阶段"。合并的 4 个关键 PR（包含 Logs 页面接入、批量 UI 修复、生产就绪认证）表明项目在 **生产就绪和本地体验** 两条线并行推进，整体健康度评估为 **高活跃+高质量**。

---

## 🚀 版本发布

**无新版本发布**（过去24小时）

待发布状态：
- **[#3708](https://github.com/nearai/ironclaw/pull/3708)** | `chore: release` PR 仍待合并
  - 计划发布：`ironclaw_common` 0.4.2 → 0.5.0（⚠️ API breaking changes）
  - `ironclaw` 0.24.0 → 0.29.1
  - `ironclaw_safety` 0.2.2 → 0.2.3
  - **风险**：包含 `ironclaw_common` 破坏性变更，需关注迁移指南

---

## 🎯 项目进展

### 已合并/关闭的关键 PR（4条）

| PR | 标题 | 影响范围 | 状态 |
|---|---|---|---|
| **[#4760](https://github.com/nearai/ironclaw/pull/4760)** | Wire WebUI v2 operator logs | 可观测性、CI | ✅ CLOSED |
| **[#4786](https://github.com/nearai/ironclaw/pull/4786)** | promote main to qa branch | 流程/CI | ✅ CLOSED |
| **[#4757](https://github.com/nearai/ironclaw/pull/4757)** | open, watch, approve triggered automation runs | WebUI 自动化工作流 | ✅ CLOSED |
| **[#4782](https://github.com/nearai/ironclaw/pull/4782)** | fix(reborn): unify outbound state store for Slack delivery | Slack 集成 | ✅ CLOSED |

**核心进展**：
- ✅ **实时日志系统上线**：WebUI v2 Logs 页面从空壳变为真实数据源，支持 level/target 过滤、秘密脱敏、有界历史记录
- ✅ **Automation 工作流修复**：触发运行现可从 Automations 页面直接打开、观察和审批
- ✅ **Slack 交付一致性**：修复了 WebUI 配置的 Slack DM 默认值未能到达 triggered-run 的问题

**累计贡献者：** @danielwpz, @henrypark133, @serrrfirat 等核心团队

---

## 💬 社区热点

### 评论最活跃的 Issues（TopN）

| Issue | 作者 | 评论数 | 核心关注点 | 链接 |
|---|---|---|---|---|
| **#3036** [EPIC] Configuration-as-Code for Reborn | @ilblackdragon | 7 | tenant blueprints, 声明式配置 | [#3036](https://github.com/nearai/ironclaw/issues/3036) |
| **#4766** Chat runtime 未使用 UI 保存的凭证 | @sunglow666 | 2 | 凭证持久化 BUG | [#4766](https://github.com/nearai/ironclaw/issues/4766) |
| **#4703** NEAR AI 模型选择器保存显示名而非 ID | @sunglow666 | 2 | 数据一致性 BUG | [#4703](https://github.com/nearai/ironclaw/issues/4703) |

### 最热 PR 讨论（TOP3）

| PR | 标题 | 关注度信号 |
|---|---|---|
| **[#4772](https://github.com/nearai/ironclaw/pull/4772)** | Reborn WebChat v2 UI 批量修复 | 汇总 8+ 前端 Bug，业界最佳实践（#4703, #4748, #4748 etc.） |
| **[#4588](https://github.com/nearai/ironclaw/pull/4588)** | 可观测性基础设施：轨迹观察器 + LLM 注入 | 为 nearai-bench 提供与旧系统对等的驱动能力 |
| **[#4769](https://github.com/nearai/ironclaw/pull/4769)** | Reborn QA E2E 测试套件（22 新测试） | 无外部依赖的确定性测试（无需密钥、Docker） |

**背后诉求**：
- **生产就绪验证**：多个 Epic (#3026, #4775) 环绕"生产就绪"，体现对稳定性的执着
- **本地开发体验**：密集的前端 Bug 反映用户在本地快速迭代的痛点
- **自动化和可观测**：从日志、测试、配置管理的需求看，项目在向"零人工"运维演进

---

## 🐛 Bug 与稳定性

### 按严重程度分类（24个待处理 Bug）

#### 🔴 **高严重度**（影响核心功能）
| Issue | 标题 | 现象 | Fix Status |
|---|---|---|---|
| **#4761** | Agent 重复工具失败后停止而非恢复 | 工具调用链中断 | ⏳ 无 Fix PR |
| **#4751** | 大响应请求失败（工具参数超 16384B） | 长文本生成崩溃 | ⏳ 无 Fix PR |
| **#4762** | 工具失败导致后续消息和活动顺序混乱 | 状态不一致 | ⏳ 无 Fix PR |
| **#4783** | 无凭证 WASM 扩展在 local-dev 中分发失败（network obligation） | 扩展不可用 | ⏳ 无 Fix PR |

#### 🟡 **中严重度**（影响体验但可绕过）
| Issue | 标题 | 现象 | Fix Status |
|---|---|---|---|
| **#4766** | Chat runtime 未持久化 UI 保存凭证 | 重启丢失配置 | ✅ PR #4772 包含修复 |
| **#4703** | 模型选择器保存显示名非 ID | 配置不可用 | ✅ PR #4772 包含修复 |
| **#4770** | 刷新后工具活动停止更新（SSE 重连问题） | 前端卡住 | ⏳ 无 Fix PR |
| **#4759** | Workspace 路径在相对路径中重复 | 路径错误 | ⏳ 无 Fix PR |
| **#4764** | 拒绝 Shell 审批导致悬挂+无反馈 | UX 死角 | ⏳ 无 Fix PR |

#### 🟢 **低严重度**（UX/文案问题）
| Issue | 标题 | Fix Status |
|---|---|---|
| **#4748** | Code block Wrap/No Wrap 切换无效 | ⏳ 无 Fix PR |
| **#4750** | Workspace 文件从 WebUI 不可发现 | ⏳ 无 Fix PR |

### 稳定性趋势
- **报告速度 > 修复速度**：24h 新增 16 个 Bug，合并仅 2 个 Bug 修复
- **Reborn WebUI v2 质量**：密集的前端 Bug 反映出本地版本号可能未达 RC 级别
- **高优先级阻塞**：#4761（工具恢复）、#4751（长文本）亟需关注

---

## ✨ 功能请求与路线图信号

### 新增需求（按优先级）

| Issue | 类型 | 来源 | 预期迭代 |
|---|---|---|---|
| **#3036** | [EPIC] Configuration-as-Code | @ilblackdragon (core) | 📅 P2，关键 Reborn 特性 |
| **#4775** | [EPIC] Reborn 二进制自动化 QA | @serrrfirat (core) | 📅 积极推进中（#4769 已 PR） |
| **#4776** | 全局 Always Allow 工具开关 | @think-in-universe (core) | 📅 小功能，本地体验优化 |
| **#4771** | Run/Thread 作用域日志过滤 | @danielwpz (core) | 📅 Post #4760 follow-up |

### 已在 PR 中推进的路线图工作

| 功能 | 对应 Issue | PR 状态 | 预计周期 |
|---|---|---|---|
| **WebChat v2 UI 稳定性** | #4692 (parent) | ✅ #4772 (XL merge ready) | 本迭代闭环 |
| **Reborn 生产就绪验证** | #3026 (parent) | ✅ #4763 关闭认证 | 本迭代闭环 |
| **扩展激活与 OAuth 加固** | #4715 | ✅ #4744 已合并 | ✓ 完成 |
| **可观测性基础设施** | N/A | ⏳ #4588 (L 待审) | 下迭代 |
| **Tenant 沙箱与自建扩展** | #3026 | ⏳ #4785 (doc 草稿) | 后续迭代 |

---

## 👥 用户反馈摘要

### 真实用户痛点（来自 @sunglow666 的密集反馈）

**主题 1：配置持久化与凭证管理**
- 💭 "为什么重启后凭证丢失？" → #4766 问题根源：UI 保存路径与 runtime 读取路径不同步
- 💭 "模型选择器为啥保存了显示名？" → #4703 问题根源：前后端字段映射错误

**主题 2：工具调用的鲁棒性**
- 💭 "工具失败就再也用不了？" → #4761 问题根源：Agent 没有重试/恢复机制
- 💭 "拒绝了 shell 请求，之后就卡住了" → #4764 问题根源：denial path 无状态更新

**主题 3：信息可见性**
- 💭 "我创建的文件去哪了？" → #4750 问题根源：WebUI 缺乏文件浏览器
- 💭 "为什么刷新后工具更新停了？" → #4770 问题根源：SSE 重连机制薄弱

**主题 4：大模型兼容性**
- 💭 "长文本生成为什么报错？" → #4751 问题根源：16KB 工具参数限制未考虑 response size

### 用户满意度信号
- ✅ **扩展系统体验改善**：#4744 OAuth 加固后反馈面向上升
- ✅ **Automation 工作流**：#4757 修复后可用性显著提升
- ❌ **本地首次运行体验**：#4692 (parent epic) 仍有 12+ 子 issue 待闭环

### 访问来源分析
- **核心贡献者反馈**：@sunglow666, @think-in-universe 代表本地测试团队
- **新用户反馈缺失**：无外部用户 Issue（GitHub Discussions 或 Forum 数据未提供）
- **企业级需求出现**：#3036 Configuration-as-Code EPIC 指向多租户/企业部署场景

---

## ⏳ 待处理积压

### 长期未响应的重要 Issue（>24h 无活动）

| Issue | 创建日期 | 天数 | 优先级信号 | 现状 |
|---|---|---|---|---|
| **#4692** | 2026-06-10 | 2天 | 🔴 PARENT EPIC | 12 个子 issue，主体仍开放 → 建议分配 owner |
| **#4775** | 2026-06-11 | 1天 | 🔴 EPIC (e2e-coverage) | 未认领，但 #4769 PR 已推进 → 建议链接 |
| **#4783** | 2026-06-11 | 1天 | 🟠 阻塞扩展系统 | 无评论，技术细节复杂 → 需要专家评审 |
| **#4761** | 2026-06-11 | 1天 | 🟠 工具恢复机制 | 无 Fix PR，高优先级 → 建议优先处理 |
| **#3036** | 2026-04-28 | 45天 | 🔴 EPIC (reborn-blocker) | 7 评论但无合并代码，长期推迟 → 需要路线图确认 |

### 待审核的关键 PR（>24h）

| PR | 创建日期 | 大小 | 风险 | 现状 | 建议 |
|---|---|---|---|---|---|
| **#3708** | 2026-05-16 | M | 🟠 medium | **27天未合并** | 🔴 严重阻塞，breaking change 需快速评审 |
| **#4588** | 2026-06-09 | L | 🟢 low | **3天未合并** | ✅ 观测性基础设施，

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报
**日期：2026-06-12** | **数据周期：过去24小时**

---

## 📊 今日速览

LobsterAI 今日呈现**高活跃度**的开发周期，24小时内合并/关闭PR 14条，待合并PR 1条，共15条PR活动，表明项目处于**快速迭代阶段**。无新版本发布，但功能与修复工作量显著。新增2条活跃Issue，其中1条为老问题被重新激活。整体项目健康度良好，持续向多Agent协作、语音实时ASR、HTML分享等方向演进。

---

## 🔧 项目进展

### 核心功能推进（14个已合并/关闭PR）

**AI能力增强：**
- **实时ASR语音输入** ([#2148](https://github.com/netease-youdao/LobsterAI/pull/2148)) - 为Cowork语音模块新增实时识别能力，支持WebSocket流式音频传输，新增设置选项切换识别模式。这是**语音交互体验的重大升级**。
- **自动模型故障转移** ([#1483](https://github.com/netease-youdao/LobsterAI/pull/1483)) - 主模型失败时自动降级至用户配置的备选模型，提升服务连续性。
- **Gmail邮件自动化触发** ([#1484](https://github.com/netease-youdao/LobsterAI/pull/1484)) - 新增Gmail Watcher模块，支持邮件驱动的Agent自动激活。

**UI/UX优化：**
- **HTML分享访问方式升级** ([#2146](https://github.com/netease-youdao/LobsterAI/pull/2146)) - 支持分享码与公开访问两种模式选择切换，提升分享灵活性。
- **文件分享功能** ([#2151](https://github.com/netease-youdao/LobsterAI/pull/2151)) - 新增分享文件能力。
- **专家工具套件UI固定化** ([#2150](https://github.com/netease-youdao/LobsterAI/pull/2150)) - 使Expert Suite页面工具栏固定显示，改进长列表浏览体验。
- **技能芯片水平滚动** ([#1481](https://github.com/netease-youdao/LobsterAI/pull/1481)) - 优化Prompt Bar中活跃技能芯片的布局，支持水平滚动，解决溢出问题。
- **技能Tooltip富文本展示** ([#1459](https://github.com/netease-youdao/LobsterAI/pull/1459)) - 悬停时显示完整技能描述，智能四方位定位，解决描述截断问题。

**稳定性与可靠性修复：**
- **网关超时增长** ([#2152](https://github.com/netease-youdao/LobsterAI/pull/2152)) - 将前置模型同步超时从30秒提升至90秒，适配低速网关冷启动场景（实测观察35-107秒延迟）。**关键修复**，防止网络不稳定环境下消息丢弃。
- **OpenClaw网关堆内存溢出** ([#2149](https://github.com/netease-youdao/LobsterAI/pull/2149)) - 显式设置V8旧空间限制，减少长时间多渠道工作负载下的OOM崩溃。
- **会话停止竞态条件** ([#2147](https://github.com/netease-youdao/LobsterAI/pull/2147)) - 修复用户停止命令到达时启动回合仍发送聊天的竞态问题。

**细节优化：**
- **定时任务编辑缺陷** ([#1482](https://github.com/netease-youdao/LobsterAI/pull/1482)) - 修复编辑后描述被清空、启用状态被强制覆盖的问题。
- **CopyButton内存泄漏** ([#1478](https://github.com/netease-youdao/LobsterAI/pull/1478)) - 清理组件卸载时未清理的定时器。
- **技能重复安装防护** ([#1479](https://github.com/netease-youdao/LobsterAI/pull/1479)) - 防止同一本地技能安装两次，失败时给出清晰提示。
- **技能安装反馈** ([#1480](https://github.com/netease-youdao/LobsterAI/pull/1480)) - 成功安装后刷新技能列表并展示Toast提示。

**📈 进展评估：** 14条PR涵盖**3大主线**（AI能力、用户体验、系统稳定性），表明项目在功能宽度与深度上均取得进展。特别是实时ASR与故障转移体现了对**生产级可靠性**与**交互现代化**的重视。

---

## 🎯 社区热点

### 活跃Issue讨论

**#1462 - Multi-Agent协作架构诉求** ([链接](https://github.com/netease-youdao/LobsterAI/issues/1462))
- **状态**：Open + Stale（创建于2026-04-04，最新活动2026-06-11，2条评论）
- **核心诉求**：
  1. 单Agent绑定模型 - 允许不同Agent使用不同的LLM模型
  2. Agent小组模式 - 引入Manager概念，支持主Agent按需调度其他Agent
- **用户背景**：对v4.3多实例功能满意，期望进一步的协调能力
- **对标产品**：提及对阿里HiClaw的期待，但认为LobsterAI交互体验更优

**#2121 - Token重复输出疑似Bug** ([链接](https://github.com/netease-youdao/LobsterAI/issues/2121))
- **状态**：Open（创建于2026-06-07，最新活动2026-06-11，1条评论）
- **核心问题**：模型输出文字重复，疑似造成Token浪费
- **追问焦点**：是否为OpenClaw问题，如何解决
- **严重程度**：用户成本敏感（Token计费），需要关注

**📌 热点分析：** 两个Issue反映了用户群体从单Agent工作流向**企业级多Agent编排**演进的诉求，以及对**成本效率**的关切。#1462的4月发起却在6月被重新激活，暗示多Agent需求的**持续热度**。

---

## 🐛 Bug与稳定性

### 已报告问题（2个活跃Issue）

| Issue | 严重程度 | 症状 | 修复状态 |
|-------|---------|------|---------|
| [#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) - 输出文本重复 | 🔴 高 | 模型回复重复，Token浪费 | ❓ 待确认 |
| [#1462](https://github.com/netease-youdao/LobsterAI/issues/1462) - 缺少多Agent协作 | 🟡 中 | 功能缺陷而非Bug | 📋 已作为特性需求 |

### 已修复的稳定性问题（14个PR）

| PR | 问题类别 | 影响范围 | 优先级 |
|-------|---------|---------|--------|
| [#2152](https://github.com/netease-youdao/LobsterAI/pull/2152) | 网关超时 | 低速网络环境消息丢弃 | 🔴 严重 |
| [#2149](https://github.com/netease-youdao/LobsterAI/pull/2149) | 内存溢出 | 长时间多渠道运行OOM崩溃 | 🔴 严重 |
| [#2147](https://github.com/netease-youdao/LobsterAI/pull/2147) | 竞态条件 | 会话停止时仍发送消息 | 🟡 中 |
| [#1482](https://github.com/netease-youdao/LobsterAI/pull/1482) | 数据丢失 | 定时任务编辑后描述消失 | 🟡 中 |
| [#1478](https://github.com/netease-youdao/LobsterAI/pull/1478) | 内存泄漏 | React组件卸载警告 | 🟠 低 |

**🔍 稳定性评估：** 昨日修复工作突出了**网络弹性**（#2152）和**资源管理**（#2149）两大痛点，表明项目正在扫除制约生产部署的关键缺陷。

---

## 💡 功能请求与路线图信号

### 用户提出的新功能需求

| 需求 | Issue | 状态 | 预期影响 |
|------|-------|------|---------|
| 单Agent绑定模型 | [#1462](https://github.com/netease-youdao/LobsterAI/issues/1462) | 🔴 计划中 | 支持异构模型编排 |
| Multi-Agent小组协作 | [#1462](https://github.com/netease-youdao/LobsterAI/issues/1462) | 🔴 计划中 | 企业级工作流 |
| 实时ASR语音 | [#2148](https://github.com/netease-youdao/LobsterAI/pull/2148) | ✅ 已实现 | 提升交互流畅性 |
| 模型自动故障转移 | [#1483](https://github.com/netease-youdao/LobsterAI/pull/1483) | ✅ 已实现 | 提升服务可用性 |
| 邮件驱动自动化 | [#1484](https://github.com/netease-youdao/LobsterAI/pull/1484) | ✅ 已实现 | 支持更多触发源 |
| HTML分享灵活选择 | [#2146](https://github.com/netease-youdao/LobsterAI/pull/2146) | ✅ 已实现 | 满足不同分享场景 |

### 下一版本信号

基于已合并PR的功能密度，**即将发布的版本**可能包含：
1. **实时语音ASR**（已完成，设计文档齐全）
2. **HTML分享增强**（已完成，模式切换功能稳定）
3. **故障转移与自动化**（已完成，涉及模型与邮件触发）
4. **多渠道稳定性加固**（已完成，网关与内存优化）

**⚠️ 关键待实现：** #1462的Multi-Agent协作诉求**仍未在已合并PR中出现**，可能纳入**更后续版本**或正在设计阶段。

---

## 👥 用户反馈摘要

### 真实用户痛点

**1. 多Agent协作能力缺失**（#1462，作者：@orion0608）
- 现状满意：v4.3多实例同IM渠道实用
- 痛点：无法为不同Agent绑定不同模型，缺少Agent间协调机制
- 期望：Manager模式下的按需调度，降低编排复杂度
- **市场信号**：对标竞品（HiClaw）仍有交互体验优势，但功能完整性有差距

**2. Token成本透明度问题**（#2121，作者：@nbjoe）
- 症状：模型输出文本重复，怀疑造成Token浪费
- 诉求隐含：用户对API成本敏感，需要可视化成本监控
- **用户群体**：可能是付费API用户或企业用户

**3. 积极特性反馈**
- 多实例功能获得认可，说明**协作方向**符合用户需求
- 用户主动对标HiClaw但倾向LobsterAI，表明**交互设计竞争力强**

### 用户满意/不满意度指标

| 维度 | 满意度 | 证据 |
|------|--------|------|
| 交互体验 | ⭐⭐⭐⭐⭐ | "交互体验确实不如lobster ai"（与HiClaw对比）|
| 多实例支持 | ⭐⭐⭐⭐⭐ | "4.3版本的同IM渠道多实例很实用" |
| 多Agent协作 | ⭐⭐⭐ | 功能不完整，诉求未满足 |
| 成本可控性 | ⭐⭐⭐ | Token重复问题暴露出成本追踪缺陷 |

---

## ⏳ 待处理积压

### 长期未关闭的活跃Issue

| Issue | 创建时间 | 最后活动 | 天数 | 评论数 | 优先级 | 建议 |
|-------|---------|---------|------|--------|--------|------|
| [#1462](https://github.com/netease-youdao/LobsterAI/issues/1462) - Multi-Agent协作 | 2026-04-04 | 2026-06-11 | **69天** | 2 | 🔴 高 | 需路线图确认，考虑发布设计RFC |
| [#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) - Token重复输出 | 2026-06-07 | 2026-06-11 | **4天** | 1 | 🔴 高 | **新增问

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报
**日期：2026-06-12**

---

## 1. 📊 今日速览

Moltis 项目今日保持稳定的开发节奏，共迎来 **1 个新 Issue 和 1 个待合并 PR**。虽然更新量不大，但新增的 PR 针对 WhatsApp 网关的关键消息投递问题进行了修复，体现了项目对消息可靠性的重视。整体来看，项目处于**功能完善与缺陷修复并行的健康状态**，社区反馈持续反映实际使用中的痛点。

---

## 2. 🚀 版本发布

无新版本发布。

---

## 3. ⚙️ 项目进展

### 待合并 PR：WhatsApp 消息投递修复

**PR #1116** - [`fix(whatsapp): deliver replies to @lid chats via PN JID rewrite`](https://github.com/moltis-org/moltis/pull/1116)
- **作者**：@juanlotito | **创建时间**：2026-06-12
- **核心修复**：解决了隐私启用模式下（@lid 聊天）的回复消息被静默丢弃的问题
  - **问题症状**：网关生成回复并在 Web UI 中可见，但消息无法送达用户，且未收到已送达回执
  - **修复方案**：通过 PN JID 重写机制重新路由回复消息
- **影响范围**：WhatsApp 集成模块，影响隐私聊天场景下的消息可靠性
- **进展评估**：该 PR 直接推进了网关消息投递的稳定性，预计合并后将显著改善用户体验

---

## 4. 💬 社区热点

### 活跃讨论

**Issue #1115** - [`[bug] Fastmail MCP Authorisation`](https://github.com/moltis-org/moltis/issues/1115)
- **报告者**：@kmath313 | **创建时间**：2026-06-11 | **活跃度**：1 条评论
- **问题分类**：认证授权问题
- **影响**：Fastmail MCP 集成的授权流程存在障碍
- **诊断建议**：报告者已完成预检清单（使用最新版本、搜索重复问题），说明问题的真实性与再现性较高

---

## 5. 🐛 Bug 与稳定性

| 优先级 | Issue ID | 标题 | 状态 | 修复进展 |
|--------|---------|------|------|---------|
| **高** | #1115 | Fastmail MCP 授权失败 | 待处理 | ❌ 无对应 PR |
| **中** | #1116 | WhatsApp @lid 聊天回复投递失败 | 待合并 | ✅ PR 已提交 |

### 分析

- **#1115 (Fastmail 授权)**：新报告的缺陷，可能反映 Moltis 在邮件服务集成中的认证机制需优化，建议维护者优先跟进根本原因
- **#1116 (WhatsApp 投递)**：虽归类为 PR，但本质上是已确认的稳定性 Bug，修复方案采用 JID 重写策略，技术方案相对成熟

---

## 6. 🎯 功能请求与路线图信号

基于今日数据，暂未发现新的功能请求。现有的 PR #1116 反映出项目在以下方向的持续投入：
- **消息网关稳定性**：隐私模式、非标准 JID 场景的处理
- **多服务集成**：WhatsApp、Fastmail 等第三方服务的完整性保证

---

## 7. 👥 用户反馈摘要

### 核心痛点提炼

1. **Fastmail 集成认证障碍**（Issue #1115）
   - 场景：用户尝试通过 MCP 集成 Fastmail
   - 痛点：授权流程失败，导致集成中断
   - 影响范围：邮件服务用户

2. **WhatsApp 隐私聊天消息可靠性**（PR #1116 背景）
   - 场景：在隐私启用的 @lid 聊天中发送回复
   - 痛点：消息无声丢失，用户感知差
   - 潜在影响：生产环境可能出现沟通中断

---

## 8. ⏳ 待处理积压

| 项目 | 类型 | 状态 | 建议 |
|------|------|------|------|
| #1115 | Issue | 创建 24h 内，未获回应 | ✅ 新鲜度高，维护者应在 24-48h 内确认 |
| #1116 | PR | 创建 <1h，待审查 | ⚠️ 关键修复，建议加速审查与合并 |

---

## 📈 项目健康度评估

| 指标 | 评分 | 备注 |
|------|------|------|
| **更新频率** | ⭐⭐⭐⭐ | 日均 2 项更新，保持稳定节奏 |
| **问题响应** | ⭐⭐⭐ | 新 Issue 响应存在延迟，建议配置 SLA |
| **修复速度** | ⭐⭐⭐⭐ | 关键 Bug 有 PR 跟进，修复意愿强 |
| **社区活跃** | ⭐⭐⭐ | 报告者完成预检，参与质量中等 |

---

**下一步建议**：
1. 维护者应优先审查并合并 PR #1116（关键消息投递修复）
2. 对 Issue #1115 进行初步诊断，判断是配置问题还是代码缺陷
3. 考虑为多服务集成（Fastmail、WhatsApp）补充集成测试覆盖

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目日报 | 2026-06-12

## 📊 今日速览

CoPaw 项目今日社区活跃度**显著提升**，过去 24 小时新增 34 条 Issue 更新（其中 21 条新开/活跃）和 41 条 PR（23 条待合并）。发布了两个补丁版本（v1.1.11.post1 / post2），主要修复 SSL 证书和进程泄漏问题。整体来看，项目处于**密集修复阶段**，用户反馈集中在桌面客户端崩溃、文件下载异常、内存泄漏等生产环保问题，需要立即关注。

---

## 🚀 版本发布

### v1.1.11.post2（最新）
- **发布时间**：2026-06-11
- **修复内容**：
  - ✅ 工具卡片标题截断显示（单行 ellipsis）
  - ✅ 版本号碰撞修复
- **关联 PR**：[#5119](https://github.com/agentscope-ai/QwenPaw/pull/5119)、[#5124](https://github.com/agentscope-ai/QwenPaw/pull/5124)

### v1.1.11.post1
- **发布时间**：2026-06-11
- **修复内容**：
  - 撤销 Discord conda-unpack compile-check（导致 Windows 构建失败）
- **关联 PR**：[#5093](https://github.com/agentscope-ai/QwenPaw/pull/5093)、[#5092](https://github.com/agentscope-ai/QwenPaw/pull/5092)

**⚠️ 注意**：post 版本频繁发布表明 v1.1.11 主版本存在突出问题，见下文「Bug 与稳定性」章节。

---

## 🔧 项目进展

### 已合并/关闭的关键 PR（过去 24h）

| PR | 作者 | 内容 | 影响 |
|---|---|---|---|
| [#5125](https://github.com/agentscope-ai/QwenPaw/pull/5125) | @jinglinpeng | **加固 Tauri Windows CI 构建** — 预取依赖 + 离线构建 + 缓存重用 | 解决 crates.io 随机 TLS 失败 |
| [#5133](https://github.com/agentscope-ai/QwenPaw/pull/5133) | @devjotaduo | **应用 AionUi 设计语言到 Console** — CSS/Less 级别重构 | 改进前端美观度，零功能破坏 |
| [#5134](https://github.com/agentscope-ai/QwenPaw/pull/5134) | @devjotaduo | **Historian agent 原型** — 自动记录开发周期文档 | DevOps 工程化进展 |
| [#5136](https://github.com/agentscope-ai/QwenPaw/pull/5136) | @devjotaduo | **完整 pt-BR 国际化支持** | 社区本地化突破 |

### 待合并的高优先级 PR（23 条）

**关键推进方向**：
1. **运行时架构升级**（[#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078)）— Runtime 2.0 + ToolCoordinator 模块化
2. **Agent OS Driver 统一抽象**（[#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067)）— MCP/A2A/ACP 统一接口
3. **Token 使用统计**（[#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130)）— 每轮对话成本可视化
4. **Langfuse 可观测性**（[#5128](https://github.com/agentscope-ai/QwenPaw/pull/5128)）— 按 Agent loop 分组
5. **安全隔离加固**（[#5117](https://github.com/agentscope-ai/QwenPaw/pull/5117)）— workspace 禁止放置在自动加载目录

---

## 🔥 社区热点

### 最受关注的 Issue（评论 + 👍 统计）

| Issue | 讨论热度 | 核心诉求 |
|-------|---------|---------|
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) **[破坏性变更] AgentScope 1.x → 2.0 迁移** | 9 条评论 | 后端升级至 AgentScope 2.0 的时间表与兼容方案 |
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) **Agent 生成的定时任务不触发** | 8 条评论 | 定时任务执行失败、无法编辑 |
| [#5106](https://github.com/agentscope-ai/QwenPaw/issues/5106) **Tauri 端 SSL 证书 + 内存泄漏致黑屏** | 7 条评论 | 💥 **严重** — 新旧桌面版本都无法启动 |
| [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) **OpenSSL 3.5 回归 bug** | 5 条评论 | Python 3.10 + OpenSSL 3.5.7 DER 证书解析失败 |
| [#5095](https://github.com/agentscope-ai/QwenPaw/issues/5095) **Windows v1.1.11 安装后无法启动** | 5 条评论 | 同上 SSL 证书问题 |

### 舆情分析
- **用户痛点集中度高**：超 50% 的讨论围绕桌面客户端崩溃和内存问题
- **版本质量堪忧**：v1.1.11 发布后快速补丁两次，仍有用户报告新问题
- **后端迁移压力**：#4727 持续征询 AgentScope 2.0 迁移的具体计划

---

## 🐛 Bug 与稳定性

### 💥 P0 级严重问题（需立即修复）

| Bug | 影响范围 | 状态 | Fix PR |
|-----|---------|------|--------|
| [#5106](https://github.com/agentscope-ai/QwenPaw/issues/5106) | Tauri Windows 端 SSL 证书异常 + 内存溢出导致黑屏 | 🔴 已关闭（待验证） | [#5125](https://github.com/agentscope-ai/QwenPaw/pull/5125)（CI 加固，非根因修复） |
| [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) | OpenSSL 3.5 DER 证书加载失败 | 🟡 已关闭 | ❌ **无** — 需要升级 Python/OpenSSL 或 workaround |
| [#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138) | Windows 客户端进程持续增加，内存占用 90%+ | 🔴 **开放** | ❌ **无** — 可能同 SSL 问题 |

### 📊 P1 级功能故障（高优先级）

| Bug | 用户影响 | 状态 | Fix PR |
|-----|---------|------|--------|
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | Agent 生成的定时任务无法触发、无法编辑 | 🔴 **开放** | ❌ **无** |
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | docx/pdf 附件下载报错 404（txt/md 正常） | 🔴 **开放** | ❌ **无** |
| [#5098](https://github.com/agentscope-ai/QwenPaw/issues/5098) | auto_memory_search 结果 UI 展示为空 | 🔴 **开放** | ❌ **无** |
| [#5142](https://github.com/agentscope-ai/QwenPaw/issues/5142) | Coding Mode 刷新页面后 Session 丢失 | 🔴 **开放** | ❌ **无** |
| [#5137](https://github.com/agentscope-ai/QwenPaw/issues/5137) | 向量模型配置未展开时保存丢失 | 🔴 **开放** | ✅ [#5144](https://github.com/agentscope-ai/QwenPaw/pull/5144) （待合并） |

### 🔄 已解决的回归问题

- [#5108](https://github.com/agentscope-ai/QwenPaw/issues/5108) — 1.1.11 无法选择 Ollama 模型（已关闭，需确认修复）
- [#5089](https://github.com/agentscope-ai/QwenPaw/issues/4989) — 本地千问 3.6-27B 无响应（已关闭）

---

## 💡 功能请求与路线图信号

### 用户主动提出的新功能（按讨论热度排序）

| Feature | Issue | 用户需求 | 已有 PR | 优先级 |
|---------|-------|---------|--------|--------|
| **Agent Team/Swarm 协作** | [#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139) | 多 Agent 团队协作（类似 WorkBuddy/JiuwenSwarm） | ❌ | ⭐⭐⭐⭐ |
| **DingTalk 私有部署自定义端点** | [#4887](https://github.com/agentscope-ai/QwenPaw/issues/4887) | 支持私有 DingTalk 平台自定义 API 地址 | ❌ | ⭐⭐⭐ |
| **Headroom 上下文压缩集成** | [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | 60-95% token 消耗减少 | ❌ | ⭐⭐⭐ |
| **对话队列 + Token 统计** | [#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103) | 类似 OpenClaw 的队列处理、精确时间戳 | ✅ [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130) (Token 统计部分) | ⭐⭐⭐ |
| **Coding Mode 代码补全** | [#5131](https://github.com/agentscope-ai/QwenPaw/issues/5131) | IDE 级别代码补全 | ❌ | ⭐⭐ |
| **对话引用/关联上文** | [#5110](https://github.com/agentscope-ai/QwenPaw/issues/5110) | 选中文本快速引用（如 Perplexity） | ❌ | ⭐⭐ |
| **交互模式可配置化** | [#5116](https://github.com/agentscope-ai/QwenPaw/issues/5116) | 多渠道中断/方向盘/队列模式替代 `/stop` | ❌ | ⭐⭐ |

### 🎯 正在推进的架构升级（来自待合并 PR）

1. **AgentScope 2.0 迁移**（[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)） — 已纳入里程碑
2. **Runtime 2.0 模块化**（[#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078)） — ToolCoordinator 细粒度控制
3. **Agent OS Driver 统一抽象**（[#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067)） — MCP/A2A/ACP

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