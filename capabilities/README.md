# capabilities/

Domain-specific knowledge docs loaded on demand, per task.

Capabilities extend a persona with specialized knowledge for a specific
type of work. They are not loaded by default — the persona or task spec
specifies which to load. Maximum 2 simultaneously unless justified.

Each capability is scoped to a single domain and stays within a
≤1,000 token budget.

| File | Purpose | Primary Consumer |
|---|---|---|
| `ai-system-design.md` | RAG, model selection, evals, prompt standards, cost | CTO |
| `security-and-compliance.md` | PII, auth, secrets, OWASP LLM Top 10 | CTO |
| `api-design-standards.md` | Contract-first, REST, versioning, error handling | CTO |
| `infrastructure-and-devops.md` | CI/CD, IaC, observability, cost management | CTO |
| `frontend-engineering.md` | Next.js, components, state, accessibility, performance | CTO |
| `requirements-gathering.md` | User stories, acceptance criteria, MoSCoW prioritization | Product Lead |
| `grounding-doc-management.md` | Grounding doc lifecycle, token budgets, governance | Agent Architect |
| `external-artifact-migration.md` | Evaluate and migrate external prompts/skills into agent-os | Agent Architect |

**Rules:**
- Use `capability-template.md` in `templates/` to author new capabilities
- New capabilities require an entry in `REGISTRY.toml`
- Do not duplicate content already in `base/` — check before adding
