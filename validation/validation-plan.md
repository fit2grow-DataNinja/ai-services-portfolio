# Validation plan

Status: Proposed; no tests executed

## Business-model validation
For each candidate compare: (A) competent employee with shared AI skill, (B) internally built integrated solution, (C) our external offering. Compare accuracy, repeatability, time to deploy, time to operate, access/integration, auditability, total cost, and maintenance.

## Reference pilot suggestion
Use existing A/B testing solution with fixed representative datasets and an expert-reviewed reference result. Compare skill-only output and structured solution on correctness, consistency, invalid-input handling, evidence traceability, human review and cost.

## Customer discovery
Interview prospective users and budget owners; document existing workflows, frequency, pain, internal skills, decision criteria, willingness to pay, support expectations, and actual purchasing constraints.

## Architecture tests
FastAPI/Open WebUI connection, tool/API contract, citation rendering, outbound sensitivity filtering, Compose on Podman and Docker, storage separation, secrets, recovery and client deployment controls.

## Sensitive-data approval validation (SEC-001; not yet tested)
Test tagged, untagged, missing-tag, conflicting-tag and incorrectly tagged inputs; approval, rejection, expiration/revocation, and unauthorized approver attempts; embedding and generation egress; log and error redaction; approval record auditability; and attempts to bypass checks through the UI or direct API. Define approval scope and authorized approvers before acceptance tests. Do not claim this control is operational until tested.

## Promotion gate
No 'validated commercial service' label without evidence of working implementation, credible business outcome, security/deployment fit, repeatable onboarding, and at least preliminary buyer evidence.

## Shared-core review at solution readiness

When a new solution reaches a verified working milestone, remind the owner to revisit the proposed `ai-services-core` approach. Compare the new solution with existing services for genuinely reusable functions, integration adapters, tests and documentation. Apply the single-source-of-truth rules in `governance/documentation-standards.md`; record the reuse/extraction/defer decision before marking the solution's documentation milestone complete. This is a review checkpoint, not authorization to create a new repository or modify the architecture.
