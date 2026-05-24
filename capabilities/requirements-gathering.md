---
name: requirements-gathering
type: capability
version: 0.1
owner: product-lead
tags: [agent-os, capability, requirements, product]
date: 2026-05
status: draft
primary_consumer: product-lead
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# Requirements Gathering

## Purpose
Defines how the Product Lead discovers, structures, and validates requirements
before handing off to engineering. Prevents underspecified work from reaching
development.

## When to Load
Load for any session involving user story writing, requirements elicitation,
acceptance criteria definition, or backlog refinement.

## Step 1 — Establish the User
Before writing any requirement, confirm:
- Who is the target user? (role, context, goal)
- What problem are they experiencing? (evidence-based, not assumed)
- What does success look like for them?

If any of these are unknown, stop and resolve before proceeding.

## Step 2 — Structure the Requirement
Use this format for every user story:

```
As a [specific user type],
I want to [take an action],
So that [I achieve an outcome].
```

Avoid vague user types ("a user", "someone"). Name the persona.

## Step 3 — Write Acceptance Criteria
Every story requires minimum 2 acceptance criteria. Use Given/When/Then:

```
Given [a precondition],
When [an action occurs],
Then [a measurable outcome results].
```

Criteria must be testable. Reject criteria like "works correctly" or "is fast."

## Step 4 — Flag Dependencies
Before handoff, identify:
- Stories that must complete before this one can start
- Shared components or data this story depends on
- CTO input needed on technical feasibility

## Step 5 — Prioritize
Apply MoSCoW within approved scope:
- **Must have:** MVP blockers — product does not function without these
- **Should have:** High value, not MVP-blocking
- **Could have:** Nice to have, defer to V2
- **Won't have:** Explicitly out of scope — document to prevent scope creep

## Output Format
Produce a structured backlog entry per story:
```
Story: [title]
User: [persona]
Story: As a... I want... So that...
Priority: [Must/Should/Could/Won't]
Acceptance Criteria:
  - Given... When... Then...
  - Given... When... Then...
Dependencies: [story IDs or "none"]
Open Questions: [list or "none"]
```

## Anti-Patterns
- Writing requirements without an identified user
- Acceptance criteria that can't be tested
- Handing off to engineering without dependency mapping
- Absorbing scope changes without escalating to operator
- Conflating features with user outcomes
