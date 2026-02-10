# 📱 Agentic FAQ Bot 

An intelligent, agentic FAQ assistant for Lauki Phones built with **LangGraph**, **RAG**, **Groq**, and **Amazon Bedrock AgentCore**. This assistant reasons through user queries to provide accurate, synthesized answers and features **persistent conversation memory**.

## 🚀 Overview

This project implements a sophisticated **Retrieval-Augmented Generation (RAG)** pipeline with **Memory**. The assistant use an **Agentic workflow** to:
1. **Analyze** the user's intent.
2. **Retrieve** context from a vector database (FAISS).
3. **Persist** conversation history using **AgentCore Memory** and `langgraph-checkpoint-aws`.
4. **Reformulate** queries dynamically if initial results are insufficient.

## 🛠️ Technology Stack

- **Framework**: [LangGraph](https://github.com/langchain-ai/langgraph) / [LangChain](https://github.com/langchain-ai/langchain)
- **Deployment**: [Amazon Bedrock AgentCore](https://aws.amazon.com/bedrock/agentcore/)
- **Memory**: `langgraph-checkpoint-aws` (Backed by AgentCore Memory)
- **LLM**: [Groq](https://groq.com/) (Ultra-low latency inference)
- **Embeddings**: `sentence-transformers/all-MiniLM-L6-v2`
- **Vector Store**: [FAISS](https://github.com/facebookresearch/faiss)
- **Package Manager**: [uv](https://github.com/astral-sh/uv)

## 📂 Project Structure

- `agentcore_runtime.py`: Entrypoint for the standard AgentCore runtime.
- `agentcore_memory.py`: Advanced agent implementation with persistent memory support.
- `00_langgraph_agent.py`: Initial core logic for the LangGraph agent.
- `lauki_qna.csv`: The knowledge base containing 75+ telecom-specific Q&A pairs.
- `.bedrock_agentcore.yaml`: Configuration for Bedrock AgentCore deployment.
- `pyproject.toml`: Project dependencies and metadata.

## ⚙️ Setup Instructions

### 1. Prerequisites
Ensure you have `uv` and `aws-cli` installed and configured.

### 2. Install Dependencies
```bash
uv sync --python 3.12
```

### 3. Environment Variables
Ensure your `.env` contains:
```env
GROQ_API_KEY=your_groq_api_key
HUGGINGFACEHUB_API_TOKEN=your_hf_token
AWS_REGION=us-east-1
```

### 4. Deploy & Invoke via AgentCore
To run the agent with memory support:
```bash
# Launch the dev server
uv run agentcore dev --agent fq_memory

# Invoke the agent
uv run agentcore invoke '{"prompt": "Hello, my name is Ganesh"}' --dev --agent fq_memory
```

## 🧠 Memory Feature

The agent uses `AgentCoreMemorySaver` and `AgentCoreMemoryStore` from `langgraph-checkpoint-aws`. This allows the agent to:
- Remember user names and preferences across sessions.
- Maintain short-term conversation context.
- Retrieve long-term memories relevant to the current query.

## 📄 License
This project is for educational purposes as part of the Agentcore Crash Course.
