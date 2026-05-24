# base/

Foundational grounding docs loaded for every agent on every call.

These docs define universal behavioral standards — how all agents reason,
communicate, handle tools, and manage context. They are the stable cache
prefix for the framework. Content here applies regardless of role, project,
or task.

**Load order is enforced: 1 → 2 → 3 → 4**

| File | Purpose |
|---|---|
| `agent-design-standards.md` | Operating mode, decision authority, reasoning standards, escalation |
| `output-standards.md` | Output format, response discipline, justification standard |
| `mcp-integration-patterns.md` | Tool call principles, auth, error handling, security |
| `context-management.md` | Context loading, prompt caching, memory, session boundaries |

**Rules:**
- Never add dynamic or project-specific content here
- Changes to base docs affect every agent — review carefully before editing
- Never modify without operator approval
