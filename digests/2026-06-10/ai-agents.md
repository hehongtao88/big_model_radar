# OpenClaw 生态日报 2026-06-10

> Issues: 500 | PRs: 500 | 覆盖项目: 12 个 | 生成时间: 2026-06-10 12:41 UTC

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
**日期：2026-06-10**

---

## 📊 今日速览

OpenClaw 项目呈现**高度活跃的开发状态**：过去24小时内 500+ Issues 更新（新开/激活 460 条，已关闭 40 条）和 500+ PR 更新（待合并 417 条，已合并/关闭 83 条）。发布了 **v2026.6.5 版本**，主要修复了 QQBot 的模型推理泄露问题和 MCP 工具结果强制转换。当前积压的待审核 PR 超过 400 条，Issues 中高优先级（P1）问题集中在**消息传递可靠性、会话状态管理和安全边界**三大类。项目整体处于**快速迭代但质量压力较大**的阶段。

---

## 🚀 版本发布

### **v2026.6.5** 
**发布时间**：2026-06-10

#### 关键修复

- **QQBot 思维链泄露修复** (#89913, #90132)
  - 问题：Claude 模型的原生 `<thinking>` 思维块内容在发送到频道前未被过滤，导致内部推理过程暴露
  - 解决：在原生交付前自动剥离模型推理/思考脚手架内容
  - 影响范围：所有使用 QQBot 的 Claude 用户

- **MCP 工具结果强制转换**
  - 资源链接、资源、音频、畸形图片等类型现已正确强制转换
  - 修复了跨频道工具调用时的类型不匹配问题

#### 迁移注意事项
- 推荐所有使用 Claude 模型的 QQBot 部署升级
- 无破坏性变更，可直接升级

---

## 🔧 项目进展

### 今日合并/关闭的重点 PR（前 10 个）

| PR | 类型 | 状态 | 焦点 |
|---|---|---|---|
| #91361 | 修复 | OPEN | **降低默认压缩超时** 从 900s → 180s，防止长会话压缩时持有写锁过久 |
| #88075 | 功能 | OPEN | **执行工具安全强化**：新增 `tools.exec.denyPathPatterns` 硬关卡，阻止危险路径执行 |
| #88084 | 修复 | OPEN | **审批命令路由修复**：允许授权的 `/approve` 命令绕过活跃回复队列 |
| #88059 | 功能 | OPEN | **浏览器工具增强**：`--labels` 标签覆盖扩展到全页面和元素截图 |
| #88062 | 修复 | OPEN | **日志优化**：避免活跃模型调用时的假"已卡住"警告 |
| #88023 | 功能 | OPEN | **会话恢复**：新增 `session:aborted` 事件 + 自动继续钩子 |
| #88098 | 功能 | OPEN | **CLI 增强**：非交互式 onboard 新增 `--custom-context-window` 标志 |
| #88078 | 修复 | OPEN | **主动记忆优化**：修剪回忆提示包络以提高精准度 |

### 进度指标
- **待合并 PR**：417 条（较高积压），主要集中在 `merge-risk: compatibility` 和 `merge-risk: security-boundary` 标签上
- **本日贡献者**：至少 35+ 位
- **关键推进方向**：安全强化、可靠性改进、用户体验优化

---

## 💬 社区热点

### 讨论最活跃的议题（按评论数排序）

#### 🔴 **高热度 Issue**

1. **#75 - Linux/Windows ClawdBot Apps** 
   - 评论：109 | 👍：79 | 优先级：P2
   - 链接：https://github.com/openclaw/openclaw/issues/75
   - 诉求：目前仅支持 macOS/iOS/Android，急需 Linux 和 Windows 版本
   - 社区声音：广泛的跨平台支持需求

2. **#25592 - 工具调用间文本泄露到消息频道**
   - 评论：30 | 👍：1 | 优先级：P1（🦞 diamond lobster 评级）
   - 链接：https://github.com/openclaw/openclaw/issues/25592
   - 诉求：Agent 在工具调用间产生的文本（错误处理、处理确认、叙述）被路由到 Slack/iMessage 等消息频道，造成 UX 混乱
   - 关联 PR：https://github.com/openclaw/openclaw/pull/52664 已暴露 `rawBody` 用于插件处理

3. **#9443 - 预构建 Android APK 发布**
   - 评论：25 | 👍：2 | 优先级：P2
   - 链接：https://github.com/openclaw/openclaw/issues/9443
   - 诉求：源码已有 Android 支持，但无预编译 APK 下载，用户难以获取
   - 背景：提交者为 Lysen 的 AI 助手 QING

4. **#44925 - 子 Agent 完成无声丢失**
   - 评论：19 | 👍：1 | 优先级：P1 | 评级：🐚 platinum hermit
   - 链接：https://github.com/openclaw/openclaw/issues/44925
   - 诉求：子 Agent 任务编排存在多个失败模式导致结果无声丢失，无重试、无通知、无自动重启
   - 影响范围：多 Agent 编排架构

5. **#22676 - Signal 守护进程停止竞态条件**
   - 评论：17 | 👍：0 | 优先级：P1
   - 链接：https://github.com/openclaw/openclaw/issues/22676
   - 诉求：SIGUSR1 网关重启时，信号守护进程在旧进程释放端口前启动新进程，导致孤立进程和发送失败
   - 系统影响：Signal 频道可靠性

#### 🟡 **功能需求热点**

| Issue | 评论 | 需求 | 优先级 |
|---|---|---|---|
| #10659 | 13 | 掩码秘密 - 阻止 Agent 访问原始 API 密钥 | P1 |
| #12602 | 13 | Slack Block Kit 支持 - 富媒体响应 | P2 |
| #22438 | 17 | 分层 bootstrap 文件加载 - 减少 Token 浪费 | P2 |
| #13583 | 11 | 前置响应强制钩子 - 高风险工作流的硬关卡 | P2 |
| #18160 | 12 | 定时任务直接执行模式 - 跳过 LLM 解释 | P2 |

---

## 🐛 Bug 与稳定性

### 严重级别分布

#### 🔴 **P1 关键 Bug**（立即修复）

| Issue | 类型 | 状态 | 修复 PR | 影响 |
|---|---|---|---|---|
| #25592 | 消息泄露 | OPEN | 进行中 | 用户体验，跨频道 |
| #44925 | 任务丢失 | OPEN | ❌ | 多 Agent 编排核心 |
| #22676 | 竞态条件 | OPEN | ❌ | Signal 频道可靠性 |
| #85030 | MCP 工具未注入 | OPEN | ❌ | 子 Agent 功能瘫痪 |
| #83184 | 心跳卡住 | OPEN | #88023 | 会话长期运行中断 |
| #87307 | Matrix 线程回归 | OPEN | ❌ | 2026.5.22 引入 |
| #57326 | CLI 后端绕过 | OPEN | ❌ | 安全边界突破 |
| #29736 | exec-approvals 路径忽略 | OPEN | ❌ | 状态持久化错误 |
| #72015 | 主动记忆阻塞 | OPEN | ❌ | 网关可靠性 |

#### 🟡 **P2 中等 Bug**（近期修复）

- #52875：`session_send` "未找到会话" 回归（已关闭）
- #88929：Feishu 流媒体卡片打字效果异常（已关闭）
- #57901：压缩模型配置忽略（#88075 相关）
- #58450：Agent 承诺后续操作但未启动（文档/行为差异）

#### 📋 **已关闭修复**

- **#52875**：会话列表回归 → 已解决
- **#88929**：Feishu 卡片截断 → 已解决  
- **#60858**：压缩哈希防卫三重检查阻挡 → 已解决

### 稳定性趋势

⚠️ **当前风险**: 
- **高并发场景**：主动记忆阻塞 (#72015)、心跳卡住 (#83184) 导致多 Agent 网关不稳定
- **消息可靠性**：工具调用间文本泄露、Matrix 线程回归、WhatsApp 消息丢失 (#50093)
- **会话状态**：子 Agent 完成无声丢失、bootstrap 文件被忽略 (#29387)

---

## ✨ 功能请求与路线图信号

### 将在近期版本纳入的功能（有关联 PR）

| 功能 | 优先级 | 关联 PR | 预期影响 |
|---|---|---|---|
| **执行工具路径拒绝列表** | P1 | #88075 | 安全强化，阻止敏感路径 |
| **WebChat 进度事件** | P2 | #88048 | 用户体验，实时反馈 |
| **浏览器标签全页覆盖** | P2 | #88059 | 视觉任务精准度 |
| **心跳驱动自动继续** | P1 | #88023 | 会话恢复自愈 |
| **压缩超时降低** | P1 | #91361 | 长会话响应性 |

### 中期规划信号（讨论中的功能）

| 功能 | 讨论热度 | 难度 | 用户痛点 |
|---|---|---|---|
| **掩码秘密（Masked Secrets）** | ⭐⭐⭐⭐⭐ | 高 | Agent 能使用但看不到 API 密钥 |
| **跨平台 ClawdBot（Linux/Win）** | ⭐⭐⭐⭐⭐ | 极高 | 企业部署需求 |
| **Slack Block Kit** | ⭐⭐⭐⭐ | 中 | 富媒体响应 |
| **分层 Bootstrap 加载** | ⭐⭐⭐⭐ | 中 | Token 优化，减少 ~3500 tok/session |
| **会话快照存档** | ⭐⭐⭐ | 高 | 长开发会话的检查点 |
| **定时任务直接执行** | ⭐⭐⭐ | 中 | 跳过 LLM 解释加速 |

---

## 👥 用户反馈摘要

### 真实用户痛点（Top 5）

#### 1️⃣ **消息/任务无声丢失** ⚠️ 最高优先级
- **用户群体**：多 Agent 编排、高并发场景用户
- **表现形式**：
  - 子 Agent 完成结果丢失（#44925）
  - 工具调用间文本误送频道（#25592）
  - WhatsApp 断线后消息未回填（#50093）
  - 心跳驱动的最终交付卡住（#83184）
- **根本原因**：异步任务编排中缺少关键同步点和死信处理
- **用户呼声**：希望看到明确的错误日志或自动重试机制

#### 2️⃣ **跨平台支持不足**
- **用户群体**：企业/Linux 服务器部署用户
- **诉求**：
  - Linux/Windows ClawdBot Apps（#75，109 条评论）
  - 预构建 Android APK（#9443，25 条评论）
- **影响**：目前仅支持 macOS/iOS/Android，企业无法标准化部署
- **用户言论**："我们的基础设施全在 Linux，无法使用 macOS 版本"

#### 3️⃣ **安全与秘密管理混乱**
- **用户群体**：金融/安全敏感的 Agent 部署者
- **诉求**：
  - Agent 能用密钥但看不到（掩码秘密，#10659）
  - AWS/Vault 原生集成（#13610）
  - 执行命令黑名单（#6615，7 条评论）
  - 执行路径拒绝列表（#88075）
- **用户困境**：密钥存储在明文配置文件中，AI 注入攻击风险高

#### 4️⃣ **Token 成本与上下文压力**
- **用户群体**：长会话、大规模 Agent 部署用户
- **诉求**：
  - 分层 bootstrap 加载（#22438，每次 session

---

## 横向生态对比

# AI 智能体开源生态纵览报告
**数据采集日期：2026-06-10**

---

## 1. 生态全景：快速迭代向稳定性收敛

当前个人 AI 助手与自主智能体开源生态处于**高速迭代但面临质量压力**的阶段。核心项目（OpenClaw、NanoBot、Zeroclaw、CoPaw 等）日均处理数十条 Issues 和 PRs，新功能层出不穷（多运行时抽象、Agent 自演进、可视化编排）。与此同时，跨项目暴露的共性问题（消息丢失、会话管理、安全隔离、兼容性）表明生态正在从"功能覆盖"过渡到"可靠性补齐"的阶段。多项目涌现的依赖升级（Electron、wasmtime、SDK 版本）与架构重构（Runtime 2.0、Reborn）预示生态整体在进行技术债偿还。

---

## 2. 各项目活跃度对比

| 项目 | 日新增 Issues | 日处理 PRs | 版本状态 | 合并率 | 健康度评估 |
|------|-------------|----------|--------|---------|------------|
| **OpenClaw** | 460 新开/40 关闭 | 500 (417 待合并) | v2026.6.5 ✅ | 17% | ⭐⭐⭐⭐⭐ 超高活跃，质量压力大 |
| **NanoBot** | 8 新增/6 解决 | 32 (13 待合并) | 无新版 | 59% | ⭐⭐⭐⭐ 高频迭代，稳定性好 |
| **Zeroclaw** | 38 新增/17 关闭 | 50 (47 待合并) | 无新版 | 40% | ⭐⭐⭐⭐ 高强度开发，架构优化中 |
| **PicoClaw** | 6 新增 | 18 (14 待合并) | v0.2.9-nightly | 22% | ⭐⭐⭐⭐ 质量补齐阶段，积压待合并 |
| **NanoClaw** | 1 新增 | 47 (5 待合并) | 无新版 | 89% | ⭐⭐⭐⭐⭐ 高效交付，专注度强 |
| **IronClaw** | 33 新增/17 关闭 | 50 (30 待合并) | v0.27.0 阻滞 | 40% | ⭐⭐⭐⭐ 快速迭代，发布管理滞后 |
| **LobsterAI** | 0 新增 | 20 合并 | 2026.6.8 预发布 | 95% | ⭐⭐⭐⭐ 高效交付，功能完善期 |
| **CoPaw** | 18 新增/18 关闭 | 48 (19 待合并) | v1.1.11-beta.3 ✅ | 60% | ⭐⭐⭐⭐⭐ 高活跃，生态扩展中 |
| **Moltis** | 1 新增 | 0 | 无新版 | — | ⭐⭐ 低活跃，维护缓慢 |
| **TinyClaw** | — | — | — | — | ⚠️ 无数据 |
| **ZeptoClaw** | — | — | — | — | ⚠️ 无数据 |
| **EasyClaw** | — | — | — | — | ⚠️ 无数据 |

**关键观察**：
- **最活跃层级**：OpenClaw（1000+ Issues/PR 日均处理）、NanoClaw（47 PR 合并率 89%）、CoPaw（36 Issues 高热度讨论）
- **中等活跃**：NanoBot、Zeroclaw、IronClaw（30-50 PR/day，4-6 周迭代周期）
- **低活跃**：Moltis（维护被搁置）、TinyClaw/ZeptoClaw/EasyClaw（无活动或私有）

---

## 3. OpenClaw 在生态中的定位

### 技术领先性
| 维度 | OpenClaw | NanoBot | Zeroclaw | CoPaw |
|------|----------|---------|----------|--------|
| **核心能力** | 多频道编排、思维链过滤 | 沙箱隔离、搜索集成 | 原生 Reborn 架构 | 插件市场、自动化任务 |
| **会话管理** | 压缩超时降低、心跳恢复 | history 隔离、自适应压缩 | 上下文预算计算优化 | 分片存储、跨会话追踪 |
| **安全防线** | 思维链泄露修复、MCP 强制转换 | pathPrepend、bwrap 隔离 | Per-sender RBAC（规划中） | 文件守卫、护栏框架 |
| **社区规模** | **500+ Issues/day** | 32 Issues/day | 40 Issues/day | 36 Issues/day |

### 生态角色分析
- **OpenClaw**：**事实上的标准参考实现**，议题最多、矛盾最激烈，反映生态最核心的痛点（消息可靠性、会话状态、多 Agent 编排）
- **NanoBot**：**稳定性典范**，修复率高（59%），适合对可靠性敏感的部署场景
- **Zeroclaw**：**架构创新者**，Reborn 范式预示下一代框架方向，但当前仍在高风险迭代
- **CoPaw**：**功能完整性最强**，插件市场与自动化特性对标商业产品
- **IronClaw**：**企业级探索者**，多租户隔离、RBAC、持久化授权等特性针对 ToB 场景

---

## 4. 共同关注的技术方向

### 🔴 **跨项目重点：可靠性与完整性**
| 诉求 | 涉及项目 | 具体表现 | 优先级 |
|------|--------|--------|--------|
| **消息/任务无声丢失** | OpenClaw, NanoBot, CoPaw | 工具调用间文本泄露、子 Agent 结果遗漏、定时任务未触发 | **P0** |
| **会话状态管理** | OpenClaw, NanoBot, Zeroclaw, CoPaw | 历史跨会话污染、压缩时状态丢失、长会话超窗口 | **P0** |
| **系统提示词优化** | Zeroclaw, LobsterAI, CoPaw | 内存权重过高、导致忽视用户指令、Token 浪费 | **P1** |
| **多 Agent 编排** | OpenClaw, NanoClaw, CoPaw | 子 Agent 完成无通知、结果聚合防幻觉、协作总线 | **P1** |

### 🟠 **跨项目热点：功能扩展与用户体验**
| 需求 | 涉及项目 | 具体表现 | 影响用户群 |
|------|--------|--------|-----------|
| **多运行时/多 LLM 支持** | OpenClaw, NanoClaw, CoPaw | 跨平台 ClawdBot、掩码秘密、Codex/Claude/本地模型混编 | 企业/多策略部署 |
| **安全隔离与隔离** | Zeroclaw, NanoClaw, IronClaw, CoPaw | RBAC、Per-sender 权限、执行路径黑名单、凭证泄露检测 | 金融/多租户 |
| **工具链完善** | NanoBot, PicoClaw, LobsterAI, NanoClaw | 工具发现、自动化（uninstall.sh、一键卸载）、Web 搜索内置 | 开发者体验 |

### 🟡 **跨项目信号：向商业化转向**
| 信号 | 项目 | 表现 |
|------|------|------|
| **插件市场/生态化** | CoPaw、NanoClaw | AgentScope 平台集成、skills 自包含化、社区贡献规范 |
| **Enterprise 特性** | IronClaw、Zeroclaw | 多租户、审批流程持久化、可观测性加强（成本核算、trace） |
| **自动化与自演进** | CoPaw、OpenClaw | Hermes Agent 借鉴、make-skill 工作流、Agent 自创建技能 |

---

## 5. 差异化定位分析

### 功能侧重矩阵
```
                     企业/多租户 ◄──────────────► 个人/开发者
                            ▲
                            │
      复杂编排 ◄─────────────┼──────────────► 简洁易用
                            │
                            │
        IronClaw          Zeroclaw        OpenClaw
          │                   │              │
         (RBAC/SSO)     (多tenant/审批)  (通道多样化)
           │                   │              │
         CoPaw          NanoClaw           NanoBot
          │                   │              │
      (插件市场)        (多运时SDK)    (沙箱稳定)
           │                   │              │
        LobsterAI        PicoClaw       (目标明确)
           │                   │
      (定时任务)       (nightly稳定)
```

### 目标用户分群
| 项目 | 目标用户 | 典型场景 | 成熟度 |
|------|--------|--------|--------|
| **OpenClaw** | 智能体框架使用者 | 多频道 Bot 部署、复杂工作流编排 | Beta (功能完整，稳定性补齐中) |
| **NanoBot** | 稳定性优先者 | 金融/医疗生产环境、需 SLA 保障 | Stable (可用于生产) |
| **IronClaw** | 企业 IT 部门 | 多部门隔离、审计合规、托管部署 | Beta (Reborn 架构冲刺) |
| **CoPaw** | 个人开发者 + 中小团队 | 快速原型、自动化任务、云集成 | Beta (快速迭代中) |
| **NanoClaw** | AI 框架开发者 | 多运时抽象实验、通道扩展 | Alpha (架构探索中) |
| **LobsterAI** | 国内用户、本地部署 | 定时任务、数据备份、飞书集成 | Stable (功能完善) |
| **Zeroclaw** | 架构研究者 | Reborn 新范式探索、从零到一 | Alpha/Beta (高风险迭代) |

### 技术架构关键差异
| 维度 | OpenClaw | NanoBot | IronClaw | CoPaw |
|------|----------|---------|----------|--------|
| **会话存储** | 内存 + 数据库 | history.jsonl | Postgres + Redis | 本地/云存储混合 |
| **工具系统** | MCP + 原生工具 | 装饰器 + 沙箱 | MCP 2.0 | Agent OS Driver（规划中） |
| **认证体系** | 频道级 | 无 | 多租户 RBAC + SSO | Agent 级 Web Auth |
| **扩展机制** | 频道插件 | 工具/供应商 | OpenAI 兼容 API | 插件市场 + 技能库 |
| **运行时** | Node.js | Python | Rust/Tauri | Electron + Node.js |

---

## 6. 社区热度与成熟度分层

### 第一梯队：超高活跃，质量管理压力大
- **OpenClaw**：日均 500+ Issues/PRs，合并率 17% 意味着**积压 400+ 审核中的改动**
  - 状态：**功能完整但脆弱**，频繁暴露的 Bug（消息泄露、任务丢失）反映快速迭代的代价
  - 适配人群：框架集成者、愿意忍受边界 case 的开发者
  
- **NanoClaw**：日均 47 PR 合并率 89%
  - 状态：**高效交付**，PR 质量高、审查严格
  - 适配人群：追求代码质量的贡献者

### 第二梯队：高活跃，功能快速迭代
- **NanoBot, Zeroclaw, CoPaw, IronClaw**：日均 30-50 PRs，40-60% 合并率
  - 状态：**功能导向**，每 2-4 周发布新特性，但积压 PR 处于评审期长（2-8 周）
  - 适配人群：跟进最新功能的开发者，需要容忍短期 API 变化
  - 风险：#7428（跨平台 clippy 仅 Linux 生效）、#5052（工具调用失败）等积压 Bug

### 第三梯队：稳定成熟，迭代缓步
- **LobsterAI**：日均 20 PRs（95% 合并率），2-4 周发布周期
  - 状态：**功能完善期**，重点在稳定性和中文适配
  - 适配人群：国内用户、追求稳定的生产环境
  
- **PicoClaw**：日均 18 PRs，类型检查与 Windows 兼容性补齐中
  - 状态：**质量巩固阶段**，14 条待合并 PR 多为稳定性修复

### 第四梯队：低活跃或无活动
- **M

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报
**日期：2026-06-10**

---

## 1. 📊 今日速览

NanoBot 昨日保持高频迭代节奏，**24小时内处理32条PR和8条Issue**，其中19条PR已合并/关闭，6条Issue已解决，合并率达59%。项目聚焦于**会话历史管理、提供商兼容性、沙箱安全**等基础设施问题，同步推进**语音转录、网络搜索、计算机使用**等新能力，整体展现健康的高活跃状态，但待合并PR积压13条值得关注。

---

## 2. 📦 版本发布

**无新版本发布**。上一个发布版本为 0.2.0（用户反馈存在流超时问题，已在本轮迭代中修复）。

---

## 3. 🚀 项目进展

### 已合并/关闭的关键PR（19条）

| 类别 | PR | 说明 | 影响 |
|------|-----|------|------|
| **稳定性修复** | [#4272](https://github.com/HKUDS/nanobot/pull/4272) | 流超时重试与降级机制 | 直接修复 #4013 用户报告的"stream stalled"问题，实现重试+多模型降级 |
| **会话隔离** | [#4274](https://github.com/HKUDS/nanobot/pull/4274) | 按会话隔离历史注入 | 修复 #4259 跨会话上下文污染，避免history.jsonl混入无关历史 |
| **Web日志紧凑** | [#4255](https://github.com/HKUDS/nanobot/pull/4255) | 按需版本检查UI | 移除后台PyPI轮询，降低系统开销 |
| **执行工具增强** | [#4273](https://github.com/HKUDS/nanobot/pull/4273) | 新增pathPrepend配置 | 修复 #3934 exec无法通过pip装包问题，支持虚拟环境优先加载 |
| **沙箱修复** | [#4239](https://github.com/HKUDS/nanobot/pull/4239) | bwrap HOME变量设置 | 修复 #4237 沙箱内工具写入权限问题 |
| **配置验证** | [#4275](https://github.com/HKUDS/nanobot/pull/4275) | 配置文件快速失败 | 提前捕获无效配置，改善启动体验 |
| **空闲压缩** | [#4270](https://github.com/HKUDS/nanobot/pull/4270) | 完整会话历史存档 | 修复 #4264，确保用户最后纠正信息被纳入总结 |
| **Provider兼容** | [#4268](https://github.com/HKUDS/nanobot/pull/4268) | GPT-5使用max_completion_tokens | 修复 #4261 Azure GPT-5模型调用失败 |
| **工具补丁** | [#4266](https://github.com/HKUDS/nanobot/pull/4266) | apply_patch行分离 | 修复文件添加操作中的行尾处理问题 |
| **WebSocket修复** | [#4267](https://github.com/HKUDS/nanobot/pull/4267) | 流合并边界情况 | 修复WebUI助手回复丢失的流式处理bug |
| **新搜索供应商** | [#4182](https://github.com/HKUDS/nanobot/pull/4182) | Bocha搜索集成 | 为中文用户添加DeepSeek官方搜索API支持 |
| **新ASR供应商** | [#4260](https://github.com/HKUDS/nanobot/pull/4260) | StepFun语音转录 | 修复 #4000，为Step Plan用户开放语音能力 |
| **新搜索供应商** | [#4213](https://github.com/HKUDS/nanobot/pull/4213) | Exa搜索集成 | 增加高质量学术搜索选项 |
| **迭代预算** | [#4269](https://github.com/HKUDS/nanobot/pull/4269) | 无工具轮终止提示 | 当达到max_iterations时返回优化提示而非通用消息 |
| **飞书集成** | [#4277](https://github.com/HKUDS/nanobot/pull/4277) | 懒加载lark SDK | 优化Feishu channel启动性能 |

**量化成果**：
- 修复**8个重要Bug**（流超时、历史污染、权限问题、Provider不兼容）
- 集成**3个新搜索/ASR供应商**
- 改进**4个配置/基础设施**问题

---

## 4. 💬 社区热点

### 讨论最活跃的Issue

| Issue | 作者 | 评论数 | 状态 | 关键点 |
|-------|------|--------|------|--------|
| [#4013](https://github.com/HKUDS/nanobot/issues/4013) | @mxnbf | **4** | ✅ 已关闭 | **"stream stalled for 90s"超时** — 从0.1.5升级0.2.0后出现，影响实际工作，已通过 #4272 完全修复（重试+降级） |
| [#3934](https://github.com/HKUDS/nanobot/issues/3934) | @chinaliufei | **3** | ✅ 已关闭 | **exec工具pip装包失败** — 系统PATH优先级问题，#4273 添加pathPrepend配置解决 |
| [#4259](https://github.com/HKUDS/nanobot/issues/4259) | @chxuan | **2** | ✅ 已关闭 | **history.jsonl跨会话污染** — 深层次架构问题，#4274 通过session_key隔离修复 |

### 新开Issue信号

- [#4279](https://github.com/HKUDS/nanobot/issues/4279) **[enhancement] 子智能体结果聚合防幻觉** — 建议将实时汇报改为批量汇报，降低LLM幻觉风险，反映多agent场景下的可靠性诉求（**待处理**）
- [#4264](https://github.com/HKUDS/nanobot/issues/4264) **[bug] idleCompact应使用完整会话历史** — 已通过 #4270 修复

---

## 5. 🐛 Bug与稳定性

### 已修复Bug（按严重程度）

| 优先级 | Bug | PR | 描述 | 修复策略 |
|--------|-----|-----|------|----------|
| **🔴 Critical** | [#4013](https://github.com/HKUDS/nanobot/issues/4013) | [#4272](https://github.com/HKUDS/nanobot/pull/4272) | LLM流超时90秒中断 | 重试+多模型自动降级，提升可用性 |
| **🔴 Critical** | [#4259](https://github.com/HKUDS/nanobot/issues/4259) | [#4274](https://github.com/HKUDS/nanobot/pull/4274) | history.jsonl跨会话污染 | session_key标记隔离 |
| **🟠 High** | [#3934](https://github.com/HKUDS/nanobot/issues/3934) | [#4273](https://github.com/HKUDS/nanobot/pull/4273) | exec无法pip装包 | pathPrepend配置优先级 |
| **🟠 High** | [#4237](https://github.com/HKUDS/nanobot/issues/4237) | [#4239](https://github.com/HKUDS/nanobot/pull/4239) | bwrap沙箱HOME权限 | 显式设置HOME为workspace路径 |
| **🟡 Medium** | [#4261](https://github.com/HKUDS/nanobot/issues/4261) | [#4268](https://github.com/HKUDS/nanobot/pull/4268) | GPT-5.x max_tokens参数 | 模型名称检测，使用max_completion_tokens |
| **🟡 Medium** | [#4264](https://github.com/HKUDS/nanobot/issues/4264) | [#4270](https://github.com/HKUDS/nanobot/pull/4270) | idleCompact遗漏末尾纠正 | 完整历史存档 |

### 未修复Bug（待处理）

**无** — 所有报告的Bug都已获得合并/关闭的修复PR或已解决

---

## 6. 💡 功能请求与路线图信号

### 已进行的特性开发

| Feature | PR | 优先级 | 状态 | 预期用途 |
|---------|-----|--------|------|----------|
| **计算机使用工具** | [#4276](https://github.com/HKUDS/nanobot/pull/4276) | ⭐⭐⭐ | 🔄 待合并 | 像Claude一样支持桌面/浏览器自动化 |
| **记录自适应压缩** | [#4247](https://github.com/HKUDS/nanobot/pull/4247) | ⭐⭐ | 🔄 待合并 | WebUI超过8MB时自动分片，防止历史丢失 |
| **只读会话** | [#4271](https://github.com/HKUDS/nanobot/pull/4271) | ⭐⭐ | 🔄 待合并 | 支持欢迎页/公告固定在侧边栏无需LLM调用 |
| **段式记录存储** | [#4278](https://github.com/HKUDS/nanobot/pull/4278) | ⭐⭐ | 🔄 待合并 | 分片存储历史，加快WebUI大对话加载 |
| **文件系统访问策略** | [#4202](https://github.com/HKUDS/nanobot/pull/4202) | ⭐ | 🔄 待合并 | 明确读写权限边界，支持extra_read/write_allowed_dirs |

### 下一版本路线图信号

基于待合并PR和Issue，预期近期优先级：
1. **多智能体可靠性** — #4279 (子agent结果聚合)
2. **大规模对话支持** — #4247, #4278 (自适应压缩+分片)
3. **计算机自动化** — #4276 (desktop/browser使用)
4. **会话管理灵活性** — #4271 (只读会话)

---

## 7. 👥 用户反馈摘要

### 痛点与满意度

| 反馈类型 | Issue | 原文摘要 | 用户情绪 | 背景 |
|---------|-------|---------|---------|------|
| **升级回归** | [#4013](https://github.com/HKUDS/nanobot/issues/4013) | "0.1.5很好用，升级0.2.0后无法工作，流90s超时中断任务" | 😤 不满 | 生产环境升级失败 |
| **工具限制** | [#3934](https://github.com/HKUDS/nanobot/issues/3934) | "exec无法通过pip装第三方库，需要导入库来执行脚本" | 😐 中立 | Python开发工作流受限 |
| **架构问题** | [#4259](https://github.com/HKUDS/nanobot/issues/4259) | "多轮对话中用户纠正后，错误信息还被记录在history.jsonl" | 😤 不满 | 长对话中的学习记忆污染 |
| **新功能需求** | [#4279](https://github.com/HKUDS/nanobot/issues/4279) | "子agent实时汇报导致LLM幻觉，建议批量汇报" | 💭 建议 | 多agent协调场景优化 |
| **使用正反馈** | [#4013评论](https://github.com/HKUDS/nanobot/issues/4013) | "版本0.1.5很不错，太好用了" | 😊 满意 | 基础版本质量获认可 |

### 关键用户场景
- **长对话作业** — 需要稳定的流式处理、历史管理、纠错学习
- **Python脚本执行** — 需要第三方库支持（虚拟环境）
- **多轮交互修正** — 用户指正后需准确更新对话记录
- **多智能体编排** — 需要子agent可靠汇报机制

---

## 8. ⏳ 待处理积压

### 高优先级未处理项

| 类型 | Issue/PR | 创建时间 | 天数 | 状态 | 建议 |
|------|---------|---------|------|------|------|
| **Enhancement** | [#4279](https://github.com/HKUDS/nanobot/issues/4279) | 2026-06-10 | 0 天 | OPEN | 新需求，SubagentManager结果聚合防幻觉，**建议评估优先级** |
| **Bug** | [#4264](https://github.com/HKUDS/nanobot/issues/4264) | 2026-06-09 | 1 天 | OPEN | 修复已合并 #4270，**建议关闭** |

### 待合并PR风险评估

**积压13条PR，其中6条关键特性**：

|

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报
**日期:** 2026-06-10 | **报告周期:** 过去24小时

---

## 📊 今日速览

Zeroclaw 项目呈现**高强度开发状态**，过去24小时新增40个Issue（38条活跃/新开）、50个PR（47条待合并），展现出强劲的社区参与度和核心团队的活跃度。无新版本发布，但PR合并速度快（50条PR中多数处于评审期），表明项目正在密集迭代以解决积压的生产级Bug。项目关注点从功能新增转向**稳定性、安全性和配置一致性**的补缺。

---

## 🔄 项目进展

### 近期合并/活跃PR概览（20个最活跃PR）

**高优先级修复（风险等级High，优先级P1）：**

| PR | 主题 | 状态 | 影响范围 |
|---|---|---|---|
| [#7440](https://github.com/zeroclaw-labs/zeroclaw/pull/7440) | 跳过系统提示超预算时的徒劳历史修剪 | 评审中 | 运行时上下文管理 |
| [#7428](https://github.com/zeroclaw-labs/zeroclaw/pull/7428) | 在全平台运行clippy，修复Windows/macOS特定代码 | 评审中 | CI/工具链 |
| [#7419](https://github.com/zeroclaw-labs/zeroclaw/pull/7419) | Fallback提供商失败时大声报错 | 评审中 | 提供商配置安全性 |
| [#7450](https://github.com/zeroclaw-labs/zeroclaw/pull/7450) | 医生命令增强：列出配置的模型、--check标志 | 评审中 | 诊断工具改进 |

**运行时稳定性修复（XS-M体积）：**

- [#7451](https://github.com/zeroclaw-labs/zeroclaw/pull/7451) - PostgreSQL内存schema版本类型修复（i32绑定）
- [#7449](https://github.com/zeroclaw-labs/zeroclaw/pull/7449) - Web控制台：修剪空白内容防止空行
- [#7447](https://github.com/zeroclaw-labs/zeroclaw/pull/7447) - OpenAI原生提供商：接入timeout_secs配置
- [#7438](https://github.com/zeroclaw-labs/zeroclaw/pull/7438) - Telegram频道：移除阻止工具使用的指令文本
- [#7437](https://github.com/zeroclaw-labs/zeroclaw/pull/7437) - WeChat频道：支持流式聊天响应

**高价值功能增强（风险High）：**

- [#7429](https://github.com/zeroclaw-labs/zeroclaw/pull/7429) - 添加wasmtime依赖，准备弃用Extism（L体积）
- [#7433](https://github.com/zeroclaw-labs/zeroclaw/pull/7433) - 提供商配置编辑后刷新活跃会话

**诊断与警告增强：**

- [#7427](https://github.com/zeroclaw-labs/zeroclaw/pull/7427) - context_aware_tools未实现时发出警告
- [#7426](https://github.com/zeroclaw-labs/zeroclaw/pull/7426) - rerank_enabled未实现时发出警告
- [#7441](https://github.com/zeroclaw-labs/zeroclaw/pull/7441) - 医生：验证自定义model_provider配置而非遗留工厂

**项目推进评价：** 今日PR集中在**Bug修复（13条）+ 质量增强（7条）**的组合，体现出项目从功能扩展阶段进入**稳定性收敛期**的演进。特别是#7428（跨平台clippy）和#7419（提供商安全）解决的是长期技术债。

---

## 🔥 社区热点

### 评论最活跃的Issue（评论数排序）

| Issue | 评论数 | 标签 | 核心诉求 |
|---|---|---|---|
| [#4710](https://github.com/zeroclaw-labs/zeroclaw/issues/4710) | **20** | enhancement, blocked | **品牌LOGO重新设计** —— 社区多次要求改进视觉识别 |
| [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) | **12** | bug, P2, 需重现 | **Agent不知道自己能用cron工具** —— 工具发现机制缺陷 |
| [#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) | **10** | enhancement, high风险 | **统一提供商架构与reqwest客户端** —— 代码重构需求 |
| [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) | **9** | enhancement, security | **多租户Agent部署的每发送者RBAC** —— 企业部署刚需 |
| [#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) | **7** | enhancement, Discord | **Discord频道限制回复范围** —— 配置灵活性需求 |

**热点分析：**
- **配置灵活性**是用户最关心的（#6378关于Discord的allowed_channels、#5982多租户隔离）
- **工具发现和能力申报**（#5862）反映Agent在复杂工具环境下的认知缺陷
- **企业级安全** (#5982 RBAC、#4853 .well-known URI技能安装) 是新兴诉求

---

## 🐛 Bug与稳定性

### 按严重程度分类

**S1级（工作流阻塞，优先级P1，7个）：**

| Issue | 标题 | 状态 | Fix PR | 诊断 |
|---|---|---|---|---|
| [#6721](https://github.com/zeroclaw-labs/zeroclaw/issues/6721) | tool_search不在default_auto_approve → 延迟加载+webhook无声挂120s后自动拒绝 | OPEN | ❌ | **MCP工具加载机制缺陷** —— 审批网关对tool_search应该例外 |
| [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) | 单轮/多轮对话丢失user message | OPEN | ❌ | **兼容提供商的消息处理bug** —— Qwen3.5返回400错误 |
| [#6646](https://github.com/zeroclaw-labs/zeroclaw/issues/6646) | web_search_tool和web_fetch在Telegram v0.7.5不触发 | OPEN | [#7438](https://github.com/zeroclaw-labs/zeroclaw/pull/7438) ✅ | **Telegram工具使用障碍** —— 已有修复PR合并中 |
| [#5844](https://github.com/zeroclaw-labs/zeroclaw/issues/5844) | 内存权重过高导致忽视当前提示 | OPEN | ❌ | **系统提示词工程问题** —— cron任务尤其受影响 |
| [#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808) | 默认32k上下文预算被系统提示+工具定义首轮超出3.3倍 | OPEN | [#7440](https://github.com/zeroclaw-labs/zeroclaw/pull/7440) ✅ | **上下文预算计算缺陷** —— 已有修复PR评审中 |
| [#6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037) | Cron任务可在运行中重复启动（20次突发） | OPEN | ❌ | **调度器并发问题** —— 无poll间隔保护 |
| [#6687](https://github.com/zeroclaw-labs/zeroclaw/issues/6687) | 两个独立SopEngine实例 —— MQTT启动运行对Agent不可见 | OPEN | ❌ | **MQTT与Agent间状态隔离** —— 架构缺陷 |

**S2级（功能降级，优先级P2，3个高风险）：**

- [#7409](https://github.com/zeroclaw-labs/zeroclaw/issues/7409) - Clippy检查仅Linux，Windows/macOS代码未被linted → [#7428 修复中](https://github.com/zeroclaw-labs/zeroclaw/pull/7428)
- [#6002](https://github.com/zeroclaw-labs/zeroclaw/issues/6002) - Telegram消息未明确指向助手（ambiguous addressing）
- [#6862](https://github.com/zeroclaw-labs/zeroclaw/issues/6862) - Gateway SPA降级服务/api/*为index.html → Web仪表盘JSON.parse崩溃

**修复覆盖率评估：**
- 已有修复PR的Bug：4/13（约31%）
- 积压未修复的严重Bug：9/13（69%）
  - 其中**需要架构调整**的：#6687 (SopEngine)、#6037 (调度器)、#5844 (系统提示词)

---

## ✨ 功能请求与路线图信号

### 新功能诉求热度排序

**企业/多租户需求（High风险，已评估）：**
1. [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) - **Per-sender RBAC** —— status:accepted，9评论 → 路线图中
2. [#6250](https://github.com/zeroclaw-labs/zeroclaw/issues/6250) - **提取require_auth至路由中间件** —— status:accepted，2评论 → 配置安全增强
3. [#6917](https://github.com/zeroclaw-labs/zeroclaw/issues/6917) - **Composio工具的动作范围过滤** —— status:accepted，3评论

**工具与集成增强（High风险）：**
4. [#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853) - **从.well-known URI安装技能** —— help wanted，status:accepted，5评论 → 标准化努力
5. [#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) - **统一提供商架构** —— status:accepted，10评论 → 重构项目
6. [#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) - **Discord allowed_channels** —— status:accepted，7评论 → 配置灵活性

**可观测性与运维（Medium-High风险）：**
7. [#7248](https://github.com/zeroclaw-labs/zeroclaw/issues/7248) - **持久化缓存token计入成本核算** —— status:accepted，1评论
8. [#6916](https://github.com/zeroclaw-labs/zeroclaw/issues/6916) - **Shell/Skill工具的进程内存限制** —— status:accepted，3评论

### 路线图信号
- **主力方向：** 安全性（RBAC、.well-known）→ 稳定性（上下文预算、工具发现）→ 可观测性（成本核算、仪表板）
- **下一版本可能包含：** 多租户RBAC、Discord灵活频道配置、统一提供商架构重构
- **望远镜需求：** 工具发现AI自学（#5862对标）、cron调度器重写（#6037）

---

## 👥 用户反馈摘要

### 真实使用场景与痛点

| 场景 | 痛点 | 来源Issue | 建议 |
|---|---|---|---|
| **企业多部门部署** | 需要为客户/运营员/开发者隔离工作空间、工具集、速率限制 | [#5982](https://github.com/zeroclaw-labs/zeroclaw/issues/5982) | RBAC已被标记accepted，应加速实现 |
| **本地LLM集成** | OpenAI兼容API超时（120s硬编码） → Qwen3.5通过LM Studio失败 | [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034), [#6002](https://github.com/zeroclaw-labs/zeroclaw/issues/6002) | [#7447已修复](https://github.com/zeroclaw-labs/zeroclaw/pull/7447)timeout_secs |
| **Cron自动化** | Agent不知道自己能用cron工具 → 需要显式告诉它 | [#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) | 工具发现需要知识库增强或上下文注入 |
| **Telegram社群支持** | web_search失效 → 需要显式工具调用指导 | [#6646](https://github.com/zeroclaw-labs/zeroclaw/issues/6646) | [#7438已修复](https://github.com/zeroclaw-labs/zeroclaw/pull/7438)，移除阻止性指令 |
| **Discord社区管理** | 需要限制Bot回复到特定频道（如#ai-chat） | [#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) | 与Matrix/Nextcloud Talk的allowed_rooms对齐 |
| **MacOS/Windows开发** | 本地开发CI/工具集不完整 → 跨平台clippy缺失 | [#7409](https://github.com/zeroclaw-labs/zeroclaw/issues/7409) | [#7428修复中](https://github.com/zeroclaw-labs/zeroclaw/pull/7428) |
| **内存管理困境** | 系统提示词权重过高 → 忽视用户当前指令（特别是cron） | [#5844](https://github.com/zeroclaw-labs

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报
**日期：2026-06-10** | **项目：[Sipeed PicoClaw](https://github.com/sipeed/picoclaw)**

---

## 📊 今日速览

PicoClaw 展现出**高度活跃的开发节奏**，24小时内新增6条 Issue 更新和18条 PR 活动，其中14条 PR 待合并。核心亮点为质量改进阶段：大量 PR 聚焦于代码健壮性（添加类型检查、错误处理），同时并行推进新功能（DeltaChat 网关、NEAR AI Cloud 集成、Agent 协作总线）。版本进入 nightly 构建周期（v0.2.9-nightly），表明项目在稳定化 0.2.9 发布前积极迭代。

---

## 🔖 版本发布

**nightly: v0.2.9-nightly.20260610.b9a8fad6**
- **性质**：自动化夜间构建，代码已集成至 `main` 分支
- **基线**：相对于 [v0.2.9](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **特性**：包含所有待合并 PR 中的修复与新功能（如 DeltaChat、NEAR AI、访问控制加固等）
- **风险等级**：⚠️ 官方标注「可能不稳定，谨慎使用」
- **迁移提示**：暂无破坏性 API 变更，但新协议支持（DeltaChat）需配置更新

---

## ✅ 项目进展

### 本周期已合并（4 条）
1. **#3064** - 配置迁移中的模型索引类型检查 [已合并] ✓
2. **#2942** - 修复默认 Claude Sonnet 模型 ID 格式（dotted → hyphenated）[已合并] ✓  
3. **#2940** - 为 claude-opus-4-7 移除 temperature 参数（模型不支持）[已合并] ✓
4. **#2937** - Agent 协作总线一阶设计实现 [已合并] ✓

### 待合并重要 PR（14 条）

**稳定性与容错性（8 条）**
- #3092, #3091, #3089, #3053, #3045, #3043 - 系统性补全类型断言的 `ok` 检查，修复 Windows 路径分隔符问题，预防 panic 和无声失败
- 评估：修复**隐性崩溃风险**，提升生产环保稳定性

**功能扩展（4 条）**
- #3083 - Web 启动器访问控制加固（可信代理配置、localhost 绕过开关）
- #3063 - DeltaChat 网关集成（新通道支持）
- #3087 - 允许工作区相对路径执行（修复误报阻止）
- #2917 - NEAR AI Cloud 提供商集成（OpenAI 兼容）

**历史功能修复（2 条）**
- #2990 - 历史会话完整消息加载（解决 #2796 消息丢失）
- #2988, #2987, #2983 - 上下文压缩、工具调用过滤、LLM 空响应重试

---

## 🔥 社区热点

### 最活跃讨论（按参与度）
| Issue/PR | 类型 | 评论 | 反应 | 关键信息 |
|---------|------|------|------|---------|
| [#2796](https://github.com/sipeed/picoclaw/issues/2796) | BUG (已关闭) | 6 | 0 | **多消息对话只显示最后一条** — 消息压缩逻辑误作用于 UI 层；已有 PR#2990 修复 |
| [#2939](https://github.com/sipeed/picoclaw/issues/2939) | BUG (已关闭) | 2 | 0 | **claude-opus-4-7 temperature 参数被拒** — API 行为变更；PR#2940 已合并 |
| [#3090](https://github.com/sipeed/picoclaw/issues/3090) | BUG (新增) | 0 | 0 | **iOS < 16.4 Safari 面板不兼容** — Web 功能降级，需调查 |
| [#2984](https://github.com/sipeed/picoclaw/issues/2984) | FEATURE (新增) | 1 | 1 | **WebSocket 转向完成信号缺失** — Protocol 级特性请求，外部客户端需要显式完成通知 |
| [#3088](https://github.com/sipeed/picoclaw/issues/3088) | FEATURE (新增) | 0 | 0 | **用 vodozemac 替代 libolm** — 加密库维护性问题，建议可选编译时选择 |

### 核心诉求分析
- **数据完整性**：用户发现历史会话丢消息（#2796），暴露压缩逻辑与展示层边界不清
- **API 兼容性**：Anthropic 新模型行为变更导致接入中断，需动态适配（已修复）
- **平台扩展**：社区推动 DeltaChat、NEAR AI、WebSocket 协议完善，需求清晰
- **安全负债**：加密库依赖老旧且无人维护（libolm），社区积极要求升级

---

## 🐛 Bug 与稳定性

### 严重度排序

| 编号 | Bug 描述 | 状态 | Fix PR | 影响范围 | 修复 ETA |
|------|---------|------|--------|---------|---------|
| **#2796** | 会话历史多消息显示不全 | ✅ 已关闭 | #2990 | 所有用户（UI）| 合并待检验 |
| **#2939** | claude-opus-4-7 API 调用失败 | ✅ 已关闭 | #2940 | 仅 opus-4-7 用户 | ✅ 已修复 |
| **#2472** | Windows 文件系统工具崩溃 | ✅ 已关闭 | #3089 | Windows 用户 | 待合并 |
| **#3090** | iOS Safari < 16.4 面板不可用 | 🔴 新增开放 | — | 低版本 iOS 用户 | **无 fix 分配** |
| **隐性 panic** | 类型断言 ok 检查缺失（6 处） | 🟡 未报告 | #3092, #3091, #3053, #3045, #3043 | 边界输入 | 待合并 |

### 稳定性评估
- **已修复系统性风险**：6 条 PR 补全类型检查，消除无声失败与 panic 隐患
- **遗留问题**：#3090 iOS 兼容性新发现，无人接手（可能需新 PR）
- **推荐优先级**：先合并 #3089、#3092、#3091 加固基础层，再发布 0.2.9 正式版

---

## 💡 功能请求与路线图信号

### 用户提出的新功能（2 条可能纳入）

| 特性 | Issue | PR状态 | 优先级 | 说明 |
|------|-------|--------|--------|------|
| **WebSocket 转向信号** | #2984 | 仅 Issue | 中 | 外部客户端需明确知道 Agent 何时完成处理，当前依赖启发式判断；**Protocol 功能需求** |
| **加密库现代化** | #3088 | 仅 Issue | 中 | libolm 无人维护，vodozemac 官方推荐替代；**安全债务** |

### 已在开发的新功能（3 条高概率入 0.2.9）

| 功能 | PR | 贡献者 | 难度 | 预期影响 |
|------|-------|--------|------|---------|
| **DeltaChat 网关** | #3063 | @trufae | 中 | 新通道支持，扩大接入生态 |
| **NEAR AI Cloud 提供商** | #2917 | @PierreLeGuen | 中 | OpenAI 兼容集成，云服务商扩展 |
| **Agent 协作总线** | #2937 | @afjcjsbx | 高 | 多 Agent 间通信基础设施（已合并）|

### 路线图信号
- **通道多样化**：Matrix、DeltaChat、WebSocket 等多协议客户端需求明确
- **LLM 生态链**：Anthropic、OpenAI、NEAR AI 等多厂商适配持续推进
- **企业级特性**：访问控制加固（#3083）、Agent 协作通信（#2937）指向分布式部署场景

---

## 👥 用户反馈摘要

### 真实痛点

**1. 数据展示准确性** (Issue #2796)
- **场景**：多轮对话后查看历史
- **痛点**：消息丢失，只能看最后一条用户输入，前面的都消失
- **根因**：压缩逻辑（用于减少 LLM token 消耗）误作用于 UI 层展示
- **启示**：内部优化不应对外部视图产生副作用

**2. API 兼容性破裂** (Issue #2939)
- **场景**：Anthropic claude-opus-4-7 调用
- **痛点**：突然 HTTP 400 "temperature is deprecated"，集成中断
- **根因**：模型能力变更，API 参数要求变更但客户端未适配
- **启示**：需要 LLM 供应商 API 变更的快速响应机制

**3. 跨平台体验缺陷** (Issue #3090)
- **场景**：iOS Safari 访问面板
- **痛点**：低版本 iOS（< 16.4）面板不可用
- **影响**：二线设备用户被排除
- **启示**：Web 兼容性测试覆盖不足

### 用户满意度信号
- ✅ 多功能集成度高（Matrix、DeltaChat、云服务）
- ✅ 快速迭代响应（API 变更 2 周内修复）
- ⚠️ 边界情况处理粗糙（消息丢失、类型错误无声失败）
- ⚠️ 平台适配不全（Windows 路径、iOS 版本）

---

## ⏳ 待处理积压

### 长期未响应的重要事项

| Issue | 创建时间 | 距今 | 状态 | 优先级 | 建议 |
|-------|---------|------|------|--------|------|
| [#2472](https://github.com/sipeed/picoclaw/issues/2472) | 2026-04-10 | 61 天 | 有 PR#3089 草稿 | 🔴 高 | **立即合并 #3089**，Windows 用户无法使用文件工具 |
| [#2984](https://github.com/sipeed/picoclaw/issues/2984) | 2026-06-02 | 8 天 | 仅 Issue | 🟡 中 | 需分配开发者设计 WebSocket Protocol 扩展 |
| [#3088](https://github.com/sipeed/picoclaw/issues/3088) | 2026-06-09 | 1 天 | 仅 Issue | 🟡 中 | 建议立项，加密库升级关乎安全，可拆分阶段执行 |
| [#3090](https://github.com/sipeed/picoclaw/issues/3090) | 2026-06-10 | 0 天 | 🆕 无 PR | 🟡 中 | 新鲜 Issue，无人认领，需内部评估 Web 兼容性策略 |

### 旧 PR 积压（2026-06-02 之前创建，仍待合并）
- **#2990, #2988, #2987, #2983** — 4 个功能修复 PR，已标注 [stale]，**建议一周内集中评审合并**
  - #2990 修复关键数据丢失（#2796 根因）
  - #2988 修复上下文计算错误
  - #2987 修复流式会话工具调用丢失
  - #2983 修复 LLM 空响应处理

---

## 📋 维护建议

1. **本周优先合并清单**（预计 5-7 工作日）
   ```
   批次1（稳定性）：#3089, #3092, #3091, #3053, #3045, #3043
   批次2（功能）：#2990, #2988, #2987, #2983
   批次3（扩展）：#3063, #3083, #3087, #2917
   ```

2. **待分配工作**
   - #3090 iOS 兼容性根因分析
   - #2984 WebSocket 协议设计讨论
   - #3088 vodozemac 迁移规划

3. **发布准备**
   - 合并上述 PR 后建议发布 v0.2.9 正式版
   - 更新 CHANGELOG 突出：Windows 支持修复、消息完整性修复、新协议支持

---

**报告生成时间**：2026-06-10 | **数据源**：GitHub API  
**下次更新**：2026-06-11 | **报告 URL**：[完整链接](https://github.com/sipeed/picoclaw)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 | 2026-06-10

## 📊 今日速览

NanoClaw 项目今日保持**高速迭代状态**，24小时内合并/关闭 PR 42 条，待合并 5 条，活跃度评估为**优秀**。虽未发布新版本，但多项核心功能（guardrails、web-search-plus、uninstall.sh）已进入审核阶段，代表项目向多运行时抽象、安全隔离、工具链完善等方向稳步推进。单日新增 Issue 仅 1 条（多运行时 SDK 抽象的架构讨论），表明社区聚焦度较高，核心诉求集中。

---

## 🚀 项目进展

### 本日已合并/关闭的关键 PR（42 条，精选重要者）

#### **安全与合规类**
- **#2722 [fix(telegram)] 使用 CSPRNG 实现配对码生成** | @dweekly
  - 将 `Math.random()` 替换为 `crypto.randomInt`，修复配对码可预测性风险（直接关联账户首次配对者可升级为 owner）
  - 状态：待合并(OPEN)，安全修复优先级高

- **#3 [安全 IPC 与命名空间隔离]** | @gavrielc  
  - 实现 per-group IPC 命名空间（`/data/ipc/{groupFolder}/`），防止权限提升攻击
  - 基于文件系统源身份而非自报身份验证，已关闭（代表已合并到主分支）

#### **功能与工具链类**
- **#2726 [feat: /add-guardrails] 输入输出护栏** | @amit-shafnir  
  - per-agent-group 级别的确定性护栏（正则/关键词规则），支持 prompt injection 阻止、凭证泄露检测
  - 支持 block/flag 双模式、聊天告警、主机端隔离审计追踪，**故障时fail-close**
  - 状态：待合并(OPEN)，安全增强关键

- **#2725 [feat: web-search-plus] 多供应商网络搜索** | @robbyczgw-cla  
  - 轻量化搜索工具，无 MCP 依赖，包含多源搜索 + URL 提取，引擎源自 hermes-web-search-plus
  - 定位为容器内 utility skill，完全自包含
  - 状态：待合并(OPEN)

- **#2719 [feat: uninstall.sh] 单副本卸载器** | @amit-shafnir  
  - 支持交互式确认、dry-run、OneCLI agent 清理，规范化卸载流程
  - 状态：待合并(OPEN)，UX 完善

#### **运维与稳定性类**
- **#2718 [fix(feishu): 清理僵尸 active_cards]** | @brookgao  
  - 修复生产问题：agent-runner 异常退出后卡片仍显示"运行中"50+ 分钟
  - 根因：`deleteActiveCard(jid)` 仅在 SDK `final` 事件内触发，已添加主动清理逻辑
  - 状态：已合并(CLOSED)

- **#2721 [docs: 定制化、技能模型、技能规范]** | @gavrielc  
  - 三份分层文档：`customizing.md`（入门）、技能模型、技能规范  
  - 建立 skills 自定制契约，解决升级时合并冲突问题
  - 状态：已合并(CLOSED)，文档完善

### 项目向前推进的关键指标
- **安全防线加强**：IPC 隔离、CSPRNG 配对码、guardrails 护栏形成三层纵深防御
- **工具链成熟**：web-search、uninstall 等运维工具补齐，降低使用门槛
- **文档体系化**：customizing.md 建立官方定制化指南，支持社区贡献 skills

---

## 💬 社区热点

### **高热讨论 Issue**
**#1690 [OPEN] 多运行时 Agent SDK 抽象** | @chiptoe-svg  
- **创建日期**：2026-04-07 | **最后更新**：2026-06-10  
- **热度**：6 条评论，3 👍
- **核心提案**：在 NanoClaw 之上构建多运行时抽象层，支持不同 Agent SDK（Claude + Codex + 本地模型）作为可插拔 skills，镜像现有通道模式（如 `/add-telegram`、`/add-slack`）
- **背景**：AgentRuntime 接口定义在主机级，应用调用 `runtime.run()`
- **社区信号**：反映用户希望 NanoClaw 成为**通用 Agent 编排平台**，而非 Claude-only 方案

**链接**：https://github.com/nanocoai/nanoclaw/issues/1690

---

## 🐛 Bug 与稳定性

### **已识别并处理的缺陷**

| 优先级 | Issue/PR | 描述 | 状态 | 修复 PR |
|-------|---------|------|------|--------|
| 🔴 **高** | #2718 | Feishu 交互卡片僵尸进程（生产严重故障） | ✅ 已合并 | #2718 |
| 🔴 **高** | #2722 | Telegram 配对码可预测性（安全漏洞） | ⏳ 待合并 | #2722 |
| 🟡 **中** | N/A | agent-runner 超时退出清理逻辑缺失 | ✅ 已修复 | #2718 |

### **未来稳定性重点**
- **IPC 权限提升风险**已通过 #3 的命名空间隔离修复
- **Feishu 生命周期管理**需继续监控（#2718 覆盖异常退出，正常路径如何）

---

## 🎯 功能请求与路线图信号

### **高优先级的新诉求**

1. **多运行时支持** (#1690)  
   - 用户需求：扩展 NanoClaw 支持 Codex、本地 LLM 等，形成通用智能体编排层
   - 路线图信号：**强烈**，3 个赞，已进入架构讨论阶段

2. **安全护栏体系** (#2726)  
   - 现状：prompt injection 阻止、凭证泄露检测已在 PR 审核
   - 预期集成版本：next release（待合并 5 条 PR 之一）

3. **Web 搜索能力** (#2725)  
   - 现状：无 MCP 的轻量搜索工具已就位
   - 竞争对手跟进：hermes-web-search-plus 引擎可用，降低依赖

4. **开发体验改善**  
   - #2719 (uninstall.sh)、#1161 (/setup-dev) 等工具链完善
   - 信号：社区共识是**skills 自包含化、开发者友好化**

---

## 👥 用户反馈摘要

### **真实用户痛点**（从 #1690 评论推断）

1. **跨模型编排需求**  
   - 痛点：现有 Claude-only 方案无法满足多 LLM 策略（Codex 做代码、Claude 做推理）
   - 期望：AgentRuntime 抽象支持动态切换，skill 可声明偏好模型

2. **安全隔离要求**  
   - 痛点：生产环境中多租户 agent-group 间存在 IPC 泄露风险（已修复 #3）
   - 期望：细粒度权限、审计追踪、凭证隔离

3. **工具链成熟度**  
   - 痛点：卸载、开发、搜索等运维工具分散或缺失
   - 期望：一体化工具链，如 `/setup-dev`、`uninstall.sh` 等

4. **文档与定制化**  
   - 痛点：升级时 merge conflict，难以维护私有 skills
   - 期望：官方定制化指南 (customizing.md) ✅ 已交付

### **满意度信号**
- #2721 (docs) 合并率高，表明**文档驱动**方向获社区认可
- #1690 多运行时讨论持续 2+ 月未冷，表明这是**长期核心诉求**

---

## ⏳ 待处理积压

### **长期未响应的关键 PR（需维护者关注）**

| 编号 | 标题 | 创建日期 | 天数 | 状态 | 优先级 |
|------|------|---------|------|------|--------|
| #212 | feat: WebUI control panel | 2026-02-13 | **117 天** | 阻塞(BLOCKED) | 🟡 中 |
| #214 | docs: 安全审计文档 | 2026-02-13 | **117 天** | 已关闭(CLOSED) | 🟢 低 |
| #337 | feat: 提示词追踪日志 | 2026-02-20 | **110 天** | 阻塞(BLOCKED) | 🟡 中 |
| #357 | feat: 外部 markdown seed 文件 | 2026-02-21 | **109 天** | 阻塞(BLOCKED) | 🟠 低 |
| #1084 | docs: 容器沙箱系统设计文档 | 2026-03-15 | **86 天** | 已关闭(CLOSED) | 🟢 低 |

### **阻塞原因分析**
- **#212 (WebUI)** 和 **#337 (提示词追踪)** 标记 `Status: Blocked` + `Status: Pending Closure`，表明维护者计划主动关闭，原因可能为：
  - 范围过大导致维护成本高
  - 社区需求调整
  - 优先级被 skills 模型重构挤压

**建议**：
1. 明确这些 PR 的最终状态（关闭/延期/重新规划）
2. 如保留，应在 2026-Q3 前给出里程碑承诺，否则清理积压
3. #1084 已关闭但未集成到主分支可见，建议补充相关文档链接

---

## 📈 数据汇总表

| 指标 | 今日数值 | 评估 |
|------|---------|------|
| Issues（24h）| +1 新增、6 评论（#1690） | ✅ 高质量讨论 |
| PRs（24h）| +47 条（5 待合并、42 已合并/关闭） | ✅ 非常活跃 |
| Releases（24h）| 0 个 | ⏳ 积累更新中 |
| 关键风险| Feishu 卡片僵尸、Telegram 配对码 | ✅ 已/即将修复 |
| 长期阻塞 PR | 3-4 条 | ⚠️ 需清理 |

---

**日报生成时间**：2026-06-10  
**数据来源**：GitHub NanoClaw Repository (github.com/qwibitai/nanoclaw)  
**下期关注**：多运行时 SDK 架构 RFC、guardrails 合并结果、长期 PR 清理进展

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报
**日期**: 2026-06-10

---

## 1. 📊 今日速览

IronClaw 项目今日呈现**高频迭代态势**，在 24 小时内处理了 50 条 Issue（新开/活跃 33 条，已关闭 17 条）和 50 条 PR（待合并 30 条，已合并/关闭 20 条），社区活跃度显著。虽无新版本发布，但 Reborn WebUI v2 的生产就绪冲刺进入关键阶段，大量本地测试反馈推动了 UI/UX 和稳定性的集中修复。项目整体向**从 Alpha 进阶到 Beta** 的方向加速迈进。

---

## 2. 📦 版本发布

**状态**: 无新版本发布

**阻滞因素** (Issue #3259):
- 已在 GitHub 标签发布至 v0.27.0（2026-04-29），但 crates.io 仅有 0.24.0（2026-03-31）
- 下游消费者通过 crates.io 被钉住在 0.24.0，无法获得最新功能与安全修复
- 根因与 wasmtime 28.x CVE 相关的依赖版本约束
- **建议**: 尽快发布 0.25.0-0.27.0 至 crates.io，解除下游阻滞

**进行中的发布准备** (PR #3708):
- 预计发布 ironclaw v0.29.1（相比 0.24.0 的大幅跨越）
- 包含多个组件的 API breaking changes（`ironclaw_common` 0.4.2→0.5.0）
- PR 状态: **OPEN**，需代码审查通过

---

## 3. 🚀 项目进展

### A. 已合并/关闭的关键 PR

| PR # | 标题 | 规模 | 影响范围 | 状态 |
|------|------|------|--------|------|
| #4681 | fix: Reborn WebUI operator LLM provider save returning service_unavailable (#4673) | L | 生产修复 | ✅ CLOSED |
| #4716 | [codex] Allow Reborn Postgres cleartext opt-in | L | 部署灵活性 | ✅ CLOSED |
| #4624 | Audit & test security headers + sanitized errors for WebChat v2 | M | 安全加固 | ✅ CLOSED |
| #4623 | Audit & test CSRF/origin/CORS + body/rate/connection limits for WebChat v2 | XS | 安全加固 | ✅ CLOSED |
| #4613 | Implement Reborn persistent approval policies | XL | 核心功能 | ✅ CLOSED |
| #4601 | [codex] Add Reborn effective config key route contract | L | 运维接口 | ✅ CLOSED |

**核心推进**:
- **安全与合规**: WebUI v2 的安全头、CSRF/CORS、速率限制全量审计完成，为生产部署奠定基础
- **认证与授权**: 持久化的 AlwaysAllow 审批策略已入库，支持用户跳过重复授权
- **运维友好性**: operator config 路由、Postgres TLS 灵活配置降低部署门槛

### B. 待合并的重点工作（30 条开放 PR）

**高优先级推进中**:
1. **#4712** - Move Slack setup into WebUI (XL) - 将 Slack 配置从 TOML 迁至 WebUI，简化用户体验
2. **#4715** - [codex] Unify GSuite Google credential reuse (XL) - 统一第一方 Google 认证，减少授权摩擦
3. **#4718** - fix(reborn): return terminal OpenAI response statuses (L) - 修复 OpenAI Responses 终止状态
4. **#4682** - feat(reborn): enforce production cutover gate (L) - 生产环境启动守护
5. **#4607** - [codex] Add Reborn first-run setup API behavior (L) - 首次启动 UX 优化
6. **#4608** - [codex] Add Reborn operator observability route shells (XL) - 运维可观测性

**项目节奏评估**: 平均 PR 规模 L~XL，表明**深度重构与新能力并行**，团队专注力集中在 Reborn 架构的 MVP 完成。

---

## 4. 🔥 社区热点

### 最活跃议题（评论数排序）

| Issue # | 标题 | 评论数 | 类型 | 状态 |
|---------|------|--------|------|------|
| #3259 | Publish 0.25.0–0.27.0 to crates.io | 14 | 发布阻滞 | 🔴 OPEN |
| #3283 | [Reborn] Migrate OpenAI-compatible chat and Responses APIs onto Reborn | 3 | 架构迁移 | ✅ CLOSED |
| #3615 | [Reborn WebUI Beta] Audit WebUI auth and security parity for Reborn routes | 1 | 安全审计 | ✅ CLOSED |
| #4604 | Reborn WebUI v2 lacks a browser-driven full-stack E2E | 1 | 测试缺口 | ✅ CLOSED |

### 今日新增热点问题（本地测试反馈洪峰）

自 2026-06-10 上午起，出现**一波集中的 WebUI v2 本地测试反馈**，均来自用户 @sunglow666 与 @think-in-universe：

| Issue # | 标题 | 影响 | 优先级 |
|---------|------|------|--------|
| #4692 | IronClaw Reborn Local Testing Findings | 综合追踪 | 🟠 P0 |
| #4724 | [Reborn] Unsent draft is lost when leaving New Conversation | UX | 🟡 P1 |
| #4725 | [Reborn] Composer remains interactive while in Working state | UX | 🟡 P1 |
| #4706 | [Reborn] Authorization flows do not recover after failed or cancelled sign-in | 功能 | 🔴 P2 |
| #4722 | [Reborn] Conversation messages do not display user or assistant identity | UX | 🟡 P1 |
| #4721 | [Reborn] Sidebar "PINNED" section represents the active conversation instead of pinned conversations | UX | 🟡 P1 |
| #4720 | [Reborn] Attachment warning persists across conversations and cannot be cleared | UX | 🟡 P1 |
| #4719 | [Reborn] Conversation content area flickers when returning to a chat | 性能 | 🟡 P1 |
| #4723 | [Reborn] New conversation composer hover state only highlights the top border | UX | 🟡 P1 |
| #4708 | Generated code blocks lack syntax highlighting in WebUI conversation page | 功能 | 🟡 P1 |
| #4697 | [Reborn] Active provider status is inconsistent in Inference settings | 运维 | 🟡 P1 |
| #4711 | [Reborn] ChatGPT subscription device code flow is confusing in Web UI | UX | 🟡 P1 |
| #4673 | [Reborn] NEAR AI provider configuration cannot be saved after successful Test connection | 功能 | 🔴 P2 |

**诊断**: 这批反馈表明 WebUI v2 **已具备可交互形态**，但尚在 UI 细节打磨与流程完整性阶段。大多数为非阻滞性 UX 问题，部分涉及关键路径（认证、配置保存）。

---

## 5. 🐛 Bug 与稳定性

### 按严重程度分类

#### 🔴 **关键路径 Bug**（已有修复）

| Bug # | 描述 | 根因 | Fix | 状态 |
|-------|------|------|-----|------|
| #4673 | NEAR AI provider configuration cannot be saved | `ResourceScope::system()` 与 reserved tenant ID 冲突 | #4681 ✅ | FIXED |
| #4642 | Strict-mode providers' null-for-unset-optionals rejected by capability-port validation | 工具调用参数验证对 null 值处理不当 | 未找到对应 PR | 🔴 OPEN |
| #4603 | Bind product adapter auth evidence to tenant scope | `VerifiedAuthClaim` 缺失 tenant identity | 设计追踪 #4585 | 进行中 |

#### 🟠 **高优先级 Bug**（影响用户体验）

| Bug # | 描述 | 影响范围 |
|-------|------|---------|
| #4706 | Authorization flows do not recover after failed/cancelled sign-in | SSO/OAuth 用户卡住，需要刷新或重启 |
| #4724 | Unsent draft lost when leaving New Conversation | 用户输入丢失，挫折感高 |
| #4719 | Conversation content area flickers | 加载状态不明确 |
| #4673 | Provider configuration save failure | 首次配置阻滞 |

#### 🟡 **中等优先级 Bug**（UX 打磨）

- #4725: Composer 在 Working 状态仍显示交互状态（误导用户）
- #4720: Attachment warning 跨对话持久化（非核心功能，当前暂无附件支持）
- #4723: Composer hover 状态不完整（CSS 缺陷）
- #4722: 消息缺失用户/助手身份标识（信息架构）

#### 🟢 **低优先级 Bug**（功能缺失）

- #4708: Code blocks 无语法高亮（可读性问题）
- #4697: Provider 状态显示不一致（信息架构）
- #4711: ChatGPT device code flow 说明不清（文案优化）

---

## 6. 💡 功能请求与路线图信号

### 新增功能需求

| Issue # | 功能需求 | 提案者 | 链接 | 预期迭代 |
|---------|---------|--------|------|---------|
| #4674 | Gmail tool: archive/label-modify actions | @pranavraja99 | [#4674](https://github.com/nearai/ironclaw/issues/4674) | 工具扩展 |
| #4657 | Unify Google OAuth credentials across GSuite scopes | @serrrfirat | [#4657](https://github.com/nearai/ironclaw/issues/4657) | PR #4715 进行中 |
| #4632 | Build out Reborn WebUI v2 end-to-end smoke coverage | @italic-jinxin | [#4632](https://github.com/nearai/ironclaw/issues/4632) | 测试覆盖 |

### 路线图信号推断

基于已合并与进行中的 PR：

1. **Reborn 架构完成度 (50%-60%)**
   - OpenAI 兼容 API 迁移: Chat Completions (#4444) ✅、Responses (#4445) 进行中
   - Auth/security parity 审计完成 (#3615 → #4623, #4624)
   - **下一阶段**: 流式响应、批处理 API、WebSocket 支持

2. **WebUI v2 生产就绪 (70%-80%)**
   - UI 交互框架: 大部分完成
   - 安全加固: ✅
   - 本地测试反馈整合: 进行中（#4692）
   - **下一阶段**: E2E 浏览器测试 (#4632)、性能优化、国际化

3. **认证与集成简化 (60%-70%)**
   - Google OAuth 统一: PR #4715
   - Slack 迁至 WebUI: PR #4712
   - **未来**: GitHub OAuth、SAML、更多内置工具

---

## 7. 👥 用户反馈摘要

### 核心使用场景痛点

#### **新用户首次启动体验**
- **问题**: 
  - 提供商配置保存失败（#4673 已修复）
  - "Test connection" 成功但 Save 无反馈
  - NEAR AI SSO 出现神秘错误（"Invalid frontend_callback"）
  
- **诉求**: 清晰的错误提示、分步引导、默认预配置

#### **对话体验完整性**
- **问题**:
  - 消息缺失发送者身份（用户头像/助手 logo）
  - Sidebar pinned 状态与预期不符
  - 草稿丢失（在新建对话离开后）
  
- **诉求**: 对话历史清晰可读、消息上下文完整、草稿自动保存

#### **认证流程可靠性**
- **问题**:
  - SSO 失败后无恢复路径（需重载）
  - ChatGPT device code 流程说明不清
  - OAuth 授权多次重复（跨工具）
  
- **诉求**: 优雅降级、单一认证、会话持久化

#### **工具功能深度**
- **问题**: Gmail 工具只能 read/trash，无 archive/label 操作（#4674）
- **诉求**: 扩展工具能力以覆盖更多实际工作流

### 用户满意度信号

- ✅ **正面**: 用户积极报告本地测试发现，反馈详细且可复现
- ⚠️ **中性**: 无明确的功能夸赞或社区扩展案例
- ❌ **负面**: UX 细节频频出现，表明用户期望值已上升至"生产级"

---

## 8. 📋 待处理积压

### 长期未解决的重要 Issue

| Issue # | 标题 | 创建日期 | 天数 | 状态 | 优先级 |
|---------|------|---------|------|------|--------|
| #3259 | Publish 0.25.0–0.27.0 to c

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报
**日期：2026-06-10** | **数据周期：过去24小时**

---

## 📊 今日速览

LobsterAI 今日保持**高度活跃的开发节奏**，共合并/关闭 20 条 PR，零新增 Issues，显示团队专注于迭代优化而非问题堆积。本日的关键亮点是**2026.6.8 版本的发布准备**，聚焦数据备份与迁移、本地登录回调、任务通知等三大功能。整体来看，项目处于**功能完善期**，代码质量管理严格，积压问题得到系统性处理。

---

## 🚀 版本发布

### **2026.6.8 Release 预发布**  
**PR #2140** | [查看详情](https://github.com/netease-youdao/LobsterAI/pull/2140)  
**作者:** @fisherdaddy | **状态:** CLOSED | **创建:** 2026-06-10

#### 核心更新
- **数据备份 & 迁移** — 支持用户备份项目配置与会话数据，迁移到新设备或备份恢复
- **本地登录回调** — 改进 OpenClaw 登录流程，支持本地回调机制
- **任务完成通知** — 定时任务执行完成后提供系统通知（已支持本地、飞书等多渠道）

#### 规模指标
- **+6,900 insertions / ~470 deletions**  
- **涉及 49 个文件**  
- 跨越 renderer、build、docs、main、openclaw、cowork、artifacts 等多个域

#### 破坏性变更
暂无明确标注的 breaking changes，本版本偏重功能增强与体验优化。

#### 迁移建议
- 如使用定时任务功能，建议升级后检查通知渠道配置
- 数据备份恢复时，项目会自动处理版本兼容性

---

## ✅ 项目进展

### 按功能域分类合并情况

#### **1. 任务通知系统（新功能）**
| PR | 功能 | 作者 | 状态 |
|-----|------|------|------|
| [#2134](https://github.com/netease-youdao/LobsterAI/pull/2134) | 任务完成通知恢复机制 | @liuzhq1986 | ✅ 合并 |
| [#1489](https://github.com/netease-youdao/LobsterAI/pull/1489) | 本地 macOS 通知渠道 | @BucleLiu | ✅ 合并 |
| [#1490](https://github.com/netease-youdao/LobsterAI/pull/1490) | 修复通知渠道编辑不同步 | @BucleLiu | ✅ 合并 |

**进展评价**：任务通知系统从零开始到多渠道支持（本地/飞书），打通了主窗口销毁后的通知恢复机制。这是**用户痛点的有效解决**——曾经关闭主窗口后任务执行无反馈。

#### **2. 定时任务增强**
| PR | 功能 | 作者 | 状态 |
|-----|------|------|------|
| [#1486](https://github.com/netease-youdao/LobsterAI/pull/1486) | 创建表单新增"Test Task"按钮 | @BucleLiu | ✅ 合并 |
| [#1507](https://github.com/netease-youdao/LobsterAI/pull/1507) | POPO AES Key 必填校验 | @kayo5994 | ✅ 合并 |

**进展评价**：缩短任务调试路径（from 保存→回列表→点运行 to 创建→测试），同时补齐配置校验。

#### **3. 技能系统修复（关键 Bug 修复）**
| PR | 问题 | 作者 | 状态 |
|-----|------|------|------|
| [#1485](https://github.com/netease-youdao/LobsterAI/pull/1485) | 禁用技能仍被调用 | @kayo5994 | ✅ 合并 |
| [#1501](https://github.com/netease-youdao/LobsterAI/pull/1501) | 禁用后 ID 残留 activeSkillIds | @MaoQianTu | ✅ 合并 |
| [#1505](https://github.com/netease-youdao/LobsterAI/pull/1505) | Agent 保存后技能列表未同步 | @MaoQianTu | ✅ 合并 |

**进展评价**：系统性修复了技能禁用流程的三个缺陷。这些修复**阻断了用户最不想看到的场景**——禁用的技能仍在起作用。

#### **4. Cowork 会话管理**
| PR | 功能 | 作者 | 状态 |
|-----|------|------|------|
| [#1499](https://github.com/netease-youdao/LobsterAI/pull/1499) | 会话自动裁剪（防止超上下文） | @linlihua | ✅ 合并 |
| [#2133](https://github.com/netease-youdao/LobsterAI/pull/2133) | 修复导出和代码复制 Bug | @fisherdaddy | ✅ 合并 |

**进展评价**：会话裁剪是**对标 OpenClaw 的关键能力补全**。使用 token 计数器替代固定字符数限制，避免长会话"输入过长"崩溃。

#### **5. UI 与编辑体验**
| PR | 功能 | 作者 | 状态 |
|-----|------|------|------|
| [#2139](https://github.com/netease-youdao/LobsterAI/pull/2139) | Markdown/代码块样式精修 | @fisherdaddy | ✅ 合并 |
| [#1503](https://github.com/netease-youdao/LobsterAI/pull/1503) | Agent 引导文件富文本编辑器 | @swuzjb | ✅ 合并 |

**进展评价**：从纯文本 textarea 升级到 Markdown 编辑器，大幅提升 Agent 配置的编辑体验。

#### **6. 平台特定功能**
| PR | 功能 | 作者 | 状态 |
|-----|------|------|------|
| [#1497](https://github.com/netease-youdao/LobsterAI/pull/1497) | Windows 关闭行为配置 | @Yang1k | ✅ 合并 |

**进展评价**：支持 Windows 用户自定义关闭按钮行为（最小化 vs 退出），体现对跨平台差异的关注。

#### **7. 数据备份与迁移**
| PR | 功能 | 作者 | 状态 |
|-----|------|------|------|
| [#2138](https://github.com/netease-youdao/LobsterAI/pull/2138) | 备份恢复时保留目标数据 | @fisherdaddy | ✅ 合并 |
| [#2137](https://github.com/netease-youdao/LobsterAI/pull/2137) | 排除词典和 OpenClaw 日志 | @fisherdaddy | ✅ 合并 |

**进展评价**：备份恢复流程细节优化，避免覆盖用户新增数据和日志。

#### **8. 依赖升级（自动化）**
| PR | 升级内容 | 作者 | 状态 |
|-----|----------|------|------|
| [#1277](https://open) | Electron 40.2.1 → 42.3.3 | @dependabot | ⏳ 待合并 |
| [#1491](https://github.com/netease-youdao/LobsterAI/pull/1491) | actions/upload-artifact 4→7 | @dependabot | ✅ 合并 |
| [#1492](https://github.com/netease-youdao/LobsterAI/pull/1492) | actions/setup-node 4→6 | @dependabot | ✅ 合并 |
| [#1493](https://github.com/netease-youdao/LobsterAI/pull/1493) | softprops/action-gh-release 1→2 | @dependabot | ✅ 合并 |

**进展评价**：CI/CD 工具链持续更新，但 Electron 大版本升级（#1277）仍在评审，需谨慎合并以避免兼容性问题。

---

### 📈 整体数学指标
- **今日合并率**：20/21 合并（95.2% 合并率）
- **平均 PR 生命周期**：从几天到 2 个月不等（依赖升级类 PR 周期长）
- **代码体量**：2026.6.8 版本贡献 ~6,900 行新增代码

---

## 🔥 社区热点

### **无新增 Issues，但已有 PR 反映的用户痛点**

由于过去 24 小时没有新开 Issues，热点来自**已合并 PR 反映的问题背景**：

#### **1. 最高优先级：长会话超出上下文窗口（#1499）**
**链接：** [#1499 Cowork 会话裁剪功能](https://github.com/netease-youdao/LobsterAI/pull/1499)  
**背景：** 用户长时间运行 Cowork 会话，对话积累到一定量级后触发"输入过长"错误，被迫删除整个会话并重新开始。  
**诉求：** 自动裁剪历史消息，保留有效上下文，防止不可恢复的崩溃。  
**解决方案：** 引入 token 计数估算（替代固定字符数限制），对标 OpenClaw 的 Session Pruning。

#### **2. 关键体验缺陷：禁用技能仍被调用（#1485, #1501, #1505）**
**链接：** [#1485](https://github.com/netease-youdao/LobsterAI/pull/1485) | [#1501](https://github.com/netease-youdao/LobsterAI/pull/1501) | [#1505](https://github.com/netease-youdao/LobsterAI/pull/1505)  
**用户反馈链:**
- 禁用技能后，ID 仍在 activeSkillIds 中
- Agent 设置保存后，当前会话技能列表不同步（需切换 Agent 才生效）  
- OpenClaw 对话中禁用技能仍被路由和调用

**分析：** 这是**典型的状态管理错误**，三个 PR 联合补缀了技能系统的全链路。反映出技能禁启逻辑在 renderer、cowork、system prompt 三个环节的不同步。

#### **3. 定时任务调试体验不佳（#1486）**
**链接：** [#1486 Test Task 按钮](https://github.com/netease-youdao/LobsterAI/pull/1486)  
**用户痛点：** 创建任务 → 保存 → 回到列表 → 点"立即运行"，路径过长。  
**改进：** 创建表单新增"Test Task"快捷按钮，支持在保存前测试指令。

#### **4. 后台通知缺失（#2134, #1489）**
**链接：** [#2134](https://github.com/netease-youdao/LobsterAI/pull/2134) | [#1489](https://github.com/netease-youdao/LobsterAI/pull/1489)  
**用户场景：** 关闭主窗口后，后台定时任务完成无提示；通知渠道配置无法生效。  
**解决：** 恢复通知处理器机制，支持本地/飞书多渠道。

---

## 🐛 Bug 与稳定性

### 今日修复的缺陷（按严重程度排列）

| 严重度 | Bug 描述 | PR | 根因 | 修复状态 |
|--------|---------|-------|------|---------|
| **🔴 Critical** | 禁用技能仍被调用，污染 Cowork 对话 | [#1485](https://github.com/netease-youdao/LobsterAI/pull/1485) | System prompt 未检查禁用状态 | ✅ 已修复 |
| **🔴 Critical** | 长会话超出模型上下文，不可恢复 | [#1499](https://github.com/netease-youdao/LobsterAI/pull/1499) | 字符数限制与实际 token 窗口脱节 | ✅ 已修复 |
| **🟠 High** | Agent 技能列表保存后当前会话不同步 | [#1505](https://github.com/netease-youdao/LobsterAI/pull/1505) | Redux dispatch 后未触发会话状态更新 | ✅ 已修复 |
| **🟠 High** | 定时任务通知渠道编辑不生效 | [#1490](https://github.com/netease-youdao/LobsterAI/pull/1490) | 详情页缓存未更新 | ✅ 已修复 |
| **🟠 High** | 关闭主窗口后任务完成通知丢失 | [#2134](https://github.com/netease-youdao/LobsterAI/pull/2134) | IPC 通知处理器销毁时序不当 | ✅ 已修复

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报
**日期：2026-06-10**

---

## 1. 📊 今日速览

Moltis 项目今日保持低度稳定活跃，新增 1 条 Bug 报告，暂无 PR 合并或版本发布。项目当前处于**平稳维护阶段**，未见紧急问题或重大进展。社区反馈零散，单个问题尚未引发讨论热潮，整体活跃度偏低。

---

## 2. 📦 版本发布

**无新版本发布**

---

## 3. ⚡ 项目进展

**无今日 PR 合并或关闭** — 项目未见代码推进，维护工作暂停或集中在其他时段进行。

---

## 4. 🔥 社区热点

**无显著热点讨论** — 今日仅有 1 条新 Issue，尚未引发社区讨论。建议关注后续评论动态。

---

## 5. 🐛 Bug 与稳定性

### 🔴 **[minor] Provider 'coqui' not configured**
- **Issue**: [#1114](https://github.com/moltis-org/moltis/issues/1114)
- **严重程度**: Minor（次要）
- **报告者**: @vvuk
- **状态**: 🟠 OPEN | 0 条评论 | 0 reactions
- **问题描述**: 用户在使用 Moltis 时遇到 Coqui TTS provider 未配置问题，Issue 描述不完整（缺少完整上下文）
- **修复状态**: ❌ 无相关 Fix PR

**稳定性评估**：当前报告量低，但该 provider 配置问题可能影响文本转语音功能可用性。建议优先补充 Issue 细节并分配处理。

---

## 6. 💡 功能请求与路线图信号

**无新功能请求** — 今日暂未见用户提出功能需求或路线图相关讨论。

---

## 7. 👥 用户反馈摘要

**Coqui Provider 配置问题** (#1114)
- **痛点**: 用户在初始化或使用 Coqui TTS provider 时配置出错
- **可能根因**: 
  - Provider 依赖未安装或路径配置错误
  - 文档不清晰导致用户配置不当
  - 系统首次检测未明确提示配置需求
- **使用场景**: TTS 文本转语音功能
- **用户满意度**: 🟡 中立（问题阶段，待解决）

---

## 8. ⏳ 待处理积压

**待追踪**：
- Issue #1114 需补充完整复现步骤与运行环境信息
- 建议维护者及时跟进，获取更多调试信息以加快问题定位

---

## 📈 **健康度指标**

| 指标 | 数值 | 趋势 |
|------|------|------|
| 日均新 Issue | 1 | ➡️ 平稳 |
| 日均 PR 活跃 | 0 | ⬇️ 低迷 |
| 平均响应时间 | — | 🕐 未知 |
| 开放问题数 | 1114+ | ⚠️ 需关注 |

---

**建议**: 项目维护节奏较缓，建议提升 Issue 响应速度，尤其是 Coqui provider 相关问题可能影响核心 TTS 功能。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目日报
**日期：2026-06-10**

---

## 📊 今日速览

CoPaw 今日活跃度高企，过去24小时共更新 **36 条 Issues**（新增/活跃 18 条，已关闭 18 条）与 **48 条 PRs**（待合并 19 条，已合并/关闭 29 条），同步发布 **v1.1.11-beta.3** 版本。项目处于**高速迭代周期**，Bug 修复与功能增强并行推进，社区反馈积极但暴露出的稳定性问题需要重点关注。总体评估：**活跃度 ⭐⭐⭐⭐⭐，稳定性 ⭐⭐⭐**。

---

## 🚀 版本发布

### **v1.1.11-beta.3** 
- **发布时间**：2026-06-10
- **关键更新**：
  - 🔧 CI 优化：移除冗余的 channel-tests 工作流（PR #5056）
  - ✨ **技能自进化**：增强 make-skill 工作流以支持自演进式技能创建（PR #4857）
  - 🔐 **安全性增强**：允许在文件守卫外预览文件（PR #5081）
  - 🎯 **性能优化**：解除事件循环阻塞、并行化启动流程，**冷启动时间从 5-8s 降至 ~3.5s**（PR #5074）
  - 💬 **DingTalk 增强**：支持内联图片预览和视频播放卡片（PR #5073）
  - 🐛 **错误信息改进**：在用户消息中直接显示原始 API 错误原因（PR #5079）

- **破坏性变更**：
  - ⚠️ **Runtime 架构重构**：引入 Runtime 2.0 模块化架构与 ToolCoordinator 层（PR #5078，首次贡献者），对现有集成可能产生兼容性影响，建议测试后升级

- **迁移建议**：
  - 若使用 MCP、A2A 或自定义工具集成，关注新的 Agent OS Driver 统一抽象层设计（PR #5067）
  - Desktop 用户：新增 Tauri 自动更新功能（PR #4669），可在 Console 头部查看

**发布链接**：[v1.1.11-beta.3](https://github.com/agentscope-ai/CoPaw/releases/tag/v1.1.11-beta.3)

---

## 📈 项目进展

### 今日已合并/关闭的关键 PR（29 条）

| PR | 标题 | 影响范围 | 贡献者 |
|----|----|---------|--------|
| #5080 | 发布 v1.1.11 | 版本管理 | @rayrayraykk |
| #5081 | 文件守卫外文件预览 | 安全性 | @zhijianma |
| #5079 | 表面原始 API 错误原因 | UX/稳定性 | @rayrayraykk |
| #5074 | 解除事件循环阻塞，加速启动 | 性能 | @rayrayraykk |
| #5077 | 简化控制台媒体消息处理 | 代码质量 | @zhijianma |
| #5076 | 回滚历史会话右侧面板特性 | 功能调整 | @zhijianma |
| #5073 | DingTalk 内联图片/视频卡片 | 频道功能 | @hongxicheng |
| #5023 | 插件市场 + AgentScope 平台集成 | 插件生态 | @Osier-Yi |
| #5082 | 锁定 aiohttp ≤3.14.0 修复 Windows 构建 SSL 错误 | CI/构建 | @rayrayraykk |

**项目进展亮点**：
- **性能突破**：启动时间优化 30-40%，解决 Desktop 应用卡顿问题
- **功能完善**：DingTalk 频道媒体支持升级、插件市场上线（与 AgentScope 平台联动）
- **稳定性修复**：错误消息可见性提升，Windows 构建 SSL 问题根治

**待合并重要 PR**（19 条）：
- PR #5067：Agent OS Driver 统一外部能力抽象（首次贡献，架构性）
- PR #5078：Runtime 2.0 重构（首次贡献，模块化，需严格审查）
- PR #4622：DataPaw 数据分析插件（12 个 BI 技能，首次贡献）
- PR #5051：Desktop 端口持久化，修复会话重启丢失问题
- PR #5036：会话文件名重复、跨代理调用故障修复

---

## 💬 社区热点

### 评论最活跃的 Issues（Top 5）

| Issue | 标题 | 评论数 | 热度指标 | 核心诉求 |
|-------|------|--------|---------|---------|
| [#4342](https://github.com/agentscope-ai/CoPaw/issues/4342) | 单元测试覆盖率（Phase 5：local_models/providers/tunnel/utils） | 11 | 🔴 已关闭 | 基础设施质量保障 |
| [#5017](https://github.com/agentscope-ai/CoPaw/issues/5017) | 学习 Hermes Agent 的"学习循环"特性，借鉴竞品优势 | 10 | 🟡 功能建议 | **代理自演进能力** |
| [#4727](https://github.com/agentscope-ai/CoPaw/issues/4727) | AgentScope 1.x → 2.0 后端迁移 | 8 | 🔵 进行中 | 架构升级（破坏性变更） |
| [#4878](https://github.com/agentscope-ai/CoPaw/issues/4878) | 微信频道推送失败（errcode=-3） | 7 | 🔴 已关闭 | 频道可靠性 |
| [#4666](https://github.com/agentscope-ai/CoPaw/issues/4666) | 新建会话后 Models 配置页丢失 | 7 | 🔴 已关闭 | UI/UX 数据持久化 |

### 🎯 热点分析

**Issue #5017** 最值得关注——用户建议关注竞品 Hermes Agent（GitHub Star 46k+）的"学习循环"设计，认为代理能从自身行为**自动创建并迭代技能**是核心创新。这反映出社区对 **Agent 自适应学习能力** 的期待，可能预示下一代代理框架的发展方向。

**Issue #4727** 反映技术债务：AgentScope 2.0 官方发布后，QwenPaw 需完整迁移新架构，涉及 API、运行时模型深度重构，属于战略性升级。

---

## 🐛 Bug 与稳定性

### 按严重程度排列的 Bug 报告

#### 🔴 **严重（功能完全不可用）**

| Bug | Issue | 版本 | 状态 | Fix PR |
|-----|-------|------|------|--------|
| **微信频道推送完全失败** | [#4878](https://github.com/agentscope-ai/CoPaw/issues/4878) | 1.1.10 | ✅ 已关闭 | 已修复（channel.py to_handle 逻辑） |
| **Agent 创建的定时任务无法触发** | [#5064](https://github.com/agentscope-ai/CoPaw/issues/5064) | 1.1.10 | 🔵 待分类 | ❌ 暂无 |
| **本地千问 3.6-27B 模型无响应** | [#4989](https://github.com/agentscope-ai/CoPaw/issues/4989) | 1.1.9/1.1.10 | 🟡 验证中 | ❌ 暂无（涉及 OpenAI 兼容性） |

#### 🟠 **高（影能会话/页面）**

| Bug | Issue | 版本 | 状态 | Fix PR |
|-----|-------|------|------|--------|
| **会话页面切换延迟 >10s** | [#5053](https://github.com/agentscope-ai/CoPaw/issues/5053) | 1.1.11-beta1 | 🟡 验证中 | 🔵 PR #5074（性能优化）已合并 |
| **Models 配置页面数据丢失** | [#4666](https://github.com/agentscope-ai/CoPaw/issues/4666) | 1.1.8+ | ✅ 已关闭 | 已修复 |
| **工具调用若干轮后失败（unexpected keyword 'arguments'）** | [#5052](https://github.com/agentscope-ai/CoPaw/issues/5052) | 1.1.10 | 🔵 开放 | ❌ 暂无（涉及 agentscope-runtime 兼容性） |

#### 🟡 **中（体验下降）**

| Bug | 问题 | 状态 |
|-----|------|------|
| **图片预览放大拖拽抖动** | [#4993](https://github.com/agentscope-ai/CoPaw/issues/4993) | ✅ 已关闭 |
| **Desktop 会话重启后代理配置丢失** | [#4733](https://github.com/agentscope-ai/CoPaw/issues/4733) | 🔵 PR #5051 进行中 |
| **MCP 服务进程泄漏（重启后累积）** | [#4834](https://github.com/agentscope-ai/CoPaw/issues/4834) | ✅ 已关闭（标记 invalid） |

### 🚨 风险评估

- **AgentScope 兼容性问题**：Issues #5052、#4989 涉及底层 runtime 版本不兼容，可能影响广泛用户群体
- **定时任务系统脆弱**：#4878、#5064 均指向调度任务推送/触发问题，需全链路审查
- **Desktop 端卡顿**：虽 PR #5074 有针对性优化，但 #5053 暴露的多会话切换延迟仍未完全消除

---

## 🎯 功能请求与路线图信号

### 高热度新功能需求

| 需求 | Issue | 关注度 | 推荐优先级 | 可能纳入版本 |
|------|-------|--------|----------|-----------|
| **代理自演进学习循环** | [#5017](https://github.com/agentscope-ai/CoPaw/issues/5017) | 🔥🔥🔥 | P0 | 2.0（战略性） |
| **独立视觉模型配置（Fallback）** | [#4992](https://github.com/agentscope-ai/CoPaw/issues/4992) | 🔥🔥 | P1 | 1.1.12+ |
| **Windows 系统托盘支持** | [#3751](https://github.com/agentscope-ai/CoPaw/issues/3751) | 🔥 | P2 | 1.2+ |
| **多外部技能路径配置** | [#4455](https://github.com/agentscope-ai/CoPaw/issues/4455) | 🔥 | P1 | 已合并（状态：CLOSED） |
| **技能分类与文件夹管理** | [#2961](https://github.com/agentscope-ai/CoPaw/issues/2961) | 🔥 | P2 | 路线图待定 |
| **DingTalk 私有部署自定义端点** | [#4887](https://github.com/agentscope-ai/CoPaw/issues/4887) | 🟡 | P2 | 1.1.12 |
| **细粒度文件守卫/工具守卫控制** | [#4356](https://github.com/agentscope-ai/CoPaw/issues/4356) | 🟡 | P2 | 研讨中 |
| **Agent 链路追踪初始化支持** | [#4057](https://github.com/agentscope-ai/CoPaw/issues/4057) | 🟡 | P2 | 待规划 |

### 已进行中的功能

- ✅ **Agent OS Driver**（PR #5067）：统一 MCP/A2A/ACP 外部能力抽象，架构优化
- ✅ **Runtime 2.0**（PR #5078）：模块化运行时、工具协调器，大幅增强可测试性
- ✅ **插件市场**（PR #5023）：AgentScope 平台集成，扩展生态
- ✅ **Tauri 自动更新**（PR #4669）：Desktop 端 OTA 升级
- ✅ **Agent 级别 Web 认证**（PR #4858）：多租户隔离

---

## 💭 用户反馈摘要

### 真实使用痛点提炼

#### 🎯 **性能与 UX**
- **页面卡顿**：Desktop 端多会话切换延迟超 10 秒（#5053），大量数据的对话页面重渲染低效（#4917）
- **长文件生成无反馈**：`write_file` 工具生成大代码文件时不流式渲染，看似卡死（#4865）
- **启动缓慢**：用户感受到应用响应迟滞，尤其 MCP 服务初始化（已优化）

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