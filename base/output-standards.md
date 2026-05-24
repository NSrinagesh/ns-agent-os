---
name: output-standards
type: base
version: 0.2
owner: agent-architect
tags: [agent-os, base]
date: 2026-05
status: draft
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
  - version: 0.2
    date: 2026-05
    note: Added Justification Standard section
---

# Output Standards

## Purpose
Defines what every agent produces, how it is formatted, and
what it must never contain.

## Default Format
Structured output is the default for programmatic consumption.
Prose for human-facing responses where structure adds no value.

"Will code or another agent consume this?"
- Yes → structured output (JSON, YAML, defined schema)
- No → prose, concise

## Structured Output Rules
- Declare schema before producing output
- Validate before returning
- Complete or fail explicitly — no partial output
- On failure, return explicit error — not prose fallback

## Response Discipline
- Lead with the answer, not the reasoning
- No preamble restating the task
- No closing summary of what was produced
- Length driven by content, not thoroughness signaling

## Confidence and Caveats
- Caveat only when it affects the operator's decision
- One caveat maximum unless multiple material risks exist
- State output first, caveat after — never lead with caveat

## Prohibited Output
- Secrets, credentials, API keys, tokens
- PII in any form
- Raw stack traces to end users
- Unhandled exceptions
- Content not validated against declared schema

## Justification Standard
Applies to all recommendations except code implementation.
Include a brief block at the end of the recommendation:
- **Basis:** Framework or concept being applied
- **Examples:** 2–3 industry leaders or current practitioners
  (draw on the field broadly — do not anchor on a fixed list)
- **Why it applies:** One sentence connecting the example
  to this specific context

## Anti-Patterns
- Prose when structured output was expected
- Output without declared schema for programmatic consumers
- Leading with caveats
- Padding to signal effort
- Surfacing internal errors as unformatted exceptions
