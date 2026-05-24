---
name: context-management
type: base
version: 0.1
owner: agent-architect
tags: [agent-os, base]
date: 2026-05
status: draft
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# Context Management

## Purpose
Defines how every agent manages what it knows, loads, and retains,
across all environments from full infrastructure to a chat session.

## Prompt Caching
Base docs are the stable cache prefix — cached tokens cost ~90% less.
To preserve cache hits:
- Base docs must never contain dynamic content
- Load order must be consistent: base → project base → persona
  → capability → dynamic content
- Do not alter base doc content or formatting between calls

## Context Loading
Load only what the current task requires.

Priority when context window is constrained:
1. Task-specific instructions
2. Relevant capability docs
3. Persona doc
4. Base docs (already loaded)

Never load capability docs speculatively.

## Memory
Persist only what is needed beyond the current session.

Degrade gracefully:
- Memory service available → write to configured store
- No memory service → document in handoff, use conversation
  as working memory

Never persist: secrets, PII, raw sensitive tool output,
unconfirmed assumptions.

## RAG
Use retrieval when a connected knowledge base is available.

Degrade gracefully:
- Vector store available → retrieve before generating
- No vector store → work with provided context, flag gaps

Never hallucinate retrieved content. If gap is material, say so.

## Session Boundaries
Start: load grounding and handoff, state what was loaded,
flag gaps, do not ask operator to re-explain documented context.

End: produce handoff — decisions, unconfirmed assumptions,
open items, next steps.

Degrade gracefully:
- Persistent storage available → write handoff there
- No storage → produce handoff as final output for operator
  to save manually

## Context Window Discipline
When approaching limits:
- Summarize completed context, do not retain verbatim
- Drop capability docs no longer relevant
- Never drop base docs or persona doc
- Flag to operator if critical context must be dropped

## Anti-Patterns
- Loading capability docs speculatively
- Writing sensitive data to memory
- Treating retrieved content as confirmed fact
- Closing without a handoff note
- Asking operator to re-explain documented context
- Hallucinating when retrieval is unavailable
