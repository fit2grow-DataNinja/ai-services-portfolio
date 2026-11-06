# Project status — AI Services Portfolio

**Last updated:** 2026-11-06  
**Status:** Active development; S02 is the current service.  
**Purpose:** Quick handoff for future work sessions. This file owns portfolio-level progress only. Service implementation details live in the respective service repositories.

## Current focus
- **Active service:** [S02 — CRM Data Quality & Freshness Auditor](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor).
- **Authoritative working step:** [S02 PROJECT-STATUS.md](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/PROJECT-STATUS.md).
- **Portfolio next action:** Apply the new portfolio definition-of-done and regression-testing standards to service milestones. S02's next implementation step remains authoritative in its own status file.

## Completed
- Established a portfolio-level [S02 case study draft](case-studies/S02-crm-data-quality-auditor.md), linked to S02's implementation evidence and deferred commercial readiness backlog; final publication awaits MVP verification and Variant 2 comparison.
- Established a [portfolio definition of done](governance/definition-of-done.md), [regression-testing standard](validation/regression-testing.md), and [service test-layout template](templates/service-test-layout.template.md) for future services.
- Approved architecture v0.1 documented: modular Python 3.11.5/FastAPI, Open WebUI, Podman development, deterministic audit rules and hosted AI explanation.
- Established portfolio and S02 repositories and reciprocal documentation links.
- Recorded verified synthetic-data S02 standalone API and Open WebUI Workspace Tool integration.
- Adopted single-source-of-truth ownership and mandatory shared-core review at each verified solution milestone.
- Created service-specific documentation and saved the S02 Open WebUI adapter in its repository.

## Upcoming portfolio milestones
1. Continue S02's incremental, regression-tested association integration under its service-specific acceptance criteria.
2. Review S02's next technical acceptance criteria and security gate; **SEC-001 is planned, not implemented**.
3. Revisit the potential `ai-services-core` approach at every new verified solution milestone. Extract only after demonstrated reuse and applicable change control.
4. Continue customer/commercial validation separately; technical integration does not establish market demand or production readiness.

## Risks and boundaries
- Synthetic-data testing only until the planned outbound-data sensitivity/manual approval control is implemented and validated.
- Do not duplicate service-specific instructions or working-step details here; link to each service's own status.
- The approved architecture is in [architecture/baseline-v0.1.md](architecture/baseline-v0.1.md); authoritative cross-service decisions are in [decisions/decision-log.md](decisions/decision-log.md).

## Handoff routine
At the end of each meaningful work session, update the active service's `PROJECT-STATUS.md` with **last completed**, **current working step**, **next tiny action**, and **blockers**. Update this portfolio file only when portfolio milestones, priorities or the active service change. In a new chat, read both status files first.

## S02 Variant 1 documentation milestone — 2026-11-06
The [S02 Variant 1 case study](case-studies/S02-crm-data-quality-auditor.md) and technical documentation are finalized for portfolio review. Nine local tests were user-reported as passing. The report does not yet enumerate all successfully evaluated checks, so one technical MVP acceptance criterion remains open. Synthetic data only; SEC-001 and production readiness are not complete. Variant 2 comparison is planned.

## S02 Variant 1 acceptance — 2026-11-06
All seven synthetic-data portfolio MVP criteria are now recorded as met. The report lists evaluated checks and coverage limitations; the developer reported `Ran 11 tests ... OK` after the fix to rule-catalogue constants. The [case study](case-studies/S02-crm-data-quality-auditor.md) reflects acceptance. This does not imply SEC-001, independent CI, customer-data clearance or commercial readiness. Next: plan Variant 2 with shared synthetic evaluation inputs.
