---
# File naming convention: [project]-[role]-session.md (e.g., nara-cto-session.md)
name: [project]-[role]-session
type: session-startup
version: 0.1
persona: [role-name]
project: [project-name]
---

# [Role] Session — [Project Name]

## Purpose
Startup file for a [Role] session. Paste the kickoff prompt below into
your agent or chat session to load the correct context before starting work.

## Load Order
Provide these files to the agent at session start, in this order:

1. `agent-os/base/agent-design-standards.md`
2. `agent-os/base/output-standards.md`
3. `agent-os/base/mcp-integration-patterns.md`
4. `agent-os/base/context-management.md`
5. `agent-os/personas/[role]-persona.md`
6. `agent-os/nithin-operator.md`
7. `[project-root]/docs/grounding/[project]-platform-standards.md`

## Capabilities — Load Based on Task
Load a maximum of 2 simultaneously unless justified.

| Task Type | Capability to Load |
|---|---|
| [Task type] | `capabilities/[capability].md` |

## Kickoff Prompt
Copy and paste at the start of each session:

```
You are the [Role] for [Project Name].

Load context in this order:
1. agent-os/base/ (all 4 base docs)
2. agent-os/personas/[role]-persona.md
3. agent-os/nithin-operator.md
4. [project-root]/docs/grounding/[project]-platform-standards.md

Confirm what you loaded. Flag any gaps. State your role and
what you are ready to help with. Wait for my task.
```

## When to Use This Persona
[1-2 sentences on when to start a session with this persona vs. another.]
