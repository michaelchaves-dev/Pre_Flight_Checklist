---
SOURCE: https://github.com/Mintplex-Labs/anything-llm
BRANCH: master (2,459 commits, ~66.6k stars at capture; SHA not captured)
CAPTURED: 2026-10-01
LICENSE: MIT
RELEVANCE: MEDIUM. Stage-3 option only (after native Gemini File Search proves limiting). Also a source of design patterns: model routing, memories, scheduled tasks, tool selection.
RAG RULE: Retrieval context only. Load when the query is about self-hosted RAG platforms, multi-user workspaces, agent skills/MCP, or token-saving tool selection.
---

# AnythingLLM

## What it is
All-in-one, local-first app: chat with documents, built-in agents, multi-user (Docker version only), vector DBs and document pipeline included. Desktop (Mac/Windows/Linux), Docker, and bare-metal deploys.

## Architecture (monorepo, six parts)
- `frontend`: Vite + React UI.
- `server`: Node/Express. Owns vector DB management and LLM calls.
- `collector`: separate Node/Express service that parses and processes uploaded documents.
- `docker`: build and run instructions.
- `embed`: submodule, embeddable website chat widget.
- `browser-extension`: submodule, Chrome extension.
Separation to note: document parsing (collector) is isolated from retrieval/chat (server).

## Features relevant to a custom Gemini agent
- Dynamic Model Routing: route each chat to a provider/model by user-defined rules. Same idea as cheapest-capable routing.
- Intelligent Skill Selection: enables unlimited tools while claiming up to 80% lower token use per query (vendor claim, unverified).
- Automatic and user-managed Memories per user/workspace.
- Scheduled Tasks: cron-style recurring prompts with agent capability.
- No-code Agent Flows, custom agents, MCP compatibility.
- Source citations in chat; full developer API.

## Backends supported
- LLMs: broad list including Google Gemini, Anthropic, OpenAI, Ollama, OpenRouter, Groq, and many others.
- Embedders: native (default), Gemini, OpenAI, Ollama, Cohere, Voyage, others.
- Vector DBs: LanceDB (default), PGVector, Pinecone, Chroma, Weaviate, Qdrant, Milvus, Zilliz, Astra.

## Dev setup (from root)
`yarn setup` (fills `.env` files; `server/.env.development` must be filled), then `yarn dev:server`, `yarn dev:frontend`, `yarn dev:collector`.

## Telemetry
Anonymous PostHog events on by default (install type, doc add/remove events, vector DB type, LLM provider/model, chat-sent events; no content). Disable with `DISABLE_TELEMETRY=true`. Outbound calls to cdn.anythingllm.com and GitHub raw continue regardless.

## Fit assessment
- Adds three services (frontend, server, collector) plus a vector DB. Violates "smallest capable architecture first" until native File Search is exhausted.
- Multi-user and embed widget are Docker-only.
- Use now as a pattern library (routing rules, memory scoping, skill selection), not as infrastructure.
