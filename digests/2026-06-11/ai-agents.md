# OpenClaw 生态日报 2026-06-11

> Issues: 500 | PRs: 500 | 覆盖项目: 12 个 | 生成时间: 2026-06-11 03:42 UTC

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

# OpenClaw 项目动态日报 🦞
**日期**: 2026-06-11 | **数据周期**: 过去24小时

---

## 1. 📊 今日速览

OpenClaw 项目今日保持**高度活跃**状态，过去24小时新增/激活 Issues 469 条、待合并 PR 395 条，呈现典型的快速迭代特征。版本 v2026.6.6-beta.1 发布，重点强化了安全边界（转录、沙盒、MCP 隔离等）。从议题分布看，**安全问题（P1）、会话状态丢失、多代理编排稳定性** 成为当前最关键的三大痛点，维护者面临的合并审查压力较大（395 PR 待合并）。

---

## 2. 🚀 版本发布

### **v2026.6.6-beta.1** 发布
- **发布时间**: 2026-06-11  
- **类型**: Beta 版本  
- **核心更新**: 安全边界全面加固
  - ✅ 转录隔离（Transcript Boundaries）
  - ✅ 沙盒绑定加强（Sandbox Binding Tightening）
  - ✅ 主机环境继承控制（Host Environment Inheritance）
  - ✅ MCP stdio 隔离
  - ✅ Codex HTTP 访问限制
  - ✅ 原生搜索策略优化
  - ✅ 提升发件人身份检查（Elevated Sender Checks）
  - ✅ 删除代理 ACP 旁路修复
  - ✅ 环回工具安全加固
  - ✅ Discord/Teams 群组访问控制

**破坏性变更预警**: 未在本次数据中详细说明，建议升级前审阅迁移指南。

---

## 3. 🔧 项目进展（今日合并/关闭的重要 PR）

| PR 编号 | 标题 | 影响 | 状态 |
|---------|------|------|------|
| **#90128** | [FIX] 保留用户 /model 覆盖跨会话滚动 | 会话一致性 | ✅ 已合并 |
| **#90110** | [FIX] Claude Haiku 4.5 静态目录引用 | 模型兼容性 | ✅ 已合并 |
| **#84938** | [FIX] 转发 OpenAI 兼容提供者的 reasoning_content | MiMo/推理模型支持 | ✅ 已合并 |
| **#92073** | [FIX] 处理显式无声助手回复 | 消息投递 | ⏳ 待审核 (P1) |
| **#92079** | [AI] 自动修复内存 providerKey 不匹配 | 内存索引 | ⏳ 待审核 |
| **#91985** | [FIX] 心跳修复：压制投递时跳过承诺标记 | 消息丢失 | ⏳ 待审核 |

**进展评估**: 过去24小时至少 **3 个关键 fix PR 合并**，主要聚焦模型兼容性、会话状态保持、消息投递可靠性，表明项目在解决核心稳定性问题上有实质推进。但 **395 条 PR 仍待合并**，审核队列压力显著。

---

## 4. 🔥 社区热点

### 评论最活跃的 Issues（前10）

| Issue | 评论数 | 标题 | 热点诉求 |
|-------|--------|------|---------|
| **#25592** | 31 | [P1 安全] 工具调用间文本泄露到消息通道 | 内部处理输出不应进入公开通道 |
| **#44925** | 19 | [P1] 子代理完成无声丢失 | 后台任务结果可靠性，需重试机制 |
| **#88838** | 19 | [P0 维护] SQLite 迁移跟踪 | 大重构分阶段着陆策略 |
| **#32473** | 17 | [P2 回归] 控制UI身份校验失败 | HTTPS/localhost 强制要求阻挡部署 |
| **#22438** | 17 | [P2 功能] 分层启动文件加载 | Token 消耗优化，减少冗余加载 |
| **#32296** | 15 | [P1] 代理回复错误消息（会话混淆） | 上下文管理缺陷导致语义错位 |
| **#58450** | 15 | [P2] 代理承诺但不启动后续 | UX 欺骗：虚假的异步承诺 |
| **#29387** | 14 | [P1 BUG] agentDir 启动文件被无视 | 按代理隔离配置不生效 |
| **#45740** | 13 | [P2 安全] gh-issues 技能注入未消毒 | Prompt 注入风险，外部数据直入子代理 |
| **#39604** | 13 | [P2 功能] web.fetch 私网访问白名单 | 企业内网集成阻力，需要可选开放 |

**背后诉求分析**:
- **安全与隐私**: 66% 的热点涉及信息泄露、隔离、注入风险
- **可靠性**: 多代理编排、消息投递、后台任务结果丢失是高频痛点
- **企业适配**: 网络隔离、多账户、访问控制需求旺盛
- **性能优化**: Token 消耗、启动加载、内存压力管理开始被提及

---

## 5. 🐛 Bug 与稳定性

### P1（关键）Bug —— 需立即关注

| Bug ID | 标题 | 现象 | 已有Fix PR | 影响范围 |
|--------|------|------|-----------|---------|
| **#25592** | 工具调用间文本泄露 | 内部处理文本进入消息通道 | ❌ 无 | Slack/iMessage 等全通道 |
| **#44925** | 子代理完成无声丢失 | 超时后结果无回复、无重试、无重启 | ❌ 无 | 多代理编排，Telegram |
| **#88838** | SQLite 迁移状态不清 | 大重构风险，需分段着陆 | 🔄 进行中（#78381） | 核心会话存储 |
| **#32296** | 代理回复错误消息 | 会话上下文混淆，回复不匹配用户输入 | ❌ 无 | 所有通道的多轮对话 |
| **#31583** | `exec` 工具不继承技能环变量 | 私密凭据无法传递到子进程 | ❌ 无 | 所有需要身份认证的脚本执行 |
| **#37634** | sandbox 隔离工作区只读 | workspaceAccess=none 时无写入权 | ❌ 无 | 沙盒安全隔离模式 |

### P2（高）Bug —— 影响可用性

| Bug ID | 标题 | 现象 | 已有Fix PR |
|--------|------|------|-----------|
| **#43661** | 会话压缩超时致无限挂起 | 消息重复发送，无恢复 | ❌ 无 |
| **#40001** | 写工具缺追加模式 | 孤立 cron 覆盖共享文件 | ❌ 无 |
| **#44905** | Discord 泄露工具调用痕迹 | 用户看到 NO_REPLY、内部JSON | ✅ #92074 修复中 |
| **#41744** | Feishu 读图工具结果丢媒体 | 图片读取成功但投递时丢失 | ❌ 无 |

**稳定性评估**: 
- 🔴 **关键稳定性缺陷 6 个** 无 fix PR（P1 打开）
- 🟡 **可用性回归 8+ 个**（消息丢失、隔离失效、覆盖问题）
- 🟢 **修复趋势**: 今日 3 个相关 fix PR 合并，但积压仍重

---

## 6. 🎯 功能请求与路线图信号

### 高优先级功能需求（从 PR 活动推测）

| 需求 | 支持度 | 关联 PR/Issue | 预期影响 |
|------|--------|--------------|---------|
| **多代理编排稳定性** | 🔴 紧急 | #43367, #78441 | P0 维护者优先级 |
| **会话 SQLite 迁移** | 🟡 进行中 | #88838, #78381 | 核心基础设施，影响全部会话 |
| **消息投递可靠性** | 🔴 紧急 | #44925, #91921 | 5+ P1 issue 依赖 |
| **安全边界加固** | 🟢 推进中 | v2026.6.6-beta 重点 | 已发布，逐步加固 |
| **私网 API 访问** | 🟡 有PR | #39604, #85664 | 企业需求，#39604 得 9 个 👍 |
| **Token 成本治理** | 🟡 有PR | #42475, #43260 | 多代理成本控制，#42475 有 PR |
| **直接工具调用 HTTP API** | 🟡 有PR | #63919, #85664 | 嵌入式集成，#85664 待审核 |
| **语音/视频通话支持** | 🟢 新增 | #92081 (Teams) | 新通道拓展，Microsoft 企业方向 |
| **分层启动文件加载** | 🟡 讨论中 | #22438 (17评论) | Token 优化，中优先级 |

**路线图信号**:
- 🎯 **Q2 2026 重点**: 多代理可靠性、SQLite 迁移、安全边界（已在 v6.6-beta）
- 🎯 **计划中**: 企业网络支持、成本治理、HTTP 直调
- 🎯 **新方向**: 语音集成（Teams VoIP）、团队协作特性

---

## 7. 👥 用户反馈摘要

### 真实用户痛点排序

**1. 可靠性与容错（最频繁）**
> "子代理任务无声丢失，没有重试机制。" — #44925  
> "后台 exec 完成无通知，代理继续等待。" — #91921  
> "孤立 cron 会话覆盖共享文件，没有追加模式。" — #40001

**用户诉求**: 需要可靠的异步结果回调、超时重试、文件操作原子性保证。

---

**2. 隔离与安全（高风险）**
> "工具调用间的文本泄露到 Slack，用户看到内部处理。" — #25592  
> "gh-issues 技能直接注入原始 issue 体到子代理。" — #45740  
> "Docker + 沙盒无法正确挂载工作

---

## 横向生态对比

# AI 智能体开源生态动态分析报告
## 2026-06-11 横向对比

---

## 1. 生态全景

当前个人 AI 助手及自主智能体开源生态呈现**分化繁荣**态势：头部项目（OpenClaw、CoPaw、LobsterAI）围绕多代理编排、会话稳定性、工具能力三大核心问题高速迭代，社区活跃度超预期；中层项目（NanoBot、Zeroclaw、IronClaw）在垂直领域（流处理、WebUI、授权）深化打磨，逐步走向生产就绪；底层基础设施层面，安全隔离、跨平台兼容性、消息投递可靠性成为**普遍痛点**，呈现行业发展阶段的必然性困境。**生态健康度评估**：11 个活跃项目日均 180+ 次更新（PR+Issue），说明整体处于快速演进期，但长期积压 PR（20-70 天）和跨平台兼容性缺陷预示着工程质量挑战日益突出。

---

## 2. 活跃度对比表

