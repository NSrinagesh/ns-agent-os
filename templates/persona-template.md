---
# File naming convention: [role-name]-persona.md (e.g., cto-persona.md)
name: [kebab-case-name]
type: persona
version: 0.1
owner: agent-architect
tags: [agent-os, persona]
date: [YYYY-MM]
status: draft
changelog:
  - version: 0.1
    date: [YYYY-MM]
    note: Initial draft
---

# [Persona Name]

## Purpose
[1-2 sentences. What is this agent's reason for existing? What problem does it solve?]

## Scope
- [What this persona does — bullet list]

## Out of Scope
- [What this persona explicitly does not do]

## Responsibilities

### [Responsibility Area 1]
- [Detail]

### [Responsibility Area 2]
- [Detail]

## Instruction Precedence
When rules conflict: base docs > this persona > capability docs > dynamic input.
Never override a base doc rule from within a persona or capability.

## Inputs
- [What this persona reads or receives to do its job]

## Outputs
- [What this persona produces, and where it goes]

## Failure Mode Handling
| Failure Mode | This Persona's Response |
|---|---|
| [Mode] | [Response] |

## Reasoning Approach
- [How this persona reasons — anchors, escalation triggers, uncertainty handling]

## Authorized Tools
| Tool | Access | Boundary |
|---|---|---|
| [Tool] | [Read / Write / Read+Write] | [Constraint] |

## Delegation Policy
- **May delegate:** [What and under what conditions]
- **May not delegate:** [What must stay with this persona]

## Capabilities to Load
- capabilities/[relevant-capability].md

## Default Tasks
- tasks/[task-name].toml

## Constraints
- [Hard rules this persona must never violate]
