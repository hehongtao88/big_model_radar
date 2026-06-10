# AI 开源趋势日报 2026-06-10

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-10 12:41 UTC

---

# 🤖 AI 开源生态日报 | 2026-06-10

---

## 📊 今日速览

**Agent 技能框架迎来爆发期**：Trending 榜单中超 50% 的项目围绕 AI Agent 能力扩展（skills/工作流），这表明开发者正在从单纯的"智能体调用"升级到"智能体技能生态"的建设。**视频生成、多源数据综合研究、知识库管理**成为新热点应用，而**向量数据库与 RAG 系统继续深度融合**。同时，**Claude Code、Cursor 等代码生成工具**的配套生态工具（提示词、内存管理、上下文工具）开始标准化，形成了独立的工具链。

---

## 🎯 各维度热门项目

### 🔧 AI 基础工具与框架

| 项目 | Stars | 今日涨幅 | 说明 |
|------|-------|--------|------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,473 | — | 🏆 全球最受欢迎的 NLP/多模态模型框架，支持 100+ 预训练模型的推理与训练 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 100,639 | — | 深度学习基础库，GPU 加速神经网络计算的业界标准 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,411 | — | 高吞吐量 LLM 推理引擎，支持批量推理与动态长度优化 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | 7,575 | — | 🆕 Rust 生态 LLM 应用构建框架，强调模块化与可扩展性 |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 72,050 | — | 统一微调框架，支持 100+ LLM 与 VLM 的高效参数调优（ACL 2024） |
| [ollama/ollama](https://github.com/ollama/ollama) | 173,757 | — | 🌟 开箱即用的本地 LLM 运行工具，支持 Qwen、DeepSeek、GLM 等主流模型 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 140,939 | — | 用户友好的 LLM WebUI，支持 Ollama、OpenAI API 等多后端 |

---

### 🤖 AI 智能体与工作流平台

| 项目 | Stars | 今日涨幅 | 说明 |
|------|-------|--------|------|
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 138,957 | — | 🏆 Agent 工程平台，LLM 应用编排的事实标准 |
| [langgenius/dify](https://github.com/langgenius/dify) | 144,701 | — | 生产级 Agent 工作流开发平台，可视化编排 + API 部署 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 184,874 | — | 自主 AI 代理框架，支持多步规划与工具调用 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 76,378 | — | AI 驱动开发助手，自动代码编写与调试 |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | 70,878 | — | 字节长链接 SuperAgent，支持沙盒、记忆、技能、子代理 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 34,542 | — | 前端 Agent 栈，React/Angular/Mobile 集成的 AG-UI 协议实现 |
| [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) | 53,451 | — | 🎨 可视化 AI Agent 编排工具，低代码构建复杂工作流 |

**🌟 Trending 新晋项目**：
- [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | **+781 today** | 生产级编码 Agent 能力集，谷歌工程师主导
- [phuryn/pm-skills](https://github.com/phuryn/pm-skills) | **+775 today** | PM 工作流技能市集，100+ 预制插件（发现→执行→增长）
- [obra/superpowers](https://github.com/obra/superpowers) | **+1011 today** | Agent 技能框架与 SD 方法论

---

### 🧠 大模型与训练

| 项目 | Stars | 今日涨幅 | 说明 |
|------|-------|--------|------|
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | 195,625 | — | 谷歌开源机器学习框架，模型定义与训练的基石 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 58,240 | — | YOLO 系列目标检测框架，计算机视觉的工业标准 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,077 | — | LLM 评估平台，支持 100+ 数据集的模型基准测试 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,265 | — | Apple Silicon LLM 推理课程，从零构建 vLLM + Qwen |
| [FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch) | 241 | **+241 today** | 从数据下载到文本生成的端到端 LLM 训练教程 |

---

### 🔍 RAG、向量数据库与知识管理

| 项目 | Stars | 今日涨幅 | 说明 |
|------|-------|--------|------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 82,386 | — | 🏆 RAG 引擎 + Agent 融合，领先的开源 RAG 系统 |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | 50,060 | — | 文档 Agent 与 OCR 平台，RAG 数据索引的标准库 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,716 | — | 大规模向量数据库，ANN 搜索的分布式引擎 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 32,001 | — | 高性能向量搜索引擎，生产级向量 DB 的 Rust 实现 |
| [meilisearch/meilisearch](https://github.com/meilisearch/meilisearch) | 58,041 | — | 🔥 闪电级搜索引擎，AI 混合搜索的新方向 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 17,756 | — | 🧠 AI 智能体持久化记忆平台，自托管知识图谱 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | 61,365 | — | 本地优先的 Agent 体验工具，完整向量 DB 与 RAG 栈 |
| [zilliztech/claude-context](https://github.com/zilliztech/claude-context) | 11,811 | — | Claude Code MCP，整个代码库作为 Agent 上下文 |

---

### 📦 应用与垂直场景

| 项目 | Stars | 今日涨幅 | 说明 |
|------|-------|--------|------|
| [ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai) | 27,022 | — | AI 驱动网页爬虫，LLM 解析 HTML 结构 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 98,071 | — | 🌐 网络自动化框架，为 AI Agent 赋予浏览器能力 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 130,950 | — | 大规模网页爬虫 API，结构化数据提取 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | — | **+1471 today** | 🎬 **新晋热点** AI 视频生成工具，一键生成高清短视频 |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | — | **+2561 today** | 🔥 **最热项目** 多源数据研究 Agent，综合 Reddit/X/YouTube/HN |
| [maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed) | — | **+535 today** | 🏥 开源医疗 AI，垂直行业模型 |
| [roboflow/supervision](https://github.com/roboflow/supervision) | — | **+699 today** | 👁️ 计算机视觉工具库，可复用 CV 组件 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 68,865 | — | 📊 金融数据平台，AI Agent 的量化工具 |

---

## 📈 趋势信号分析

**1. Agent 技能生态的模块化爆发**  
Trending 榜单中 50% 以上项目聚焦于 Agent skills/工作流扩展，从 `agent-skills`（+781）到 `pm-skills`（+775）到 `superpowers`（+1011），表明开发者正在从"调用模型"转向"构建技能市集"。这与 Claude Code、Cursor 等代码生成工具的普及直接相关——开发者需要标准化的方式将多个工具/API 组合成 Agent 可用的"超能力"。

**2. 多源数据研究与综合成为刚需**  
`last30days-skill`（+2561，今日热榜第一）同时爬取 Reddit/X/YouTube/HN/Polymarket/Web，体现了用户对 Agent 的新期待：**不是单点任务执行，而是跨域数据聚合与决策**。这类 Agent 与传统 RAG 的区别在于实时性与多源融合。

**3. 垂直应用快速具象化**  
医疗 AI（openmed +535）、视频生成（MoneyPrinterTurbo +1471）、PM 工作流（pm-skills +775）等具体应用登榜，表明 AI 已从通用 Agent 框架进入**行业垂直解决方案阶段**。与上周相比，纯框架项目涨幅下降，应用工具涨幅上升。

**4. 向量 DB + 记忆系统成为 Agent 基础设施**  
`cognee`（AI 记忆平台）、`claude-context`（代码库上下文）等项目强调**长期记忆与上下文持久化**，这是 Agent 超越单轮对话的必要条件。结合 RAGFlow、Llama Index 的高热度，形成了"RAG + 向量 DB + 智能体"的三角形基础架构。

**5. 本地化与隐私优先成为背景趋势**  
AnythingLLM、Ollama、Open WebUI 等一直高热，加上新晋 Agent 框架普遍支持本地部署，反映了企业与个人对**数据隐私 + 成本控制**的诉求。

---

## 🌟 社区关注热点

### 💎 **必关注项目**

1. **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** (+2561 today)  
   🎯 **为什么关注**：这是 Agent 应用的新范式——实时多源数据聚合。结合 Agent 决策能力，可构建"7天内容精选"、"行业动态监测"等生产应用。开发者可参考其架构实现类似的信息流 Agent。

2. **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** (+781 today)  
   🎯 **为什么关注**：Google 工程师 Addy Osmani 主导的生产级 Agent 技能框架，代表了大厂对 AI 编码助手的标准化思路。与 Claude Code 生态深度对齐。

3. **[langgenius/dify](https://github.com/langgenius/dify)** (144,701 ⭐)  
   🎯 **为什么关注**：可视化 Agent 工作流平台，今年最快速度登顶生产应用。无代码快速原型化的最佳选择。

4. **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** (82,386 ⭐)  
   🎯 **为什么关注**：整合了 RAG + Agent 的完整引擎。如果你要构建知识驱动的智能体（如客服机器人、研究助手），这是最成熟的开源选择。

5. **[browser-use/browser-use](https://github.com/browser-use/browser-use)** (98,071 ⭐)  
   🎯 **为什么关注**：为 Agent 提供网络操作能力的新标杆。电商自动化、网页爬取、RPA 场景下的首选库。

6. **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** (+1471 today)  
   🎯 **为什么关注**：AI 内容生成应用的爆款案例。展示了 LLM + 视频生成的商业可行性。

---

## 📅 下期预测

- **Agent 内存与持久化**将成为下周热点（cognee、mem0 等项目会继续活跃）
- **多模态 Agent**（视觉 + 文本）的工具链完善
- **Claude Code 生态工具**继续围绕"提示词工程"与"上下文优化"迭代

---

**数据来源**：GitHub Trending (2026-06-10) + GitHub Search API (topic 标签，7天活跃)  
**下次更新**：2026-06-11

---
*本日报由 [Big Model Radar](https://github.com/hehongtao88/big_model_radar) 自动生成。*