| 项目 | 新增 Issues | 待合并 PR | 今日合并 PR | 新版本 | 健康度评估 | 核心状态 |
|------|-----------|----------|-----------|--------|----------|---------|
| **OpenClaw** | 469 | 395 | 3+ | v2026.6.6-β | 🔴 积压严重 | 快速迭代，审核瓶颈 |
| **CoPaw** | 33 | 19 | 30 | v1.1.11 | 🟢 流畅 | 版本稳定发布，迭代高效 |
| **LobsterAI** | 0 | 1 | 24 | 2026.6.10 | 🟢 优秀 | 核心功能成熟，节奏稳定 |
| **IronClaw** | 50 | - | 8 | 否 | 🟡 高热 | Reborn 产品化，社区认可高 |
| **Zeroclaw** | 24 | 40 | 10 | 否 | 🟡 积压 | 跨平台测试危机（Windows 74失败） |
| **NanoBot** | 4 | 14 | 17 | 否 | 🟢 良好 | 功能聚焦，修复及时 |
| **PicoClaw** | 5 | 9 | 6 | nightly | 🟢 良好 | 代码质量改进中，安全主动 |
| **NanoClaw** | 2 | 8 | 4 | 否 | 🟡 中速 | Telegram/安全并行推进，审核压力 |
| **TinyClaw** | 0 | - | - | 否 | ⚪ 休眠 | 无活动 |
| **Moltis** | 0 | - | - | 否 | ⚪ 休眠 | 无活动 |
| **ZeptoClaw** | 0 | - | - | 否 | ⚪ 休眠 | 无活动 |

**关键观察**：
- **核心圈层**（OpenClaw、CoPaw、LobsterAI）日均更新 50+ 条，远超其他项目
- **审核瓶颈**：OpenClaw 395 待审 PR 为生态最高，预示社区规模超出维护能力
- **发布频率**：LobsterAI、CoPaw 每月稳定发布，OpenClaw 仅 Beta 版本说明审核严格

---

## 3. OpenClaw 在生态中的定位

| 维度 | OpenClaw | 同类竞品（CoPaw/IronClaw） | 优劣分析 |
|------|----------|------------------------|---------|
| **社区规模** | 469 新增 Issues/24h（最高） | CoPaw 33、IronClaw 50 | ✅ **绝对领导** — 社区驱动力最强，但社区期望管理压力大 |
| **技术路线** | 多代理编排 + MCP 隔离 + 安全边界 | CoPaw：模型供应商中心；IronClaw：Reborn WebUI | ✅ **基础设施优先** — 更底层的系统性解决方案 |
| **成熟度** | v2026.6.6-Beta（仍在安全边界加固） | CoPaw v1.1.11 正式；IronClaw v0.27.0 稳定 | ⚠️ **略显保守** — 频繁 Beta 版本、P1 Bug 堆积（6个无 Fix PR）表明追求完备性 |
| **通道支持** | Slack/iMessage/Discord/Teams/群组控制 | CoPaw：DingTalk/WeChat/Telegram；IronClaw：Slack/Telegram | 🟢 **广但不深** — 通道广泛但单通道可靠性待验证 |
| **核心差异** | **系统性隔离**（转录隔离、沙盒绑定、MCP stdio 隔离） | **能力充足性**（多模型供应商、工具集成） | OpenClaw = 基础设施安全；CoPaw/IronClaw = 能力广度 |

**战略定位**：OpenClaw 是 AI 智能体基础设施层的"内核"，强调隔离、安全、多代理可靠性，目标是成为企业级多智能体系统的信任基座。相比之下，CoPaw/IronClaw 更接近面向开发者的"工具链"（模型接入、WebUI、技能生态）。

---

## 4. 共同关注的技术方向

### **A. 多代理编排稳定性（5 个项目共同痛点）**

| 项目 | 具体表现 | 优先级 |
|------|--------|--------|
| **OpenClaw** | #44925 子代理完成无声丢失，无重试机制；#91921 后台 exec 完成无回复 | P1 紧急 |
| **Zeroclaw** | #6034 消息丢失；#7263 子代理未继承 cwd | P1 阻塞 |
| **CoPaw** | #5064 Agent 定时任务无法触发；#4878 WeChat 推送失败 | 高 |
| **NanoClaw** | #2731 网络隔离导致本地服务不可达；子代理结果回注机制 | 高 |
| **IronClaw** | #4706 授权后无恢复；批准弹窗无错误细节；#4746 已修复但流程仍复杂 | 中高 |

**共同诉求**：可靠的异步结果回调、超时重试、失败恢复机制。表明多代理架构已成必需能力，但异步任务生命周期管理是行业级瓶颈。

---

### **B. 会话/消息投递可靠性（4 个项目）**

| 项目 | Bug 表现 | 关联数据 |
|------|--------|---------|
| **OpenClaw** | #88838 SQLite 迁移风险；#43661 会话压缩超时致挂起 | 多通道全部影响 |
| **LobsterAI** | #2145 压缩后上下文连续性改进（已修复） | 核心稳定性投入 |
| **CoPaw** | #5053 Windows 多会话切换卡顿；#4865 长文件生成卡顿 | UX 层面 |
| **PicoClaw** | #3094 spawn 异步任务重复推送 | 低优但用户显著感知 |

**共同方向**：从单个会话的完整性，升级到跨会话的并发管理和性能优化。SQLite 迁移、流式渲染、消息批处理成为核心投入。

---

### **C. 安全隔离与边界强化（3 个项目）**

| 项目 | 关键需求 | 现状 |
|------|--------|------|
| **OpenClaw** | 转录隔离、沙盒绑定、MCP stdio 隔离、删代理 ACP 旁路修复 | v2026.6.6-beta 重点发布 |
| **PicoClaw** | SSRF 防护（198.18.0.0/15）、sandbox 隔离工作区读写 | #3085 已合并，#3077 已修复 |
| **NanoClaw** | per-group IPC 隔离、egress-lockdown 网络隔离 | #3 已合并，#2731 新报告问题 |

**隐含趋势**：安全隐患不再从外部攻击角度，而是从**内部逻辑泄露**（工具调用间文本泄露、提示注入、权限上下文丢失）出发。Prompt 注入、SSRF、权限提升成为高频威胁。

---

### **D. 跨平台兼容性（3 个项目）**

| 项目 | 缺陷 | 规模 |
|------|------|------|
| **Zeroclaw** | Windows 测试套件 74 失败（Unix 命令、路径分隔符、控制台编码） | 🔴 系统性 |
| **PicoClaw** | #2472 Windows 路径分隔符导致 list_dir 失败（62 天未合并）；#3090 iOS Safari 不可用 | 中 |
| **LobsterAI** | Windows 应用内更新失效、NSIS 初始化问题；Electron 升级积压 70 天 | 中 |

**观察**：Zeroclaw 的"合并队列支持 `merge_group` 触发器"（#7487）是尝试解决 CI 复杂性的信号——跨平台测试的配置成本已显著。

---

## 5. 差异化定位分析

### **技术架构维度**

```
基础设施层        多代理系统      |  LLM 适配层      通道集成层
                                |
OpenClaw    ====> 隔离、编排      |  MCP 驱动    ====> 全通道覆盖
            (系统边界强化)        |              (广但单深)
            
CoPaw       ====> 模块化运行时    |  供应商聚合  ====> DingTalk/WeChat
            (Runtime 2.0 规划)    |              (企业垂直)
            
LobsterAI   ====> 对话管理        |  模型无关    ====> 桌面优先
            (会话压缩与连续性)    |  (Computer Use MVP)
            
IronClaw    ====> WebUI/授权      |  OAuth 完善  ====> Slack/事件驱动
            (产品化重心)          |              (企业 SaaS)
            
Zeroclaw    ====> CLI + 可观测性  |  多提供商    ====> 通用网关
            (OTel 集成)           |              (标准化)
```

**关键差异**：
- **OpenClaw** = 系统内核（隔离、安全、可靠性优先）
- **CoPaw** = 运行时平台（模块化、扩展性优先）
- **LobsterAI** = 用户体验（可用性、性能优先）
- **IronClaw** = 企业应用（授权、工作流优先）
- **Zeroclaw** = 标准化接口（可观测性、多提供商）

---

### **目标用户分层**

| 用户类型 | 主要项目 | 核心吸引力 |
|---------|--------|----------|
| **企业 DevOps / 平台团队** | OpenClaw（隔离）、Zeroclaw（OTel） | 安全、多租户隔离、可观测性 |
| **LLM 应用开发者** | CoPaw（多供应商）、Zeroclaw（CLI） |

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报
## 2026-06-11

---

## 📊 今日速览

NanoBot 项目今日保持高活跃度：**过去24小时处理 11 条 Issues 更新（新增4条，关闭7条）和 31 条 PR 更新（合并/关闭17条，待审14条）**。虽未发布新版本，但核心功能迭代和稳定性修复持续推进。项目在流模型、会话上下文隔离、字幕转录等领域均有显著改进，团队响应速度和修复意愿较强，但已知的回归问题和边界场景需要持续关注。

---

## 🔄 项目进展

### 本周期已合并的关键 PR（17 条）

