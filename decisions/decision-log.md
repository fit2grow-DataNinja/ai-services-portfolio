# Decision log

Status: Approved decisions and pending questions | 2026-10-21

| ID | Status | Decision |
|---|---|---|
| SC-001 | Approved | EU SME/mid-market focus; adjacent analytics/marketing/reporting/documentation domains |
| SC-002 | Approved | Shared AI skills and structured workflows both allowed; low-code/Python/SQL/APIs |
| SC-003 | Approved | Prefer EU hosting and EU-operable technologies |
| AR-000 | Approved | Architecture baseline v0.1 frozen for research; not production verified |
| AC-001 | Approved | FastAPI service API |
| D-002 | Approved | One modular FastAPI application initially |
| D-003 | Approved | Open WebUI default; alternatives require justification |
| CP-001 | Approved | Business outcome first; client-operated and provider-managed options |
| CP-002 | Approved | Client-operated solution with bounded recurring maintenance/advisory preferred where suitable |
| CP-003 | Approved | Avoid unnecessary app development when shared skill suffices |
| RS-001 | Approved | Platform-first evaluation and explicit architecture change notices |
| SEC-001 | Recorded planned requirement; implementation pending | Tag client-sensitive data and require manual approval for applicable tagged-data operations; enforcement must fail closed. Scope of approval gate remains to be decided. |

## Repository organization and S02 milestone (2026-10-26)

The portfolio is the authority for shared strategy, architecture, governance and catalog; service repositories own their own implementation and technical documentation. Revisit potential `ai-services-core` extraction at every verified solution milestone, but do not introduce it without demonstrated reuse and applicable change approval. S02's synthetic-data FastAPI/Open WebUI Workspace Tool integration is verified; SEC-001 and production readiness are not. See [S02 registry](../services/S02.md).

## Pending
Source-by-source current verification; service prioritization and difficulty calibration; customer interviews and pricing; skill sharing/licensing requirements by client platform; implementation tests; SEC-001 approval scope, tag taxonomy, approver roles and audit/retention design; final documentation taxonomy if future expansion requires changes.
