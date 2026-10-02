---
SOURCE: https://github.com/langchain-ai/rag-research-agent-template
BRANCH: main (15 commits; ARCHIVED read-only 2026-03-11; SHA not captured)
CAPTURED: 2026-10-01
LICENSE: MIT
RELEVANCE: MEDIUM for agent design patterns (routing, planning, parallel retrieval). LOW as a dependency: archived, defaults to Anthropic/OpenAI models, needs Elasticsearch/Mongo/Pinecone.
RAG RULE: Retrieval context only. Load when the query is about query routing, ambiguity handling, research planning, or multi-step retrieval.
---

# rag-research-agent-template (LangGraph)

## What it is
LangGraph starter for a RAG research agent, built for LangGraph Studio. Generated from langchain-ai/react-agent. Archived: no further updates, so pinned dependency and prompt versions will drift.

## Three graphs
- Index graph (`src/index_graph/graph.py`): takes document objects, indexes them. Empty input indexes `src/sample_docs.json`.
- Retrieval graph (`src/retrieval_graph/graph.py`): manages chat history and answers from retrieved docs.
- Researcher subgraph (`src/retrieval_graph/researcher_graph/graph.py`): runs per research-plan step.

## Retrieval graph logic (the reusable part)
1. Take user query.
2. Route it:
   - On-topic (here, LangChain): build a research plan, pass to researcher subgraph.
   - Ambiguous: ask the user for more information. (Direct analogue of an ambiguity gate.)
   - Off-topic: tell the user it is out of scope.
3. Researcher subgraph, per plan step: generate a list of queries from the step, retrieve for all queries in parallel, return docs.
4. Generate the final response from retrieved docs plus conversation context.

## Config surface
- retriever_provider: elastic-local (default), or MongoDB Atlas, Pinecone serverless.
- response_model default: anthropic/claude-3-5-sonnet-20240620. query_model default: anthropic/claude-3-haiku-20240307. Two-tier model split: cheap model for query generation, stronger model for the answer. (Model IDs are from the archived README and are outdated.)
- embedding_model default: openai/text-embedding-3-small (Cohere supported).
- search_kwargs controls doc count and similarity thresholds.
- Prompts live in `src/retrieval_graph/prompts.py` (research_plan_system_prompt, generate_queries_system_prompt, response_system_prompt).

## Setup notes
- Mongo Atlas: create an Atlas Vector Search index (not Atlas Search), path `embedding`, cosine, numDimensions must match the embedding model (1536 in the example), plus an indexed filter on `user_id`.
- Elasticsearch local: Docker single-node, use host.docker.internal from LangGraph Studio.
- Indexing is done when the indexer graph deletes content from its own memory after persisting.

## Patterns worth copying into a Gemini agent
- Route before retrieving: classify (on-topic / ambiguous / off-topic) so unnecessary retrieval and tokens are skipped.
- Cheap model for routing and query generation, stronger model only for the final answer.
- Plan, then retrieve per step, in parallel.
- Keep prompts in one file so they can be edited without touching graph logic.

## Caveats
- Archived. Do not build on it.
- Reimplementing it in Gemini means rewriting the model/provider layer. The graph structure transfers, the config does not.
