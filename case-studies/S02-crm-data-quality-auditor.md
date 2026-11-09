# S02 — CRM Data Quality Auditor
## Two-variant portfolio case study: deterministic checks, AI-assisted explanation

**Status:** **S02 portfolio MVP complete and closed (9 November 2026): both variants accepted for the defined synthetic-data scope.** Variant 1 met 7/7 documented MVP criteria; Variant 2 was accepted on the recorded implementation, user-confirmed regression/parity/reuse evidence and documentation-access test. Neither variant is production-ready.  
**Evidence:** [Variant 1 implementation](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor) · [Variant 1 validation](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md) · [Variant 2 implementation](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor-skill) · [Variant 2 validation](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor-skill/blob/main/docs/validation.md)

> **Scope:** Self-directed demonstration using synthetic CRM exports. No customer deployment, validated commercial impact or production-readiness claim.

## Business challenge

Sales and operations teams depend on trustworthy CRM data. Missing deal owners, duplicate contact information, invalid values and inconsistent relationships can undermine pipeline reporting and create manual review work. The objective was to identify **specific, reviewable data-quality findings** and explain them in business language—without letting an AI model invent the underlying audit results.

## Solution and workflow

Variant 1 combines a small **Python/FastAPI** auditing service with an **Open WebUI Workspace Tool** and an AI explanation layer.

```text
Synthetic contacts.csv + deals.csv [+ associations.csv]
                    |
          Open WebUI Workspace Tool
                    |
             FastAPI POST /audit
                    |
         Deterministic Python rules
                    |
     ZIP: summary.json, issues.csv, report.md
                    |
        Workspace Tool reads report output
                    |
         AI-assisted explanation in chat
```

The service returns structured audit artifacts; the Open WebUI Workspace Tool passes the relevant report content to the model for explanation.

The standalone API works independently of Open WebUI. The Workspace Tool is the validated conversational integration; the direct OpenAPI upload path was not successful.

## Deterministic audit scope

The implemented rules examine missing or duplicate record identifiers; missing, invalid or repeated contact emails; missing or repeated deal names; unknown deal stages; invalid deal amounts; missing amounts at Negotiation; missing owners from Qualified onward; and references to unknown contacts or deals in optional association files.

Findings identify the affected record, rule, severity and reason. The missing-owner requirement is a **provisional business-policy hypothesis**, not a universal CRM rule. The service does not edit source records.

**Coverage is explicit:** A partial association file can validate references present in it but cannot prove missing relationships. Freshness and original close-date reconciliation are not evaluated without extract timestamps and original source values.

## AI responsibilities, guardrails and trust boundaries

The architectural distinction is central to this use case: **Python decides what the audit found; AI explains the supplied results.** However, not every intended AI boundary is technically enforced.

| Boundary | Mechanism and actual status |
| --- | --- |
| **Audit decisions and severity** | **Software-enforced separation:** deterministic Python rules compute findings; the model does not execute or modify those rules through this workflow. |
| **Information supplied to AI** | **Adapter-controlled:** the tool returns the structured summary and report text, not the ZIP itself or separate `issues.csv` rows. This is a defined tool-response boundary, not a comprehensive data-leakage control. |
| **Read-only behavior** | **Tool capability limit:** this workflow audits uploaded exports and exposes no CRM write operation. |
| **Faithful explanation** | **Behavioral expectation:** the model should summarize supplied findings, avoid inventing new violations and preserve coverage caveats. Instructions alone cannot guarantee this. |
| **Independent explanation verification** | **Not implemented:** no automated checker validates each model statement against the deterministic output. |
| **Sensitive-data handling** | **Not implemented:** the planned SEC-001 outbound-data sensitivity and manual-approval gate is absent. **Synthetic data only.** |

This distinction matters: **repeatable rule output does not automatically guarantee a faithful natural-language explanation**. The two-variant comparison therefore distinguishes boundaries enforced by executable code from those dependent on model instructions.

## Demonstration and verification

Two synthetic scenarios provide evidence of the implemented workflow:

| Scenario | Recorded outcome |
| --- | --- |
| Larger CRM export | **202 contacts**, **121 deals**, **92 medium-severity missing-owner findings** |
| Live Open WebUI three-file demonstration | **1 contact**, **1 deal**, **1 known association**, **0 findings** |

The 92 findings are records flagged for review under a pilot rule, **not 92 confirmed business errors**. The three-file conversational result was user-reported; no independent network-level trace was captured.

