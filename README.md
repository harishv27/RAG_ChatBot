# RAG System

AI-powered Q&A assistant built on Nemi Wealth's internal knowledge base using Retrieval-Augmented Generation (RAG).

---

## What This Does

Ask plain-English financial questions about mutual funds, tax planning, insurance, retirement, or debt management and get accurate answers grounded strictly in the KB. Answers never go beyond the knowledge base. Every investment answer includes the SEBI/AMFI compliance disclaimer automatically.

---

## System Architecture

```
KB_TEXT (plain text, 8 knowledge domains)
        |
        v
RecursiveCharacterTextSplitter
  chunk_size = 400, overlap = 80
  splits on KB section boundaries first
        |
        v
OpenAI text-embedding-3-small
  1536-dimensional vectors
  cost ~ $0.0005 for the full KB
        |
        v
FAISS Vector Store (saved locally)
        |
        |   user query comes in
        v
Similarity Search — top 4 chunks retrieved
        |
        v
Nemi Wealth System Prompt
  + retrieved context chunks
  + user question
        |
        v
GPT-4o-mini
  temperature = 0.2, max_tokens = 600
        |
        v
Answer + SEBI compliance disclaimer
```

---

## Knowledge Base

| Section | Topics |
|---|---|
| KB-1 | Mutual Funds, Stocks, ETFs, FDs, Real Estate, Gold, Crypto |
| KB-2 | Goal Planning, Retirement, Child Planning, Women's Finance |
| KB-3 | 80C/80D Tax Saving, Capital Gains, Tax Harvesting, Regimes |
| KB-4 | Loan Types, Debt Payoff Strategies, EMI Rules, Credit Score |
| KB-5 | Term Insurance, Health Insurance, Life Stage Needs |
| KB-6 | Risk Profiles, Investor Biases, Financial Habits |
| KB-7 | Market Benchmarks, India Macro 2026, Inflation & Rates |
| KB-8 | Nemi Wealth Services, ARN, Business Model, Disclaimers |

---

## Tech Stack

| Component | Tool |
|---|---|
| LLM | OpenAI GPT-4o-mini |
| Embeddings | OpenAI text-embedding-3-small |
| Vector Store | FAISS (faiss-cpu) |
| Orchestration | LangChain 0.3.x |
| Notebook | Google Colab |

---

## Quick Start

**1. Clone the repo**
```bash
git clone https://github.com/harishv27/RAG_ChatBot.git
cd RAG_ChatBot
```

**2. Open notebook in Google Colab**

Upload `RAG_System_Nemi_Wealth.ipynb` at [colab.research.google.com](https://colab.research.google.com)

**3. Run Step 1 — install packages**

After it finishes: Runtime → Restart session

**4. Add your OpenAI API key**

In Colab left sidebar → key icon → Secrets → add `OPENAI_API_KEY`

**5. Run all remaining steps top to bottom**

---

## Notebook Steps

| Step | What it does |
|---|---|
| Step 1 | Install all packages with pinned versions |
| Step 2 | Verify package versions + import all libraries |
| Step 3 | Set OpenAI API key |
| Step 4 | Ping GPT-4o-mini and confirm model is live |
| Step 5 | Load the full Nemi Wealth KB |
| Step 6 | Chunk → Embed → Build FAISS vector store |
| Step 7 | Build GPT-4o-mini RetrievalQA chain |
| Step 8 | Test 1 — tax query with source chunks |
| Step 9 | Test 2 — insurance + planning query with sources |
| Step 10 | Interactive chatbot loop |

