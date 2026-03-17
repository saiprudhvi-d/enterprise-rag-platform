# Enterprise RAG Platform — Financial Document Intelligence

![Tests](https://github.com/saiprudhvi-d/enterprise-rag-platform/actions/workflows/test.yml/badge.svg)
![Python](https://img.shields.io/badge/Python-3.11-blue)
![LangChain](https://img.shields.io/badge/LangChain-0.1.x-green)

## Overview
An enterprise-grade RAG platform for **financial document intelligence**. Enables natural language querying across SEC filings, compliance manuals, and policy documents with hybrid retrieval, source citation, and LLM guardrails — built under strict latency (<3s), reliability, and compliance constraints.

## Business Problem
Financial analysts spend hours manually searching policy documents and regulatory filings. This platform reduces research time from hours to minutes by enabling accurate, grounded natural language Q&A — with built-in guardrails to prevent hallucinations and ensure regulatory compliance.

## Architecture
```
User Query → [ComplianceFilter] → [Hybrid Retrieval: BM25 + Vector + RRF]
          → [Cross-Encoder Reranking] → [Prompt Assembly]
          → [LLM Inference] → [HallucinationChecker] → Structured Response + Sources
```

## Tech Stack
Python · LangChain · OpenAI · Pinecone · FAISS · FastAPI · Docker · AWS ECS

## Key Features
- **Hybrid retrieval** — BM25 + vector search fused via Reciprocal Rank Fusion
- **Compliance guardrails** — blocks queries requesting regulated financial advice
- **Hallucination checker** — validates every answer is grounded in retrieved chunks
- **Source citation** — every response includes document name + page number

## Setup
```bash
git clone https://github.com/saiprudhvi-d/enterprise-rag-platform
pip install -r requirements.txt
cp .env.example .env  # Add OPENAI_API_KEY, PINECONE_API_KEY
uvicorn app.app:app --reload
```

## Future Improvements
- Multi-modal support (tables, charts in PDFs)
- Fine-tuned embedding model for financial domain
- RAGAS evaluation dashboard
- Redis caching layer for frequent queries