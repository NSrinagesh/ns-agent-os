# templates/

Starter files for authoring new agent-os artifacts.

Use these when creating a new persona, capability, task spec, or session
startup file. Each template includes required frontmatter, section structure,
and inline guidance. Copy the relevant template, rename it per convention,
fill it in, and register it in `REGISTRY.toml`.

**Naming convention for templates: `[artifact-type]-template.[ext]`**

| File | Use when creating... | Naming convention for output |
|---|---|---|
| `persona-template.md` | A new agent persona | `[role-name]-persona.md` |
| `capability-template.md` | A new capability doc | `[domain-name].md` |
| `task-template.toml` | A new task spec | `[task-name].toml` |
| `session-startup-template.md` | A session startup file | `[project]-[role]-session.md` |

**Rules:**
- Never load templates as grounding docs — they are authoring scaffolding only
- After creating a new artifact from a template, register it in `REGISTRY.toml`
- Templates themselves are registered in REGISTRY.toml under `[[templates]]`
- Do not store executable prompt content here — that belongs in `prompts/`
