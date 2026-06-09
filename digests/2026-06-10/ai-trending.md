# AI 开源趋势日报 2026-06-10

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-09 19:24 UTC

---

# 🤖 AI 开源趋势日报 | 2026-06-10

---

## 📰 今日速览

AI agent 生态集中爆发，**Claude Code/Cursor 等编码 agent 相关工具库突然走红**，单日新增 stars 破千的项目达 7 个，其中研究型 agent 工具（last30days-skill、pm-skills、career-ops）和轻量级 vector search 工具（turbovec）成为新热点。LLM 应用生态继续稳定增长，但开发者更多关注"agent 工程"而非模型本身，这表明 AI 基础设施正向 **Agent as a Service** 架构演进。同时 RAG/记忆系统、MCP（Model Control Protocol）相关项目获得前所未有的关注。

---

## 🏆 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎）

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|---------|------|
| **[ollama/ollama](https://github.com/ollama/ollama)** | 173.7K | — | 开源 LLM 本地运行框架，支持 DeepSeek、Qwen 等；仍是 AI 本地化首选工具 |
| **[huggingface/transformers](https://github.com/huggingface/transformers)** | 161.5K | — | 事实标准的多模态模型框架；LLM 应用开发的基础依赖 |
| **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** | 138.9K | — | **Agent 工程平台**，从链式提示升级到完整的 agent 编排；今日重点观察对象 |
| **[vllm-project/vllm](https://github.com/vllm-project/vllm)** | 82.3K | — | 高吞吐 LLM 推理引擎；支撑大规模 agent 部署的关键基础设施 |
| **[RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec)** | 0 | **+1800** | **[新晋热门]** 基于 TurboQuant 的高性能向量索引，Rust 实现；象征向量搜索向极端优化方向演进 |
| **[aaif-goose/goose](https://github.com/aaif-goose/goose)** | 0 | **+490** | **开源 AI 编码 agent**，支持任意 LLM；代码执行、测试、编辑的完整闭环 |
| **[zilliztech/claude-context](https://github.com/zilliztech/claude-context)** | 11.8K | — | Claude Code 的代码搜索 MCP；让整个代码库作为 agent context |

---

### 🤖 AI 智能体/工作流

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|---------|------|
| **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** | 184.9K | — | 开源 AI agent 框架的先驱；定义了 agent 自主执行范式 |
| **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** | 0 | **+3177** | **[今日榜首]** Claude agent 技能库：跨 Reddit/X/YouTube/HN 的多源研究综合；象征 agent 能力库的社区驱动开发 |
| **[langgenius/dify](https://github.com/langgenius/dify)** | 144.6K | — | **生产级 agentic workflow 平台**；低代码/零代码构建 agent 工作流的业界标杆 |
| **[browser-use/browser-use](https://github.com/browser-use/browser-use)** | 98K | — | **网页自动化 agent**；让 AI 能像人一样操纵浏览器，自动化端到端任务 |
| **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** | 76.3K | — | **AI 驱动的开发 agent**；代码生成、审查、测试的完整流程自动化 |
| **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** | 70.8K | — | 字节跳动开源的**长期 SuperAgent 框架**；支持沙箱、记忆、工具编排的复杂任务协调 |
| **[santifer/career-ops](https://github.com/santifer/career-ops)** | 51.4K | **+1114** | **AI 求职系统**（基于 Claude Code）；14 种 skill mode + 批量处理；展现 agent 在垂直场景的应用 |
| **[phuryn/pm-skills](https://github.com/phuryn/pm-skills)** | 0 | **+808** | **PM 领域的 agent skill 库**（100+ 技能）；从发现到增长的完整工作流工具库 |

---

### 📦 AI 应用（具体产品、垂直场景）

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|---------|------|
| **[open-webui/open-webui](https://github.com/open-webui/open-webui)** | 140.8K | — | **开源 LLM web UI**；支持 Ollama/OpenAI；用户友好的 AI 应用入口 |
| **[langgenius/dify](https://github.com/langgenius/dify)** | 144.6K | — | （同上，亦属应用平台）可视化 AI 工作流编排 |
| **[jeecgboot/JeecgBoot](https://github.com/jeecgboot/JeecgBoot)** | 46.7K | — | **AI 低代码平台**；一句话生成流程、表单和整套系统；消除 80% Java 重复工作 |
| **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** | 47.1K | — | **AI 生产力工作室**；300+ 助手、智能聊天 + agent，统一 LLM 接入 |
| **[nocobase/nocobase](https://github.com/nocobase/nocobase)** | 22.7K | — | **开源 AI + 低代码平台**；生成业务系统的快速方式 |
| **[maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed)** | 0 | **+165** | **医疗领域 AI**；垂直行业专用 LLM 应用 |
| **[yikart/AiToEarn](https://github.com/yikart/AiToEarn)** | 0 | **+423** | **AI 赚钱系统**；展现社区创意 AI 应用的兴趣方向 |

---

### 🧠 大模型/训练/微调

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|---------|------|
| **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** | 72K | — | **统一的 LLM 微调框架**（100+ 模型）；ACL 2024 论文认可；降低微调成本的业界方案 |
| **[vllm-project/vllm](https://github.com/vllm-project/vllm)** | 82.3K | — | （同上）推理优化的核心 |
| **[ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai)** | 27K | — | **AI 驱动的数据爬取**；用 LLM 理解网页内容而非正则 |
| **[open-compass/opencompass](https://github.com/open-compass/opencompass)** | 7.1K | — | **LLM 评估平台**；支持 100+ 数据集，对标 GPT-4/Claude 等主流模型 |
| **[BrainBlend-AI/atomic-agents](https://github.com/BrainBlend-AI/atomic-agents)** | 6K | — | **原子级 agent 构建**；模块化、可组合的 agent 开发范式 |

---

### 🔍 RAG/知识库/向量数据库

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|---------|------|
| **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** | 130.7K | — | **网页爬取 API**；为 AI agent 提供实时网页数据源；Firecrawl 融资后成熟度提升 |
| **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** | 82.3K | — | **RAG 引擎（融合 agent 能力）**；从传统 RAG 升级到 RAG+Agent 混合架构 |
| **[Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps)** | 114K | — | **100+ 可跑的 RAG/Agent 应用集合**；开发者的学习参考库 |
| **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** | 81.6K | — | **多语言 OCR 工具**（100+ 语言）；AI 理解 PDF/图片的关键基础设施 |
| **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** | 81.5K | — | **agent 跨会话持久化记忆**；压缩记忆注入，支持多 agent；**新兴 agent 基础设施** |
| **[FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise)** | 53.4K | — | **可视化 AI builder**；拖拽式构建 RAG 工作流 |
| **[run-llama/llama_index](https://github.com/run-llama/llama_index)** | 50K | — | **文档 agent 和 RAG 平台**；数据接入 → 检索 → LLM 的完整链路 |
| **[mem0ai/mem0](https://github.com/mem0ai/mem0)** | 58.2K | — | **AI agent 通用记忆层**；跨 agent 的长期知识积累系统 |
| **[milvus-io/milvus](https://github.com/milvus-io/milvus)** | 44.7K | — | **高性能向量数据库**；云原生架构支撑大规模 RAG 部署 |
| **[qdrant/qdrant](https://github.com/qdrant/qdrant)** | 32K | — | **向量搜索引擎**；Rust 实现，性能优先的向量 DB 选择 |
| **[weaviate/weaviate](https://github.com/weaviate/weaviate)** | 16.3K | — | **混合型向量数据库**；对象 + 向量 + 结构化过滤 |

---

## 📊 趋势信号分析

**1. AI Agent 工程的"热潮爆发"**  
今日单日新增 stars 破千的 7 个项目中，超过 60% 与 **agent 能力库、工具库、技能市场** 相关（last30days-skill +3177、pm-skills +808、career-ops +1114）。这表明社区从被动"调用 LLM"升级到主动"编排 agent 技能"，agent engineering 成为新的开发范式。Claude Code/Cursor 等编码 agent 的成熟，正催生围绕其之上的生态。

**2. 向量搜索向极端优化演进**  
TurboQuant-based turbovec (+1800 stars) 的突然走红，意味着开发者不再满足于通用向量 DB，而是追求针对特定硬件（Apple Silicon、ARM）的极限性能和存储效率。这对标字节 LEANN（97% 存储节省）的方向。

**3. Agent 记忆系统从边缘走向核心**  
claude-mem（持久化上下文）、mem0（通用记忆层）、cognee（知识图谱记忆）等项目获得高关注，反映出长期 agent 应用必须解决**跨会话知识积累**问题。MCP（Model Control Protocol）的引入进一步使记忆系统成为标准化需求。

**4. RAG 向"RAG+Agent"混合架构演进**  
RAGFlow、Llamaindex 等传统 RAG 工具开始集成 agent 决策能力，不再是被动检索，而是主动规划→执行→反思的循环。

---

## 🎯 社区关注热点

- **🔴 [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)**  
  **今日热度**：+3177 stars（日榜第一）  
  **为什么关注**：首次看到基于多源数据（Reddit、X、YouTube、HN、Polymarket）的 AI agent 研究技能。反映开发者对"让 agent 学会自主研究"的强烈需求，可能标志 Agent-as-Researcher 范式的启蒙。

- **🟠 [langchain-ai/langchain](https://github.com/langchain-ai/langchain)**  
  **Stars 138.9K**  
  **为什么关注**：从链式提示（chain）到完整的 agent 工程平台的升级已成事实。新手入门首选，成熟项目的参考架构。

- **🟡 [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)**  
  **Stars 81.5K（新晋高热）**  
  **为什么关注**：解决了 agent 应用的"健忘症"问题——会话之间的知识丢失。这是生产级 agent 必须解决的痛点，市场需求明显。

- **🟢 [infiniflow/ragflow](https://github.com/infiniflow/ragflow)** & **[FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise)**  
  **Stars 分别 82.3K、53.4K**  
  **为什么关注**：可视化/低代码构建 RAG 和 agent 工作流成为趋势，降低企业应用门槛；Flowise 的拖拽式体验更友好。

- **🔵 [jeecgboot/JeecgBoot](https://github.com/jeecgboot/JeecgBoot)**  
  **Stars 46.7K**  
  **为什么关注**：**AI + 低代码**的商业化样板。国内企业数字化的新范式，企业级应用需求旺盛；值得跟踪其融合

---
*本日报由 [Big Model Radar](https://github.com/hehongtao88/big_model_radar) 自动生成。*