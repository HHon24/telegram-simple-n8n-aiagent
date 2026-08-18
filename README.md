# 🤖 Telegram Multimodal AI Agent Workflow (n8n + MongoDB + Gemini)
*Read this in other languages: [English](#english), [中文](#中文)*

---

<a name="english"></a>
## 🇬🇧 English

An automated, production-ready AI Agent workflow built with **n8n**, **Telegram Bot API**, **Google Gemini**, and **MongoDB Atlas**. This workflow handles multimodal inputs (text and document uploads), implements full Retrieval-Augmented Generation (RAG), maintains persistent session-based conversation memory, and executes dynamic tool calling.

### 📌 Architecture Overview
<img width="1572" height="952" alt="image" src="https://github.com/user-attachments/assets/6d54d6ea-012b-46fd-9c60-69b6b863060b" />
<img width="1012" height="497" alt="image" src="https://github.com/user-attachments/assets/c11719c2-c5b1-4d7b-9803-60b55e8be4f3" />
<img width="648" height="456" alt="image" src="https://github.com/user-attachments/assets/d3885157-dbdb-4d70-8c7b-5960262538e3" />

The workflow consists of two main execution branches:
* **Document Ingestion Branch (RAG Pipeline)**: Automatically detects uploaded files (PDF/Docs), parses and chunks text via Document Loaders, generates embeddings with Google Gemini, and indexes vectors into the knowledge base.
* **Conversational Agent Branch**: Receives text queries, tracks context via MongoDB session memory, dynamically executes tools (Weather, Currency, Calculator, Wikipedia), and queries the RAG vector store before replying to Telegram.

### ✨ Key Features

* **Multimodal Routing**: Automatically branches between document ingestion and conversational Q&A based on message payloads.
* **Persistent Session Memory**: Uses MongoDB Atlas Chat Memory with Telegram `chat.id` mapping to isolate and maintain conversation history across reboots.
* **Dynamic Tool Calling**:
  * **Custom Workflow Sub-nodes**: Real-time Weather & Currency exchange sub-workflows.
  * **Knowledge Retrieval**: Semantic search over uploaded documents using Gemini Embeddings.
  * **Utility Tools**: Built-in Calculator and Wikipedia search.
* **Resilience & Rate Limiting**: Built-in Error Handling workflows and retry logic for high-availability production runs.

### 🛠️ Tech Stack & Integrations

* **Orchestration**: [n8n](https://n8n.io/)
* **LLM & Embeddings**: Google Gemini Chat Model (`gemini-1.5-flash` / `pro`), Gemini Embeddings
* **Database & Memory**: MongoDB Atlas (Chat Memory & Vector Store)
* **Messaging Platform**: Telegram Bot API
* **External APIs**: OpenWeatherMap API, Exchange Rates API, Wikipedia API

### 🚀 Getting Started / How to Import

1. **Prerequisites**:
   * A running instance of n8n (Self-hosted or Cloud)
   * Telegram Bot Token (from [@BotFather](https://t.me/botfather))
   * Google Gemini API Key
   * MongoDB Atlas Cluster Connection String
2. **Import Workflow**:
   * Clone this repository or download `workflow.json`.
   * Open your n8n workspace, create a new workflow, and click **Import from File** (or drag & drop `workflow.json`).
3. **Configure Credentials**:
   * Set up **Telegram API**, **Google Gemini API**, and **MongoDB Account** credentials.
4. **Activate**:
   * Toggle the **Active** switch in the top right to start the bot.

---

<a name="中文"></a>
## 🇨🇳 中文

基于 **n8n**、**Telegram Bot API**、**Google Gemini** 与 **MongoDB Atlas** 构建的自动化生产级多模态 AI Agent 工作流。该系统支持文本与文档多模态输入分流、知识库检索增强生成（RAG）、基于 MongoDB 的持久化多轮会话记忆以及多工具自主调用。

### 📌 架构设计

<img width="1572" height="952" alt="image" src="https://github.com/user-attachments/assets/0d3aced6-41d4-4c9a-9785-92653babe329" />
<img width="1012" height="497" alt="image" src="https://github.com/user-attachments/assets/19188b22-d692-4b9a-bd08-4eb7c4ac5640" />
<img width="648" height="456" alt="image" src="https://github.com/user-attachments/assets/515f22ad-a352-4016-8f2b-c2aef3dcda82" />


整体流程分为两大执行分支：
* **文档入库分支 (RAG Pipeline)**：自动识别用户上传的文件（PDF/文本等），通过数据加载器分块切片，调用 Google Gemini 生成向量嵌入并存储至知识库。
* **智能 Agent 对话分支**：接收用户文本消息，通过 MongoDB 加载历史会话记忆，根据意图自主调用外部工具（天气、汇率、计算器、维基百科）及 RAG 知识检索，最终生成精准回复推送回 Telegram。

### ✨ 核心功能

* **多模态智能路由**：依据消息载荷类型，自动将文档上传与普通文本对话进行无缝分流。
* **持久化会话记忆**：集成 MongoDB Atlas Chat Memory，基于 Telegram `chat.id` 进行用户会话隔离与持久化存储，服务重启不丢上下文。
* **动态工具调用 (Tool Calling)**：
  * **自定义子工作流**：支持实时天气与汇率换算子流程调用。
  * **私域知识检索**：结合 Gemini Embeddings 实现文档语义检索。
  * **基础生产力工具**：内置高精度数学计算器与维基百科查询。
* **高可用与异常处理**：独立挂载全局 Error Handling 监控工作流与重试机制，确保生产环境稳定运行。

### 🛠️ 技术栈与依赖

* **工作流编排**：[n8n](https://n8n.io/)
* **大模型与向量**：Google Gemini Chat Model (`gemini-1.5-flash` / `pro`)、Gemini Embeddings
* **数据库与存储**：MongoDB Atlas (Chat Memory & Vector Store)
* **交互端**：Telegram Bot API
* **外部数据源**：OpenWeatherMap API、Exchange Rates API、Wikipedia API

### 🚀 快速开始与导入指南

1. **准备工作**：
   * 运行中的 n8n 实例（自建 Docker 或 Cloud 版）
   * Telegram Bot Token（通过 [@BotFather](https://t.me/botfather) 获取）
   * Google Gemini API Key
   * MongoDB Atlas 集群连接串（Connection String）
2. **导入工作流**：
   * 克隆本仓库或下载 `workflow.json`。
   * 打开 n8n，新建工作流并选择 **Import from File**（或直接拖拽 `workflow.json` 入画布）。
3. **配置凭据 (Credentials)**：
   * 在 n8n 中绑定 **Telegram API**、**Google Gemini API** 及 **MongoDB Account** 凭据。
4. **上线运行**：
   * 确认节点参数无误后，打开右上角 **Active** 开关即可全天候运行。

---

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
