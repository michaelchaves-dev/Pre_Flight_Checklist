# 04_DECISIONS

DATE: 2026-10-02
PROJECT: Pre_Flight_Checklist
DECISION: The uploaded search-discipline file is 01_OPERATING_RULES.md and is the newest behavior record.
WHY: It defines exact task, minimum retrieval, minimum tooling, and exact delivery.
EVIDENCE: User upload titled GEMINI RAG + SEARCH DISCIPLINE.
STATUS: active
SUPERSEDES:
SOURCE: chat upload 2026-10-02

DATE: 2026-10-02
PROJECT: Pre_Flight_Checklist
DECISION: Keep WHAT / WHERE / WHEN / DELIVERY. Add, do not replace: trivial-skip, max 3 questions with defaults, reversibility, cheapest rung, max 2 opt-in improvements.
WHY: The upload uses that card. The additions stop interview-mode and token padding without fighting it.
STATUS: active
SUPERSEDES:
SOURCE: this design thread

DATE: 2026-10-02
PROJECT: Pre_Flight_Checklist
DECISION: Corpus text is in the repo. Agents read 00_INDEX.md first and one relevant file. They do not preload the folder.
WHY: The operating rule says this file is retrieval context, not mandatory prompt context.
STATUS: active

DATE: 2026-10-02
PROJECT: Pre_Flight_Checklist
DECISION: Screenshots and both Drive videos (Claudtokenmax, ClaudTokenMaxv0) are not in git.
WHY: Both videos are over GitHub's 100MB file limit. Images are evidence of banned media padding. Loading them violates the operating rule.
STATUS: active

DATE: 2026-10-02
PROJECT: Pre_Flight_Checklist
DECISION: Do not invent 02_IDENTITY_CONTEXT, 03_PROJECTS, or 06_TERMINOLOGY.
WHY: No source text was provided. The architecture file only names them.
STATUS: active

DATE: 2026-10-02
PROJECT: Pre_Flight_Checklist
DECISION: No unsolicited links, video, images, citations, or resource lists. A link only when that URL is the named deliverable.
WHY: User ban on token-maxxing and cheap substitute tactics, restated in the operating rules.
STATUS: active
