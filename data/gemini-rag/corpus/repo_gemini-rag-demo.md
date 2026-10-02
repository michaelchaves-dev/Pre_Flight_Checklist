---
SOURCE: https://github.com/ColRuDev/gemini-rag-demo
BRANCH: main (2 commits at capture; SHA not captured)
CAPTURED: 2026-10-01
LICENSE: MIT
RELEVANCE: HIGH. Closest match to the Gemini File Search upgrade path. Reference implementation for hosted RAG with citations.
RAG RULE: Retrieval context only. Load when the query is about Gemini File Search, grounding, citations, or the upload/query pipeline.
---

# gemini-rag-demo

## What it is
Minimal RAG demo on the Gemini File Search tool (native to the `google-genai` SDK). No self-managed vector DB. Ships a Streamlit UI and a CLI pipeline. Dependencies: `google-genai`, `python-dotenv`, `streamlit`.

## Core mechanism
1. Upload documents into a managed File Search Store (Google chunks, embeds, and indexes them).
2. Query with the `FileSearch` tool attached to `generate_content_stream`. Retrieval is automatic.
3. Read citations from `grounding_metadata` on the final streamed chunk (source titles).
4. Model used: `gemini-2.5-flash-lite`.

## CLI pipeline order (src/main.py)
Upload -> Check (list indexed doc names) -> Generate (streamed) -> Cite.

## Module map
- `src/gemini_client.py`: module-level singleton client for CLI; `create_client()` for per-session UI clients.
- `src/upload_docs.py`: ingestion into the File Search Store.
- `src/check_docs.py`: list indexed documents.
- `src/query_docs.py`: grounded generation with FileSearch tool.
- `src/citate_docs.py`: citation extraction from grounding metadata.
- `src/configs.py`: constants.
- `src/streamlit_ui/`: `streamlit_app.py` (entry), `sidebar.py`, `chat.py`, `helpers.py`, `state.py`.

## Config (src/configs.py, verbatim values)
- FILE_SEARCH_STORE_NAME = "rag-demo"
- MODEL = "gemini-2.5-flash-lite"
- DOCS_DIR = "./docs/"
- SUPPORTED_FILETYPES: pdf, txt, html, htm, csv, md, xml

## Patterns worth copying
- Per-session client in the UI so one user's API key never leaks into another session; singleton only for CLI.
- Pending-file queue: stage, dedupe against already-indexed names, then upload.
- Errors during streaming or indexing are caught and shown without killing the session.
- Session reset preserves the API key but clears the chat and store state.

## Run
`uv sync` then `uv run streamlit run src/streamlit_ui/streamlit_app.py` or `uv run python src/main.py`. CLI needs `GEMINI_API_KEY` in `.env`.

## Limits and caveats
- README clone URL points at NickEsColR/gemini-rag-demo, not ColRuDev. Treat as a naming inconsistency, not a different repo.
- Only 2 commits. Treat as a reference, not a maintained dependency.
- Supported types exclude DOCX. Convert to PDF/MD/TXT before upload.
- Store lifecycle (deletion, per-store limits, pricing) is not documented in the repo. Verify against current Gemini API docs before relying on it.