On **6 November 2026**, the developer reported **11 automated tests passing** with `python -m unittest discover -s tests -v`. The suite covers representative rules, invalid schemas and associations, API behavior, two-/three-file adapter forwarding, a missing required attachment rejected before HTTP upload, and evaluated-check reporting with and without associations. See the [validation record](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md). This is local regression evidence, not independent fresh-environment or CI verification.

## MVP scope, deliberate exclusions and commercial readiness

The decision was to build a **credible, verifiable portfolio MVP**, not to disguise a prototype as a commercial service. Production security and privacy controls, authentication and isolation, deployment hardening, monitoring, full source-data completeness, customer-specific rule acceptance and commercial validation were considered but deliberately deferred.

In particular, **SEC-001 remains unimplemented**: no real customer CRM data may be used. Comprehensive freshness and close-date checks also require data not present in the current exports.

These are recorded decisions, not forgotten requirements. See [SDR-001: MVP scope](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/decisions.md), the [commercial-readiness backlog](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/commercial-readiness-backlog.md), and the [definition of done](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/definition-of-done.md).

## What this demonstrates—and what comes next

This project demonstrates translation of a business problem into explicit rules, separation of deterministic computation from AI explanation, API/tool integration, regression testing, and disciplined MVP scoping. It also surfaces an important AI-governance question: **how much of the desired model behavior is enforceable, rather than merely instructed?**

Variant 1 meets all seven documented portfolio MVP acceptance criteria. Its 11-test local suite was user-reported passing, with CI and independent fresh-environment verification deferred.

**Variant 2 is now implemented as a ChatGPT Skill with deterministic Python execution.** Its GitHub repository contains the Skill instructions, Python audit/CLI, three synthetic CSV header templates and a 17-case Python regression suite. Previously reported Skill exercises include the shared 202 contacts / 121 deals / 92 medium missing-owner findings scenario, matching issue-level audit results in two ChatGPT conversations, and successful header-only three-file execution (zero findings). The owner confirmed successful execution of the 17-test suite from a fresh repository checkout on 8 November 2026; raw checkout logs, Python version and tested commit SHA were not supplied. These are user-reported evidence, not independently captured runs.

## Business comparison — advantages, disadvantages and when to choose each variant

The two approaches address the same business problem: identify reviewable CRM data-quality issues and explain them without allowing AI to invent the audit findings. The business decision is therefore less about which variant detects more issues in the shared synthetic scenario, and more about **how the organization wants to operate the workflow**.

| Business consideration | Variant 1 — dedicated audit service | Variant 2 — ChatGPT Skill |
| --- | --- | --- |
| **Primary advantage** | Clearer path to a centrally operated, standardized audit service and other software integrations | Lightweight, conversational, on-demand audit experience without operating a separate audit API |
| **Primary disadvantage** | Additional service infrastructure, integration and maintenance responsibility | Depends on ChatGPT Skill availability and execution environment; central rollout/update governance is not yet established |
| **Getting started** | Requires setup of the service and chat adapter | Potentially simpler for people already using ChatGPT; setup effort has not been measured |
| **Working with colleagues** | Shared-service architecture is a plausible fit, but organization-wide operation has not been proven | **Successfully tested by a second ChatGPT user with matching deterministic audit results, as confirmed by the project owner**; centrally managed version updates remain untested |
| **Standardization and oversight** | Better architectural fit for a centrally managed business process, subject to future security/operations work | Suitable for distributed, user-initiated checks; consistent Skill release governance needs separate validation |
| **Future integrations** | More direct architectural path to APIs, scheduled jobs and other systems | Good fit for ChatGPT-first workflows; automation and external integrations would require additional design |
| **Costs and maintenance** | Hosting, integration and operational maintenance are likely cost drivers | ChatGPT access, Skill upkeep and platform/runtime constraints are likely cost drivers; no total-cost comparison has been measured |
| **Business outcome demonstrated** | Synthetic deterministic audit with conversational explanation | Same synthetic audit scenario with reported issue-level parity and user-confirmed cross-user reuse |

### Advantages, trade-offs and practical fit

**Variant 1 advantages:** more flexibility for integration and central operational control. **Trade-offs:** greater infrastructure, configuration and ongoing support burden. It is the more natural candidate for a company planning a centrally managed, repeatable audit service, but this is an architectural assessment—not a validated production deployment.

**Variant 2 advantages:** a simpler user-facing path for people who already work in ChatGPT; the Skill has also been used successfully by a second ChatGPT user with matching audit results. **Trade-offs:** reliance on ChatGPT execution capabilities and unresolved centralized release/version governance. It is the more natural candidate for occasional or team-led, on-demand reviews, subject to organizational access and security requirements.