**流稳定性与模型降级**
- [#4272](https://github.com/HKUDS/nanobot/pull/4272) [CLOSED] **fix(providers): allow retry and fallback on stream stalled timeout**  
  直接修复了 #4013 报告的"stream stalled for more than 90 seconds"问题，实现了中断流的重试和模型降级机制。

**WebUI 存储与性能优化**
- [#4278](https://github.com/HKUDS/nanobot/pull/4278) [CLOSED] **feat(webui): segment transcript storage**  
  将单文件转录存储改为分段存储，解决大型聊天会话的加载性能问题。
- [#4247](https://github.com/HKUDS/nanobot/pull/4247) [CLOSED] **fix(webui): auto-compact transcript when file exceeds size limit**  
  自动处理超过 8MB 限制的转录文件，防止历史消失。

**会话上下文隔离**
- [#4274](https://github.com/HKUDS/nanobot/pull/4274) [CLOSED] **Scope prompt recent history by session**  
  修复了 #4259 报告的 `history.jsonl` 跨会话注入导致的上下文污染问题。

**配置与工具链**
- [#4273](https://github.com/HKUDS/nanobot/pull/4273) [CLOSED] **feat(exec): add pathPrepend config**  
  解决 #3934 中 pip 安装第三方库的路径优先级问题。
- [#4275](https://github.com/HKUDS/nanobot/pull/4275) [CLOSED] **Fail fast on invalid config files**  
  增强了配置文件的错误提前暴露机制。

**转录与集成**
- [#4281](https://github.com/HKUDS/nanobot/pull/4281) [CLOSED] **feat(transcription): add SiliconFlow as transcription provider**  
  扩展转录能力，支持 SiliconFlow ASR。
- [#4277](https://github.com/HKUDS/nanobot/pull/4277) [CLOSED] **fix(feishu): lazy-load lark SDK during gateway startup**  
  优化飞书集成的启动性能。

**版本检查与 WebUI 改进**
- [#4255](https://github.com/HKUDS/nanobot/pull/4255) [CLOSED] **refactor(webui): on-demand version check in Settings > About**  
  实现了 #4233 的需求，移除后台 PyPI 轮询，改为按需检查。

---

## 🔥 社区热点

### 评论最多的议题

| Issue/PR | 评论数 | 关键内容 | 状态 |
|---------|--------|---------|------|
| [#4013](https://github.com/HKUDS/nanobot/issues/4013) | 4 | Stream timeout 在升级到 0.2.0 后频繁出现，用户反馈严重影响实际工作 | ✅ CLOSED / [PR#4272](https://github.com/HKUDS/nanobot/pull/4272) 已修复 |
| [#4233](https://github.com/HKUDS/nanobot/issues/4233) | 2 | 用户希望在 WebUI 中显示版本号，便于快速识别 | ✅ CLOSED / [PR#4255](https://github.com/HKUDS/nanobot/pull/4255) 已实现 |
| [#4259](https://github.com/HKUDS/nanobot/issues/4259) | 2 | 技术细节：history.jsonl 缺乏会话隔离导致系统提示污染 | ✅ CLOSED / [PR#4274](https://github.com/HKUDS/nanobot/pull/4274) 已修复 |

**新开 Issue 热度分析**
- [#4290](https://github.com/HKUDS/nanobot/issues/4290) - CronJob 与 Subagent 协作的阻塞问题，刚发现今天被迅速处理
- [#4279](https://github.com/HKUDS/nanobot/issues/4279) - Subagent 实时通知导致 LLM 幻觉，提出了聚合通知的架构建议

---

## 🐛 Bug 与稳定性

### 已关闭/修复（7 条）

| Issue | 严重性 | 描述 | Fix PR |
|-------|--------|------|---------|
| [#4013](https://github.com/HKUDS/nanobot/issues/4013) | 🔴 **高** | LLM stream stalled 导致用户被迫手动重启任务 | [#4272](https://github.com/HKUDS/nanobot/pull/4272) |
| [#4261](https://github.com/HKUDS/nanobot/issues/4261) | 🟡 **中** | GPT-5.x 期望 max_completion_tokens 而非 max_tokens | 直接修复 |
| [#4237](https://github.com/HKUDS/nanobot/issues/4237) | 🟡 **中** | bwrap 沙箱未重置 HOME，导致工具写入失败 | 直接修复 |
| [#3934](https://github.com/HKUDS/nanobot/issues/3934) | 🟡 **中** | exec 工具 PATH 优先级问题，pip install 被系统 Python 拦截 | [#4273](https://github.com/HKUDS/nanobot/pull/4273) |
| [#4259](https://github.com/HKUDS/nanobot/issues/4259) | 🟡 **中** | 会话历史跨会话污染系统提示 | [#4274](https://github.com/HKUDS/nanobot/pull/4274) |
| [#4000](https://github.com/HKUDS/nanobot/issues/4000) | 🟢 **低** | feat: StepFun ASR provider 支持 | 设计建议 |
| [#4233](https://github.com/HKUDS/nanobot/issues/4233) | 🟢 **低** | 功能需求：WebUI 版本显示 | [#4255](https://github.com/HKUDS/nanobot/pull/4255) |

### 待处理/新增（5 条 OPEN）

| Issue | 严重性 | 描述 | 关联 PR |
|-------|--------|------|---------|
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) | 🔴 **高** | 空 API 返回无法触发降级模型，DeepSeek 在高峰期返回无 choices | [#4288](https://github.com/HKUDS/nanobot/pull/4288) 待审 |
| [#4290](https://github.com/HKUDS/nanobot/issues/4290) | 🔴 **高** | CronJob 生成子代理时早期退出，子代理结果无法回注，导致后续工作流失败 | [#4293](https://github.com/HKUDS/nanobot/pull/4293) 待审 |
| [#4286](https://github.com/HKUDS/nanobot/issues/4286) | 🟡 **中** | 用户报告"sustained goal"上下文缺失，影响长期任务连贯性 | - |
| [#4279](https://github.com/HKUDS/nanobot/issues/4279) | 🟡 **中** | 架构议题：Subagent 实时通知增加 LLM 幻觉风险 | - |

---

## ✨ 功能请求与路线图信号

### 已实现（本周期）
- ✅ [#4233](https://github.com/HKUDS/nanobot/issues/4233) WebUI 版本显示 → [#4255](https://github.com/HKUDS/nanobot/pull/4255)
- ✅ [#4000](https://github.com/HKUDS/nanobot/issues/4000) StepFun ASR 支持 → 计划中
- ✅ [#3934](https://github.com/HKUDS/nanobot/issues/3934) exec 路径优先级 → [#4273](https://github.com/HKUDS/nanobot/pull/4273)

### 进行中（PR 待审）
- 🔄 [#4291](https://github.com/HKUDS/nanobot/pull/4291) **feat(spawn): allow subagents to use configurable model presets**  
  支持子代理使用不同的模型配置，增强多模型编排能力。

- 🔄 [#4289](https://github.com/HKUDS/nanobot/pull/4289) **feat(slack): add groupRequireMention to scope allowlist channels**  
  Slack 集成增强，允许在白名单频道中仅响应 @mention。

- 🔄 [#4284](https://github.com/HKUDS/nanobot/pull/4284) **feat(webui): activate skills from slash palette**  
  WebUI 斜杠命令支持技能激活。

- 🔄 [#4282](https://github.com/HKUDS/nanobot/pull/4282) **feat: add file management features to the settings view**  
  解决用户手动复制生成文件的痛点，增加文件浏览与管理。

### 架构讨论/增强建议
- 💡 [#4279](https://github.com/HKUDS/nanobot/issues/4279) **Support aggregated notifications for subagents**  
  提议聚合 Subagent 通知而非实时推送，降低 LLM 幻觉风险。

---

## 💬 用户反馈摘要

### 核心痛点

1. **流稳定性** ([#4013](https://github.com/HKUDS/nanobot/issues/4013))  
   用户从 0.1.5 升级到 0.2.0 后频繁遇到"stream stalled for more

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 | 2026-06-11

## 1. 今日速览

ZeroClaw 项目今日保持**高度活跃**，过去24小时共更新 **43条 Issue**（新开/活跃 24条，已关闭 19条）和 **50条 PR**（待合并 40条，已合并/关闭 10条），零版本发布。当前项目重心聚焦跨平台支持（Windows/macOS 测试框架）、MCP 工具体系完善、多代理委托模式安全性优化，以及 ZeroClaw 核心轻量化的架构讨论。整体呈现**快速迭代、问题导向**的健康开发节奏。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

### 今日合并/活跃 PR 梗概（按重要性排序）

| PR | 类型 | 摘要 | 状态 |
|---|------|------|------|
| [#7487](https://github.com/zeroclaw-labs/zeroclaw/pull/7487) | CI | 质量门质量在合并队列上支持 `merge_group` 触发器（步骤1/2启用merge queue） | 开放 |
| [#7385](https://github.com/zeroclaw-labs/zeroclaw/pull/7385) | 可观测性 | 添加转向元数据到观察者事件，按 turn_id 关联 OTel spans | 开放，大型，高风险 |
| [#7450](https://github.com/zeroclaw-labs/zeroclaw/pull/7450) | Doctor | `models list`/`doctor` 展示配置的模型；增加 `--check` 标志；折叠探针行 | 开放，中等，高风险 |
| [#7483](https://github.com/zeroclaw-labs/zeroclaw/pull/7483) | ZeroCode UX | 将默认编辑器从 vi 改为 nano（容器镜像兼容性） | 开放，修复 #7469 |
| [#7484](https://github.com/zeroclaw-labs/zeroclaw/pull/7484) | ZeroCode UX | 防止 macOS Cmd-C 触发 Quit 快捷键 | 开放，修复 #7378 |
| [#7481](https://github.com/zeroclaw-labs/zeroclaw/pull/7481) | 本地化 | quickstart 提供者选择器提示本地化（支持现有 CLI 语言） | 开放 |
| [#7475](https://github.com/zeroclaw-labs/zeroclaw/pull/7475) | 文档 | 添加无根 Debian Compose 示例（修复 #6760） | 开放 |

**关键推进**：可观测性模块增强（OTel 关联），Doctor 命令增强（模型可见性），ZeroClaw UX 跨平台兼容性修复（编辑器、快捷键），本地化扩展。项目在**易用性**和**可观测性**两个维度并行推进。

---

## 4. 社区热点

### 评论最活跃的 Issues

| 排序 | Issue | 评论数 | 作者 | 核心诉求 |
|------|-------|--------|------|---------|
| 1 | [#3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) 「Full Docker Image」 | 12 | @LaurensBosscher | 提供包含所有特性标志的完整 Docker 镜像（如 WhatsApp），降低新用户入门门槛 |
| 2 | [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) 「User Message Loss Bug」 | 6 | @lazy-hs | 单轮/多轮对话中 user message 丢失现象（P1 阻塞工作流） |
| 3 | [#6721](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) 「tool_search Hanging」 | 5 | @nick-pape | tool_search 不在 default_auto_approve，webhook 模式下挂起 120s 后自动拒绝（P1） |
| 4 | [#6309](https://github.com/zeroclaw-labs/zeroclaw/issues/6309) 「schema_version Stomp」 | 5 | @eugeneb50 | model_routing_config upsert 覆盖 schema_version=2 设置（已关闭） |

### 分析

- **最活跃 Issue 反映产品层需求**：#3642（Docker UX）反映新用户上手痛点——现有最小化镜像策略对非技术用户不友好
- **P1 Bug 集中在数据一致性**：#6034（消息丢失）和 #6721（工具拒绝）都触及"沉默失败"危害，需优先修复
- **配置系统存在版本迁移问题**：#6309 反映 schema 升级场景下的向后兼容性漏洞

---

## 5. Bug 与稳定性

### 优先级梯度分布

#### **P1 级别（工作流阻塞，需立即处理）**

| Issue | 标签 | 风险 | 状态 | Fix PR | 摘要 |
|-------|------|------|------|--------|------|
| [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) | provider, runtime | 高 | 开放 | ❌ | 单/多轮对话丢失 user message（运行时守护进程） |
| [#6721](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) | agent, tool:mcp, gateway | 高 | 开放 | ❌ | tool_search 缺失 default_auto_approve，webhook 模式挂起 120s |
| [#7263](https://github.com/zeroclaw-labs/zeroclaw/issues/7263) | agent, gateway, tool | 高 | 开放 | ❌ | 子代理在 ACP 会话中未继承 cwd（ACP 频道工作流破坏） |
| [#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470) | agent, security, tool:delegate | 高 | 开放 | ❌ | delegate 代理模式：empty allowed_tools 被拒，同级风险配置阻止严格委托目标 |
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | ci, tests, runtime | 高 | 开放 | ❌ | **74 个 Windows 测试失败**（Unix-only 命令、路径语义、控制台编码） |

#### **P2 级别（功能降级，需近期处理）**

| Issue | 类型 | 状态 | Fix PR | 简述 |
|-------|------|------|--------|------|
| [#6722](https://github.com/zeroclaw-labs/zeroclaw/issues/6722) | bug, config, memory | 关闭 | ✅ | MemoryConfig.rerank_enabled/rerank_threshold 已移除但无消费方 |
| [#7436](https://github.com/zeroclaw-labs/zeroclaw/issues/7436) | bug, tool:image_info | 开放 | ❌ | image_info 工具输出在相对路径调用时未传递给视觉模型 |
| [#6958](https://github.com/zeroclaw-labs/zeroclaw/issues/6958) | bug, channel:matrix | 关闭 | ✅ | Matrix 频道按 event_id 建立会话导致消息间"失忆"（已修复） |

#### **安全/数据损失级（S0-S2）**

| Issue | 严重程度 | 摘要 | 状态 |
|-------|---------|------|------|
| [#4627](https://github.com/zeroclaw-labs/zeroclaw/issues/4627) | S0 - 数据丢失/安全风险 | file_write 工具报告成功但主机文件系统不可见（Docker 安全隔离问题） | 关闭 ✅ |
| [#5810](https://github.com/zeroclaw-labs/zeroclaw/issues/5810) | S2 - 配置安全可见 | security.otp.gated_actions 无效验证，接受任意字符串 | 关闭 ✅ |

### 跨平台支持危机

**核心问题**：Linux 是唯一的 CI 测试环境（#7409 已关闭）。Windows 测试套件包含 74 个失败：
- Unix-only 命令（find, touch, head）
- 路径分隔符语义（\ vs /）
- 控制台编码（936 简体中文 vs UTF-8）

对应 PR [#7486](https://github.com/zeroclaw-labs/zeroclaw/issues/7486) 建议添加非必需的跨平台 Clippy 工作流（已关闭，恢复为 Linux-only）。

---

## 6. 功能请求与路线图信号

### 社区提议的主要增强（RFC/Feature）

| Issue | 作者 | 标题 | 风险/优先级 | 信号 | 链接 |
|-------|------|------|-----------|------|------|
| [#3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) | @LaurensBosscher | Full Docker Image (all features) | 中/P2，已接受 | **UX 关键路径**：新用户现阶段被迫选择功能受限镜像 | [详情](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) |
| [#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) | @ilteoood | RFC: 轻量化 ZeroClaw 核心（通过外部集成） | 高/P2，已接受 | **架构重构信号**：将 gws-cli、jira、github 等移至 skills，减少核心依赖 | [详情](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) |
| [#7431](https://github.com/zeroclaw-labs/zeroclaw/issues/7431) | @mov-xound-glitch | Pre-turn 路由意图提取 | 高/P2，已接受 | **Agent 行为改进**：send_via 路由需要轻量级预检测，避免显式调用 | [详情](https://github.com/zeroclaw-labs/zeroclaw/issues/7431) |
| [#7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) | @Nillth | RFC: 统一三个 Agent Turn 引擎 | 高/P2 | **代码质量**：run_tool_call_loop、turn_streamed、Agent::turn 三套引擎重复，两套缺安全审计 | [详情](https://github.com/zeroclaw-labs/zeroclaw/issues/7415) |
| [#7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) | @Vitaly567 | RFC: 原生动态库插件系统 | 高/P2 | **扩展性愿景**：替代当前单体架构，支持生态级插件市场 | [详情](https://github.com/zeroclaw-labs/zeroclaw/issues/7420) |
| [#7468](https://github.com/zeroclaw-labs/zeroclaw/issues/7468) | @damajor | Allow aliases to be renamed | 中/P2 | **ZeroCode TUI 增强**：别名改名功能缺失，配置编辑体验不完整 | [详情](https://github.com/zeroclaw-labs/zeroclaw/issues/7468) |
| [#7467

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报
**日期**: 2026-06-11 | **周期**: 过去24小时

---

## 📊 今日速览

PicoClaw 项目今日活跃度**中等偏高**，共发生 20 项更新（5 个 Issues + 15 个 PRs），其中 6 个 PR 已合并/关闭，维护节奏保持稳定。值得关注的是，今日新增 2 个 **安全问题**（1 个已修复）和 2 个**核心功能 Bug**（均已有对应 PR），核心功能与安全防御得到及时响应。同时，15 个 PRs 中包含多个代码质量改进（类型断言检查），反映项目对稳定性的持续投入。发布了 nightly build v0.2.9-nightly.20260611，继续迭代中。

---

## 🚀 版本发布

### Nightly Build: v0.2.9-nightly.20260611
- **发布时间**: 2026-06-11
- **构建哈希**: d955d5bb
- **性质**: 自动化构建，**不稳定，请谨慎使用**
- **完整变更日志**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **说明**: Nightly 版本用于开发测试，不建议生产环境部署

---

## ✅ 项目进展

### 已合并/关闭的 PR（6 项）

| PR | 类型 | 说明 |
|---|---|---|
| [#3089](https://github.com/sipeed/picoclaw/pull/3089) | 🐞 修复 | **os.Root Windows 兼容性** — 修复 `list_dir` 在 Windows 上因路径分隔符不匹配导致的"invalid argument"错误（关联 Issue [#2472](https://github.com/sipeed/picoclaw/issues/2472)） |
| [#3085](https://github.com/sipeed/picoclaw/pull/3085) | 🔒 安全 | **SSRF 防护加固** — 阻止 RFC 2544 基准地址范围 198.18.0.0/15（关联 Issue [#3077](https://github.com/sipeed/picoclaw/issues/3077)） |
| [#3043](https://github.com/sipeed/picoclaw/pull/3043) | 🐞 修复 | **错误处理完善** — 修复 `strconv.Atoi` 和 `json.Unmarshal` 的错误被忽略问题 |
| [#2951](https://github.com/sipeed/picoclaw/pull/2951) | 🐞 修复 | **Web Search API 兼容性** — 改用 function 类型以兼容不支持 `web_search_preview` 的 OpenAI 端点 |
| [#2948](https://github.com/sipeed/picoclaw/pull/2948) | 🐞 修复 | **Claude Opus 4.7 模型支持** — 移除不支持的 temperature 参数 |
| [#2945](https://github.com/sipeed/picoclaw/pull/2945) | ✨ 新功能 | **调试工具** — 新增 picoclaw-tracer，提供 JSON-Lines 日志的实时 LLM 调用链可视化 |

**评估**: 修复了 1 个平台兼容性关键问题、1 个安全漏洞、3 个 API 兼容性问题，新增 1 个开发者工具。项目整体**稳定性和兼容性提升显著**。

---

## 🔥 社区热点

### 评论/反应最活跃（按热度排序）

1. **[#2472](https://github.com/sipeed/picoclaw/issues/2472) — Windows 路径分隔符 Bug** ⭐ 高
   - 评论: 5 条 | 👍: 1 | 状态: OPEN（已有 Fix PR #3089）
   - 背景: `list_dir` 因路径分隔符不匹配在 Windows 失败，已存在超过 2 个月（创建于 2026-04-10）
   - 社区关注: 表明 **Windows 用户基数显著** 且该问题影响文件操作基础功能
   - 进展: PR 已完成，待合并

2. **[#3094](https://github.com/sipeed/picoclaw/issues/3094) — 异步子代理重复消息 Bug** ⚠️ 中高
   - 状态: 刚新开（2026-06-10），暂无评论
   - 影响: `spawn` 工具派发异步任务时会在飞书/Telegram 重复推送（1 条原始、1 条汇总）
   - 用户体验问题，**迫切需要修复**

3. **[#3077](https://github.com/sipeed/picoclaw/issues/3077) — SSRF 绕过漏洞** 🔴 严重
   - 状态: 已关闭（2026-06-10）
   - 内容: `web_fetch` 因忽略 198.18.0.0/15 范围导致 SSRF 绕过
   - 进展: 已发布修复 PR #3085，及时响应

---

## 🐛 Bug 与稳定性

### 按严重程度分类（5 个 Issues）

#### 🔴 **严重级** 

| Issue | 简述 | 状态 | Fix |
|-------|------|------|-----|
| [#2472](https://github.com/sipeed/picoclaw/issues/2472) | Windows 路径分隔符导致 `list_dir` 失败 | OPEN | [PR #3089](https://github.com/sipeed/picoclaw/pull/3089) 已合并 |
| [#3077](https://github.com/sipeed/picoclaw/issues/3077) | SSRF 防护绕过（198.18.0.0/15） | CLOSED | [PR #3085](https://github.com/sipeed/picoclaw/pull/3085) 已合并 ✅ |

#### ⚠️ **高级**

| Issue | 简述 | 状态 | Fix |
|-------|------|------|-----|
| [#3094](https://github.com/sipeed/picoclaw/issues/3094) | spawn 异步任务重复推送消息 | OPEN | **无 PR，需要新建** |
| [#3090](https://github.com/sipeed/picoclaw/issues/3090) | iOS < 16.4 Safari 上 Panel 不可用 | OPEN | **无 PR** |

#### 💡 **低级/功能请求**

| Issue | 简述 | 状态 | 
|-------|------|------|
| [#3093](https://github.com/sipeed/picoclaw/issues/3093) | 功能请求: SimpleX/Tox 网关支持 | OPEN |

### 代码质量风险

今日合并的 PRs 中，多个 **代码质量修复** 待合并（仍在 OPEN）：
- [#3095](https://github.com/sipeed/picoclaw/pull/3095): `CreateHTTPClient` 类型断言缺少 `ok` 检查（panic 风险）
- [#3091](https://github.com/sipeed/picoclaw/pull/3091): openai_compat 类型断言缺少 `ok` 检查
- [#3092](https://github.com/sipeed/picoclaw/pull/3092): skills_install 类型断言缺少 `ok` 检查
- [#3053](https://github.com/sipeed/picoclaw/pull/3053): evolution 模块 sync.Map 类型断言缺少 `ok` 检查

**风险评估**: 这些都是**隐藏的 panic 风险**，需要优先合并以提升稳定性。

---

## 🎯 功能请求与路线图信号

### 新功能需求

| 需求 | 提出者 | 链接 | 分析 |
|-----|-------|------|------|
| SimpleX/Wire/Tox 网关支持 | @Damian-o2 | [#3093](https://github.com/sipeed/picoclaw/issues/3093) | **通信隐私工具**：用户需要更多去中心化通信渠道，表明安全/隐私用户占比提升 |

### 已进行中的重要特性

| PR | 特性 | 进度 | 说明 |
|----|------|------|------|
| [#2937](https://github.com/sipeed/picoclaw/pull/2937) | Agent Collaboration Bus | OPEN + 已标记 stale | 多智能体内部通信框架，功能完整但未合并，可能需要重新评估 |
| [#3087](https://github.com/sipeed/picoclaw/pull/3087) | 工作空间相对路径 exec 支持 | OPEN | 修复 `restrict_to_workspace` 的误判，改进用户体验 |
| [#3083](https://github.com/sipeed/picoclaw/pull/3083) | Launcher 网络访问控制强化 | OPEN | 加强部署安全性，支持信任代理配置 |

---

## 💬 用户反馈摘要

### 核心用户痛点

1. **跨平台兼容性** (Windows/iOS)
   - Windows 用户反映 `list_dir` 路径问题（已修复）
   - iOS < 16.4 用户 Safari 无法使用 Panel
   - **信号**: 需要更完善的跨平台测试覆盖

2. **消息投递可靠性**
   - 异步子代理任务完成时重复推送（#3094）
   - 表明多通道投递逻辑需要重新设计

3. **安全/隐私诉求**
   - 新增 SimpleX/Tox 网关需求（端到端加密）
   - 前期的 SSRF 漏洞反映安全防护仍有盲点

4. **开发者体验**
   - picoclaw-tracer 新增（#2945），说明用户需要更好的调试工具
   - workspace 相对路径支持请求（#3087），反映本地开发场景复杂

---

## ⏳ 待处理积压

### 长期未响应的重要 Issue/PR

| 项目 | 创建时间 | 天数 | 优先级 | 说明 |
|-----|---------|------|-------|------|
| [#2472](https://github.com/sipeed/picoclaw/issues/2472) | 2026-04-10 | **62 天** | 🔴 严重 | Windows 路径问题，已有 PR 但未看到最新更新，建议加速合并 |
| [#2937](https://github.com/sipeed/picoclaw/pull/2937) | 2026-05-24 | **18 天** | 🟡 中等 | Agent Collaboration Bus，标记 stale，核心功能未推进，需要决策：继续还是搁置 |
| [#3067](https://github.com/sipeed/picoclaw/pull/3067) | 2026-06-09 | 2 天 | 🟡 中等 | 会话范围配置无法保存，影响用户配置持久化，应尽快合并 |

### 待合并 PR 堆积（9 个）

仍在 OPEN 状态、未合并的 PR 数量较多，建议：
1. **优先级排序**: 代码质量 (panic 风险) > 用户配置持久化 > 新特性
2. **Review 加速**: 多个 PR 已准备就绪，Review 瓶颈可能需要加强
3. **Stale 清理**: [#2937](https://github.com/sipeed/picoclaw/pull/2937) 、[#2951](https://github.com/sipeed/picoclaw/pull/2951) 等已合并，建议标记为 stale 的 PR 明确状态

---

## 📈 总体评估

| 指标 | 状态 | 评论 |
|-----|------|------|
| **活跃度** | ✅ 健康 | 20 项更新/日，维护者响应及时 |
| **稳定性** | ⚠️ 需关注 | 5 个活跃 Bug，其中 2 个严重；多个 panic 风险代码待修复 |
| **安全性** | ✅ 主动 | 及时发现并修复 SSRF 漏洞，防护意识强 |
| **社区** | 🟡 中等 | 用户反馈积极，功能诉求多元（跨平台、隐私、开发工具） |
| **代码质量** | 🟡 改进中 |

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报（2026-06-11）

## 1. 📊 今日速览

NanoClaw 今日保持高速迭代节奏，24小时内新增2个 Issue、12条 PR，其中4条已合并/关闭，8条待处理。项目活跃度高，特别是 Telegram 集成、容器日志、安全加固等多条主线同步推进。新报告的 Bug（#2731 egress-lockdown 网络隔离问题）表明生产环境正面临网络配置挑战，亟需修复。**整体评估**：开发高速但潜在技术债积累，待合并 PR 积压需加快审核。

---

## 2. 📦 版本发布

**无新版本发布**

---

## 3. 🚀 项目进展

### 已合并/关闭（4条）

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#2719](https://github.com/nanocoai/nanoclaw/pull/2719) | feat: add uninstall.sh | CLOSED | 新增按副本卸载器，含确认、模拟运行、OneCLI 清理，提升用户体验 |
| [#2721](https://github.com/nanocoai/nanoclaw/pull/2721) | docs: customizing intro & skill guidelines | CLOSED | 文档框架完善，确立技能模型定制规范（解决更新冲突问题） |
| [#3](https://github.com/nanocoai/nanoclaw/pull/3) | feat: per-group namespace IPC | CLOSED | 安全加固：IPC 命名空间隔离防止特权提升（长期任务，今日闭合） |
| [#2724](https://github.com/nanocoai/nanoclaw/pull/2724) | （误提交） | CLOSED | 忽略 |

**核心进展**：安全隔离完成、文档框架确立、卸载流程优化，项目朝向生产就绪迈进。

---

## 4. 💬 社区热点

### 高热度讨论

**[#1690 - Multi-runtime agent SDK abstraction](https://github.com/nanocoai/nanoclaw/issues/1690)**
- **状态**: OPEN | **讨论热度**: 6 评论，3 👍 | **创建**: 2026-04-07 | **最后活跃**: 2026-06-10
- **核心话题**: 提议在 NanoClaw 上实现多运行时抽象层（Claude + Codex + 本地模型），模式化为 skill（如 `/add-telegram`）
- **诉求分析**: 用户希望将不同 Agent SDK 作为可插拔模块集成，解决 SDK 多样化问题
- **状态**: 讨论中，未有 PR 响应

**[#2731 - Egress lockdown hijacks host.docker.internal](https://github.com/nanocoai/nanoclaw/issues/2731)** ⚠️ **新报告**
- **状态**: OPEN（刚刚报告，0 评论）| **创建**: 2026-06-11 | **严重性**: 高
- **问题**: `NANOCLAW_EGRESS_LOCKDOWN=true` 启用时，agents 无法访问 host 本地服务（ollama、localhost 代理等）
- **影响范围**: 所有依赖 `host.docker.internal` 的内网 agents
- **响应状态**: 无人认领，等待 [@sturdy4days](https://github.com/sturdy4days) 跟进

---

## 5. 🐛 Bug 与稳定性

### 待修复（2条）

| Issue | 标题 | 严重性 | 相关 PR | 进度 |
|---|---|---|---|---|
| [#2731](https://github.com/nanocoai/nanoclaw/issues/2731) | Egress lockdown 劫持 host.docker.internal | **高** | 无 | 新报告，需立即处理 |
| 隐含于 [#2730](https://github.com/nanocoai/nanoclaw/pull/2730) | .env 环境变量不被 launchd/systemd 加载 | **中** | [#2730](https://github.com/nanocoai/nanoclaw/pull/2730) 待合并 | PR 已就绪，待审核 |

### 已有修复 PR（3条）

| PR | Bug 描述 | 状态 |
|---|---|---|
| [#2730](https://github.com/nanocoai/nanoclaw/pull/2730) | NANOCLAW_* flags 在 .env 中被忽略 | **OPEN 待审** |
| [#2728](https://github.com/nanocoai/nanoclaw/pull/2728) | Telegram wire-to 配对未创建数据库行 | **OPEN 待审** |
| [#2729](https://github.com/nanocoai/nanoclaw/pull/2729) | Telegram 文档状态块命名不一致 + 适配器 pin 错误 | **OPEN 待审** |
| [#2611](https://github.com/nanocoai/nanoclaw/pull/2611) | 【安全】approval 后丢失 caller context | **OPEN 待审** |

**稳定性评估**：环境变量加载、Telegram 集成在暴露问题，egress-lockdown 隔离策略需要重新评估。

---

## 6. 🎯 功能请求与路线图信号

### 待合并新功能（7条）

| PR | 功能 | 优先级信号 | 预期影响 |
|---|---|---|---|
| [#2726](https://github.com/nanocoai/nanoclaw/pull/2726) | `/add-guardrails` skill - 每组 Agent 输入/输出守护栏 | **高** | 安全加固，正则/关键词规则，阻止提示注入、凭证泄露 |
| [#2727](https://github.com/nanocoai/nanoclaw/pull/2727) | Agent 容器 stdout/stderr 持久化到磁盘 | **中** | 提升可观测性，配合 amplifier-app-nanoclaw#7 |
| [#2725](https://github.com/nanocoai/nanoclaw/pull/2725) | `web-search-plus` skill - 多源网络搜索 + 抽取 | **中** | 无 MCP 依赖，源于 hermes-web-search-plus |
| [#2211](https://github.com/nanocoai/nanoclaw/pull/2211) | `tool-visibility` skill - 工具调用实时预览 | **中** | 长期任务（5月3日开始），符合 skill 指南重构 |
| [#1690](https://github.com/nanocoai/nanoclaw/issues/1690) | 多运行时 SDK 抽象（无对应 PR） | **低** | 讨论阶段，尚未有实现 |

**路线图信号**：
- **安全加固** 是核心方向（guardrails、per-group IPC）
- **Skill 生态** 快速扩展（tool-visibility、web-search-plus、guardrails）
- **可观测性** 持续改进（容器日志、tool 可见性）
- **多运行时支持** 仍在讨论，短期无进展

---

## 7. 👥 用户反馈摘要

### 来自 Issue #1690（多运行时抽象）
- **用户痛点**: Agent SDK 多样化（Claude、Codex、本地模型），需要统一接口
- **期望模式**: 作为 skill 插件化，而非核心功能
- **反应度**: 3 👍，6 评论，表明社区关注但进展缓慢

### 来自 Issue #2731（Egress lockdown）
- **实际使用场景**: 用户配置了 ollama 或 host-side 代理，期望 agents 能访问
- **安全与可用性矛盾**: 启用网络隔离后服务完全不可达，当前方案过度严格
- **紧急性**: 刚报告（今日），无迂回方案，生产环境受影响

### 隐含需求（从多个 PR）
- **Telegram 集成** 用户较多（#2728、#2729 均在修复）
- **文档完整性** 重视（skill 指南、customizing 文档已成体系）
- **安全性** 被优先级提升（guardrails、IPC 隔离、caller context 保留）

---

## 8. ⏳ 待处理积压

### 高优先级积压

| PR/Issue | 类型 | 开启时间 | 天数 | 状态 | 建议 |
|---|---|---|---|---|---|
| [#2611](https://github.com/nanocoai/nanoclaw/pull/2611) | 安全 PR | 2026-05-25 | **17 天** | OPEN 待审 | **加快审核**，涉及权限上下文，风险敏感 |
| [#2211](https://github.com/nanocoai/nanoclaw/pull/2211) | 功能 PR | 2026-05-03 | **39 天** | OPEN 待审 | **超长期积压**，已符合 skill 指南，建议立即合并或拒绝 |
| [#1690](https://github.com/nanocoai/nanoclaw/issues/1690) | 讨论 Issue | 2026-04-07 | **65 天** | OPEN | **方向确认缺失**，维护者未表态是否纳入路线图 |

### 新增紧急

| Issue | 类型 | 报告时间 | 影响 | 建议 |
|---|---|---|---|---|
| [#2731](https://github.com/nanocoai/nanoclaw/issues/2731) | 高危 Bug | 2026-06-11（今日）| Egress lockdown 完全破坏本地服务可达性 | **立即处理**，可能需要重新设计网络隔离策略 |

### 审核队列现状
- **待审核 PR**: 8 条（#2611, #2730, #2729, #2728, #2727, #2726, #2211, #2725）
- **平均等待时间**: 约 10-39 天
- **建议**: 建立 PR 审核 SLA（安全 PR < 3 天，功能 PR < 7 天）

---

## 📈 关键指标

| 指标 | 值 | 评价 |
|---|---|---|
| 24h 活跃度（PR + Issue） | 14 条 | ✅ 很高 |
| 合并率（过去24h） | 33%（4/12） | ⚠️ 正常但积压累积 |
| 安全相关 PR | 2 条（#2611, #3） | ✅ 重视安全 |
| 文档更新 | 2 条（#2721, #2729） | ✅ 同步维护 |
| 新 Bug 报告 | 1 条（#2731） | ⚠️ 生产环境有隐患 |
| 待处理高优先级 | 3 条 | ⚠️ 需加速 |

---

**报告日期**: 2026-06-11 | **数据来源**: GitHub API | **下次更新**: 2026-06-12

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-06-11

## 1. 今日速览

IronClaw 项目今日保持极高活跃度：**过去24小时新增/更新 50 个 Issues 与 50 个 PRs**，其中 15 个 Issues 已关闭，22 个 PRs 已合并/关闭。项目重心集中在 **Reborn WebUI v2 产品化** 和 **认证/授权流程完善** 上，但尚未发布新版本（最后发布停留在 v0.24.0，crates.io 尚未同步最新 tag）。社区反馈中 UX 问题和配置体验最为集中。

---

## 2. 版本发布

**无新版本今日发布。** 

⚠️ **待发布版本积压：** 
- **#3259** [14 评论] — 发布 0.25.0–0.27.0 到 crates.io：GitHub repo 已发布至 v0.27.0（2026-04-29），但 crates.io 仅有 0.24.0（2026-03-31）。下游消费者受 wasmtime 28.x CVE 影响被钉死在 0.24.0。
- **#3708** [开放中] — 自动发布 PR 包含：`ironclaw_common` 0.4.2→0.5.0（**破坏性变更**），`ironclaw_safety` 0.2.2→0.2.3，主版本 0.24.0→0.29.1。

---

## 3. 项目进展

**今日已合并/关闭 8 个关键 PR，推进核心功能：**

| PR | 功能模块 | 进展说明 |
|---|---|---|
| **#4746** [已关闭] | 认证门控恢复 | OAuth 完成后自动重新派遣能力调用（修复 Google Calendar 功能状态） |
| **#4745** [已关闭] | 自动化面板重构 | 将 Automations 面板从能力派遣改为直接 TriggerRepository 读取，简化架构 |
| **#4743** [已关闭] | NEAR 错误分类 | 修复 NEAR/Anthropic `prompt too long` 响应的 ContextLengthExceeded 分类与 token 计数解析 |
| **#4742** [已关闭] | 手动 token 凭证 | 线程化运行时凭证模式（ManualToken vs OAuth）支持，允许手动 token 满足运行时请求 |
| **#4717** [已关闭] | WebUI v2 Always Approval | 恢复始终批准（Always Allow）affordance，保留在 live gate 事件与投影重放中 |
| **#4730** [已关闭] | Slack DM 触发交付 | 完成个人范围事件交付：用户配对 Slack → 自动配置 DM 目标 → 在 Settings 选择为默认 |
| **#4739** [已关闭] | QA 环境 Slack 启用 | 在 Railway 烤地配置中启用 Slack |
| **#4652** [已关闭] | 文档 + 启动脚本 | 发布 Reborn serve/WebUI 完整测试流程文档 + `run-reborn-webui.sh` 一键启动器 |

**整体评估：** Reborn 产品闭环加速，认证/授权、事件交付、WebUI 交互等核心体验在逐日完善。

---

## 4. 社区热点

**讨论最活跃的 Issue & PR：**

| # | 标题 | 评论 | 链接 | 要点 |
|---|---|---|---|---|
| **#3259** | Publish 0.25.0–0.27.0 to crates.io — downstream pinned by wasmtime CVEs | 14 | [详情](https://github.com/nearai/ironclaw/issues/3259) | 版本同步延迟导致下游被迫停留在有 CVE 的版本；发布流程堵塞 |
| **#3036** | [EPIC] Configuration-as-Code for IronClaw Reborn | 6 | [详情](https://github.com/nearai/ironclaw/issues/3036) | 操作员呼声：声明式配置（`.env` + 工作区文档 → schema-driven blueprint） |
| **#3283** | [Reborn] Migrate OpenAI-compatible chat APIs onto Reborn | 3 | [详情](https://github.com/nearai/ironclaw/issues/3283) | 关键战略：OpenAI API 兼容性迁移到 Reborn（已关闭，合并中） |

---

## 5. Bug 与稳定性

**今日报告 20+ 新 Bug，按严重程度排列：**

### 🔴 **临界（阻断功能）**
- **#4703** — NEAR AI provider 成功添加后无法使用（test connection ✓ → save ✗）；#4731 PR 修复中
- **#4729** — NEAR AI OAuth 本地构建失败：private.near.ai 拒绝非 .near.ai 回调地址
- **#4706** — 授权流程失败/取消后无恢复：GitHub/Google 登录失败、钱包取消后卡死；#4746 部分修复

### 🟠 **高优（影响首次体验）**
- **#4683** — 无效模型配置返回通用 "driver unavailable" 错误（无法诊断）；#4731 改进
- **#4704** — `builtin.http` 批准后失败，重复提示批准无错误细节
- **#4701** — 批准弹窗缺少 `builtin.http` 请求上下文（无法判断批准内容）

### 🟡 **中等（WebUI/UX 问题）**
- **#4748** — Wrap/No Wrap 代码块切换无效果
- **#4733** — 响应中的链接在当前标签页打开，离开对话
- **#4724** — 新对话的未发送草稿在切换后丢失
- **#4725** — 在 Working 状态下 composer 交互提示仍可交互（视觉误导）
- **#4723** — 新对话 composer 悬停状态仅高亮顶边框
- **#4708** — 代码块缺少语法高亮
- **#4707** — 对话页面字体过小

### 🔵 **低优（报告/诊断问题）**
- **#4741** — 本地开发密钥损坏时错误信息不可理解（"Invalid master key"）
- **#4740** — Slack 工具 schema 仅声明 `action`，其他参数无类型（模型猜测错误）

**已有 Fix PR：** #4731（包含 save + 模型发现 + Settings UI 修复）、#4726（NEAR AI MCP 自动启用）

---

## 6. 功能请求与路线图信号

**进行中的重要特性：**

| PR | 特性 | 规模 | 状态 | 意义 |
|---|---|---|---|---|
| **#4726** | 从 Reborn 环境自动启用 NEAR AI MCP | XL | 开放中 | 改善首次体验：检测 `NEARAI_*` env → 自动激活 MCP |
| **#4731** | LLM provider 配置端到端修复 | XL | 开放中 | 完整 provider setup → model discovery → 活跃 provider 解析 |
| **#4738** | 附件上传 WebUI（WebChat v2 SPA） | XL | 开放中 | 补齐后端附件存储的前端端点 |
| **#4744** | 根据 product auth 门控扩展激活 | XL | 开放中 | 在发布能力前验证扩展凭证需求 |
| **#4735** | 可编程 MCP 服务器配置 + PATCH | XL | 开放中 | 扩展 API：一次性配置 MCP 服务器 + 后续更新而无需拆卸 |
| **#4559** | Trace Commons 邀请链接自动化 | XL | 开放中 | 取代 15+ CLI 参数的 agent 驱动 onboarding |

**Epic 级别需求：**
- **#3036** — Configuration-as-Code（6 评论持续讨论）：声明式 blueprint + use-case harness，取代手编 `.env` + workspace docs

---

## 7. 用户反馈摘要

从 20+ 新 Issues 中提炼用户真实痛点：

**🎯 首次体验与入门：**
- **配置困扰** — provider 配置无 schema、无 diff、无审计跟踪（#3036）
- **提供商设置不完整** — NEAR AI 添加后无法使用、OAuth 回调在本地构建失败（#4703, #4729）
- **模型发现缺失** — Settings UI 无法清晰列出可用模型（#4731 修复中）

**💬 对话体验：**
- **信息丢失** — 未发送草稿被清除；link 点击离开对话；权限流失败后卡死（#4724, #4733, #4706）
- **细节磨损** — 字体小、代码块无高亮、批准弹窗无上下文（#4707, #4708, #4701）
- **交互反馈不清** — Working 状态下 UI 仍显示可交互；Wrap 切换无反应（#4725, #4748）

**⚙️ 工具与能力：**
- **批准体验差** — http 工具失败后重复提示批准无错误细节（#4704）
- **Schema 覆盖不足** — Slack 工具仅声明部分参数，导致模型调用错误（#4740）

**🔐 认证与权限：**
- **恢复能力缺失** — OAuth 后需要用户重新请求功能（#4746 已修复）
- **错误诊断模糊** — 无效 provider 返回通用错误；密钥损坏错误不可操作（#4683, #4741）

---

## 8. 待处理积压

**长期未解决的关键 Issue：**

| # | 标题 | 创建 | 最后更新 | 天数 | 评论 | 严重级 |
|---|---|---|---|---|---|---|
| **

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报
**日期**: 2026-06-11

---

## 1. 今日速览

LobsterAI 在过去24小时展现出**极高的开发活跃度**，共处理 **25 条 PR**（24 条已合并/关闭，1 条待合并），同步发布了新版本 **2026.6.10**。虽然未新增 Issue 反馈（0 条），但 PR 的数量和质量反映了核心开发团队的高效迭代周期。项目在 **AI 智能体能力扩展**（Computer Use MVP）和 **会话稳定性**（Cowork 上下文连续性）两条主线上取得重要进展。总体健康度评估：**开发活跃，功能演进快速，版本迭代节奏稳定**。

---

## 2. 版本发布

### 📦 LobsterAI 2026.6.10
**发布时间**: 2026-06-10  
**发布链接**: [Release 2026.6.10](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.10)

**核心变更**：
- **feat(data-migration)**: 用户数据备份与恢复能力 (@fisherdaddy, #2125)
- **feat(auth)**: 本地回调登录流 (@liuzhq1986, #2122)
- **feat(settings)**: OpenCla 配置界面支持（摘要被截断，需补充）

**版本特点**：
- ~6,900 行代码新增，~470 行删除，涉及 49 个文件（#2140）
- 包含三大主要功能 + 多项 UI 和 Cowork 会话优化
- 无明显破坏性变更提示，应为兼容性升级

**迁移注意**: 用户数据备份/恢复功能上线，建议在升级前备份关键数据；本地登录支持可能改变认证流，旧版本用户首次升级时需重新配置。

---

## 3. 项目进展

### 本周期合并的重点 PR（按功能维度）

**🤖 AI 能力拓展**
- **#2143**: Computer Use MVP 正式登陆 (@btc69m979y-dotcom) 
  - Windows x64 原生支持，内置计算机使用工具包
  - 支持应用列表、窗口管理、应用启动、屏幕截图等能力
  - 完整的 MCP 服务桥接和运行时生命周期管理
  - [PR 链接](https://github.com/netease-youdao/LobsterAI/pull/2143)

**🧠 会话稳定性与上下文管理**
- **#2145**: Cowork 会话压缩后的上下文连续性改进 (@liuzhq1986)
  - 在 OpenClaw 压缩聊天历史后，Agent 能更可靠地继续任务
  - 新增 LobsterAI 自有的连续性层、安全诊断、会话级任务状态保留
  - [PR 链接](https://github.com/netease-youdao/LobsterAI/pull/2145)

**🔐 认证与基础设施**
- **#2144**: 认证门户 Fallback URL 更新 (@liuzhq1986)
  - 指向新的 LobsterAI 官方门户域名
  - 测试环境与生产环境分离，端点和回调 URL 测试覆盖完整
  - [PR 链接](https://github.com/netease-youdao/LobsterAI/pull/2144)

**🎨 UI 细节优化**
- **#2139**: Markdown、代码块、模型选择器样式精细化 (@fisherdaddy)
  - One Dark/One Light 代码高亮主题切换
  - 代码块默认自动换行，提升可读性
  - [PR 链接](https://github.com/netease-youdao/LobsterAI/pull/2139)

**📋 任务通知与 UI 流程**
- **#2134**: 任务完成通知恢复 (@liuzhq1986)
  - 主窗口关闭后也能通过通知恢复会话
  - macOS 通知中心点击保活（系统通知引用管理）
  - [PR 链接](https://github.com/netease-youdao/LobsterAI/pull/2134)

**📦 Windows 工程化**
- **#2142**: NSIS 破坏性初始化修复 & 引擎加载页重设计 (@fisherdaddy)
- **#2141**: Windows 应用内更新修复 (@fisherdaddy)

---

## 4. 社区热点

**当日最重要的讨论与反应**：

由于提供的数据中评论数多为 `undefined`，无法按讨论热度直接排序。但从 **PR 创建时间和功能重要性** 推断：

| PR | 话题 | 热度信号 | 链接 |
|---|---|---|---|
| #2143 | Computer Use MVP 发布 | 🔴 关键功能 | [查看](https://github.com/netease-youdao/LobsterAI/pull/2143) |
| #2145 | Cowork 上下文连续性 | 🔴 核心稳定性 | [查看](https://github.com/netease-youdao/LobsterAI/pull/2145) |
| #2140 | 2026.6.8 版本发布 | 🟠 版本协调 | [查看](https://github.com/netease-youdao/LobsterAI/pull/2140) |
| #1277 | Electron 依赖升级 (stale) | 🟡 技术债 | [查看](https://github.com/netease-youdao/LobsterAI/pull/1277) |

**观察**: 项目近期聚焦于**智能体工具扩展**（Computer Use）和**会话管理健壮性**，这两个方向与 AI 智能体的核心价值主张（更强的自主能力 + 更长的任务生命周期）高度对齐。

---

## 5. Bug 与稳定性

### 已修复的缺陷（本周期）

| 编号 | 标题 | 严重度 | 状态 | 链接 |
|---|---|---|---|---|
| #2142 | NSIS 破坏性初始化 & 引擎加载页 | 🔴 高 | ✅ 已修复 | [PR 2142](https://github.com/netease-youdao/LobsterAI/pull/2142) |
| #2141 | Windows 应用内更新失效 | 🟠 中 | ✅ 已修复 | [PR 2141](https://github.com/netease-youdao/LobsterAI/pull/2141) |
| #1485 | 已禁用技能仍在系统提示中生效 | 🟠 中 | ✅ 已修复 (4月) | [PR 1485](https://github.com/netease-youdao/LobsterAI/pull/1485) |
| #1501 | 禁用技能后仍留在 activeSkillIds | 🟠 中 | ✅ 已修复 (4月) | [PR 1501](https://github.com/netease-youdao/LobsterAI/pull/1501) |

### 潜在稳定性隐患

- **长期积压**：#1277（Electron 版本升级从 40.2.1 → 42.3.3）于 4 月创建，至今仍在 OPEN 状态，可能带来安全更新滞后或依赖不兼容风险。建议优先处理。

---

## 6. 功能请求与路线图信号

### 从 PR 反推的产品方向（下一季度可能重点）

**🤖 已确认交付中：**
- ✅ **Computer Use 工具链** — #2143 已合并，下个版本将全量支持应用自动化
- ✅ **会话上下文智能管理** — #2145 已合并，长对话不再中断
- ✅ **数据迁移与备份** — 2026.6.10 版本已包含，用户可安全迁移配置

**📋 历史积压中可能推进的：**
- 🟠 **Electron 安全更新** (#1277) — 依赖升级需要尽快完成
- 🟠 **定时任务通知渠道** (#1489, #1490, #1486) — 已有多个 PR 改进通知体验，可能在近期集成

**🔮 隐含信号（从 PR 标签和代码区域推测）：**
- `area: cowork` 高频出现 → Cowork 会话稳定性是持续投入点
- `area: renderer` 高频出现 → UI 渲染性能和样式仍在持续磨光
- `area: artifacts` 出现 → 文件/工件管理能力可能在扩展中

---

## 7. 用户反馈摘要

### 从 PR 描述中提炼的用户痛点

| 痛点类别 | 具体表现 | 相关 PR | 用户诉求 |
|---|---|---|---|
| **长对话崩溃** | 会话超出 token 窗口无法恢复 | #1499 | 需要自动会话裁剪，而非强制删除 |
| **技能管理混乱** | 禁用的技能仍被调用 | #1485, #1501 | 配置应立即生效，不留死角 |
| **通知体验割裂** | 多种通知渠道支持不一致 | #1486, #1489, #1490 | 需要统一的本地/远程通知策略 |
| **任务调试低效** | 创建定时任务需反复保存-测试 | #1486 | 想要快速验证功能（Test Task 按钮）|
| **Markdown 编辑原始** | Agent 配置文件编辑体验差 | #1503 | 需要富文本编辑器而非纯文本 |
| **Windows 更新失灵** | 应用内更新无法正常执行 | #2141 | 需要稳定的自动更新流程 |

**总体评估**: 用户反馈围绕 **稳定性**（长对话、通知、更新）和 **体验效率**（编辑、调试、配置）两个核心痛点，团队的 PR 修复方向与用户诉求高度吻合。

---

## 8. 待处理积压

### 长期未响应的关键项

| PR/Issue | 创建时间 | 滞后天数 | 优先级 | 备注 | 链接 |
|---|---|---|---|---|---|
| #1277 | 2026-04-02 | 70+ | 🔴 高 | **Electron 版本升级** (40.2.1 → 42.3.3)，涉及依赖链，可能影响安全性 | [PR 1277](https://github.com/netease-youdao/LobsterAI/pull/1277) |
| #1491 | 2026-04-06 | 66+ | 🟠 中 | GitHub Actions 制品上传插件升级，标记为 `stale` | [PR 1491](https://github.com/netease-youdao/LobsterAI/pull/1491) |
| #1492 | 2026-04-06 | 66+ | 🟠 中 | GitHub Actions Node 配置升级，标记为 `stale` | [PR 1492](https://github.com/netease-youdao/LobsterAI/pull/1492) |
| #1493 | 2026-04-06 | 66+ | 🟠 中 | GitHub Actions Release 上传工具升级，标记为 `stale` | [PR 1493](https://github.com/netease-youdao/LobsterAI/pull/1493) |

### 建议行动

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

# CoPaw 项目动态日报 — 2026-06-11

## 📊 今日速览

CoPaw 项目今日活跃度**极高**，过去24小时共处理 **49 条 PR**（已合并/关闭 30 条，待合并 19 条）和 **33 条 Issue**（新开/活跃 18 条，已关闭 15 条）。项目同步发布 **v1.1.11 正式版**及 beta 版本，核心聚焦于**模型提供商、运行时架构、安全和性能**，整体表现为高效的迭代周期与社区响应。

---

## 🚀 版本发布

### v1.1.11（正式版）
**发布时间**：2026-06-10 | **PR**：[#5080](https://github.com/agentscope-ai/QwenPaw/pull/5080)

**新增功能：**
- **Free Model OAuth**：零配置免费模型一键 OAuth 认证 ([#5049](https://github.com/agentscope-ai/QwenPaw/pull/5049))
- **Xiaomi MiMo Provider**：新增小米 MiMo 内置供应商（Token 计划支持）([#4722](https://github.com/agentscope-ai/QwenPaw/pull/4722))

**关键修复：**
- 修复 Windows OpenSSL 3.5.7 回归 bug（导致桌面客户端无法启动）([#5096](https://github.com/agentscope-ai/QwenPaw/pull/5096))
- DingTalk AI Card 空内容问题修复 ([#5057](https://github.com/agentscope-ai/QwenPaw/issues/5057))

⚠️ **已知问题**：Windows v1.1.11 发布后即刻报告崩溃，已通过 pinning OpenSSL 版本解决 ([#5095](https://github.com/agentscope-ai/QwenPaw/issues/5095), [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086))

### v1.1.11-beta.3
**发布时间**：2026-06-10

**变更**：
- CI 工作流优化（移除冗余 channel-tests）
- **Skill 流程增强**：支持自进化 skill 创建 ([#4857](https://github.com/agentscope-ai/QwenPaw/pull/4857))

---

## ✅ 项目进展

### 本日已合并重要 PR（30 条）

| PR ID | 标题 | 影响范围 | 状态 |
|-------|------|--------|------|
| [#5096](https://github.com/agentscope-ai/QwenPaw/pull/5096) | fix(pack): pin Windows OpenSSL for desktop build | 🟥 关键 | 已合并 |
| [#5094](https://github.com/agentscope-ai/QwenPaw/pull/5094) | fix(security): fix Shield icon centering | 🟩 UI | 已合并 |
| [#5093](https://github.com/agentscope-ai/QwenPaw/pull/5093) | chore: bump version to 1.1.11.post1 | 📌 版本 | 已合并 |
| [#5092](https://github.com/agentscope-ai/QwenPaw/pull/5092) | Revert "fix(pack): compile-check discord" | 🔧 构建 | 已合并 |
| [#5080](https://github.com/agentscope-ai/QwenPaw/pull/5080) | chore: release v1.1.11 | 🚀 版本 | 已合并 |

**19 条待合并 PR 包括**：
- 🏗️ **Runtime 2.0 架构重构** ([#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078))：模块化运行时 + ToolCoordinator，破坏性变更
- 📊 **DataPaw 数据分析插件** ([#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622))：12 个 BI skill，需审核
- 🛡️ **Agent OS Driver** ([#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067))：MCP/A2A/ACP 统一抽象层
- 📈 **Token 使用统计面板** ([#4433](https://github.com/agentscope-ai/QwenPaw/pull/4433))：浮动 Badge + markdown 流式输出

---

## 💬 社区热点

### 评论最多的 5 大 Issues

1. **[#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)** | 评论数：8 | 👍 2
   - **标题**：[Breaking Change] Migrate backend from AgentScope 1.x to AgentScope 2.0
   - **关键内容**：官方计划升级 AgentScope 依赖（从 1.0.20 → 2.0），采纳新架构与 API
   - **社区反应**：2 个 👍，说明用户关注迭代速度与兼容性问题

2. **[#4342](https://github.com/agentscope-ai/QwenPaw/issues/4342)** | 评论数：11 | CLOSED
   - **标题**：[test] local_models + providers + tunnel + utils unit test coverage (Phase 5)
   - **进度**：已关闭，体现测试覆盖率补齐的系统性推进

3. **[#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878)** | 评论数：7 | CLOSED
   - **标题**：[Bug] WeChat 频道定时任务推送失败（ret=-3）
   - **根因**：WeChat OpenID 处理逻辑缺陷，已修复

4. **[#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)** | 评论数：6 | OPEN
   - **标题**：[Bug] Agent 生成的定时任务无法触发且无法编辑
   - **影响**：定时任务关键功能受阻，需紧急跟进

5. **[#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992)** | 评论数：4 | OPEN | 👍 1
   - **标题**：[Feature] 支持独立视觉模型配置（Visual Model Fallback）
   - **用户诉求**：主模型不支持多模态时自动降级到视觉模型

---

## 🐛 Bug 与稳定性

### 🔴 关键（Critical）

| Issue | 标题 | 首次报告 | 状态 | Fix PR |
|-------|------|--------|------|--------|
| [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) | OpenSSL 3.5 回归导致 Desktop 无法启动 | 2026-06-10 | OPEN | [#5096](https://github.com/agentscope-ai/QwenPaw/pull/5096) ✅ |
| [#5095](https://github.com/agentscope-ai/QwenPaw/issues/5095) | Windows v1.1.11 安装后无法启动 | 2026-06-11 | CLOSED | [#5096](https://github.com/agentscope-ai/QwenPaw/pull/5096) ✅ |

### 🟠 高（High）

| Issue | 标题 | 首次报告 | 状态 | 备注 |
|-------|------|--------|------|------|
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | Agent 定时任务无法触发且无法编辑 | 2026-06-10 | OPEN | 功能受阻，**需立即响应** |
| [#5053](https://github.com/agentscope-ai/QwenPaw/issues/5053) | Windows 多会话切换卡顿（>10s） | 2026-06-09 | OPEN | 性能退化 |
| [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | 本地 Qwen 3.6-27B 对话无响应 | 2026-06-06 | CLOSED | 从 v1.1.8 → v1.1.9 引入 |

### 🟡 中等（Medium）

| Issue | 标题 | 用户数 | 状态 |
|-------|------|--------|------|
| [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) | 多模态降级需求 | 1 👍 | OPEN，[设计中] |
| [#4865](https://github.com/agentscope-ai/QwenPaw/issues/4865) | write_file 长内容生成卡顿 | 2 👍 | OPEN，影响 UX |
| [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) | 图片预览拖拽抖动 | — | CLOSED |

---

## 🎯 功能请求与路线图信号

### 优先级矩阵

| 需求 | Issue | 热度 | 进展状态 | 预期版本 |
|------|-------|------|--------|---------|
| **AgentScope 2.0 迁移** | [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | 🔥🔥🔥 | 规划阶段 | v1.2.0？ |
| **Runtime 2.0 模块化** | [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) | 🔥🔥 | 待审核 PR | v1.2.0？ |
| **Agent OS Driver** | [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) | 🔥 | 待审核 PR | v1.2.0？ |
| **多技能路径配置** | [#4455](https://github.com/agentscope-ai/QwenPaw/issues/4455) | 中 | CLOSED | v1.1.11 ✅ |
| **Token 使用统计** | [#4433](https://github.com/agentscope-ai/QwenPaw/pull/4433) | 中 | 待审核 PR | v1.2.0？ |
| **视觉模型降级** | [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) | 低 | 提议中 | Backlog |
| **DingTalk 私有部署** | [#4887](https://github.com/agentscope-ai/QwenPaw/issues/4887) | 低 | OPEN | Backlog |
| **Headroom 上下文压缩** | [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | 低 | 提议中 | 研究阶段 |

---

## 👥 用户反馈摘要

### 真实用户痛点（从 Issue 描述提炼）

**1. 本地模型兼容性问题**
- 用户使用本地部署 Qwen 3.6-27B（vLLM OpenAI 兼容）后无响应（[#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989)）
  - **原因**：v1.1.9+ 版本回归
  - **解决**：已在 v1.1.11 修复

**2. 定时任务功能破损**
- Agent 生成的定时任务**无法触发**且**无法编辑**（[#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064)）
- WeChat 频道推送失败（ret=-3）（[#4878](https://github.com/agentscope-ai/QwenPaw/issues/4878)）
  - **用户诉求**：需要可靠的自动化执行能力

**3. 性能与 UX 问题**
- Windows 多会话频繁切换卡顿 >10s（[#5053](https://github.com/agentscope-ai/QwenPaw/issues/5053)）
- 长文件生成时界面"卡死"（无流式渲染）（[#4865](https://github.com/agentscope-ai/Qw

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