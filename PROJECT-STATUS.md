# Project status — AI Services Portfolio

**Last updated:** 2026-11-09  
**Status:** S02's synthetic-data portfolio MVP and two-variant comparison are complete and closed. The portfolio is in public-readiness review.  
**Purpose:** Portfolio-level handoff. Service implementation details remain in their respective repositories.

## Completed portfolio milestone

- S02 Variant 1 (FastAPI/Open WebUI) and Variant 2 (ChatGPT Skill/Python) are complete and accepted for the defined synthetic-data scope.
- The portfolio comparison is complete; see the [S02 case study](case-studies/S02-crm-data-quality-auditor.md).
- The [S02 service overview](services/S02.md) records current evidence and boundaries.
- Portfolio architecture, governance, service use cases, and improvement opportunities are maintained in this repository; implementation code and detailed technical documentation live in the service repositories.

## Evidence and boundaries

- Variant 1 met 7/7 documented portfolio MVP criteria; its 11-test local pass was user-reported.
- Variant 2 includes a 17-test suite with fresh-checkout execution confirmed by the owner, reported issue-level parity on the shared synthetic scenario, and owner-confirmed successful use by a second ChatGPT user.
- Evidence details and limitations are linked from the case study and variant validation records.
- Both variants use synthetic data only. SEC-001 is not implemented; neither variant is production-ready or commercially validated. The missing-owner policy remains provisional.

## Current portfolio focus

Continue the public-readiness review: reconcile remaining status and handoff documents, settle repository licensing and historical-contact details, and prepare a publication checklist. Repository visibility changes require separate approval.

## Portfolio standards

- [Definition of done](governance/definition-of-done.md)
- [Regression-testing standard](validation/regression-testing.md)
- [Architecture baseline](architecture/baseline-v0.1.md)
- [Cross-service decision log](decisions/decision-log.md)

## Handoff

The S02 MVP is closed; do not reopen its development as part of portfolio presentation work. Future services may use documented improvement opportunities and shared-core review, but reuse should be demonstrated before extracting common components. No customer demand, revenue, production readiness, or commercial validation is claimed.
