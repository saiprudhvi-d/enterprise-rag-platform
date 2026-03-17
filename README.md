# Enterprise RAG Platform — Financial Document Intelligence

![Tests](https://github.com/saiprudhvi-d/enterprise-rag-platform/actions/workflows/test.yml/badge.svg)
![Python](https://img.shields.io/badge/Python-3.11-blue)

## Overview
An enterprise-grade RAG platform for financial document intelligence. Enables natural language querying across SEC filings, compliance manuals, and policy documents with hybrid retrieval, source citation, and LLM guardrails — built under strict latency (<3s), reliability, and compliance constraints.

## Business Problem
Financial analysts spend hours manually searching policy documents and regulatory filings. This platform reduces research time from hours to minutes by enabling accurate, grounded natural language Q&A — with built-in guardrails to prevent hallucinations and ensure regulatory compliance.

## Architecture
```
User Query → [ComplianceFilter] → [Hybrid Retrieval: BM25 + Vector] → [Cross-Encoder Reranking]
          → [Prompt Assembly] → [LLM Inference] → [HallucinationChecker] → Structured Response
```

## Tech Stack
- Python 3.11, LangChain, OpenAI / Azure OpenAI
- Pinecone / FAISS, rank-bm25 (hybrid retrieval)
- FastAPI, Docker, Kubernetes, AWS ECS
- pytest + GitHub Actions CI/CD

## Project Structure
```
enterprise-rag-platform/
├── .github/workflows/test.yml
├── app/app.py                    # FastAPI application
├── src/
│   ├── ingestion/                # PDF loading and chunking
│   ├── retrieval/                # Hybrid BM25 + vector + RRF fusion
│   ├── guardrails/               # Hallucination check + compliance filter
│   ├── prompts/                  # RAG prompt templates
│   └── llm/                     # LLM inference layer
├── docs/architecture.md
├── tests/
└── requirements.txt
```

## Setup
```bash
git clone https://github.com/saiprudhvi-d/enterprise-rag-platform
pip install -r requirements.txt
cp .env.example .env  # Add OPENAI_API_KEY and PINECONE_API_KEY
uvicorn app.app:app --reload
```

## Key Features
- **Hybrid retrieval**: BM25 + vector search fused via Reciprocal Rank Fusion (RRF)
- **Compliance guardrails**: blocks queries requesting regulated financial advice
- **Hallucination checker**: validates every answer is grounded in retrieved chunks
- **Source citation**: every response includes source document + page number

## CI/CD
Tests run automatically on every push via GitHub Actions.

## Future Improvements
- Multi-modal support (tables, charts in PDFs)
- Fine-tuned embedding model for financial domain
- RAGAS evaluation dashboard