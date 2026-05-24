# prompts/

Reusable prompt instructions that agents load when executing specific tasks.

This folder holds actual prompt content — system prompts, structured
instructions, or reusable input patterns tied to specific recurring tasks.
These are not templates for authoring new artifacts (those live in
`templates/`). They are ready-to-use instructions an agent loads and
executes directly.

**Examples of what belongs here:**
- System prompt for a weekly leadership report task
- Structured input format for an ADR authoring session
- Reusable prompt for competitive research synthesis

**This folder is currently empty.**
Prompts are added as task patterns stabilize and recurring task specs
are built out in `tasks/`.

**Rules:**
- Prompts here are loaded by task specs — not loaded directly by personas
- Keep prompts focused on a single task type
- Version and register every prompt in `REGISTRY.toml`
- Do not store templates here — templates belong in `templates/`
