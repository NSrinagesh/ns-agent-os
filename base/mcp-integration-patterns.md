---
name: mcp-integration-patterns
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

# MCP Integration Patterns

## Purpose
Defines how every agent interacts with external tools via MCP,
regardless of role, project, or connected tools.

## Tool Call Principles
- Use only tools required for the current task
- Never infer missing parameters — surface the gap and stop
- Confirm before destructive or irreversible actions
- Tool access does not imply authorization — verify action
  is within task scope

## Auth
- Credentials never appear in grounding docs, prompts, or output
- Auth resolved at runtime via configured secrets layer
- On auth failure, surface explicitly — never retry with
  degraded or alternative credentials

## Error Handling
- Transient failures (rate limits, 5xx): retry
- Client errors (4xx): surface immediately, do not retry
- Silent failure never acceptable
- On retry exhaustion: stop, document failure, do not proceed
  on partial results

## Logging
Log every tool call to available output. Degrade gracefully:
- Logging service available → log there
- No logging service → log to console or session transcript
- Never block execution due to logging unavailability
- Document logging gaps in session handoff

## Data Classification
Classify data before passing to any tool:
- Public — no restriction
- Internal — confirm tool is authorized
- Sensitive (PII, credentials, regulated) — do not pass without
  explicit architectural approval
- When in doubt, treat as sensitive

## Security Constraints
Never:
- Pass credentials or secrets as tool parameters
- Access systems outside current project scope
- Chain calls that escalate permissions beyond task requirements
- Retain sensitive tool output beyond current task scope

## Anti-Patterns
- Inferring missing parameters to avoid stopping
- Retrying 4xx errors
- Proceeding on partial tool results
- Passing unclassified data to tools
- Treating tool access as blanket authorization
