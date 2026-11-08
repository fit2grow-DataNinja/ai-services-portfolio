# S02 — CRM Data Quality Auditor
## Two-variant portfolio case study: deterministic checks, AI-assisted explanation

**Status:** Variant 1 synthetic-data portfolio MVP accepted (7/7 criteria); Variant 2 Skill/Python implementation and reported regression/parity evidence documented, with final comparison and review still open. Neither variant is production-ready · **November 2026**  
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

This distinction matters: **repeatable rule output does not automatically guarantee a faithful natural-language explanation**. It also creates a concrete comparison criterion for the future skill-based Variant 2: which audit and AI boundaries are enforced by executable code, and which depend on model instructions?

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

## Two-variant comparison — current evidence

| Dimension | Variant 1: FastAPI + Open WebUI | Variant 2: ChatGPT Skill + Python |
| --- | --- | --- |
| Deterministic audit | Python service invoked via API and Open WebUI Workspace Tool | Python script invoked via Skill runtime |
| Business-rule scope | Reference rule IDs, severity and explicit coverage disclosure | Equivalent rules and coverage targeted; populated issue-level parity reported |
| Structured output | ZIP contains `summary.json`, `issues.csv`, `report.md` | Files `summary.json`, `issues.csv`, `report.md` written locally |
| Regression tests | 11 passed, user-reported local run | 17-case suite; local pass reported and fresh-checkout execution user-confirmed |
| Conversation path | Open WebUI Workspace Tool demonstrated | ChatGPT Skill audit exercises reported in two conversations |
| Multi-user distribution/version consistency | Not a Variant 1 MVP acceptance gate | Comparison criterion; untested for Skill installation, sharing and centrally aligned versions |
| CI / commercial security | CI deferred; SEC-001 not implemented | CI deferred; SEC-001 not implemented |

**Interpretation:** The available evidence supports functional feasibility and reported deterministic-result parity on shared synthetic cases. It does **not** establish independent clean-environment audit parity, model-explanation faithfulness, guaranteed multi-user installation/version synchronization, measured setup/maintenance cost, or production safety. Sharing a similar Python rule engine compares integration/orchestration, not independent algorithmic accuracy. Further comparison and final portfolio acceptance should retain these limitations.

Both variants intentionally exclude real customer data, complete freshness/close-date reconciliation, inference of missing associations from partial exports, production hardening, GitHub CI, and commercial rollout from their portfolio MVP scope. The missing-owner policy remains provisional. Proposed future detection → review → approve → notify → verify functionality in Variant 2 is **not implemented**. See [Variant 2 roadmap](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor-skill/blob/main/docs/future-improvements-and-commercial-readiness.md).

The two source repositories remain the technical authorities; **this case study is the one portfolio-level use-case narrative**, not a duplicate installation or operational guide.

**Technical detail:** [Source](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/tree/main/s02) · [Tests](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/tree/main/tests) · [Security](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/security.md)