**Illustrative business scenarios:**
- A **solo sales-operations analyst** checking occasional synthetic exports would likely favor Variant 2's conversational workflow.
- A **sales team** needing centrally scheduled, governed audits may favor Variant 1's service architecture; neither MVP currently implements that full operational process.
- A **company integrating CRM data-quality checks into other business systems** would likely favor Variant 1's API-oriented design, while weighing integration and maintenance costs.

**Decision guidance:** Prefer Variant 2 for lightweight ChatGPT-first, user-initiated auditing; prefer Variant 1 when central service operation and future system integration dominate. These are reasoned recommendations, **not measured business advantages**. Neither variant is approved for real customer CRM data: SEC-001 is not implemented, and neither is production-ready.

## Portfolio MVP closure (2026-11-09)
The S02 two-variant evaluation is **closed at the synthetic portfolio MVP level**. Variant 1's 7/7 acceptance and reported 11-test local pass remain the baseline. Variant 2 has committed deterministic Python/Skill implementation, a 17-case regression suite with owner-confirmed fresh-checkout execution, reported issue-level parity on the 202/121/92 synthetic case, and owner-confirmed successful reuse by a second ChatGPT user. The approved ChatGPT user guide was incorporated into the Skill package; the owner manually added it to the installed Skill and supplied a documentation-only response that correctly cited `user-guide.md`, listed required/optional CSV headers and reported no audit execution. The installed editor flattened the uploaded guide to the Skill root, so its `SKILL.md` reference was manually adjusted; the GitHub package retains `references/user-guide.md`.

**Evidence boundary:** User confirmations and shared responses are not independently captured runtime transcripts. No centrally managed Skill update propagation, comprehensive AI-explanation fidelity verification, CI, SEC-001 enforcement, or production security has been demonstrated. Approach B GitHub-to-ChatGPT packaging/publishing is explicitly deferred beyond MVP. Closure is not commercial authorization.

## Two-variant comparison — current evidence

| Dimension | Variant 1: FastAPI + Open WebUI | Variant 2: ChatGPT Skill + Python |
| --- | --- | --- |
| Deterministic audit | Python service invoked via API and Open WebUI Workspace Tool | Python script invoked via Skill runtime |
| Business-rule scope | Reference rule IDs, severity and explicit coverage disclosure | Equivalent rules and coverage targeted; populated issue-level parity reported |
| Structured output | ZIP contains `summary.json`, `issues.csv`, `report.md` | Files `summary.json`, `issues.csv`, `report.md` written locally |
| Regression tests | 11 passed, user-reported local run | 17-case suite; local pass reported and fresh-checkout execution user-confirmed |
| Conversation path | Open WebUI Workspace Tool demonstrated | ChatGPT Skill audit exercises reported in two conversations |
| Multi-user distribution/version consistency | Not a Variant 1 MVP acceptance gate | Second-user sharing and matching results owner-confirmed; centrally aligned versions and automated updates untested |
| CI / commercial security | CI deferred; SEC-001 not implemented | CI deferred; SEC-001 not implemented |

**Interpretation:** The available evidence supports functional feasibility and reported deterministic-result parity on shared synthetic cases. It does **not** establish independent clean-environment audit parity, model-explanation faithfulness, universal multi-user installation or centrally enforced version synchronization, measured setup/maintenance cost, or production safety. Sharing a similar Python rule engine compares integration/orchestration, not independent algorithmic accuracy. The owner has additionally confirmed that a second ChatGPT user successfully ran the Skill and received matching results; this supports practical cross-user reuse, but does not establish centralized release/version governance. Final portfolio acceptance retains these limitations; they are documented post-MVP questions, not unresolved MVP gates.

Both variants intentionally exclude real customer data, complete freshness/close-date reconciliation, inference of missing associations from partial exports, production hardening, GitHub CI, and commercial rollout from their portfolio MVP scope. The missing-owner policy remains provisional. Proposed future detection → review → approve → notify → verify functionality in Variant 2 is **not implemented**. See [Variant 2 roadmap](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor-skill/blob/main/docs/future-improvements-and-commercial-readiness.md).

The two source repositories remain the technical authorities; **this case study is the one portfolio-level use-case narrative**, not a duplicate installation or operational guide.

**Technical detail:** [Source](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/tree/main/s02) · [Tests](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/tree/main/tests) · [Security](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/security.md)
