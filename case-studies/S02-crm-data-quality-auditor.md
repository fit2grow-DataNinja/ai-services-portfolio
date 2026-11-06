# S02 — CRM Data Quality Auditor
## Variant 1 case study: deterministic checks, AI-assisted explanation

**Status:** Variant 1 documentation finalized; one technical reporting acceptance criterion remains open · **November 2026**  
**Evidence:** [Implementation](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor) · [Architecture](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/architecture.md) · [Tests and validation](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md)

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

This distinction matters: **repeatable rule output does not automatically guarantee a faithful natural-language explanation**. It also creates a concrete comparison criterion for the future skill-based Variant 2: which audit and AI boundaries are enforced by executable code, and which depend on model instructions?

## Demonstration and verification

Two synthetic scenarios provide evidence of the implemented workflow:

| Scenario | Recorded outcome |
| --- | --- |
| Larger CRM export | **202 contacts**, **121 deals**, **92 medium-severity missing-owner findings** |
| Live Open WebUI three-file demonstration | **1 contact**, **1 deal**, **1 known association**, **0 findings** |

The 92 findings are records flagged for review under a pilot rule, **not 92 confirmed business errors**. The three-file conversational result was user-reported; no independent network-level trace was captured.

On **6 November 2026**, the developer reported **9 automated tests passing** with `python -m unittest discover -s tests -v`. The suite covers representative rules, invalid schemas and associations, API behavior, two-/three-file adapter forwarding, and a missing required attachment rejected before HTTP upload. See the [validation record](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md). This is local regression evidence, not independent fresh-environment or CI verification.

## MVP scope, deliberate exclusions and commercial readiness

The decision was to build a **credible, verifiable portfolio MVP**, not to disguise a prototype as a commercial service. Production security and privacy controls, authentication and isolation, deployment hardening, monitoring, full source-data completeness, customer-specific rule acceptance and commercial validation were considered but deliberately deferred.

In particular, **SEC-001 remains unimplemented**: no real customer CRM data may be used. Comprehensive freshness and close-date checks also require data not present in the current exports.

These are recorded decisions, not forgotten requirements. See [SDR-001: MVP scope](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/decisions.md), the [commercial-readiness backlog](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/commercial-readiness-backlog.md), and the [definition of done](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/definition-of-done.md).

## What this demonstrates—and what comes next

This project demonstrates translation of a business problem into explicit rules, separation of deterministic computation from AI explanation, API/tool integration, regression testing, and disciplined MVP scoping. It also surfaces an important AI-governance question: **how much of the desired model behavior is enforceable, rather than merely instructed?**

Variant 1 documentation and evidence review are complete. The report discloses checks that could not be evaluated, but does not enumerate every successfully evaluated rule; this remains one open technical acceptance criterion. No additional tests were run for documentation sign-off. A planned **Variant 2, using a ChatGPT Skill-based approach**, will be tested on shared synthetic inputs and compared on finding accuracy, repeatability, explanation faithfulness, AI controllability, setup/maintenance effort and data-exposure boundaries. Its execution capabilities and results are **not yet established**.

**Technical detail:** [Source](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/tree/main/s02) · [Tests](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/tree/main/tests) · [Security](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/security.md)
