# Architecture change control

Status: Approved policy

For every proposed change record: ID, date, status, Add/Replace/Upgrade/Configure, triggering business requirement, options using baseline, proposed component, effect on maintenance/deployment/security/cost, experiment and acceptance criteria, final decision.

## Decision history
- AC-001: **Approved** — FastAPI as standard Python API boundary, integration still to be tested.
- D-002: **Approved** — one modular FastAPI application initially.
- D-003: **Approved** — Open WebUI default; UI additions require justification.

No other new infrastructure component is approved at this stage.

## Security requirement pending detailed design
- SEC-001: **Recorded, not implemented** — sensitivity tagging and manual approval for applicable operations involving tagged client data. Resolve scope and workflow design first. Any additional infrastructure requires its own architecture change notice.
