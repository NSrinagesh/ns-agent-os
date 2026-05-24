---
name: infrastructure-and-devops
type: capability
version: 0.1
owner: cto
tags: [agent-os, capability, infrastructure, devops, cicd, observability]
date: 2026-05
status: draft
primary_consumer: cto
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# Infrastructure and DevOps

## Purpose
Defines the CTO's approach to infrastructure architecture, CI/CD pipeline
design, observability, and cost management. Cloud-provider-agnostic
patterns — load project grounding doc for project-specific provider
and tooling decisions.

## When to Load
Load for any session involving infrastructure design, CI/CD setup,
deployment architecture, observability, or cloud cost review.

## Infrastructure Principles
- **Infrastructure as Code (IaC):** all infrastructure defined in code,
  version controlled, reviewed like application code
- **Immutable infrastructure:** deploy new instances rather than
  patching running ones
- **Least privilege:** every service has only the permissions it needs —
  no wildcards, no shared credentials
- **Environment parity:** dev, staging, and prod environments mirror
  each other in configuration; differences documented explicitly

## CI/CD Pipeline
Minimum viable pipeline for every service:

| Stage | What happens |
|---|---|
| Build | Compile, lint, static analysis |
| Test | Unit tests, integration tests (real dependencies, no mocks) |
| Security scan | Dependency vulnerability check, secrets scan |
| Deploy to staging | Automated on merge to main |
| Smoke test | Automated post-deploy verification |
| Deploy to prod | Manual gate or automated with rollback trigger |

- Main branch always deployable — no broken builds merge
- Feature branches max 3 days; PRs require review before merge
- Load project grounding doc for project-specific CI/CD tooling

## Deployment Patterns
- **Containerize all services** — consistent runtime across environments
- **Health checks** on every service — liveness and readiness probes
- **Graceful shutdown** — drain in-flight requests before termination
- **Rollback plan** required for every production deployment

## Observability
Three pillars — all required before a service is production-ready:

**Logs**
- Structured JSON — never plain text in production
- Include: service name, request ID, timestamp, severity, message
- Never log PII — apply security-and-compliance rules

**Metrics**
- Track: request rate, error rate, latency (p50/p95/p99), saturation
- Expose a `/metrics` endpoint per service
- Alert on error rate spike and latency p99 breach

**Traces**
- Distributed tracing on all cross-service calls
- Correlate via request ID propagated through all services

## Cost Management
- Tag all cloud resources by: environment, service, owner
- Set budget alerts before costs become a problem — not after
- Review costs weekly at MVP stage; automate anomaly alerting at scale
- Prefer managed services over self-hosted at MVP — operational
  overhead is the bigger cost
- Shut down non-prod resources outside working hours at MVP

## Sources
- Google SRE Book (sre.google/sre-book) — observability, reliability, and operational standards
- DORA metrics (dora.dev) — CI/CD pipeline performance benchmarks
- Twelve-Factor App methodology (12factor.net) — environment parity, IaC, config standards
- The DevOps Handbook (Kim, Humble, Debois, Willis) — CI/CD pipeline design
- GCP Architecture Framework (cloud.google.com/architecture/framework) — cloud infrastructure patterns

## Anti-Patterns
- Manual infrastructure changes outside of IaC
- Shared credentials or service accounts across environments
- Deploying to prod without staging validation
- Plain-text logging in production
- No rollback plan for production deployments
- Untagged cloud resources
