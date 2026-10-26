# Project status — AI Services Portfolio

**Last updated:** 2026-10-26  
**Status:** Active development; S02 is the current service.  
**Purpose:** Quick handoff for future work sessions. This file owns portfolio-level progress only. Service implementation details live in the respective service repositories.

## Current focus
- **Active service:** [S02 — CRM Data Quality & Freshness Auditor](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor).
- **Authoritative working step:** [S02 PROJECT-STATUS.md](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/PROJECT-STATUS.md).
- **Portfolio next action:** Support S02 source-code transfer and reproducible validation. Do not expand scope or modify the approved architecture without approval.

## Completed
- Approved architecture v0.1 documented: modular Python 3.11.5/FastAPI, Open WebUI, Podman development, deterministic audit rules and hosted AI explanation.
- Established portfolio and S02 repositories and reciprocal documentation links.
- Recorded verified synthetic-data S02 standalone API and Open WebUI Workspace Tool integration.
- Adopted single-source-of-truth ownership and mandatory shared-core review at each verified solution milestone.
- Created service-specific documentation and saved the S02 Open WebUI adapter in its repository.

## Upcoming portfolio milestones
1. Complete S02 source transfer and rerun reproducible tests from the repository.
2. Review S02's next technical acceptance criteria and security gate; **SEC-001 is planned, not implemented**.
3. Revisit the potential `ai-services-core` approach at every new verified solution milestone. Extract only after demonstrated reuse and applicable change control.
4. Continue customer/commercial validation separately; technical integration does not establish market demand or production readiness.

## Risks and boundaries
- Synthetic-data testing only until the planned outbound-data sensitivity/manual approval control is implemented and validated.
- Do not duplicate service-specific instructions or working-step details here; link to each service's own status.
- The approved architecture is in [architecture/baseline-v0.1.md](architecture/baseline-v0.1.md); authoritative cross-service decisions are in [decisions/decision-log.md](decisions/decision-log.md).

## Handoff routine
At the end of each meaningful work session, update the active service's `PROJECT-STATUS.md` with **last completed**, **current working step**, **next tiny action**, and **blockers**. Update this portfolio file only when portfolio milestones, priorities or the active service change. In a new chat, read both status files first.
