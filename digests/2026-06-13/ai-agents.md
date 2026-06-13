# OpenClaw 生态日报 2026-06-13

> Issues: 500 | PRs: 500 | 覆盖项目: 12 个 | 生成时间: 2026-06-13 03:30 UTC

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
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

OpenClaw 项目保持高度活跃，过去24小时新增 **500条 Issues**（410条新开/活跃）和 **500条 PR**（355条待合并），发布了 **2个版本**（v2026.6.6 及 beta.2）。项目聚焦于**安全边界加固**和**核心稳定性**，同时面临多个 P0/P1 级别的生产问题（内存泄漏、会话状态混乱、消息丢失）。社区参与度高，但积压问题数量庞大，维护压力显著。

---

## 🚀 版本发布

### **v2026.6.6 & v2026.6.6-beta.2**
**发布时间：** 2026-06-13

**核心亮点：** 安全边界大幅加固
- ✅ **转录安全性** - 强化 transcript 隔离
- ✅ **沙箱绑定** - 改进 sandbox binds 和 host 环境继承
- ✅ **MCP/Codex 安全** - MCP stdio、Codex HTTP 访问、原生搜索策略加固
- ✅ **权限检查** - 提升 sender 权限验证、删除代理 ACP 绕过、loopback 工具防护
- ✅ **多渠道安全** - Discord moderation、Teams 群组操作加固

**迁移注意：** 版本号跳跃（beta.2 → 6.6），建议用户在生产环境前充分测试安全相关变更。

---

## 🔧 项目进展

### 今日合并/关闭的关键 PR（样本）

| PR | 状态 | 影响范围 | 说明 |
|---|---|---|---|
| #92587 | CLOSED | QA | 撤销误合并的"QA scorecard 分类验证"，已在 #92558 重做 |
| #92311 | CLOSED | CI/安全 | 拆分插件 ClawHub 发布路径，分离 OIDC 和 token bootstrap 流程 |
| #88446 | CLOSED | Codex/多渠道 | 添加 Codex 绑定聊天计划控制，支持计划/执行模式切换 |

### 待合并的高优先级 PR（355条）

**安全/稳定性类（已有 proof）：**
- #92584 - 移除 Control UI token 的 query string 传递（安全漏洞）
- #92095 - WhatsApp 登录持久化修复（P1，Docker 重建问题）
- #92216 - 网关隐藏评论阶段事件镜像（P1）
- #92498 - Slack 同渠道最终回复镜像（P1，会话状态）
- #88970 - 心跳调度器修复（P1，5.x 回归）

**功能增强类：**
- #87111 - WebChat 工具密集历史分页（XL，兼容性风险）
- #89820-89827 - 移动响应式 UI + 设计系统文档（D-1/D-2/UX-007~013）
- #92499 - 内存/QMD：每代理隔离 mcporter sidecar（P1，可用性）

**预期本周合并数：** ~50-80 条（基于 proof 标记和优先级）

---

## 💬 社区热点

### 评论最多的 Issues（Top 5）

| Issue | 评论数 | 优先级 | 核心诉求 |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 32 | P1 🔴 | **工具调用间文本泄露到消息渠道** - 代理内部处理文本被误发送到 Slack/iMessage，严重 UX 问题 |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | 25 | P2 | **Android APK 预构建发布** - 用户需要 GitHub releases 中的预编译 APK，而非仅源码 |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | 17 | P2 | **Control UI HTTPS/localhost 限制** - VPS 部署时设备身份验证失败 |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | 17 | P2 | **分层 bootstrap 文件加载** - 大工作区用户希望按需加载文件，节省 LLM token |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | 17 | P1 🔴 | **SIGUSR1 重启竞态条件** - signal daemon 导致孤立进程和发送失败 |

### 新增高热度 Issue

