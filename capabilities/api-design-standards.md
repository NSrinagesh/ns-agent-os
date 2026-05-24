---
name: api-design-standards
type: capability
version: 0.1
owner: cto
tags: [agent-os, capability, api, rest, design, standards]
date: 2026-05
status: draft
primary_consumer: cto
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# API Design Standards

## Purpose
Defines how the CTO approaches API design — contract-first principles,
REST conventions, versioning, error handling, and documentation standards.
Ensures consistent interfaces that the Full Stack Developer can build
against and external consumers can rely on.

## When to Load
Load for any session involving API design, endpoint definition, service
interface design, versioning decisions, or API review.

## Contract-First Principle
Define the API contract (schema, endpoints, request/response shapes)
before writing implementation code. The contract is the source of truth.

- Document in OpenAPI 3.x format
- API contract reviewed by CTO before implementation starts
- Contract changes require versioning — never break existing consumers silently

## REST Conventions
- Use nouns for resources, not verbs: `/resumes` not `/getResumes`
- HTTP methods map to actions: GET (read), POST (create), PUT/PATCH
  (update), DELETE (remove)
- Plural resource names: `/users`, `/documents`
- Nested resources for clear ownership: `/users/{id}/resumes`
- Keep nesting shallow — max 2 levels deep

## Versioning
- Version in the URL path: `/v1/resumes`
- Never change a v1 contract without bumping to v2
- Maintain at least one prior version while consumers migrate
- Deprecation: announce in response headers before removal

## Request and Response Standards
- Always return JSON
- Consistent response envelope:
```json
{
  "data": {},
  "error": null,
  "meta": { "requestId": "", "timestamp": "" }
}
```
- On error, `data` is null; `error` contains code and message
- Never return raw stack traces or internal error details to clients

## Error Handling
| HTTP Status | When to Use |
|---|---|
| 200 | Success |
| 201 | Resource created |
| 400 | Bad request — client error, invalid input |
| 401 | Unauthenticated |
| 403 | Authenticated but not authorized |
| 404 | Resource not found |
| 422 | Validation error — input received but semantically invalid |
| 429 | Rate limit exceeded |
| 500 | Server error — never expose internals |

Error response must include a machine-readable `code` and
human-readable `message`. Never use 200 for errors.

## Documentation
- Every endpoint documented in OpenAPI spec
- Include example request and response for each endpoint
- Document all error codes an endpoint can return
- Keep docs in sync with code — treat drift as a bug

## Sources
- OpenAPI Specification 3.x (openapis.org) — contract-first standard
- Google API Design Guide (cloud.google.com/apis/design) — REST conventions and resource naming
- Microsoft REST API Guidelines (github.com/microsoft/api-guidelines) — versioning and error handling
- Stripe API Design — industry reference for consistency and DX
- Fielding (2000) REST dissertation — foundational REST constraints

## Anti-Patterns
- Verbs in resource URLs
- Breaking changes without version bump
- 200 status codes on error responses
- Exposing internal error details or stack traces to clients
- Undocumented endpoints
- Deep nesting beyond 2 levels
