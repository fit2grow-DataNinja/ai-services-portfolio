# B2B AI Service Portfolio

Status: working project repository | Baseline: architecture v0.1 | Updated: 2026-10-21

## Purpose
Develop reusable, customizable AI-enabled business services for EU SMEs and mid-market companies, initially concentrating on familiar business analysis, digital analytics, marketing, reporting, data quality, and documentation domains.

Sell a defined business outcome, not a technology. Each service may be delivered as a shared internal AI skill, a client-operated technical application, or a provider-managed service depending on requirements and economics.

## Repository map
- `governance/`: project scope, working principles, documentation conventions.
- `strategy/`: positioning, target segments, competition, business areas.
  - [Future improvements register](strategy/future-improvements.md) — eight proposed, deferred design elements to evaluate when a service need arises.
- `architecture/`: approved platform baseline and change control.
- `research/`: methodology, evidence, scoring, candidate register.
- `services/`: existing reference solutions and future service specifications.
- `commercial/`: delivery options, maintenance, pricing hypotheses.
- `validation/`: planned tests and future results.
- `decisions/`: approved decisions and unresolved questions.
- `templates/`: reusable Markdown document templates.

## Document status convention
`Approved` = explicitly agreed; `Proposed` = recommendation awaiting decision; `Hypothesis` = unvalidated commercial or technical assessment; `Planned` = not implemented; `Verified` = supported by actual evidence/test.

## Service repositories
- [S02 — CRM Data Quality & Freshness Auditor](services/S02.md) — [technical repository](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor); synthetic-data MVP integration verified, source transfer pending.

## Current priorities
1. Research recurring business problems and service opportunities.
2. Evaluate internal shared-skill alternatives before investing in custom development.
3. Validate commercial differentiation and delivery economics.
4. Extend verified S02 integration with reproducible source control, security design and deployment validation.

No live customer demand, revenue, price points, or production-readiness claims have yet been validated.

## Security design note (SEC-001)
The portfolio records a **planned** sensitivity-tagging and manual-approval gate for client-sensitive data. Its scope and implementation remain open; see `architecture/baseline-v0.1.md`, `validation/validation-plan.md`, and `decisions/decision-log.md`. This update does not modify the separate RAG-MVP project.
