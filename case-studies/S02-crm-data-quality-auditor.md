# S02 — CRM Data Quality Auditor | Portfolio case study

**Status:** Draft outline; Variant 1 portfolio MVP completion in progress. Variant 2 comparison planned.  
**Implementation and test evidence:** [S02 technical repository](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor) · [Validation](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md) · [Definition of done](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/definition-of-done.md)

> This case study is a portfolio showcase, not a claim of customer deployment, commercial validation or production readiness. All demonstration data is synthetic.

## Business problem
CRM exports can contain incomplete contact details, duplicate identities, missing deal owners, inconsistent deal values and broken relationship references. The goal is to produce explainable, evidence-based quality findings without silently modifying source records.

## Variant 1 — Mini software with AI-assisted explanation
A deterministic Python auditor performs rule checks; FastAPI accepts CSV uploads and produces structured audit artifacts; an Open WebUI Workspace Tool passes attachments to the service and lets an AI model explain the deterministic report. The AI does not invent or calculate findings.

**Demonstrated synthetic results:** A larger sample with 202 contacts and 121 deals produced 92 medium-severity missing-deal-owner findings. A separate live three-file Open WebUI test reported one contact, one deal, one known association and zero findings. These are demonstration results, not customer outcomes.

## Verification and limitations
The local regression suite was reported as **7 tests passed** on 2026-11-06; see the [validation record](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md) for the evidence scope. Partial association exports cannot establish missing associations; freshness and original close-date reconciliation need additional source metadata. SEC-001 is not implemented, so customer data must not be used.

## MVP scope, deliberate exclusions and commercial readiness
The goal is to demonstrate business understanding, engineering implementation, API/tool integration, test discipline and sound scope decisions—not a commercially deployable product. The [S02 commercial readiness backlog](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/commercial-readiness-backlog.md) lists deliberately deferred security, privacy, operational, comprehensive business-rule and commercial acceptance work. The [S02 decision log](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/decisions.md) records the rationale.

## Variant 2 — ChatGPT Skill-based approach (planned)
Revisit the same synthetic CRM auditing scenario with a reusable skill workflow. Compare the two variants on accuracy, repeatability, explainability, setup and maintenance effort, and security boundaries. Do not claim equivalence until both are tested on shared inputs.

## Before publication as a finished case study
- [ ] Complete and verify the Variant 1 portfolio MVP acceptance criteria.
- [ ] Add a concise architecture visual or link to an existing verified diagram.
- [ ] Confirm all demonstration numbers and limitations against current evidence.
- [ ] Document Variant 2 results and the comparison after implementation.
- [ ] Edit the narrative for a business reader while keeping direct links to technical evidence.