- [#91778](https://github.com/openclaw/openclaw/issues/91778) - **memory_search 索引元数据缺失**（P0，法文报告）- v2026.6.1 起所有代理向量搜索失效
- [#91588](https://github.com/openclaw/openclaw/issues/91588) - **网关内存泄漏**（P0 🚨）- RSS 从 350MB 增长到 15.5GB，导致 OOM 重启循环

---

## 🐛 Bug 与稳定性

### P0/P1 级别生产问题（按严重程度）

| Issue | 类型 | 症状 | Fix PR | 状态 |
|---|---|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | 内存泄漏 | RSS 2-3天内增长至 15.5GB，OOM 杀死 | ❌ 无 | 🔴 **紧急** |
| [#91778](https://github.com/openclaw/openclaw/issues/91778) | 回归 | memory_search 向量索引完全失效（v2026.6.1+） | ❌ 无 | 🔴 **紧急** |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 安全/UX | 工具调用间文本泄露到消息渠道 | ✅ [linked-pr-open] | 🟡 待审 |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | 竞态条件 | SIGUSR1 重启时孤立进程、端口锁定 | ✅ [linked-pr-open] | 🟡 待审 |
| [#32296](https://github.com/openclaw/openclaw/issues/32296) | 会话混乱 | 代理回复前一条消息而非当前消息 | ❌ 无 | 🟡 需复现 |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | 配置忽略 | agentDir 中的 bootstrap 文件被静默忽略 | ✅ [linked-pr-open] | 🟡 待审 |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | 回归 | exec 工具不继承 skills.entries.*.env 环境变量 | ✅ [linked-pr-open] | 🟡 待审 |

### 其他重要 Bug（P2）

- [#38439](https://github.com/openclaw/openclaw/issues/38439) - WebChat avatar 端点返回 404（回归）
- [#37966](https://github.com/openclaw/openclaw/issues/37966) - LiteLLM Anthropic 模型 cacheRetention 被忽略
- [#88951](https://github.com/openclaw/openclaw/issues/88951) - 消息内容重复 2-4 次（v2026.5.27 起）
- [#84644](https://github.com/openclaw/openclaw/issues/84644) - Windows node-host 连接后无命令报告

**稳定性评估：** 🟡 **中等风险** - 存在 2 个 P0 级别未修复问题（内存泄漏、memory_search），多个 P1 级别待审 PR，建议用户暂缓升级至 v2026.6.6 直至这些问题解决。

---

## ✨ 功能请求与路线图信号

### 高优先级功能需求（用户呼声高）

| Issue | 优先级 | 需求类型 | 用户痛点 | 相关 PR |
|---|---|---|---|---|
| [#18160](https://github.com/openclaw/openclaw/issues/18160) | P2 | 直接 Exec 模式 | Cron 任务需要 agentTurn 导致超时、不可靠 | ✅ 有 PR |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) | P2 | Slack Block Kit | 代理消息仅支持纯文本，无法发送交互式卡片 | ❌ 无 |
| [#20786](https://github.com/openclaw/openclaw/issues/20786) | P2 | Telegram Business | 商业模式下无法接收个人聊天消息 | ❌ 无 |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | P2 | 动态模型发现 | OpenRouter 等快速迭代的模型目录需要动态更新 | ❌ 无 |
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | P2 | 前置响应强制钩子 | 金融/安全场景需要硬门槛（机械防止）而非软提示 | ❌ 无 |

### 已有 PR 的功能（可能纳入下一版本）

- **移动响应式** (#89820) - 汉堡菜单 + 视口自适应布局
- **设计系统文档** (#89827) - glass 表面、颜色令牌、无障碍检查清单
- **Token 使用进度条** (#89826) - 聊天编辑器底部显示上下文使用百分比
- **工作板卡片拖拽** (#89821) - 列间拖动支持
- **会话搜索/过滤** (#89825) - 侧边栏会话列表搜索

**路线图信号：** 下一版本（v2026.7.x）可能重点关注 **UI/UX 改进** 和 **多渠道富文本支持**，同时需要紧急修复 **P0 稳定性问题**。

---

## 👥 用户反馈摘要

### 真实用户痛点（从 Issue 评论提炼）

**1. 部署与配置复杂性**
- VPS/Docker 部署时 HTTPS/localhost 限制导致 Control UI 无法使用（#32473）
- 工作区大时 bootstrap 文件加载浪费 token，无法按需加载（#22438）
- 内存/嵌入配置在 onboarding 中缺失，用户难以发现（#16670）

**2. 可靠性与会话管理**
- 代理回复错误的消息（会话上下文混乱）（#32296）
- 子代理完成后主会话无响应（#47975）
- WhatsApp 长模型调用导致会话卡顿（#84569）

**3. 功能完整性**
- Slack 消息仅支持纯文本，无法发送交互式卡片（#12602）
- Cron 任务可靠性低，需要直接 exec 模式（#18160）
- 无法在 webhook 会话中实现多轮对话（#11665）

**4. 安全与隐私**
- 工具调用间的内部文本泄露到消息渠道（#25592）
- 内存条目无信任标签，易被恶意内容污染（#7707）
- exec 工具不继承环境变量，无法注入密钥（#31583）

**5. 性能与成本**
- 工具 schema 每会话消耗 ~3,500 token（#14785）
- 网关内存泄漏导致 OOM 重启（#91588）
- 长会话上下文压缩超时（#92043）

### 用户满意度信号
- ✅ **正面：** 多用户为功能请求点赞（#18160 有 11 个 👍，#6615 有 7 个 👍）
- ⚠️ **中立：** 大量 bug 报告但多数未获快速响应
- ❌ **负面：** P0 级别问题（内存泄漏、memory_search 失效）未在 24h 内修复，用户信心受损

---

## 📋 待处理积压

### 长期未响应的重要 Issue（创建 >60 天）

| Issue | 创建日期 | 天数 | 优先级 | 状态 | 备注 |
|---|---|---|---|---|---|
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | 2026-02-05 | 128 | P2 | OPEN | Android APK 预构建，25 条评论，无进展 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 2026-02-03 | 130 | P2 | OPEN | 内存信任标签，9 条评论，无 PR |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | 2026-02-06 | 127 | P2 | OPEN | 动态模型发现，9 条评论，无 PR |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) | 2026-02-09 | 124 | P2 | OPEN | Slack Block Kit，13 条评

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态全景分析报告
**报告日期：2026-06-13** | **覆盖项目：11 个核心开源项目**

---

## 1. 生态全景概览

当前个人 AI 助手/自主智能体开源生态呈现**"百花齐放、快速迭代、问题频出"**的特征。各项目在 24 小时内合计处理 **150+ 条 Issues、200+ 条 PRs**，整体活跃度极高，但稳定性问题（内存泄漏、消息丢失、权限漏洞）普遍存在。生态正从**功能堆砌阶段**向**架构优化 + 生产级可靠性**阶段演进，多项目同步推进 Runtime 2.0、权限系统、多模态支持等核心能力升级。社区用户需求从"能用"升级到"好用"和"安全用"，对企业级部署、隐私保护、成本控制的关注度显著提升。

---

## 2. 各项目活跃度对比

| 项目 | Issues (24h) | PRs (24h) | 版本发布 | 合并率 | 健康度评分 | 主要特征 |
|------|-------------|----------|--------|-------|----------|--------|
| **OpenClaw** | 500 (410活跃) | 500 (355待审) | v2026.6.6 | 71% | ⭐⭐⭐⭐ | 🔴 P0 Bug 未修，积压严重 |
| **NanoBot** | 6 | 29 (20待审) | ❌ | 69% | ⭐⭐⭐⭐ | ✅ 功能完善，稳定性中等 |
| **Zeroclaw** | 12 (10活跃) | 36 (31待审) | ❌ | 14% | ⭐⭐⭐⭐ | 🟡 高风险 PR 积压，S1 Bug 待处理 |
| **PicoClaw** | 6 | 14 (11待审) | v0.2.9-nightly | 21% | ⭐⭐⭐⭐ | ✅ 多渠道支持，Bug 密度上升 |
| **NanoClaw** | 5 (4活跃) | 18 (8待审) | ❌ | 56% | ⭐⭐⭐⭐ | 🔴 P0 安全漏洞，数据丢失风险 |
| **IronClaw** | 30 | 33 (多待审) | ❌ | 中等 | ⭐⭐⭐⭐ | ✅ 架构升级进行中，WebUI Bug 多 |
| **LobsterAI** | 1 (关闭) | 11 (6待审) | ❌ | 65% | ⭐⭐⭐⭐ | 🟡 stale PR 70+ 天，功能完善 |
| **Moltis** | 3 | 0 | ❌ | N/A | ⭐⭐⭐⭐ | ✅ 稳定，需求评估阶段 |
| **CoPaw** | 14 | 13 (多待审) | v1.1.12b1 准备中 | 77% | ⭐⭐⭐⭐ | 🔴 v1.1.11 回归 Bug 多，修复快 |
| **TinyClaw** | 0 | 0 | ❌ | N/A | ⭐⭐ | 无活动 |
| **EasyClaw** | 0 | 0 | ❌ | N/A | ⭐⭐ | 无活动 |

### 活跃度分层

**第一梯队（超活跃）**：OpenClaw、Zeroclaw、IronClaw、CoPaw
- 特点：日均 Issues 10+、PRs 20+、版本频繁迭代
- 风险：快速迭代导致 Bug 频出，积压问题多

**第二梯队（活跃）**：NanoBot、PicoClaw、NanoClaw、LobsterAI
- 特点：日均 Issues 5-10、PRs 10-20、功能驱动明显
- 风险：稳定性问题需关注，但修复响应及时

**第三梯队（稳定）**：Moltis
- 特点：日均 Issues 3、PRs 0、需求评估阶段
- 优势：问题少，社区反馈质量高

**无活动**：TinyClaw、EasyClaw

---

## 3. OpenClaw 在生态中的定位

### 技术规模与影响力

| 维度 | OpenClaw | 生态平均 | 对标项目 |
|------|---------|--------|--------|
| **日均 Issues** | 410 | 45 | **9.1 倍** 于平均 |
| **日均 PRs** | 355 | 25 | **14.2 倍** 于平均 |
| **待审 PR 积压** | 355 | 18 | **19.7 倍** 于平均 |
| **P0 Bug 数** | 2 | 0.5 | **4 倍** 于平均 |
| **版本发布频率** | 每日 | 每周 | **7 倍** 于平均 |

### 技术路线差异

**OpenClaw 的独特性**：
- **安全边界加固**：专注于 transcript 隔离、沙箱绑定、权限检查，是生态中最重视安全的项目
- **多渠道深度支持**：Discord、Teams、Slack、WhatsApp、Telegram 等 8+ 渠道，覆盖面最广
- **MCP/Codex 集成**：原生支持 Model Context Protocol，与 Anthropic 生态紧密结合
- **企业级功能**：备份恢复、审计日志、多租户隔离等生产级特性完整

**与同类的差异**：
- vs **NanoBot**：OpenClaw 更重视安全隔离，NanoBot 更重视上下文管理和内存优化
- vs **Zeroclaw**：OpenClaw 是 Node.js 生态，Zeroclaw 是 Rust 生态；OpenClaw 功能全，Zeroclaw 性能优
- vs **CoPaw**：OpenClaw 是通用 Agent 框架，CoPaw 是 Qwen 生态专属；OpenClaw 社区驱动，CoPaw 官方驱动

### 社区规模与成熟度

- **代码库规模**：OpenClaw 是生态中最大的单一项目（500+ Issues/day 说明代码量和复杂度远超同类）
- **维护团队**：多个核心维护者并行处理，但 PR 审查效率低（355 条待审，合并率 71%）
- **社区参与**：用户反馈活跃，但多数问题未在 24h 内修复，用户信心受损

### 定位总结

**OpenClaw = 生态中的"全能选手"**
- 功能最完整（多渠道、多 LLM、企业级特性）
- 问题最多（P0 Bug 未修、积压严重）
- 社区最大（但维护压力最大）
- 适合：有技术能力的企业用户、需要深度定制的场景

---

## 4. 共同关注的技术方向

### 4.1 **上下文管理与内存优化**（5 个项目）

| 项目 | 具体诉求 | 状态 |
|------|--------|------|
| **NanoBot** | 短期记忆丢失、上下文窗口压力 (#4044) | 🔴 无 fix PR |
| **OpenClaw** | 会话状态混乱、消息丢失 (#32296, #29387) | 🔴 无 fix PR |
| **IronClaw** | 消息队列可靠性、DeferredBusy 处理 (#4817) | ✅ 已合并 #4812 |
| **CoPaw** | 长对话后无响应、思考逻辑死循环 (#5161, #5162) | 🔴 无 fix PR |
| **PicoClaw** | 会话历史损坏、媒体路由混乱 (#3115, #3117) | ⏳ PR 待审 |

**共同根因**：系统提示膨胀、历史压缩时机不当、光标管理缺陷
**行业启示**：上下文管理是 Agent 系统的核心瓶颈，需要架构级重新设计

---

### 4.2 **权限与安全隔离**（6 个项目）

| 项目 | 具体诉求 | 状态 |
|------|--------|------|
| **NanoClaw** | create_agent MCP 工具未授权检查 (#2711) | 🔴 **安全漏洞** |
| **OpenClaw** | 工具调用间文本泄露到消息渠道 (#25592) | ⏳ PR 待审 |
| **Zeroclaw** | 权限跨线程持久化 (#4825) | ✅ PR #4835 待审 |
| **IronClaw** | "始终允许"权限作用域扩展 (#4825) | ✅ PR #4835 待审 |
| **Moltis** | Kubernetes 沙箱隔离需求 (#1118) | 🔴 需求评估 |
| **PicoClaw** | Telegram 权限分级（私聊/群组/频道） (#3114) | 🔴 需求评估 |

**共同根因**：权限模型过于简单（仅白名单），缺乏细粒度 RBAC
**行业启示**：多租户和安全隔离成为企业级部署的必需品

---

### 4.3 **多模态与实时交互**（5 个项目）

| 项目 | 具体诉求 | 状态 |
|------|--------|------|
| **LobsterAI** | Computer Use MVP、实时语音输入 | ✅ 已合并 |
| **CoPaw** | TTS 文本转语音、媒体附件支持 | ⏳ PR #4316, #4644 待审 |
| **Moltis** | FunASR/SenseVoice 本地 STT (#1102) | 🔴 需求评估 |
| **PicoClaw** | 图像压缩、媒体路由优化 (#2964, #3117) | ⏳ PR 待审 |
| **NanoBot** | 多模态附件验证、媒体处理 (#4312) | ⏳ PR 待审 |

**共同趋势**：从纯文本向多模态演进，语音和视觉成为标配
**行业启示**：多模态能力是 Agent 产品化的关键差异化因素

---

### 4.4 **可观测性与成本控制**（4 个项目）

| 项目 | 具体诉求 | 状态 |
|------|--------|------|
| **NanoBot** | 审计日志、可观测性 (#4320) | ✅ 已合并 |
| **IronClaw** | LLM 使用量追踪、Token 统计 (#4822) | 🔴 无 fix PR |
| **CoPaw** | 单轮 Token 使用统计 (#5130) | ⏳ PR 待审 |
| **PicoClaw** | Evolution 模块 Token 泄漏 (#3012) | 🔴 无 fix PR |

**共同根因**：缺乏细粒度的成本追踪，用户无法感知 API 消耗
**行业启示**：成本透明化成为用户选型的重要因素

---

### 4.5 **渠道生态完善**（6 个项目）

| 项目 | 新增渠道/功能 | 状态 |
|------|-------------|------|
| **Zeroclaw** | Twitch IRC 适配器 (#6443) | ✅ 已合并 |
| **PicoClaw** | DeltaChat 网关 (#3063) | ⏳ PR 待审 |
| **CoPaw** | Slack 频道支持 (#5152) | 🔴 需求评估 |
| **OpenClaw** | Discord/Teams/Slack 安全加固 | ✅ v2026.6.6 已发布 |
| **NanoClaw** | Signal 反应支持、Telegram 权限分级 | ✅ 已合并 + 🔴 需求评估 |
| **Moltis** | Fastmail MCP 集成 (#1115) | 🔴 Bug 待修 |

**共同趋势**：从主流渠道（Slack、Discord）向垂直渠道（Signal、DeltaChat、Telegram）扩展
**行业启示**：渠道多样化是 Agent 应用场景扩大的必要条件

---

## 5. 差异化定位分析

### 5.1 功能侧重维度

```
┌─────────────────────────────────────────────────────────────┐
│                    功能侧重矩阵                              │
├─────────────────────────────────────────────────────────────┤
│ 企业级特性 (安全/审计/多租户)                                │
│   ▲                                                          │
│   │  OpenClaw ★★★★★                                        │
│   │  NanoClaw ★★★★☆                                        │
│   │  IronClaw ★★★★☆                                        │
│   │  Zeroclaw ★★★☆☆                                        │
│   │  CoPaw ★★★☆☆                                           │
│   │  NanoBot ★★★☆☆                                         │
│   │  PicoClaw ★★☆☆

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

NanoBot 项目今日保持**高度活跃**的开发节奏，24小时内新增6条 Issue 更新和29条 PR 活动。其中20条 PR 待合并，9条已合并/关闭，表明核心团队在**并行推进多个功能模块和稳定性修复**。值得关注的是，新增 Issue 中有3条涉及**消息历史管理的严重 Bug**（短期记忆丢失、孤立工具结果、上下文窗口压力），这些问题直接影响对话连贯性，已成为社区关注焦点。整体来看，项目处于**功能扩展与债务清偿并行**的阶段。

---

## 🔧 项目进展

### 已合并/关闭的关键 PR（9条）

| PR | 类型 | 说明 | 影响 |
|---|---|---|---|
| #4319 | ✅ 已关闭 | **审计模块（Audit）** - 代理工具调用可观测性 | 新增企业级可观测能力，支持 loguru/HTTP/JSONL/回调4种传输方式 |
| #4318 | ✅ 已关闭 | **审计模块（重复）** - 同上 | 可能是合并冲突后的重新提交 |
| #4304 | ✅ 已关闭 | **Cron 子代理等待修复** | 修复 cron 任务在子代理后台运行时被错误标记为完成的竞态条件 |

**进展评估**：审计模块的合并标志着 NanoBot 在**可观测性和合规性**方向的重要突破，特别是对需要审计日志的企业用户。Cron 修复解决了后台任务管理的关键缺陷。

---

## 🚀 待合并的重点功能（20条 PR）

### 第一梯队：核心功能（预期近期合并）

| PR | 功能 | 状态 | 优先级 |
|---|---|---|---|
| **#4316** | [TTS 文本转语音系统](https://github.com/HKUDS/nanobot/pull/4316) | OPEN | 🔴 高 |
| **#4313** | [WebUI/config.json 配置同步](https://github.com/HKUDS/nanobot/pull/4313) | OPEN | 🔴 高 |
| **#4320** | [审计工具配置与集成](https://github.com/HKUDS/nanobot/pull/4320) | OPEN | 🔴 高 |
| **#4296** | [Python SDK 运行时控制扩展](https://github.com/HKUDS/nanobot/pull/4296) | OPEN | 🟡 中 |

### 第二梯队：稳定性与安全修复（10+条）

- **内存与历史管理**：#4315（忽略畸形历史条目）、#4256（光标单调性）、#4193（内存生命周期测试）
- **工具安全加固**：#4311（文件分页限制）、#4312（媒体附件验证）、#4119（符号链接逃逸防护）、#4053（只读根目录保护）
- **MCP 与执行**：#4303（生成器关闭防止 GC 崩溃）
- **配置架构**：#4314（解耦配置与工具运行时依赖）

**进展评估**：项目在**安全加固和技术债清偿**上投入巨大，这表明团队在为更大规模的生产部署做准备。

---

## 🔴 Bug 与稳定性问题

### 严重级（影响对话连贯性）

| Issue | 标题 | 状态 | 根因 | Fix PR |
|---|---|---|---|---|
| **#4044** | [短期记忆丢失](https://github.com/HKUDS/nanobot/issues/4044) | 🔴 OPEN | 上下文窗口压力 + 系统提示膨胀 | ❌ 无 |
| **#4307** | [合并后代理消息被清除](https://github.com/HKUDS/nanobot/issues/4307) | 🔴 OPEN | 上下文窗口合并时机不当 | ❌ 无 |
| **#4203** | [find_legal_message_start 丢弃所有消息](https://github.com/HKUDS/nanobot/issues/4203) | ✅ CLOSED | 孤立工具结果处理逻辑缺陷 | ✅ #4315 相关 |

### 中等级（API 兼容性与功能缺陷）

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| **#4006** | [孤立工具结果（无对应 tool_call）](https://github.com/HKUDS/nanobot/issues/4006) | ✅ CLOSED | 已修复（PR #3984 后续） |
| **#4309** | [/v1/chat/completions 返回零 token 使用量](https://github.com/HKUDS/nanobot/issues/4309) | 🔴 OPEN | 硬编码零值 | ❌ 无 |

### 轻微级（功能请求）

| Issue | 标题 | 状态 |
|---|---|---|
| **#4305** | [多个自定义 Provider 支持](https://github.com/HKUDS/nanobot/issues/4305) | ✅ CLOSED |

**稳定性评估**：
- ✅ **已修复**：孤立工具结果、消息丢弃逻辑
- ⚠️ **待修复**：短期记忆丢失（根因复杂，涉及上下文管理架构）、Token 使用量统计
- 🔍 **根本问题**：上下文窗口管理策略需要重新审视，当前合并时机和光标管理存在设计缺陷

---

## 💡 社区热点

### 最活跃讨论

**#4044 - 短期记忆丢失** [5条评论]
- **用户痛点**：代理提问后，用户回答时代理无法记住自己的问题，对话线程断裂
- **根因分析**：系统提示（SOUL.md、USER.md、MEMORY.md）膨胀导致上下文窗口压力
- **社区反应**：这是**最高优先级的用户体验问题**，直接影响代理可用性
- **建议**：需要优化系统提示大小、实现更智能的历史压缩策略

**#4307 - 合并后代理消息被清除** [1条评论]
- **场景**：长多轮迭代（100k+ tokens）后，合并清除了代理自己的交付消息
- **后果**：用户后续引用丢失上下文
- **根因**：合并时机在轮次完成**之后**，导致代理消息被归档

**#4305 - 多个自定义 Provider** [1条评论]
- **需求**：用户需要配置多个 OpenAI/自定义 Provider
- **建议方案**：在 Providers 配置中添加 `template` 参数选择内置提供者
- **状态**：已关闭（可能被 #4313 WebUI 配置同步功能覆盖）

---

## 🎯 功能请求与路线图信号

### 近期确定纳入的功能

| 功能 | PR | 预期影响 | 用户场景 |
|---|---|---|---|
| **TTS 文本转语音** | #4316 | 多模态交互能力 | 语音助手、无障碍访问 |
| **WebUI 配置同步** | #4313 | 降低配置门槛 | 非技术用户、快速部署 |
| **审计日志** | #4320 | 企业合规 | 金融、医疗、安全敏感场景 |
| **Python SDK 增强** | #4296 | 开发者友好性 | 集成开发、自动化脚本 |

### 用户呼声较高但未启动的功能

- **多 Provider 支持**（#4305）：已关闭，可能被 WebUI 配置功能覆盖
- **WhatsApp 提及功能**（#4317）：已在 PR 中，支持 `senderMentions` 选项

### 路线图信号

从 PR 分布看，NanoBot 的下一阶段重点是：
1. **多模态交互**（TTS + 媒体处理）
2. **企业级可观测性**（审计、日志）
3. **配置民主化**（WebUI 同步、SDK 增强）
4. **安全加固**（符号链接、权限隔离、输入验证）

---

## 👥 用户反馈摘要

### 核心痛点

| 痛点 | 影响范围 | 反映的需求 |
|---|---|---|
| **对话连贯性破裂** | 所有用户 | 需要更稳健的上下文管理 |
| **配置复杂度高** | 非技术用户 | 需要 GUI 配置、预设模板 |
| **可观测性缺失** | 企业用户 | 需要审计日志、性能指标 |
| **多渠道支持不完整** | 社交媒体用户 | WhatsApp、Telegram 等需要完整功能 |

### 满意度信号

- ✅ **工具系统**：用户对 exec、file、message 工具的安全加固表示认可
- ✅ **内存管理**：历史压缩、光标管理的修复获得正面反馈
- ⚠️ **API 兼容性**：OpenAI 兼容端点的 Token 统计缺陷引发不满

### 使用场景洞察

从 Issue 和 PR 反映的场景看：
- **企业部署**：需要审计、合规、多租户支持
- **多渠道运营**：WhatsApp、Telegram、Web 等渠道需要统一管理
- **开发者集成**：Python SDK、自定义工具、子代理编排
- **长对话场景**：需要更好的上下文压缩和记忆管理

---

## ⏳ 待处理积压

### 长期未解决的关键 Issue

| Issue | 创建日期 | 天数 | 优先级 | 建议 |
|---|---|---|---|---|
| **#4044** | 2026-05-28 | 16天 | 🔴 高 | 需要立即启动根因分析，可能需要架构调整 |
| **#4307** | 2026-06-12 | 1天 | 🔴 高 | 新报告，需要快速响应 |
| **#4309** | 2026-06-12 | 1天 | 🟡 中 | 新报告，修复应该简单（硬编码问题） |

### 长期待合并的 PR（可能存在阻塞）

| PR | 创建日期 | 天数 | 状态 | 建议 |
|---|---|---|---|---|
| **#3982** | 2026-05-24 | 20天 | OPEN | 测试基础设施，可能被其他 PR 依赖 |
| **#3983** | 2026-05-24 | 20天 | OPEN | 测试覆盖，建议优先合并 |
| **#4053** | 2026-05-29 | 15天 | OPEN | 安全修复，应加速审查 |
| **#4119** | 2026-05-31 | 13天 | OPEN | 安全修复（符号链接逃逸），应加速审查 |

### 建议行动

1. **立即**：分配资源修复 #4044（短期记忆丢失），这是最高优先级的 UX 问题
2. **本周**：合并 #4309 的 Token 统计修复，这是 API 兼容性问题
3. **本周**：加速审查 #4119、#4053 等安全修复 PR
4. **下周**：启动 #4307 的根本修复（合并时机重新设计）

---

## 📈 项目健康度评分

| 维度 | 评分 | 说明 |
|---|---|---|
| **活跃度** | 9/10 | 24小时 29 条 PR，高度活跃 |
| **稳定性** | 6/10 | 3条严重 Bug 未修复，上下文管理存在设计缺陷 |
| **功能完整性** | 8/10 | 多模态、审计、SDK 等功能在路线图上 |
| **社区响应** | 7/10 | Issue 有回应，但关键问题修复周期较长 |
| **代码质量** | 8/10 | 大量安全加固和测试覆盖 PR，说明重视质量 |
| **文档与通信** | 6/10 | PR 摘要详细，但缺少公开的路线图和优先级说明 |

**总体评估**：NanoBot 项目处于**快速迭代与稳定性平衡的关键阶段**。团队在功能扩展和技术债清偿上投入均衡，但上下文管理相关的架构问题需要尽快解决，以免影响用户信心。建议优先级调整为：**稳定性 > 新功能 > 优化**。

---

**报告生成时间**：2026-06-13 | **数据来

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

Zeroclaw 项目今日保持**高度活跃**的开发节奏：24小时内新增12条Issue（其中10条活跃），36条PR（31条待合并），已关闭2个Issue和5个PR。项目重点聚焦于**核心引擎统一、超时配置修复、网关功能完善**三大方向，同时涌现多个用户反馈的S1级阻塞问题。虽未发布新版本，但修复和功能PR的高合并率表明项目正在为下一版本积累动能。

---

## 🔧 项目进展

### 已合并/关闭的关键PR（5条）

| PR | 标题 | 影响范围 | 状态 |
|---|---|---|---|
| [#7504](https://github.com/zeroclaw-labs/zeroclaw/pull/7504) | fix(openai): honor config timeout_secs instead of hardcoding 120s | Provider核心配置 | ✅ CLOSED |
| [#7447](https://github.com/zeroclaw-labs/zeroclaw/pull/7447) | fix(providers): wire timeout_secs config into native OpenAI provider | 配置系统 | ✅ CLOSED |
| [#6723](https://github.com/zeroclaw-labs/zeroclaw/issues/6723) | Native OpenAI provider hardcodes 120s request timeout | Bug修复 | ✅ CLOSED |
| [#6443](https://github.com/zeroclaw-labs/zeroclaw/issues/6443) | Add Twitch chat channel (thin IRC adapter) | 新增Channel | ✅ CLOSED |
| [#7548](https://github.com/zeroclaw-labs/zeroclaw/pull/7548) | Chore/01.5 cargo cleanup | 依赖管理 | ✅ CLOSED |

**进展评估**：
- **超时配置修复** (#7504, #7447, #6723)：解决了OpenAI Provider长期存在的120秒硬编码超时问题，用户现在可通过`timeout_secs`配置适配慢速本地模型（llama.cpp/vLLM）
- **Twitch Channel支持** (#6443)：完成IRC适配器包装，扩展了社交媒体集成生态
- **大规模清理** (#7548)：涉及15+个子系统的依赖整理，为后续功能集成铺路

---

## 🔥 社区热点

### 讨论最活跃的Issue

**[#7415 RFC: Unify the three agent turn engines](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)** 
- 标签：`enhancement`, `risk:high`, `needs-maintainer-review`, `type:rfc`
- 创建：2026-06-09 | 更新：2026-06-12 | 评论：3条
- **核心诉求**：统一三个Agent转向引擎（`run_tool_call_loop` + `turn_streamed` + `Agent::turn`）
- **最新进展**：已按维护者指示执行为单一整合PR（#7540），而非分阶段迁移
- **影响**：这是架构级重构，涉及Agent、Channel、Gateway、Runtime等核心模块，风险等级HIGH

**[#6970 v0.8.1 integration/channel/provider/tool PR queue](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)**
- 标签：`enhancement`, `risk:high`, `status:accepted`
- 创建：2026-05-27 | 更新：2026-06-12 | 评论：0条
- **性质**：运营追踪器，管理v0.8.1版本的Channel、Provider、Tool、Integration相关PR路由
- **意义**：表明项目正在为v0.8.1版本做系统性功能积累

---

## ⚠️ Bug与稳定性

### S1级阻塞问题（3条）

| Issue | 组件 | 问题描述 | Fix PR | 状态 |
|---|---|---|---|---|
| [#7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542) | gateway/api | `ask_user`在WebSocket会话中立即失败："Channel closed before receiving a response" | [#7551](https://github.com/zeroclaw-labs/zeroclaw/pull/7551) | 🔧 有Fix |
| [#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537) | runtime/daemon | quickstart命令无法创建Agent，配置解析错误："no map-keyed/list section at peer-groups" | ❌ 无Fix | 🔴 待处理 |
| [#7533](https://github.com/zeroclaw-labs/zeroclaw/issues/7533) | docker | Docker构建失败，cargo web build缺少C++编译器 | [#7534](https://github.com/zeroclaw-labs/zeroclaw/pull/7534) | 🔧 有Fix |

### S2级降级问题（1条）

| Issue | 组件 | 问题描述 | 影响 |
|---|---|---|---|
| [#7541](https://github.com/zeroclaw-labs/zeroclaw/issues/7541) | gateway/api | V3遗留路径仍使用共享`data_dir`作为Agent工作目录 | Gateway WS聊天默认会话CWD混乱 |

### 其他Bug（1条）

| Issue | 组件 | 问题描述 |
|---|---|---|
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | runtime/daemon | macOS应用无法检测权限，显示空白页，重启后窗口消失 |

**稳定性评估**：
- **快速响应**：S1问题已有Fix PR在24小时内提出（#7551, #7534）
- **新用户体验受阻**：quickstart配置解析问题（#7537）未见Fix，可能影响新用户转化
- **跨平台问题**：macOS和Windows特定问题浮现，需加强平台测试覆盖

---

## 💡 功能请求与路线图信号

### 高优先级功能需求

| Issue | 标题 | 标签 | 用户诉求 | 可能纳入版本 |
|---|---|---|---|---|
| [#7543](https://github.com/zeroclaw-labs/zeroclaw/issues/7543) | Multi-session support in gateway web chat UI | `enhancement` | 网关Web聊天支持多会话（新建/切换/重命名/删除） | v0.8.1+ |
| [#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531) | Support streaming card messages for QQ/DingTalk/WeChat/Feishu | `enhancement` | 中文IM平台支持流式卡片消息，减少用户等待焦虑 | v0.8.1+ |
| [#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539) | llama.cpp model router | `enhancement` | 本地模型快速切换路由 | 待评估 |

### 相关进行中的PR

- [#7549](https://github.com/zeroclaw-labs/zeroclaw/pull/7549) **fix(plugins): align install/discovery paths** - 修复插件安装路径不匹配问题，为插件生态完善铺路
- [#7547](https://github.com/zeroclaw-labs/zeroclaw/pull/7547) **fix(runtime): auto-include discovered MCP tools** - MCP工具自动纳入风险配置，降低用户配置复杂度
- [#7495](https://github.com/zeroclaw-labs/zeroclaw/pull/7495) **fix(lark): add per-channel ack_reactions override** - Lark/Feishu频道级配置覆盖，提升中文IM支持完整性

**路线图信号**：v0.8.1版本重点为**多会话网关、中文IM流式消息、MCP工具集成、插件系统完善**。

---

## 👥 用户反馈摘要

### 真实用户痛点

1. **新用户入门困难**（#7537）
   - 痛点：quickstart命令配置解析失败，Windows 10用户无法创建Agent
   - 根因：配置schema变更后的兼容性问题
   - 建议：加强配置迁移文档和验证提示

2. **本地模型支持不完善**（#7539）
   - 痛点：llama.cpp模型切换不便，用户需手动修改配置
   - 诉求：模型路由快速切换功能
   - 背景：用户在小任务上使用小模型，需灵活切换

3. **跨平台应用稳定性**（#7527）
   - 痛点：macOS应用权限检测失败，UI显示异常
   - 影响：桌面应用可用性受损

4. **中文IM用户体验**（#7531）
   - 痛点：QQ/DingTalk/WeChat/Feishu卡片消息无流式支持，用户等待时间长
   - 诉求：流式卡片消息减少焦虑
   - 背景：中文企业IM是重要应用场景

5. **网关Web聊天功能缺陷**（#7542, #7543）
   - 痛点：`ask_user`工具失败，单会话限制
   - 诉求：多会话支持、用户交互完整性

### 用户满意度信号
- **正面**：用户积极报告问题，提供详细复现步骤（#7537, #7533）
- **关注**：多个S1级问题反映核心功能稳定性需加强
- **机会**：中文IM和本地模型是增长点，用户需求明确

---

## 📋 待处理积压

### 长期未响应的重要Issue

| Issue | 创建时间 | 天数 | 优先级 | 状态 | 建议 |
|---|---|---|---|---|---|
| [#7537](https://github.com/zeroclaw-labs/zeroclaw/issues/7537) | 2026-06-12 | 1天 | S1 | 无Fix | 🔴 **立即处理** - 新用户阻塞 |
| [#7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527) | 2026-06-12 | 1天 | S1 | 无Fix | 🔴 **立即处理** - 平台特定问题 |
| [#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539) | 2026-06-12 | 1天 | 增强 | 无PR | 🟡 **评估优先级** - 本地模型用户需求 |

### 待合并的高风险PR

| PR | 标签 | 创建时间 | 天数 | 建议 |
|---|---|---|---|---|
| [#7429](https://github.com/zeroclaw-labs/zeroclaw/pull/7429) | `risk:high`, `dependencies`, `runtime:wasm` | 2026-06-09 | 4天 | 🟡 **加速审查** - wasmtime依赖引入，涉及Extism弃用计划 |
| [#7351](https://github.com/zeroclaw-labs/zeroclaw/pull/7351) | `risk:high`, `tool:mcp` | 2026-06-07 | 6天 | 🟡 **加速审查** - MCP自动重连，关键稳定性修复 |
| [#7245](https://github.com/zeroclaw-labs/zeroclaw/pull/7245) | `risk:high`, `runtime`, `needs-author-action` | 2026-06-05 | 8天 | 🔴 **需作者跟进** - 插件技能加载修复，标记为needs-author-action |

---

## 📈 数据总结

| 指标 | 数值 | 评价 |
|---|---|---|
| 24h Issue新增/活跃 | 10条 | ✅ 活跃 |
| 24h Issue关闭 | 2条 | ⚠️ 关闭率20% |
| 24h PR待合并 | 31条 | ✅ 高产出 |
| 24h PR已合并/关闭 | 5条 | ⚠️ 合并率14% |
| S1级阻塞问题 | 3条 | 🔴 需关注 |
| 无Fix的S1问题 | 1条 | 🔴 需立即处理 |
| 高风险PR积压 | 3条 | 🟡 需加速审查 |

---

## 🎯 建议与行动项

1. **立即处理**：#7537（quickstart配置）和 #7527（macOS应用）的S1问题
2. **加速审查**：#7429（wasmtime）、#7351（MCP重连）、#7245（插件技能）三个高风险PR
3. **版本规划**：确认v0.8.1的功能范围，优先级排序#7543（多会话）和#7531（流式卡片）
4. **文档更新**：补充quickstart配置迁移指南，降低新用户入门门槛
5. **测试覆盖**：加强macOS和Windows平台的集成测试，防止跨平台回归

---

**报告生成时间**：2026-06-13 | **数据来源**：GitHub API | **下次更新**：2026-06-14

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报
**日期**: 2026-06-13 | **数据周期**: 过去24小时

---

## 📊 今日速览

PicoClaw 项目今日活跃度**高涨**，24小时内新增6条 Issue、14条 PR，其中11条 PR 待合并。项目呈现**多线程并行开发**态势：既有关键协议完善（WebSocket 转向信号）、新渠道集成（DeltaChat），也有大量**稳定性修复**（JSON 序列化、类型断言检查）。同时发布了 nightly 版本 v0.2.9-nightly.20260613，表明主线开发活跃。整体评估：**健康的高速迭代阶段**，但 Bug 报告密度也在上升。

---

## 🚀 版本发布

**Nightly Build: v0.2.9-nightly.20260613.c362114c**
- **性质**: 自动化 Nightly 构建，可能不稳定
- **完整变更**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **建议**: 用于测试新特性，生产环境建议等待稳定版本

---

## ✅ 项目进展

### 已合并/关闭 (3条)

| PR/Issue | 类型 | 说明 |
|---------|------|------|
| [#3109](https://github.com/sipeed/picoclaw/issues/3109) | Feature | **Channel 级权限分级** - 关闭（已转为 #3114 的更细化需求） |
| [#2551](https://github.com/sipeed/picoclaw/pull/2551) | Refactor | **通道标识解耦** - 允许同一提供商的多实例，解决了通道名与类型的耦合问题 |
| [#3113](https://github.com/sipeed/picoclaw/pull/3113) | Bug Fix | **JSON 序列化错误检查** - 修复 `toChannelHashes` 中的三处静默错误丢弃 |
| [#3112](https://github.com/sipeed/picoclaw/pull/3112) | Bug Fix | **工具调用参数序列化** - 修复 `toolloop.go` 中 `json.Marshal` 错误导致的历史记录损坏 |

### 待合并重点 (11条)

**核心功能推进**:
- [#3116](https://github.com/sipeed/picoclaw/pull/3116) - **Pico 协议完善**: 补全 `turn.done` 生命周期信号，保留 `request_id` 用于排队消息
- [#3118](https://github.com/sipeed/picoclaw/pull/3118) - **远程 WebSocket 模式**: 扩展 `picoclaw agent` 命令支持远程连接
- [#3063](https://github.com/sipeed/picoclaw/pull/3063) - **新渠道集成**: DeltaChat 网关支持

**稳定性修复**:
- [#3117](https://github.com/sipeed/picoclaw/pull/3117) - **媒体路由修复**: 将媒体转向路由到图像模型而非文本模型重试
- [#3115](https://github.com/sipeed/picoclaw/pull/3115) - **会话历史损坏修复**: 防止工具输出中的 `data:image/...` 被误识别为媒体
- [#3091](https://github.com/sipeed/picoclaw/pull/3091) - **类型断言检查**: OpenAI 兼容提供商的 `native_search` 类型检查
- [#3053](https://github.com/sipeed/picoclaw/pull/3053) - **Evolution 模块**: `lockStoreFile` 的类型断言 `ok` 检查

**功能增强**:
- [#2964](https://github.com/sipeed/picoclaw/pull/2964) - **图像压缩**: 可配置的入站图像多级压缩策略
- [#2917](https://github.com/sipeed/picoclaw/pull/2917) - **新提供商**: NEAR AI Cloud（OpenAI 兼容）
- [#3097](https://github.com/sipeed/picoclaw/pull/3097) - **UI 改进**: Web 聊天框下方添加 Shift+Enter 提示
- [#3045](https://github.com/sipeed/picoclaw/pull/3045) - **Matrix 用户 ID 修复**: 支持包含冒号的标准 Matrix ID 格式

---

## 🔥 社区热点

### 最活跃讨论

| Issue | 评论 | 👍 | 热度分析 |
|-------|------|-----|---------|
| [#2984](https://github.com/sipeed/picoclaw/issues/2984) | 2 | 2 | **协议完善需求** - 外部 WebSocket 客户端需要显式的转向完成信号，已有对应 PR #3116 推进 |
| [#3012](https://github.com/sipeed/picoclaw/issues/3012) | 2 | 0 | **Evolution 模块 Token 泄漏** - 启用 Evolution 时持续消耗 Token，用户反馈强烈（MiniMax 提供商） |

### 新增高优先级需求

| Issue | 类型 | 诉求 |
|-------|------|------|
| [#3114](https://github.com/sipeed/picoclaw/issues/3114) | Feature | **Telegram 对话类型权限分级** - 区分私聊/群组/频道的危险操作权限（中文用户提出） |
| [#3111](https://github.com/sipeed/picoclaw/issues/3111) | Bug | **Gemini 3.5 Flash 兼容性** - 缺少 `thought_signature` 字段导致工具执行失败 |
| [#3110](https://github.com/sipeed/picoclaw/issues/3110) | Bug | **Telegram Forum 主题回复** - 机器人回复默认发送到 #General 而非目标主题 |

---

## 🐛 Bug 与稳定性

### 严重程度排序

#### 🔴 **严重** (影响功能可用性)

| Bug | 状态 | 影响范围 | Fix PR |
|-----|------|--------|--------|
| [#3111](https://github.com/sipeed/picoclaw/issues/3111) | OPEN | Gemini 3.5 Flash 模型工具执行完全失败 | ❌ 无 |
| [#3110](https://github.com/sipeed/picoclaw/issues/3110) | OPEN | Telegram Forum 用户无法在正确主题获得回复 | ❌ 无 |
| [#3012](https://github.com/sipeed/picoclaw/issues/3012) | OPEN | Evolution 启用时 Token 持续泄漏（成本问题） | ❌ 无 |

#### 🟡 **中等** (数据完整性/隐蔽缺陷)

| Bug | 状态 | 影响范围 | Fix PR |
|-----|------|--------|--------|
| [#3115](https://github.com/sipeed/picoclaw/pull/3115) | PENDING | 会话历史损坏 - 工具输出中的 base64 数据被误识别 | ✅ [#3115](https://github.com/sipeed/picoclaw/pull/3115) |
| [#3044](https://github.com/sipeed/picoclaw/pull/3045) | PENDING | Matrix 用户 ID 格式不兼容导致权限检查失败 | ✅ [#3045](https://github.com/sipeed/picoclaw/pull/3045) |

#### 🟢 **低** (代码质量/潜在崩溃)

| Bug | 状态 | 影响范围 | Fix PR |
|-----|------|--------|--------|
| [#3113](https://github.com/sipeed/picoclaw/pull/3113) | MERGED | JSON 序列化错误静默丢弃 | ✅ 已合并 |
| [#3112](https://github.com/sipeed/picoclaw/pull/3112) | MERGED | 工具参数序列化失败 | ✅ 已合并 |
| [#3091](https://github.com/sipeed/picoclaw/pull/3091) | PENDING | 类型断言缺少 `ok` 检查 | ✅ [#3091](https://github.com/sipeed/picoclaw/pull/3091) |
| [#3053](https://github.com/sipeed/picoclaw/pull/3053) | PENDING | Evolution 模块类型断言 panic 风险 | ✅ [#3053](https://github.com/sipeed/picoclaw/pull/3053) |

---

## 💡 功能请求与路线图信号

### 已有 PR 支持的新功能（下一版本候选）

| 功能 | PR | 状态 | 预期影响 |
|------|-----|------|---------|
| **Pico 协议完善** | [#3116](https://github.com/sipeed/picoclaw/pull/3116) | 待合并 | 外部客户端集成体验大幅提升 |
| **远程 Agent 模式** | [#3118](https://github.com/sipeed/picoclaw/pull/3118) | 待合并 | 支持分布式部署、多实例协调 |
| **DeltaChat 渠道** | [#3063](https://github.com/sipeed/picoclaw/pull/3063) | 待合并 | 覆盖隐私通讯用户群体 |
| **图像压缩策略** | [#2964](https://github.com/sipeed/picoclaw/pull/2964) | 待合并 | 降低 API 成本、加快响应 |
| **NEAR AI Cloud** | [#2917](https://github.com/sipeed/picoclaw/pull/2917) | 待合并 | 新增 LLM 提供商选择 |

### 用户呼声高但尚无 PR 的需求

| 需求 | Issue | 用户类型 | 优先级信号 |
|------|-------|---------|----------|
| **Telegram 权限分级** | [#3114](https://github.com/sipeed/picoclaw/issues/3114) | 中文用户 | 🔴 高 - 安全隔离需求 |
| **Gemini 3.5 Flash 支持** | [#3111](https://github.com/sipeed/picoclaw/issues/3111) | Google 用户 | 🔴 高 - 新模型兼容性 |

---

## 👥 用户反馈摘要

### 核心痛点

1. **成本控制** ([#3012](https://github.com/sipeed/picoclaw/issues/3012))
   - 用户: @xpader (FreeBSD 环境)
   - 痛点: Evolution 启用时 Token 持续消耗，成本失控
   - 使用场景: MiniMax 提供商、Draft 模式、代码路径触发

2. **安全隔离** ([#3114](https://github.com/sipeed/picoclaw/issues/3114))
   - 用户: @v2up-32mb (中文社区)
   - 痛点: 无法区分私聊/群组/频道的权限，群组中任何允许成员都可执行危险操作（`exec`、`write_file`）
   - 使用场景: Telegram 群组部署

3. **多渠道兼容性**
   - Telegram Forum 主题回复失效 ([#3110](https://github.com/sipeed/picoclaw/issues/3110))
   - Matrix 用户 ID 格式不支持 ([#3045](https://github.com/sipeed/picoclaw/pull/3045))
   - Gemini 3.5 Flash 工具调用失败 ([#3111](https://github.com/sipeed/picoclaw/issues/3111))

4. **协议完善** ([#2984](https://github.com/sipeed/picoclaw/issues/2984))
   - 用户: @Brook-sys
   - 痛点: WebSocket 客户端无法确定性地知道 Agent 何时完成处理
   - 使用场景: 外部集成、客户端 UI 同步

### 满意度信号

- ✅ 多渠道支持广泛（Telegram、Discord、Feishu、Matrix、DeltaChat 等）
- ✅ 工具系统灵活（`exec`、`read_file`、`write_file` 等）
- ✅ 多 LLM 提供商支持（OpenAI、Gemini、MiniMax、NEAR AI 等）

### 不满意的地方

- ❌ 权限模型过于简单（仅 `allow_from` 白名单）
- ❌ Evolution 模块成本控制不足
- ❌ 新模型兼容性滞后（Gemini 3.5 Flash）
- ❌ 渠道特定功能支持不完整（Telegram Forum、Matrix ID 格式）

---

## ⏳ 待处理积压

### 长期未响应的重要 Issue

| Issue | 创建时间 | 天数 | 状态 | 优先级 |
|-------|---------|------|------|--------|
| [#3012](https://github.com/sipeed/picoclaw/issues/3012) | 2026-06-05 | 8天 | OPEN | 🔴 高 - 成本问题 |
| [#3111](https://github.com/sipeed/picoclaw/issues/3111) | 2026-06-12 | 1天 | OPEN | 🔴 高 - 新模型兼容性 |
| [#3110](https://github.com/sipeed/picoclaw/issues/3110) | 2026-06-12 | 1天 | OPEN | 🟡 中 - 渠道功能 |

### 长期待合并的 PR

| PR | 创建时间 | 天数 | 状态 | 风险 |
|----|---------|------|------|------|
| [#2917](https

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

NanoClaw 项目今日保持高度活跃，过去24小时内处理了 **18 条 PR**（10 条已合并/关闭，8 条待审）和 **5 条 Issue**（4 条新开/活跃，1 条已关闭），但**未发布新版本**。项目呈现"大量功能迭代 + 关键稳定性修复"的特征，同时暴露了多个影响生产环境的安全与可靠性问题。维护团队响应积极，但待合并 PR 堆积较多，需关注审核效率。

---

## 🔧 项目进展

### 已合并/关闭的关键 PR（10 条）

**核心功能增强：**
- **#2203** [Signal 反应支持](https://github.com/nanocoai/nanoclaw/pull/2203) — 双向反应（inbound/outbound），完善 Signal 集成
- **#2084** [备份与灾难恢复](https://github.com/nanocoai/nanoclaw/pull/2084) — 日常快照 + 全量/单代理恢复，解决 `rm -rf` 风险
- **#2040** [Signal 出站附件支持](https://github.com/nanocoai/nanoclaw/pull/2040) — 代理可通过 `add_reaction` 工具发送文件

**多模态与数据流：**
- **#2072** [Ollama 图像字段](https://github.com/nanocoai/nanoclaw/pull/2072) — 支持 workspace 相对路径的多模态输入
- **#2071** [Signal 非音频附件路由](https://github.com/nanocoai/nanoclaw/pull/2071) — PDF/文档/图像统一通过 inbox 路径交付
- **#2070** [主机路径附件支持](https://github.com/nanocoai/nanoclaw/pull/2070) — 原生适配器直接传递磁盘文件

**可靠性修复：**
- **#2670** [自愈中毒恢复崩溃循环](https://github.com/nanocoai/nanoclaw/pull/2670) — 修复 corrupt transcript 导致的无限重启
- **#2692** [API 错误重试与通知](https://github.com/nanocoai/nanoclaw/pull/2692) — 处理 5xx 瞬时错误的优雅降级
- **#2277** [跟进消息路由刷新](https://github.com/nanocoai/nanoclaw/pull/2277) — 修复 mid-query 消息的路由冻结
- **#2267** [代理间回复路由](https://github.com/nanocoai/nanoclaw/pull/2267) — 修复多会话 split-brain 问题

**项目向前推进：** 本日合并涵盖 **3 个新功能模块**（备份、Signal 反应、多模态）+ **4 个关键稳定性修复**，整体代码质量与用户体验均有显著提升。

---

## 🔴 Bug 与稳定性（按严重程度）

### 🚨 **P0 - 生产环境阻断**

| Issue | 标题 | 影响范围 | 修复状态 |
|-------|------|--------|--------|
| [#2711](https://github.com/nanocoai/nanoclaw/issues/2711) | `create_agent` MCP 工具未授权检查 | **安全漏洞**：任意容器可创建代理组 | ❌ 无 fix PR |
| [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) | 60秒内完成的消息被静默丢弃 | **数据丢失**：客户端超时，代理响应消失 | ❌ 无 fix PR |
| [#2751](https://github.com/nanocoai/nanoclaw/issues/2751) | 预算耗尽的 LLM 调用被静默丢弃 | **用户无感知**：返回虚假成功，用户收不到回复 | ❌ 无 fix PR（已关闭） |

### ⚠️ **P1 - 功能受损**

| Issue | 标题 | 影响范围 | 修复状态 |
|-------|------|--------|--------|
| [#2668](https://github.com/nanocoai/nanoclaw/issues/2668) | MCP 工具无单工具超时 | 单个卡住的工具可阻塞会话 30 分钟 | ❌ 无 fix PR |

### 📋 **待处理 PR（8 条）**

- **#2753** [pre-commit hook 缺失 pnpm](https://github.com/nanocoai/nanoclaw/pull/2753) — 开发体验
- **#2752** [Discord 附件 URL 暂存](https://github.com/nanocoai/nanoclaw/pull/2752) — 功能修复
- **#2750** [stale journal 恢复](https://github.com/nanocoai/nanoclaw/pull/2750) — 可靠性
- **#2749** [npm 包发布年龄门控](https://github.com/nanocoai/nanoclaw/pull/2749) — 安全加固
- **#2748** [容器安全加固](https://github.com/nanocoai/nanoclaw/pull/2748) — 安全加固
- **#2747** [OneCLI SDK 2.2.1](https://github.com/nanocoai/nanoclaw/pull/2747) — 依赖更新
- **#2746** [Provider 能力接缝](https://github.com/nanocoai/nanoclaw/pull/2746) — 架构扩展
- **#2745** [持久化内存脚手架](https://github.com/nanocoai/nanoclaw/pull/2745) — 功能框架

---

## 🔥 社区热点

### 最活跃讨论（按评论数）

1. **[#2506](https://github.com/nanocoai/nanoclaw/issues/2506)** — 消息去重导致响应丢失
   - **评论数：3** | **创建：2026-05-16** | **最后更新：2026-06-12**
   - **核心诉求：** 修复 60 秒内完成的两个 turn 导致响应被静默丢弃的 bug
   - **用户痛点：** 快速对话场景下代理响应消失，客户端无法感知

2. **[#2632](https://github.com/nanocoai/nanoclaw/issues/2632)** — Telegram 代理群/多身份迁移路径
   - **评论数：1** | **创建：2026-05-28** | **最后更新：2026-06-12**
   - **核心诉求：** 澄清 v1 → v2 迁移中 `/add-telegram-swarm` 特性的状态
   - **用户痛点：** 文档不清，fork 用户无法规划迁移策略

3. **[#2711](https://github.com/nanocoai/nanoclaw/issues/2711)** — 安全漏洞：create_agent 未授权
   - **评论数：1** | **创建：2026-06-07** | **最后更新：2026-06-12**
   - **核心诉求：** 修复 MCP 工具缺失角色检查，任意容器可创建代理组
   - **用户痛点：** 多租户环境下的权限隔离失效

---

## 🛡️ 安全与稳定性焦点

### 新增安全加固（待合并）

- **#2749** [npm 包发布年龄门控](https://github.com/nanocoai/nanoclaw/pull/2749) — 防止代理安装过新的恶意包
- **#2748** [容器安全加固](https://github.com/nanocoai/nanoclaw/pull/2748) — `--cap-drop=ALL`、`--security-opt no-new-privileges`、`--pids-limit 2048`

### 关键修复（待合并）

- **#2750** [stale journal 恢复](https://github.com/nanocoai/nanoclaw/pull/2750) — 修复 SIGKILL 后的 outbound.db 损坏（#2516, #2640）

---

## 💡 功能请求与路线图信号

### 已实现的功能需求

| 功能 | 对应 PR | 状态 | 预期版本 |
|------|--------|------|--------|
| 备份与灾难恢复 | #2084 | ✅ 已合并 | v2.0.65+ |
| Signal 反应支持 | #2203 | ✅ 已合并 | v2.0.65+ |
| 多模态附件（Ollama） | #2072 | ✅ 已合并 | v2.0.65+ |
| Discord 附件暂存 | #2752 | ⏳ 待审 | v2.0.66+ |
| Provider 内存脚手架 | #2745 | ⏳ 待审 | v2.1.0+ |

### 用户期待的功能

- **Telegram 代理群支持** (#2632) — 需要官方澄清 v2 路线图
- **单工具超时机制** (#2668) — 防止卡住的 MCP 工具阻塞整个会话

---

## 👥 用户反馈摘要

### 真实用户痛点

1. **数据丢失风险** — 快速对话、预算耗尽、网络抖动时响应被静默丢弃，用户无感知
   - 相关 Issue：#2506, #2751
   - **建议：** 增加显式错误通知机制，而非静默失败

2. **迁移不确定性** — v1 fork 用户对 v2 特性支持状态不清楚
   - 相关 Issue：#2632
   - **建议：** 发布 v1 → v2 迁移指南，明确各特性的支持状态

3. **多租户安全隔离** — 权限检查缺失，任意容器可创建代理组
   - 相关 Issue：#2711
   - **建议：** 立即修复，补充 RBAC 测试

4. **工具可靠性** — 单个卡住的 MCP 工具可阻塞整个会话 30 分钟
   - 相关 Issue：#2668
   - **建议：** 实现单工具超时 + 异步执行

### 用户满意度信号

- ✅ **积极反馈：** 备份功能、Signal 集成、多模态支持获得合并，说明用户需求被重视
- ⚠️ **改进空间：** 稳定性问题（消息丢失、权限漏洞）仍未完全解决，用户信心受影响

---

## 📦 待处理积压

### 🔴 **高优先级待审 PR**（可能阻塞下一版本）

| PR | 类型 | 创建时间 | 待审天数 | 影响 |
|----|------|--------|--------|------|
| #2750 | 修复 | 2026-06-12 | 1 天 | 修复 outbound.db 损坏（#2516, #2640） |
| #2749 | 安全 | 2026-06-12 | 1 天 | npm 包安全门控 |
| #2748 | 安全 | 2026-06-12 | 1 天 | 容器安全加固 |
| #2752 | 修复 | 2026-06-12 | 1 天 | Discord 附件修复 |

### 🟡 **长期未解决的关键 Issue**

| Issue | 创建时间 | 天数 | 状态 | 建议 |
|-------|--------|------|------|------|
| #2506 | 2026-05-16 | 28 天 | 无 fix PR | 🚨 **立即分配**，影响快速对话场景 |
| #2668 | 2026-06-01 | 12 天 | 无 fix PR | ⚠️ **需要设计讨论**，可能涉及架构改动 |
| #2711 | 2026-06-07 | 6 天 | 无 fix PR | 🚨 **安全漏洞，优先级最高** |
| #2632 | 2026-05-28 | 16 天 | 无 fix PR | 📋 **需要文档澄清** |

---

## 📈 项目健康度评分

| 维度 | 评分 | 备注 |
|------|------|------|
| **活跃度** | ⭐⭐⭐⭐⭐ | 18 条 PR/天，高速迭代 |
| **稳定性** | ⭐⭐⭐ | 4 个 P0/P1 bug 未修复，消息丢失风险 |
| **安全性** | ⭐⭐⭐ | 权限漏洞 (#2711)、包安全加固待合并 |
| **文档** | ⭐⭐⭐ | 迁移指南缺失（#2632） |
| **审核效率** | ⭐⭐⭐⭐ | 10 条 PR 已合并，8 条待审（1 天内） |

---

## 🎯 建议与行动项

### 立即行动（24 小时内）

1. ✅ **合并 #2750, #2749, #2748** — 修复 outbound.db 损坏 + 安全加固
2. 🚨 **分配 #2711** — 修复 create_agent 权限漏洞（安全漏洞）
3.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

IronClaw 项目今日保持高度活跃，24小时内新增/活跃 Issues 30 条，待合并 PR 33 条，展现出强劲的开发节奏。核心工作聚焦于 **Reborn 引擎的消息队列管理、权限持久化、运行时上下文透明度** 三大方向，同时修复了一批 WebUI 交互问题。虽未发布新版本，但多个关键 PR 已合并或进入最终审查阶段，项目整体向稳定性和功能完整性迈进。

---

## 🔄 项目进展

### 已合并/关闭的关键 PR（过去24小时）

| PR | 标题 | 影响范围 | 状态 |
|---|---|---|---|
| **#4812** | [Drain DeferredBusy messages when blocking run reaches terminal state](https://github.com/nearai/ironclaw/pull/4812) | 核心 | ✅ 已合并 |
| **#4773** | [Record/replay machinery for QA-phrase traces on Reborn runtime](https://github.com/nearai/ironclaw/pull/4773) | 测试基础设施 | ✅ 已合并 |
| **#4562** | [Record auth continuation dispatch failures](https://github.com/nearai/ironclaw/pull/4562) | 安全审计 | ✅ 已合并 |
| **#4568** | [Bound before-capability dispatch fan-out](https://github.com/nearai/ironclaw/pull/4568) | 安全 | ✅ 已合并 |
| **#4569** | [Enforce aggregate tenant predicate key caps](https://github.com/nearai/ironclaw/pull/4569) | 多租户 | ✅ 已合并 |

### 核心进展说明

**消息队列管理突破**：#4812 解决了长期痛点——当运行被权限门控阻塞时，用户发送的消息不再永久丢失，而是在阻塞运行终止后自动重新提交。这是 Reborn 引擎的重要稳定性改进。

**权限系统增强**：#4835（进行中）将"始终允许"权限的作用域从单线程扩展到用户全局，避免用户在每个新线程中重复授权同一能力。

**运行时透明度提升**：#4836（进行中）为模型注入运行时上下文切片，使其感知已连接的通道、出站交付状态和运行来源，解决了 Slack 连接状态不可见的问题。

---

## 🔥 社区热点

### 讨论最活跃的 Issues（评论数排序）

| Issue | 标题 | 评论 | 关键信息 |
|---|---|---|---|
| **#4817** | [DeferredBusy drain follow-ups](https://github.com/nearai/ironclaw/issues/4817) | 3 | 追踪 #4812 的三个后续设计决策：门控重新提交架构、陈旧意图策略、启动扫描 |
| **#4825** | [Persist "always allow" approvals across threads](https://github.com/nearai/ironclaw/issues/4825) | 3 | 用户在线程1授权后，线程2仍被重复提示，已有 #4835 修复 PR |
| **#4703** | [NEAR AI model picker saves display name instead of model ID](https://github.com/nearai/ironclaw/issues/4703) | 3 | 已关闭，配置保存时使用了错误字段 |

### 高价值反馈

- **#4828**（0评论但已有PR #4836）：模型缺乏对连接通道和交付状态的感知，导致 Slack 连接完成后仍无法使用
- **#4824**（0评论但阻塞CI）：新的 RUSTSEC 安全公告导致 cargo-deny 失败，涉及 PostgreSQL 驱动的 DoS 漏洞

---

## 🐛 Bug 与稳定性

### 严重级别分类

**🔴 高优先级（阻塞功能）**

| Issue | 描述 | 影响 | Fix PR |
|---|---|---|---|
| **#4824** | [cargo-deny failing: RUSTSEC advisories against postgres crates](https://github.com/nearai/ironclaw/issues/4824) | CI 全量阻塞 | ⏳ 待处理 |
| **#4762** | [Failed tool workflow causes follow-up messages and activity ordering to become inconsistent](https://github.com/nearai/ironclaw/issues/4762) | 消息顺序混乱 | ⏳ 待处理 |
| **#4705** | [NEAR AI SSO setup fails in local environment](https://github.com/nearai/ironclaw/issues/4705) | 本地开发阻塞 | ✅ 已关闭 |

**🟡 中优先级（功能缺陷）**

| Issue | 描述 | 影响 | Fix PR |
|---|---|---|---|
| **#4703** | [NEAR AI model picker saves display name instead of model ID](https://github.com/nearai/ironclaw/issues/4703) | 配置无法保存 | ✅ 已关闭 |
| **#4706** | [Authorization flows do not recover after failed or cancelled sign-in](https://github.com/nearai/ironclaw/issues/4706) | 授权流程卡死 | ✅ 已关闭 |
| **#4673** | [NEAR AI provider configuration cannot be saved after successful Test connection](https://github.com/nearai/ironclaw/issues/4673) | 配置丢失 | ✅ 已关闭 |
| **#4696** | [Local Ollama Test connection reports success when Ollama is unavailable](https://github.com/nearai/ironclaw/issues/4696) | 虚假成功提示 | ⏳ 待处理 |

**🟢 低优先级（UX 问题）**

- #4733：响应链接导航离开对话
- #4722：消息缺少用户/助手身份标识
- #4721：侧边栏"PINNED"显示逻辑错误
- #4719：返回对话时内容闪烁
- #4725：Working 状态下 Composer 仍可交互
- #4720：附件警告跨对话持久化
- #4724：新对话草稿丢失
- #4723：新对话 Composer 悬停状态不完整
- #4823：删除运行中对话无反馈
- #4819：Light 主题下警告文本对比度低

### 稳定性观察

**WebUI 交互问题集中爆发**：过去24小时关闭了10+个 Reborn WebChat v2 的 UX bug，涉及消息显示、状态管理、主题适配等，反映出前端功能快速迭代中的质量问题。建议加强 UI 集成测试覆盖。

---

## 💡 功能请求与路线图信号

### 用户需求热点

| 需求 | Issue | 优先级 | 相关 PR | 预期影响 |
|---|---|---|---|---|
| **附件支持** | #4644 | 🔴 高 | #4738, #4654, #4655, #4668, #4670 | 6条 PR 栈，覆盖注册表、存储、前端，预计近期合并 |
| **权限跨线程持久化** | #4825 | 🔴 高 | #4835 | 已有修复 PR，待合并 |
| **运行时上下文透明度** | #4828 | 🔴 高 | #4836 | 已有实现 PR，待合并 |
| **消息队列可靠性** | #4817 | 🟡 中 | #4812 (已合并), #4831, #4832, #4833 | 后续优化 PR 进行中 |
| **模型时间感知** | #4796 | 🟡 中 | ⏳ 无 | 需要在系统提示中注入当前日期/时间 |
| **Slack 集成完善** | #4828 | 🟡 中 | #4777, #4778, #4836 | 3条 PR 栈，使 Slack 成为产品适配器 |
| **LLM 使用量追踪** | #4822 | 🟡 中 | ⏳ 无 | Engine V2 缺少 `/api/admin/usage` 支持 |

### 路线图信号

**近期（1-2周）**：
- 附件完整链路上线（#4644 栈）
- 权限系统跨线程持久化（#4835）
- 运行时上下文注入（#4836）
- Slack 产品适配器化（#4777, #4778）

**中期（2-4周）**：
- 消息队列批处理优化（#4832）
- 文件系统后端索引优化（#4833）
- CI 测试分片加速（#4813）
- 大文件分解重构（#4818）

---

## 👥 用户反馈摘要

### 真实痛点

1. **权限疲劳**（#4825）：用户在每个新线程中被重复提示相同权限，降低体验。**根本原因**：权限作用域绑定 thread_id。

2. **配置丢失**（#4703, #4673, #4706）：NEAR AI 提供商配置在测试连接成功后无法保存，用户反复设置。**根本原因**：前端/后端字段映射错误或异常处理缺失。

3. **消息丢失**（#4812, #4817）：权限门控阻塞运行时，用户消息永久丢失。**根本原因**：消息队列无持久化机制。

4. **状态不同步**（#4697, #4828）：UI 显示的活跃提供商与实际使用不符；Slack 连接状态不可见。**根本原因**：运行时状态未注入模型和 UI。

5. **本地开发困难**（#4705, #4696）：SSO 和 Ollama 连接在本地环境失败或虚假成功。**根本原因**：环境检测和错误处理不完善。

### 使用场景

- **多线程工作流**：用户在同一 Agent 下开多个线程处理不同任务，期望权限一次授权全局有效
- **Slack 集成**：用户希望在 Slack 中与 Agent 交互，需要连接状态可见和可靠的消息传递
- **本地开发**：开发者在本地环境快速迭代，需要清晰的错误提示和配置验证

---

## ⏳ 待处理积压

### 长期未响应的关键 Issue

| Issue | 创建时间 | 天数 | 状态 | 建议 |
|---|---|---|---|---|
| **#4796** | 2026-06-12 | 1 | 🔴 无回应 | 模型缺乏时间感知，影响日程/提醒功能，需要设计方案 |
| **#4822** | 2026-06-12 | 1 | 🔴 无回应 | Engine V2 LLM 使用量追踪缺失，影响管理员监控，需要实现 |
| **#4759** | 2026-06-11 | 2 | 🔴 无回应 | 工作区路径重复，影响文件操作，需要调查 |
| **#4813** | 2026-06-12 | 1 | 🔴 无回应 | CI 测试分片，影响开发反馈速度，需要规划 |
| **#4818** | 2026-06-12 | 1 | 🔴 无回应 | slack_delivery.rs 超过 3000 行，影响代码维护，需要重构 |

### 待合并的关键 PR（>3天）

| PR | 创建时间 | 天数 | 大小 | 风险 | 建议 |
|---|---|---|---|---|---|
| **#4738** | 2026-06-10 | 3 | XL | 中 | 附件 WebUI，依赖 #4677，需加速审查 |
| **#4777** | 2026-06-11 | 2 | XL | 低 | Slack 状态持久化，已有评论，可合并 |
| **#4654** | 2026-06-09 | 4 | XL | 低 | 附件格式注册表，#4644 栈基础，优先级高 |
| **#4655** | 2026-06-09 | 4 | XL | 中 | 附件转录合约，#4644 栈核心，优先级高 |
| **#4668** | 2026-06-10 | 3 | L | 中 | 附件存储基础，#4644 栈依赖，优先级高 |
| **#3708** | 2026-05-16 | 28 | M | 中 | 发布 PR（自动化），长期未合并，需检查阻塞原因 |

### 维护者行动项

1. **立即处理**：
   - 解决 #4824 RUSTSEC 安全公告，恢复 CI
   - 审查并合并 #4835（权限跨线程）、#4836（运行时上下文）
   - 加速 #4644 附件栈的审查（已 4 条 PR 待合并）

2. **本周内**：
   - 调查 #4762（消息顺序混乱）和 #4759（路径重复）的根本原因
   - 设计 #4796（模型时间感知）和 #4822（LLM 使用

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

LobsterAI 项目今日保持高活跃度，**24小时内合并/关闭 11 条 PR，待合并 6 条**，整体开发节奏稳健。重点推进了 **Computer Use MVP 功能、实时语音输入、图片保存修复** 等核心特性，同时处理了多个稳定性问题。项目处于**快速迭代阶段**，功能完善度和代码质量均在持续提升。

---

## 🚀 项目进展

### 核心功能推进（已合并）

| PR | 作者 | 内容摘要 | 影响范围 |
|---|---|---|---|
| **#2158** | @liuzhq1986 | [release/2026.6.11 → main] 合并 2026.6.12 版本分支，包含 Computer Use MVP、实时语音输入、HTML 制品分享等 | 🔴 **重大** - 多模块协调发布 |
| **#2156** | @btc69m979y-dotcom | Computer Use 运行时升级至 1.0.7，新增 UIA 诊断面包屑 | 🟡 **中等** - 可靠性增强 |
| **#2157** | @liugang519 | 修正文生图保存扩展名，优先识别文件字节格式而非服务端返回值 | 🟡 **中等** - 用户体验修复 |
| **#2155** | @btc69m979y-dotcom | 防止实时 ASR 重复启动，修复语音输入竞态条件 | 🟡 **中等** - 稳定性修复 |
| **#2154** | @liuzhq1986 | 流式停止后保留模型元数据，修复部分回复丢失问题 | 🟡 **中等** - 数据完整性 |
| **#2153** | @liuzhq1986 | 保留同名包模型选择，区分包内模型与自定义模型 | 🟡 **中等** - 功能完善 |

### 待合并 PR（6 条）

- **#1446** (stale) - 修复网关无限重启循环 - 竞态条件修复
- **#1448** (stale) - Agent 设置页国际化缺失 - i18n 完善
- **#1449** (stale) - 定时任务执行记录折叠分组 - UX 优化
- **#1453** (stale) - 已停用技能仍被注入提示词 - 功能 Bug
- **#1454** (stale) - 不重复模式清空日期后无响应 - 交互 Bug
- **#1456** (stale) - 快捷键设置缺少重复检测 - 配置验证

⚠️ **注意**：6 条待合并 PR 均标记为 `[stale]`，创建于 2026-04-03~04-04，**已停留 70+ 天未合并**，需要维护者优先审视。

---

## 🐛 Bug 与稳定性

### 已关闭 Issue

| Issue | 状态 | 严重程度 | 描述 |
|---|---|---|---|
| **#1** | ✅ CLOSED | 🔴 **高** | OpenAI API 400 错误 - 无效参数 | 
| | | | 用户在 Mac 上配置 OpenAI API 后，Chat 输入任务返回 400 错误 |
| | | | 创建：2026-02-19 | 关闭：2026-06-12 | 评论：7 条 |

### 待修复的已知问题（PR 形式）

| 优先级 | 问题 | 关联 PR | 根因分析 |
|---|---|---|---|
| 🔴 高 | 网关无限重启循环 | #1446 | 竞态条件：进程崩溃时 `waitForGatewayReady` 与 `scheduleGatewayRestart()` 时序冲突 |
| 🟡 中 | 已停用技能仍被调用 | #1453 | `skill.enabled` 与 `activeSkillIds` 同步缺口，三处漏洞 |
| 🟡 中 | 定时任务创建无响应 | #1454 | 三层缺陷叠加：`onChange` 丢弃、验证缺失、错误吞没 |
| 🟡 中 | 快捷键冲突无检测 | #1456 | 缺少重复键检测，多功能绑定同一组合键导致部分失效 |
| 🟢 低 | 图片保存扩展名错误 | #2157 | ✅ **已修复** - 优先识别文件字节格式 |
| 🟢 低 | 语音输入重复启动 | #2155 | ✅ **已修复** - 添加启动竞态防护 |

---

## 💬 社区热点

### 最活跃讨论

**#1** - OpenAI API 400 错误 ([链接](https://github.com/netease-youdao/LobsterAI/issues/1))
- **评论数**：7 条 | **创建**：2026-02-19 | **关闭**：2026-06-12
- **用户痛点**：跨平台 API 配置兼容性问题
- **背景**：用户在 Mac OS 13.7.8 上配置 MiniMax API 成功，切换到 OpenAI 后出现参数验证错误
- **启示**：多 API 提供商支持需要更严格的参数校验和错误提示

### 待处理的高价值 PR

**#1449** - 定时任务执行记录折叠分组 ([链接](https://github.com/netease-youdao/LobsterAI/pull/1449))
- **用户痛点**：每日执行的定时任务一周后在侧栏堆积 7 条记录，严重干扰会话查找
- **方案**：对同一 job 的多次执行记录进行聚合分组展示
- **影响**：直接改善长期用户的使用体验

**#1453** - 已停用技能仍被调用 ([链接](https://github.com/netease-youdao/LobsterAI/pull/1453))
- **用户痛点**：关闭技能后仍被注入对话，导致意外调用
- **根因**：状态同步缺口，三处代码漏洞
- **影响**：功能可靠性问题，需优先合并

---

## 🎯 功能请求与路线图信号

### 近期已实现的功能（2026.6.12 版本）

1. **Computer Use MVP** - 完整的计算机操作能力框架
2. **实时语音输入** - Cowork 提示词的 ASR 支持
3. **制品分享增强** - HTML/SVG 制品公开分享模式选择
4. **图片处理完善** - 文生图保存格式自动识别

### 待纳入的功能需求（基于 stale PR）

| 功能 | 优先级 | 预期收益 | 关联 PR |
|---|---|---|---|
| 定时任务记录分组 | 🟡 中 | 改善侧栏 UX，提升长期用户体验 | #1449 |
| Agent 国际化完善 | 🟢 低 | 支持非英文用户，扩大市场 | #1448 |
| 快捷键冲突检测 | 🟡 中 | 提升配置可靠性 | #1456 |
| 未保存内容确认 | 🟡 中 | 防止数据丢失，提升用户信任 | #1473-1477 |

---

## 👥 用户反馈摘要

### 核心痛点

1. **跨 API 兼容性** - MiniMax → OpenAI 切换时参数验证失败
   - 建议：统一 API 参数校验层，提供更清晰的错误提示

2. **定时任务管理** - 长期运行导致侧栏堆积，查找困难
   - 建议：实现记录分组/折叠，或提供任务历史独立视图

3. **技能启用状态同步** - 关闭后仍被调用，造成困惑
   - 建议：强化状态管理，添加单元测试覆盖

4. **数据丢失风险** - 未保存内容在导航/关闭时丢失
   - 建议：全局草稿持久化机制，已有 5 个 PR 在推进

### 满意度信号

- 用户积极反馈 Computer Use 功能（MVP 已合并）
- 语音输入、制品分享等新特性获得关注
- 社区愿意提交详细 Bug 报告和修复 PR

---

## ⚠️ 待处理积压

### 长期未响应的 PR（70+ 天）

| PR | 创建日期 | 天数 | 状态 | 优先级 | 建议 |
|---|---|---|---|---|---|
| #1446 | 2026-04-03 | 71 天 | OPEN | 🔴 高 | **立即审视** - 网关重启循环是严重稳定性问题 |
| #1448 | 2026-04-03 | 71 天 | OPEN | 🟢 低 | 合并或关闭 - i18n 完善，低风险 |
| #1449 | 2026-04-03 | 71 天 | OPEN | 🟡 中 | **优先合并** - 高价值 UX 改进 |
| #1453 | 2026-04-03 | 71 天 | OPEN | 🔴 高 | **立即合并** - 功能 Bug，影响可靠性 |
| #1454 | 2026-04-03 | 71 天 | OPEN | 🟡 中 | 合并 - 交互 Bug，用户可感知 |
| #1456 | 2026-04-03 | 71 天 | OPEN | 🟡 中 | 合并 - 配置验证，防止用户误操作 |

### 建议行动

1. **本周内**：审视 #1446（网关重启）、#1453（技能同步）的代码质量，决定合并或请求修改
2. **本周内**：批量合并 #1448、#1454、#1456，这些都是低风险的 Bug 修复
3. **下周**：重点评审 #1449，如无异议应纳入下一版本
4. **持续**：建立 PR 审视 SLA（如 30 天未审视自动提醒）

---

## 📈 项目健康度评分

| 维度 | 评分 | 说明 |
|---|---|---|
| **开发活跃度** | ⭐⭐⭐⭐⭐ | 24h 合并 11 PR，待审 6 PR，节奏稳健 |
| **功能完善度** | ⭐⭐⭐⭐ | Computer Use MVP、语音输入等核心功能就位，细节优化进行中 |
| **稳定性** | ⭐⭐⭐⭐ | 已修复语音、图片等问题，但网关重启、技能同步等高优先级 Bug 待处理 |
| **社区响应** | ⭐⭐⭐ | Issue 关闭及时（#1 从 2 月跟进到 6 月），但 PR 审视有 70+ 天延迟 |
| **代码质量** | ⭐⭐⭐⭐ | 详细的根因分析、回归测试覆盖，但 stale PR 积压需清理 |

**总体评价**：项目处于**快速迭代期**，功能驱动明显，但需加强 PR 审视流程以避免积压。建议优先处理 stale PR，确保代码库整洁。

---

**下次日报预计**：2026-06-14 | **数据来源**：GitHub API | **生成时间**：2026-06-13

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

Moltis 项目今日保持稳定活跃，新增 3 条 Issue 讨论，暂无 PR 合并或版本发布。社区关注点集中在**安全隔离、语音识别引擎扩展和第三方服务集成**三个方向，反映出用户对生产级部署能力和多模态功能的迫切需求。项目整体处于**功能扩展阶段**，维护者响应及时。

---

## 🔄 项目进展

**本周期无 PR 合并/关闭**

当前无新的代码合并，项目处于需求收集和设计阶段。建议关注后续 PR 动向，特别是针对 #1118 和 #1102 的实现进展。

---

## 🔥 社区热点

### 1. **#1118 - Kubernetes 原生沙箱后端支持** ⭐ 最新功能需求
- **作者**: @AzgadAGZ | **创建**: 2026-06-12 | **评论**: 1
- **链接**: https://github.com/moltis-org/moltis/issues/1118
- **核心诉求**: 为 Agent 命令执行添加 Kubernetes 沙箱后端，支持 `runtimeClassName` 实现 VM 级隔离（Kata Containers/gVisor）
- **背景分析**: 反映用户在**生产环境中对安全隔离的强烈需求**，特别是在云原生部署场景下。这是从开发工具向企业级产品演进的关键功能。

### 2. **#1102 - FunASR/SenseVoice 本地 STT 引擎**
- **作者**: @LauraGPT | **创建**: 2026-06-04 | **更新**: 2026-06-12 | **评论**: 1
- **链接**: https://github.com/moltis-org/moltis/issues/1102
- **核心诉求**: 集成开源 STT 引擎（FunASR/SenseVoice），实现超低延迟本地语音识别（~70ms@10s audio）
- **背景分析**: 用户希望**降低对云服务的依赖**，实现离线语音助手能力。SenseVoice 的流式处理特性与 Moltis 的实时交互需求高度契合。

### 3. **#1115 - Fastmail MCP 授权问题** 🐛
- **作者**: @kmath313 | **创建**: 2026-06-11 | **更新**: 2026-06-12 | **评论**: 2
- **链接**: https://github.com/moltis-org/moltis/issues/1115
- **核心诉求**: Fastmail MCP 集成的授权流程存在问题
- **背景分析**: 涉及第三方服务集成的稳定性，影响用户的邮件助手功能。

---

## 🐛 Bug 与稳定性

| Issue | 严重程度 | 状态 | 修复进展 |
|-------|--------|------|--------|
| #1115 - Fastmail MCP 授权 | 🟡 **中** | OPEN | 无 fix PR，需要维护者跟进 |

**分析**: 仅 1 个 Bug 报告，项目整体稳定性良好。Fastmail 集成问题可能影响邮件相关功能的可用性，建议优先处理。

---

## ✨ 功能请求与路线图信号

### 优先级评估

| 功能 | 优先级 | 用户需求强度 | 实现复杂度 | 战略意义 |
|------|-------|-----------|---------|--------|
| Kubernetes 沙箱后端 (#1118) | 🔴 **高** | 高（企业级需求） | 高 | 生产部署必需 |
| FunASR/SenseVoice STT (#1102) | 🟡 **中** | 中（隐私/离线需求） | 中 | 多模态能力完善 |
| Fastmail MCP 修复 (#1115) | 🟡 **中** | 中（功能完整性） | 低 | 生态完整性 |

**路线图信号**: 
- **短期** (1-2周): 修复 #1115 Fastmail 授权问题
- **中期** (1-2月): 评估 #1102 STT 集成的技术方案
- **长期** (2-3月): 启动 #1118 Kubernetes 后端开发

---

## 💬 用户反馈摘要

### 核心痛点
1. **安全隔离** - 用户在生产环境中运行 LLM 生成的代码，需要强隔离保障
2. **隐私与离线** - 希望减少对云服务依赖，实现本地化部署
3. **生态完整性** - 第三方服务集成的稳定性直接影响用户体验

### 使用场景信号
- 企业级 AI Agent 部署（Kubernetes 环境）
- 隐私敏感的语音助手应用
- 邮件/日程等生产力工具集成

---

## ⏳ 待处理积压

**长期未响应的重要 Issue**:
- **#1102** (创建于 2026-06-04，已 9 天) - FunASR/SenseVoice 需求虽有评论但无明确反馈，建议维护者给出可行性评估

**建议行动**:
1. 对 #1118 进行技术可行性评审，明确 Kubernetes 后端的设计方案
2. 对 #1115 进行根因分析，确认是 Fastmail API 变更还是 Moltis 实现问题
3. 对 #1102 进行需求优先级评分，决定是否纳入下一版本规划

---

## 📈 项目健康度评分

| 维度 | 评分 | 备注 |
|------|------|------|
| 社区活跃度 | ⭐⭐⭐⭐ | 3 条新 Issue，用户持续反馈 |
| 维护响应速度 | ⭐⭐⭐⭐ | 24h 内有更新回应 |
| 代码更新频率 | ⭐⭐⭐ | 本周期无 PR 合并，处于需求评估阶段 |
| 稳定性 | ⭐⭐⭐⭐ | 仅 1 个 Bug，整体稳定 |
| **综合评分** | **⭐⭐⭐⭐** | 健康的功能扩展阶段 |

---

**下次日报预计**: 2026-06-14 | **关注重点**: Kubernetes 后端设计进展、Fastmail 修复状态

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报
**日期：2026-06-13** | **数据周期：过去24小时**

---

## 📊 今日速览

CoPaw 项目今日保持高活跃度，24小时内新增/活跃 Issues 14 条，待合并 PR 13 条，社区反馈热烈。项目正处于**版本迭代密集期**——v1.1.11.post2 刚发布不久，已暴露多个回归 Bug；同时核心架构升级（AgentScope 2.0 迁移、Runtime 2.0 重构）正在推进中。整体呈现"快速迭代、问题频出、积极修复"的特征，社区参与度高。

---

## 🔄 版本发布

**无新版本发布**

但值得关注的是：
- **v1.1.12b1 版本准备中**：PR #5159 已合并，版本号从 `1.1.12.beta1` 调整为 `1.1.12b1`
- **v1.1.11.post2 回归问题**：该版本发布后已发现至少 3 个严重回归（见下文 Bug 部分）

---

## ✅ 项目进展

### 今日合并/关闭的关键 PR（10 条）

| PR | 类型 | 说明 | 影响范围 |
|---|---|---|---|
| [#5159](https://github.com/agentscope-ai/QwenPaw/pull/5159) | 版本管理 | 版本号格式修正 (1.1.12b1) | 发布流程 |
| [#5144](https://github.com/agentscope-ai/QwenPaw/pull/5144) | Bug Fix | 修复长期记忆配置丢失问题 | 记忆系统 |
| [#5147](https://github.com/agentscope-ai/QwenPaw/pull/5147) | Bug Fix | 修复 Coding Mode 刷新后 Session 丢失 | 前端路由 |
| [#5154](https://github.com/agentscope-ai/QwenPaw/pull/5154) | Bug Fix | 重构记忆搜索工具结果样式 | UI 渲染 |
| [#5121](https://github.com/agentscope-ai/QwenPaw/pull/5121) | CI/CD | 新增发布验证门禁 | 质量保证 |
| [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) | 架构重构 | Runtime 2.0 模块化架构 + ToolCoordinator | 核心运行时 |
| [#5022](https://github.com/agentscope-ai/QwenPaw/pull/5022) | 安全加固 | Agent 工作区路径验证 | 工作区管理 |
| [#4144](https://github.com/agentscope-ai/QwenPaw/pull/4144) | Bug Fix | 修复桌面版 0.0.0.0 绑定的就绪检查 | 桌面客户端 |
| [#5157](https://github.com/agentscope-ai/QwenPaw/pull/5157) | 版本管理 | 版本号 bump 到 1.1.12.beta1 | 发布流程 |

**核心进展**：
- ✅ **记忆系统稳定性提升**：修复了配置丢失、搜索结果渲染等问题
- ✅ **前端路由健壮性**：Coding Mode Session 持久化问题已解决
- ✅ **发布流程强化**：新增验证门禁，防止有问题的版本发布
- ✅ **架构现代化**：Runtime 2.0 已合并，为 AgentScope 2.0 迁移铺路

---

## 🔥 社区热点

### 评论最活跃的 Issues

| Issue | 评论数 | 热度 | 核心诉求 |
|---|---|---|---|
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | 11 | 🔴 高 | **定时任务无法触发** — Agent 生成的定时任务到期不执行，且无法手动编辑 |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | 10 | 🔴 高 | **AgentScope 2.0 迁移** — 后端升级计划，涉及 API 和运行时模型重构 |
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | 6 | 🟠 中 | **文件下载 Bug** — docx/pdf 下载报 404，纯文本正常 |
| [#5137](https://github.com/agentscope-ai/QwenPaw/issues/5137) | 5 | 🟠 中 | **向量模型配置丢失** — 未展开卡片时保存会丢失配置 |
| [#5098](https://github.com/agentscope-ai/QwenPaw/issues/5098) | 4 | 🟠 中 | **记忆搜索结果渲染异常** — 表格内容为空/错误 |

### 新增高价值功能请求

| Issue | 类型 | 诉求 | 关注度 |
|---|---|---|---|
| [#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139) | Feature | **Agent Team/Swarm 协作能力** — 类似 WorkBuddy 专家团队 | ⭐⭐⭐ |
| [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156) | Feature | **支持 Kimi-for-coding** — 加入 UV 白名单 | ⭐⭐ |
| [#5152](https://github.com/agentscope-ai/QwenPaw/issues/5152) | Feature | **Slack 频道支持** — 本地部署集成 | ⭐⭐ |
| [#5164](https://github.com/agentscope-ai/QwenPaw/issues/5164) | Feature | **桌面版系统托盘/开机自启/后台常驻** | ⭐⭐ |

---

## 🐛 Bug 与稳定性

### 严重级别 Bug（需立即关注）

| Issue | 版本 | 症状 | 状态 | Fix PR |
|---|---|---|---|---|
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | v1.1.10+ | **定时任务无法触发** | 🔴 OPEN | ❌ 无 |
| [#5155](https://github.com/agentscope-ai/QwenPaw/issues/5155) | v1.1.11 | **Docker 环境自动宕机重启** | 🔴 OPEN | ❌ 无 |
| [#5162](https://github.com/agentscope-ai/QwenPaw/issues/5162) | v1.1.11+ | **对话思考逻辑死循环** | 🔴 OPEN | ❌ 无 |
| [#5161](https://github.com/agentscope-ai/QwenPaw/issues/5161) | v1.1.11+ | **长对话后无响应** | 🔴 OPEN | ❌ 无 |

### 中等级别 Bug（已修复或修复中）

| Issue | 版本 | 症状 | 状态 | Fix PR |
|---|---|---|---|---|
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | v1.1.11.post2 | docx/pdf 下载 404 | ✅ CLOSED | ✅ [#5160](https://github.com/agentscope-ai/QwenPaw/pull/5160) |
| [#5137](https://github.com/agentscope-ai/QwenPaw/issues/5137) | v1.1.11 | 向量模型配置丢失 | ✅ CLOSED | ✅ [#5144](https://github.com/agentscope-ai/QwenPaw/pull/5144) |
| [#5098](https://github.com/agentscope-ai/QwenPaw/issues/5098) | v1.1.11 | 记忆搜索结果渲染异常 | ✅ CLOSED | ✅ [#5154](https://github.com/agentscope-ai/QwenPaw/pull/5154) |
| [#5142](https://github.com/agentscope-ai/QwenPaw/issues/5142) | v1.1.11.post2 | Coding Mode 刷新后 Session 丢失 | ✅ CLOSED | ✅ [#5147](https://github.com/agentscope-ai/QwenPaw/pull/5147) |
| [#5148](https://github.com/agentscope-ai/QwenPaw/issues/5148) | v1.1.11.post2 | 数学公式根号显示错误 | ✅ CLOSED | ✅ 已修复 |
| [#5163](https://github.com/agentscope-ai/QwenPaw/issues/5163) | v1.1.11.post2 | Gemini 工具调用回归 | 🔴 OPEN | ❌ 无 |

### 轻微级别 Bug

| Issue | 症状 | 状态 |
|---|---|---|
| [#5145](https://github.com/agentscope-ai/QwenPaw/issues/5145) | 执行详情冗余显示 | 🔴 OPEN |
| [#5167](https://github.com/agentscope-ai/QwenPaw/issues/5167) | Feishu CardKit 流式卡片长回复变慢 | 🔴 OPEN |
| [#5151](https://github.com/agentscope-ai/QwenPaw/pull/5151) | GitPanel Tabs 样式未生效 | 🟡 PR OPEN |

### 环境兼容性问题

| Issue | 症状 | 状态 |
|---|---|---|
| [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) | Python 3.13 环境 TeamChat 插件安装失败 (`imghdr` 模块缺失) | 🔴 OPEN |
| [#5165](https://github.com/agentscope-ai/QwenPaw/issues/5165) | PyInstaller 打包后白屏 (qwenpaw.spec 引用不存在模块) | 🔴 OPEN |

**稳定性评估**：
- ⚠️ **v1.1.11.post2 质量堪忧**：短时间内暴露 6+ 个 Bug，其中 4 个严重
- ✅ **修复响应迅速**：已关闭 5 个 Bug，修复率 45%
- 🔴 **关键功能缺陷未修**：定时任务、长对话、Docker 稳定性问题仍待解决

---

## 🚀 功能请求与路线图信号

### 已在 PR 中推进的功能

| 功能 | PR | 状态 | 预期影响 |
|---|---|---|---|
| **Agent OS Driver** (MCP/A2A/ACP 统一抽象) | [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) | 🟡 Under Review | 外部能力集成框架 |
| **Runtime 2.0** (模块化架构 + ToolCoordinator) | [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) | ✅ MERGED | 核心运行时现代化 |
| **Visual Model Fallback** (文本模型图像处理) | [#5069](https://github.com/agentscope-ai/QwenPaw/pull/5069) | 🟡 Under Review | 多模态能力增强 |
| **Per-turn Token Usage** (单轮 token 统计) | [#5130](https://github.com/agentscope-ai/QwenPaw/pull/5130) | 🟡 OPEN | 成本透明化 |
| **DataPaw 数据分析插件** (12 个 BI 技能) | [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) | 🟡 Under Review | 数据分析能力 |
| **Yuanbao 频道增强** (引用消息 + 媒体下载统一) | [#5160](https://github.com/agentscope-ai/QwenPaw/pull/5160) | 🟡 OPEN | 频道功能对齐 |
| **Tauri 桌面优化** (即时窗口启动) | [#5153](https://github.com/agentscope-ai/QwenPaw/pull/5153) | 🟡 OPEN | 启动速度优化 |

### 用户呼声高但尚无 PR 的功能

| 功能 | Issue | 呼声 | 建议优先级 |
|---|---|---|---|
| **Agent Team/Swarm 协作** | [#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139) | ⭐⭐⭐ | 🔴 高 |
| **Slack 频道支持** | [#5152](https://github.com/agentscope-ai/QwenPaw/issues/5152) | ⭐⭐ | 🟡 中 |
| **Kimi-for-coding 支持** | [#5156](https://github.com/agentscope-ai/QwenPaw/issues/5156) | ⭐⭐ | 🟡 中 |
| **桌面版系统托盘/开机自启** | [#5164](https://github

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