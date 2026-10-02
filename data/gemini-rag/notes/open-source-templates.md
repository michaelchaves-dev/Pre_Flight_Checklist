GEMINI RAG — OPEN-SOURCE REFERENCE TEMPLATES

Purpose
Shortlist of strong free/open-source RAG references for building and improving the Gemini_RAG system. Borrow only the useful patterns; avoid unnecessary framework bloat.

1. Gemini RAG Demo — ColRuDev
Use: lightweight Gemini-native RAG reference; useful for File Search, citations, and a simple end-to-end implementation.
Load: corpus/repo_gemini-rag-demo.md

2. AnythingLLM — Mintplex Labs
Use: mature open-source RAG/agent architecture; useful for ingestion, workspace memory, model/provider routing, citations, and vector-store patterns.
Load: corpus/repo_anything-llm.md

3. LangChain RAG Starter — pubudini-rathnayake
Use: compact Gemini + LangChain RAG baseline; useful for separating ingestion, retrieval, API, and vector-store layers.
Load: corpus/repo_langchain-rag-starter.md

4. RAG Research Agent Template — LangChain AI
Use: advanced reference for research-agent workflows, query decomposition, retrieval planning, iterative search, and evidence synthesis.
Load: corpus/repo_rag-research-agent-template.md

IMPLEMENTATION PRINCIPLE
Start with the smallest capable architecture. Use these repositories as reference libraries rather than automatically adopting every dependency or framework.

Default progression:
Gemini_RAG files → native Gemini retrieval/File Search → targeted borrowed patterns → external vector database/framework only if native retrieval becomes limiting.
