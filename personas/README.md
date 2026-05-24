# personas/

Role definitions for every agent in the framework.

A persona defines who an agent is — its purpose, scope, responsibilities,
authorized tools, delegation policy, and which capabilities to load.
Personas are loaded after base docs and before capabilities.

**Naming convention: `[role-name]-persona.md`**

| File | Role | Status |
|---|---|---|
| `agent-architect-persona.md` | Meta-agent — designs and governs all agent-os artifacts | Draft |
| `cto-persona.md` | Technical decision-maker — architecture, standards, AI design | Draft |
| `product-lead-persona.md` | Product definition — PRDs, user stories, prioritization | Draft |
| `full-stack-developer-persona.md` | Implementation — frontend, backend, testing, PRs | Draft |

**Rules:**
- Use `persona-template.md` in `templates/` to author new personas
- New personas require an entry in `REGISTRY.toml`
- Personas must not contain project-specific content — use a project
  grounding doc for that (see `docs/grounding/` in your project repo)
- Each new persona ships with minimum 2 default task specs
- Do not promote from draft to active without session validation
