---
name: external-artifact-migration
type: capability
version: 0.1
owner: agent-architect
tags: [agent-os, capability, migration, prompts]
date: 2026-05
status: draft
primary_consumer: agent-architect
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# External Artifact Migration

## Purpose
Defines how the Agent Architect evaluates, classifies, refactors, and
migrates external prompts, skills, personas, or similar artifacts into
the agent-os framework.

## Step 1 — Evaluate

Assess the artifact before touching it. Answer these questions:

| Question | Why it matters |
|---|---|
| What does it do? | Determines classification |
| What model/platform was it built for? | Flags compatibility issues |
| Does it conflict with base doc standards? | Blocks adoption if yes |
| Does it duplicate something we already have? | Check REGISTRY.toml |
| What is its token footprint? | Determines if it fits budget |
| Does it contain hardcoded credentials, PII, or sensitive data? | Blocks adoption if yes |

If it conflicts with a base doc rule, stop. Do not adopt. Document the
conflict and escalate to operator.

## Step 2 — Classify

Map the artifact to one target type:

| If the artifact is... | It becomes... | Goes in... |
|---|---|---|
| A role or persona definition | Persona doc | `personas/` |
| Domain knowledge or best practices | Capability doc | `capabilities/` |
| A reusable instruction for a specific task | Prompt template | `prompts/` |
| An orchestration recipe (when/what/output) | Task spec | `tasks/` |
| A tool bundle (Cowork skill, MCP) | Execution layer only | Referenced in task specs, not stored as a doc |

When classification is ambiguous, prefer the narrower scope. A prompt
template over a capability doc; a capability doc over a persona.

## Step 3 — Refactor

Adapt the artifact to agent-os conventions:

- Add frontmatter (name, type, version, owner, tags, date, status, changelog)
- Remove or replace any hardcoded model names, API keys, or platform-specific syntax
- Trim content to token budget: persona ≤1,500, capability ≤1,000, prompt ≤500
- Align output instructions with output-standards.md
- Replace behavioral overrides that conflict with agent-design-standards.md
- Note the original source in the changelog

## Step 4 — Produce Migration Brief

Before writing any files, produce a brief for operator review:

```
Artifact: [name or source URL]
Classification: [persona | capability | prompt | task | execution-layer-only]
Target file: [proposed path]
Token estimate: [estimated tokens after refactor]

Conflicts: [list any conflicts with base docs, or "none"]
Technical hurdles: [list any platform-specific syntax, model dependencies,
                   missing context, or adaptation complexity]
Recommendation: [adopt as-is | adopt with modifications | reject]
Modifications required: [bullet list if applicable]
```

Wait for operator approval before writing files.

## Step 5 — Migrate

On operator approval:
1. Write the refactored artifact to the target path
2. Add entry to REGISTRY.toml
3. Note source and original author in changelog if known

## Anti-Patterns
- Adopting without evaluating for base doc conflicts
- Skipping the migration brief — never write files without operator review
- Storing tool bundles (Cowork skills, MCP servers) as grounding docs
- Adopting artifacts that contain hardcoded credentials or PII
- Inflating token budget to preserve original content verbatim
