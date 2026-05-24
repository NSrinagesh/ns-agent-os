---
name: security-and-compliance
type: capability
version: 0.1
owner: cto
tags: [agent-os, capability, security, compliance, pii, auth]
date: 2026-05
status: draft
primary_consumer: cto
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# Security and Compliance

## Purpose
Defines security and compliance standards for the CTO — covering PII
handling, data classification, auth patterns, secrets management, and
AI-specific security risks (OWASP LLM Top 10).

## When to Load
Load for any session involving auth design, PII or sensitive data
handling, secrets management, security review, or AI safety assessment.

## Data Classification
Classify all data before designing storage or transmission:

| Class | Definition | Handling |
|---|---|---|
| Public | No harm if disclosed | Standard controls |
| Internal | Business-sensitive | Encrypted at rest and in transit |
| Confidential | PII, credentials, health, financial | Strict access control, audit log, no third-party sharing without review |
| Restricted | Legal hold, regulated data | Legal review required before any processing |

Resumes and career data are **Confidential** by default — treat as PII.

## PII Handling
- Never log PII — sanitize before writing to any log output
- Never pass raw PII to third-party model APIs without legal review
- Anonymize or pseudonymize PII in dev and test environments
- Enforce data minimization — collect only what the product requires
- Define and document retention periods; implement deletion on request

## Auth Patterns
- Authenticate every request — no unauthenticated endpoints except
  public health checks
- Use short-lived tokens (JWT); refresh server-side
- Scope permissions to minimum required (principle of least privilege)
- Never roll custom auth crypto — use established libraries only
- Load project grounding doc for project-specific auth stack decisions

## Secrets Management
- No secrets in code, config files, or version control — no exceptions
- Rotate secrets on suspected exposure immediately
- Use project-defined secrets service (see project grounding doc)
- Audit secret access — log who accessed what and when

## OWASP LLM Top 10 — Key Risks
Apply these checks to any AI feature before shipping:

| Risk | Mitigation |
|---|---|
| Prompt injection | Sanitize user inputs; separate system and user content clearly |
| Insecure output handling | Validate and parse LLM output before downstream use |
| Training data poisoning | Vet and version all data used for fine-tuning or RAG |
| Model denial of service | Rate limit requests; set max token budgets per session |
| Sensitive data exposure | Apply PII handling rules before any model call |
| Excessive agency | Scope AI actions explicitly — never grant open-ended tool access |

## Security Review Checklist
Before any feature ships, confirm:
- [ ] No secrets in code or config
- [ ] PII classified and handled per above
- [ ] Auth applied to all endpoints
- [ ] LLM inputs sanitized and outputs validated
- [ ] Logging does not capture PII
- [ ] OWASP LLM risks reviewed for AI features

## Sources
- OWASP LLM Top 10 (owasp.org/www-project-top-10-for-large-language-model-applications)
- OWASP Top 10 Web Application Security Risks (owasp.org)
- NIST Cybersecurity Framework (nist.gov/cyberframework)
- GDPR / CCPA — PII handling and data minimization principles
- Stripe security practices — secrets management and auth patterns

## Anti-Patterns
- Logging raw request bodies that may contain PII
- Passing PII to third-party APIs without review
- Hardcoded credentials of any kind
- Rolling custom auth or crypto implementations
- Granting AI agents open-ended tool or data access
