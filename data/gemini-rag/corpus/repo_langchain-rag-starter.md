---
SOURCE: https://github.com/pubudini-rathnayake/langchain-rag-starter
BRANCH: main (4 commits at capture; SHA not captured)
CAPTURED: 2026-10-01
LICENSE: MIT
RELEVANCE: LOW-MEDIUM. Reference for the "external vector DB" stage only. Introduces LangChain + ChromaDB + FastAPI, which the current plan defers.
RAG RULE: Retrieval context only. Load when the query is about a self-managed RAG stack, chunking parameters, or a REST API wrapper around retrieval.
---

# langchain-rag-starter

## What it is
Starter RAG pipeline: LangChain + ChromaDB + FastAPI + Streamlit, using Gemini 2.5 Flash Lite. PDF and TXT only.

## Flow
User query -> Streamlit UI -> FastAPI `POST /api/v1/query` -> LangChain RAG chain (retriever over ChromaDB + Gemini LLM + prompt template) -> answer + sources.

## Module map
- `app/api/routes.py`: FastAPI endpoints.
- `app/core/config.py`: settings from `.env`. `app/core/prompts.py`: prompt templates.
- `app/services/embedder.py`: Gemini embeddings. `vectorstore.py`: ChromaDB setup. `rag_chain.py`: the chain.
- `ingest.py`: one-shot ingestion script (run manually before serving).
- `main.py`: FastAPI entry. `streamlit_ui/app.py`: demo UI. `tests/test_rag.py`.

## API contract
Request: `{"question": "..."}`. Response: `{"answer": "...", "sources": ["data/sample_docs/file.pdf"]}`.

## Config defaults
CHROMA_DB_PATH=./chroma_db, COLLECTION_NAME=rag_collection, CHUNK_SIZE=500 (characters), CHUNK_OVERLAP=50, GEMINI_API_KEY required.

## Run
Python 3.11 venv, `pip install -r requirements.txt`, `python ingest.py`, `uvicorn main:app --reload`, `streamlit run streamlit_ui/app.py`.

## Caveats
- Called "production-ready" in the README. It is not: no auth, no file-upload endpoint, no Docker, ingestion is manual (all listed on its own roadmap). 4 commits, 0 stars.
- 500-character chunks with 50 overlap is small for structured Markdown. Headings and records can split mid-block, which hurts retrieval on a corpus built from the planned 00-06 files.
- README says it supports Gemini and OpenAI; the architecture and config shown are Gemini-only.
- Use as a structural reference. Do not adopt as a base.
