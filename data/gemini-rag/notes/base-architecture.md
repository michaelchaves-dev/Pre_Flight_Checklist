GEMINI RAG — BASE ARCHITECTURE & FILE MAP

RAG RULE
This file is retrieval context, not mandatory prompt context.
Load only sections materially relevant to the current query.
Prefer the newest authoritative record.
Do not repeat retrieved material unless needed for the answer.

ARCHITECTURE PRINCIPLE
For this setup, do not add Chroma, Qdrant, LangChain, or another vector database yet.

Gemini’s official Cookbook exposes File Search as a hosted RAG mechanism, including hybrid File Search + Google Search grounding. That provides a native upgrade path without immediately adding infrastructure.

Recommended progression:
Drive Gemini_RAG → disciplined Markdown corpus → Gemini File Search → only then consider external vector DB / AnythingLLM / custom API if native retrieval becomes limiting.

Core principle:
SMALLEST CAPABLE ARCHITECTURE FIRST.

FOLDER / FILE MAP

Gemini_RAG/
├── 00_INDEX.md
├── 01_OPERATING_RULES.md
├── 02_IDENTITY_CONTEXT.md
├── 03_PROJECTS.md
├── 04_DECISIONS.md
├── 05_ACTIVE_STATE.md
├── 06_TERMINOLOGY.md
└── CHANGELOG.md

--------------------------------------------------
00_INDEX.md
--------------------------------------------------
Purpose:
Routing map for the RAG.

Contains:
- what each file contains
- retrieval priority
- authoritative-source rules
- last-updated timestamps

Rule:
Retrieve only files relevant to the current request.
Never preload the entire RAG.

--------------------------------------------------
01_OPERATING_RULES.md
--------------------------------------------------
Purpose:
Gemini behavior.

Include:
- Hey Gem boot protocol
- mandatory preflight
- minimalism
- token discipline
- no unsolicited video/media
- cheapest-capable routing
- ambiguity gate
- loop killer
- delta mode
- read ≠ write
- truth/evidence rules

--------------------------------------------------
02_IDENTITY_CONTEXT.md
--------------------------------------------------
Purpose:
Durable context needed to understand the operator and organization.

Include only stable facts:
- Subtract Architect Studios
- major systems/products
- working methodology
- recurring preferences
- important collaborators/roles

Exclude temporary conversation details.

--------------------------------------------------
03_PROJECTS.md
--------------------------------------------------
Purpose:
Project registry.

For each project:
NAME:
PURPOSE:
STATUS:
AUTHORITATIVE LOCATION:
RELATED REPO/DRIVE:
CURRENT VERSION:
NEXT ACTION:
LAST UPDATED:

Keep this file as an index.
Detailed material stays in the actual project files/repos.

--------------------------------------------------
04_DECISIONS.md
--------------------------------------------------
Purpose:
Prevent forgotten decisions and repeated debates.

Format:
DATE:
PROJECT:
DECISION:
WHY:
EVIDENCE:
STATUS: active / superseded / experimental
SUPERSEDES:
SOURCE:

--------------------------------------------------
05_ACTIVE_STATE.md
--------------------------------------------------
Purpose:
Current working state.

Only:
- active projects
- current experiments
- unresolved blockers
- immediate next actions
- recent discoveries

Aggressively prune stale information.
This is the first project-state file Gemini should consult.

--------------------------------------------------
06_TERMINOLOGY.md
--------------------------------------------------
Purpose:
Stop terminology drift.

Format:
TERM:
CANONICAL MEANING:
DO NOT CONFUSE WITH:
RELATED SYSTEM:

Examples:
QST = Quantum Subtraction Theory
-Step0 = ...
SubtracToken = ...
bellaOS = ...

--------------------------------------------------
CHANGELOG.md
--------------------------------------------------
Purpose:
Chronological durable updates.

Format:
DATE:
PROJECT:
CHANGE:
EVIDENCE/SOURCE:
FILES AFFECTED:

Only record meaningful state changes.
Do not store entire conversations.
