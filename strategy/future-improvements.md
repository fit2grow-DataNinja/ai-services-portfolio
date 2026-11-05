# Future improvements — reusable AI business-solution framework

**Status:** Proposed / deferred — idea register, not an approved architecture change or implementation commitment  
**Recorded:** 2026-11-05  
**Owner:** Portfolio owner (to confirm at selection)  
**Source:** Review of the supplied *Claude Client Acquisition Team: 200 Roles in 20 Functions* framework (20 role files and supporting operational documents). This is an adaptation of its design patterns, not an adoption of its 200 Claude prompts.  
**Scope:** Cross-service portfolio design; individual implementations remain in service repositories.

## Purpose and use

Preserve eight candidate design improvements so they can be evaluated **one at a time when a real service need arises**. Nothing here changes the approved architecture v0.1, the current S02 delivery priorities, or the planned (not implemented) SEC-001 control.

When selecting an item:
1. Name the concrete service, business problem, and expected measurable benefit.
2. Check what already exists in the portfolio and service repository; avoid duplicated abstractions.
3. Define scope, alternatives (including no AI / deterministic logic), data sensitivity, and evidence required.
4. Prototype locally in the service repository where possible; validate with tests and human review.
5. If the change affects approved architecture or creates shared infrastructure, use [architecture change control](../architecture/change-control.md) and record the decision in [decision log](../decisions/decision-log.md).
6. At each verified service milestone, revisit potential shared-core extraction as required by [documentation standards](../governance/documentation-standards.md); do not extract before demonstrated reuse in at least two solutions.
7. Update the row's status, decision link, evidence, and next step. A proposal is not a verified capability.

## Candidate improvement register

| ID | Element | Proposed portfolio adaptation | First possible application | Status |
|---|---|---|---|---|
| FI-01 | Business function structure | Organize service opportunities by customer business domains and outcomes; avoid forcing every solution into an agent taxonomy. | Map Sales/CRM, Marketing, Data/Reporting, Operations and Knowledge Management to existing [business areas](../strategy/business-areas.md). | Proposed / deferred |
| FI-02 | Specialized AI roles / capabilities | Define small, reusable task capabilities; decide per task whether AI, deterministic code, or human judgment is appropriate. | S02 audit findings explanation versus deterministic CRM checks. | Proposed / deferred |
| FI-03 | Standardized capability specifications | Add a common specification: purpose, trigger, required/optional inputs, outputs/schema, constraints, failure cases, tests, human approval, owner. | Extend [service specification template](../templates/service-specification.template.md) only when a real use case requires it. | Proposed / deferred |
| FI-04 | Shared business context | Version customer/business context with provenance, scope and sensitivity boundaries; avoid leaking client context across tenants or projects. | S02 client-specific configuration; later knowledge workflows. | Proposed / deferred |
| FI-05 | Structured workflows and handoffs | Define explicit step transitions, input/output contracts, missing-input handling and reviewer ownership; avoid premature multi-agent orchestration. | S02 audit → findings validation → explanation → reviewer-approved report. | Proposed / deferred |
| FI-06 | Evidence and traceability | Link claims to source records, label assumptions, preserve run context and distinguish verified findings from AI interpretations. | S02 audit evidence and report traceability. | Proposed / deferred |
| FI-07 | Human oversight and approval | Introduce risk-based review gates for external communication, data changes, sensitive exports and consequential recommendations. | SEC-001-sensitive data handling and approval design; **not implemented**. | Proposed / deferred |
| FI-08 | Quality assurance and validation | Validate schemas, deterministic rules, model outputs and complete workflows; track failure modes and reproducibility. | S02 regression tests and output validation. | Proposed / deferred |

## Selection worksheet (copy when activating an item)

- **Improvement ID / title:**
- **Decision status:** Proposed / Under evaluation / Approved / Deferred / Rejected / Implemented and verified
- **Service and repository:**
- **Problem / user / measurable outcome:**
- **Current implementation and gap:**
- **Alternatives:** No change / deterministic solution / AI-assisted solution / shared capability
- **Required inputs, output contract and evidence:**
- **Security, privacy, approval and operational risks:**
- **Dependencies and impact on architecture v0.1:**
- **Smallest validation experiment and acceptance criteria:**
- **Owner / reviewer:**
- **Decision-log or change-request link:**
- **Evidence / test results:**
- **Next action / revisit trigger:**

## Revisit triggers

- A service needs one of the capabilities to deliver an agreed customer outcome.
- Two verified solutions demonstrate the same cross-service requirement (consider shared-core review, not automatic extraction).
- A new verified service milestone triggers the mandatory shared-core checkpoint.
- An observed quality, traceability, security or handoff failure justifies a targeted improvement.

## Boundaries and open questions

- **Not approved:** no new platform, orchestration engine, agent fleet, shared repository, connector or infrastructure is authorized by this register.
- **Not verified:** the Claude framework's role structure is documented, but effectiveness in this portfolio is untested.
- **Open:** Which candidate first solves a validated business need? What is the smallest useful implementation? What existing repository should own it?
- **Source note:** The supplied framework uses a shared context brief, task-specific role cards, evidence ledger, handoff object, and human review. Its examples are illustrative and should not be treated as customer proof.
