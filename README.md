# 📱 Agentic FAQ Bot 

An intelligent, agentic FAQ assistant for Lauki Phones built with **LangGraph**, **RAG**, and **Groq**. This assistant doesn't just search for text; it reasons through user queries to provide accurate, synthesized answers from a specialized telecom knowledge base.

## 🚀 Overview

This project implements a sophisticated **Retrieval-Augmented Generation (RAG)** pipeline. Unlike static search engines, this assistant uses an **Agentic workflow** to:
1. **Analyze** the user's intent.
2. **Search** a vector database (FAISS) for relevant context.
3. **Reformulate** queries if initial results are too broad or narrow.
4. **Synthesize** a final, helpful response for the customer.

## 🛠️ Technology Stack

- **Framework**: [LangGraph](https://github.com/langchain-ai/langgraph) / [LangChain](https://github.com/langchain-ai/langchain)
- **LLM**: [Groq](https://groq.com/) (GPT-4 class performance with ultra-low latency)
- **Embeddings**: `sentence-transformers/all-MiniLM-L6-v2` (via HuggingFace)
- **Vector Store**: [FAISS](https://github.com/facebookresearch/faiss)
- **Package Manager**: [uv](https://github.com/astral-sh/uv)
- **Environment**: Python 3.13+

## 📂 Project Structure

- `00_langgraph_agent.py`: Core logic for the LangGraph agent and RAG tools.
- `lauki_qna.csv`: The knowledge base containing 75+ telecom-specific Q&A pairs.
- `.env`: (Local only) API keys and configuration.
- `pyproject.toml`: Project dependencies and metadata.

## ⚙️ Setup Instructions

### 1. Prerequisites
Ensure you have `uv` installed:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Install Dependencies
```bash
uv venv
source .venv/bin/activate
uv sync
```

### 3. Environment Variables
Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_groq_api_key
# Optional: For tracing
LANGSMITH_TRACING=true
LANGSMITH_API_KEY=your_langsmith_api_key
```

### 4. Run the Agent
```bash
uv run python 00_langgraph_agent.py
```

## 🧠 How it Works

The agent uses a multi-tool strategy:
- `search_faq`: General semantic search across the FAQ database.
- `search_detailed_faq`: High-recall search for complex queries.
- `reformulate_query`: Intelligent query expansion to target specific "aspects" (e.g., troubleshooting, pricing).

## 📄 License
This project is for educational purposes as part of the Agentcore Crash Course.
