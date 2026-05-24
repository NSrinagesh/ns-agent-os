---
name: ai-system-design
type: capability
version: 0.1
owner: cto
tags: [agent-os, capability, ai, llm, rag, evals]
date: 2026-05
status: draft
primary_consumer: cto
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# AI System Design

## Purpose
Defines how the CTO approaches AI/LLM architecture decisions — model
selection, RAG design, prompt engineering standards, evaluation, cost
management, and guardrails.

## When to Load
Load for any session involving AI feature design, model selection,
RAG architecture, prompt standards, eval framework setup, or
inference cost review.

## Model Selection
Choose based on task requirements, not defaults:

| Task Type | Guidance |
|---|---|
| Complex reasoning, multi-step | Largest capable model; benchmark before committing |
| Document processing, summarization | Mid-tier model; cost/quality tradeoff matters |
| Classification, structured extraction | Smallest model that meets accuracy bar |
| Real-time / high-volume | Optimize for latency and cost — eval thoroughly |

Always wrap model calls behind a service interface. Product code
never calls model APIs directly. This isolates model changes from
product logic.

## RAG Architecture
Standard pattern for knowledge-grounded responses:

1. **Chunking** — chunk by semantic unit, not fixed token count;
   overlap 10–20% to preserve context across boundaries
2. **Embedding** — use consistent embedding model; never mix models
   in the same vector index
3. **Retrieval** — hybrid search (vector + keyword) outperforms
   pure vector in most production cases; test both
4. **Reranking** — apply reranker before passing to LLM when
   retrieval precision matters
5. **Generation** — ground the prompt with retrieved context;
   instruct model to cite sources or flag when context is insufficient

## Prompt Engineering Standards
- System prompt: stable, versioned, treated as code
- Few-shot examples: 2–3 minimum for structured output tasks
- Chain-of-thought: require for multi-step reasoning tasks
- Temperature: 0 for deterministic tasks; ≤0.7 for creative tasks
- Never embed business logic in prompts — logic belongs in code

## Evaluation (Evals)
Every AI feature ships with an eval before going to production.
Use RAGAS (RAG Assessment) for RAG pipelines; DeepEval for general
LLM evals — both are open-source and integrate with CI/CD.

Core metrics (per RAGAS):
- **Faithfulness** — answer grounded in retrieved context?
- **Answer relevance** — answer addresses the question?
- **Context precision** — retrieved context actually useful?
- **Context recall** — relevant context retrieved at all?

Run evals on every model or prompt change. Start with a small
golden dataset; expand with real usage data over time.

## Inference Cost Management
- Log token usage per request from day one
- Set hard limits per request and per user session
- Prefer streaming for long-form responses — improves perceived latency
- Cache deterministic responses where possible (e.g., embeddings)

## AI Guardrails
- Input validation: sanitize and length-limit user inputs before
  passing to model
- Output validation: parse and validate structured outputs before
  using downstream
- PII: never pass raw PII to third-party model APIs without review —
  load security-and-compliance capability for PII handling rules
- Hallucination mitigation: require grounding context for factual
  claims; instruct model to express uncertainty explicitly

## Sources
- Anthropic prompt engineering guide (docs.anthropic.com)
- RAGAS eval framework (ragas.io) — RAG evaluation metrics
- DeepEval (confident-ai.com) — general LLM eval framework
- LangChain / LlamaIndex documentation — RAG architecture patterns
- Google MLOps Practitioner Guide — model lifecycle and eval standards

## Anti-Patterns
- Calling model APIs directly from product code
- Shipping AI features without evals
- Using a single large model for all tasks regardless of cost
- Mixing embedding models in the same vector index
- Hardcoding prompts without versioning
