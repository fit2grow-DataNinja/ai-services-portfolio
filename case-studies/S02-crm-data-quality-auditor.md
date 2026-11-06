# S02 — CRM Data Quality Auditor
## Variant 1 case study: deterministic auditing with AI-assisted explanation

**Project type:** Synthetic-data portfolio MVP · **Status:** Implemented and regression-tested; final portfolio acceptance review pending · **Date:** November 2026

**Technical evidence:** [Implementation repository](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor) · [Architecture](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/architecture.md) · [Validation record](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md) · [Source code](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/tree/main/s02)

> **Evidence boundary:** This is a self-directed demonstration with synthetic CRM data, not a client engagement. It does not establish production readiness, business impact, customer adoption, or commercial demand.

## The business challenge

CRM data quality affects how confidently sales and operations teams can interpret their pipelines. In exported contact and deal records, missing owners, duplicate identifiers, inconsistent values and broken relationship references can make reports less reliable and increase manual review work.

The challenge for this project was to produce a **repeatable, explainable audit** of common CRM export issues without requiring an AI model to judge the underlying data independently. The solution should identify concrete records for review, make its coverage limits visible and leave source records unchanged.

## The solution

Variant 1 is a small, locally operated Python application with a conversational explanation layer:

1. A user provides **contacts.csv** and **deals.csv**, optionally adding **associations.csv**.
2. A **FastAPI** endpoint receives the CSV files and runs deterministic Python validation rules.
3. The service returns a ZIP containing **summary.json**, **issues.csv** and **report.md**.
4. An **Open WebUI Workspace Tool** forwards chat attachments to the API, reads the structured summary and Markdown report, and makes those findings available for AI-assisted explanation.

**Responsibility boundary:** Python determines the findings and their severity. The AI model may summarize and explain those findings, but it is not the source of audit decisions. The tool is read-only with respect to CRM source records.

### Architecture at a glance

```text
Synthetic CRM CSV exports
  contacts.csv + deals.csv [+ associations.csv]
                    |
        Open WebUI Workspace Tool
                    |
           FastAPI POST /audit
                    |
        Deterministic Python rules
                    |
        summary.json | issues.csv | report.md
                    |
          ZIP response to adapter
                    |
     AI-assisted explanation in Open WebUI
```

The standalone FastAPI upload path is also usable without the conversational interface. A direct OpenAPI-based chat upload was attempted but failed to forward required multipart attachments (HTTP 422); the **Workspace Tool adapter** is the verified conversational integration path. See the [implementation architecture](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/architecture.md).

## What the audit checks

The current rule set includes:

- Missing or duplicate contact and deal record IDs.
- Missing, malformed or repeated contact email addresses.
- Missing or repeated deal names; unknown deal stages.
- Invalid, negative or non-finite deal amounts; missing amounts at the Negotiation stage.
- Missing deal owners from Qualified onward, under an explicitly **provisional pilot policy**.
- Association rows that reference contact or deal IDs absent from the supplied exports.

Findings identify the rule, severity, affected object and record, field, observed value and explanation. The rules are a demonstration catalogue, **not universal CRM policy**; in particular, a missing owner may be legitimate for a specific business.

## Demonstrated results

<details>
<summary>Evidence from two synthetic scenarios</summary>

| Scenario | Observed result | What it demonstrates |
| --- | --- | --- |
| Larger CRM sample | **202 contacts**, **121 deals**, **92 medium-severity findings**, all missing deal owners | Deterministic rules can flag a concrete review queue |
| Live three-file Open WebUI test | **1 contact**, **1 deal**, **1 known association**, **0 findings** | User-reported successful optional-association workflow and zero-finding output |

</details>

The 92 findings are **not 92 confirmed business errors**. They are records flagged under the pilot owner-assignment rule, requiring policy review. The live Open WebUI result is user-reported; it was not independently captured as a network-level multipart trace.

The output separates **audit findings** from **coverage information**. For example, a partial association reference file is useful for validating references present in that file, but cannot prove that deals absent from the file lack contacts in the CRM.

## Verification and engineering evidence

On **6 November 2026**, the developer reported **9 automated tests passing** with:

```bash
python -m unittest discover -s tests -v
```

The regression suite covers representative deterministic rule behavior, schema rejection, FastAPI uploads and responses, invalid association references, two-file and three-file adapter forwarding, missing-deal-owner detection and rejection of a missing required attachment before any HTTP upload.

Standalone API and Open WebUI integration milestones were also demonstrated using synthetic data. Test execution and integration observations are documented in the [validation record](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md). The recorded local results are evidence of those runs, **not a claim of independently reproduced deployment or CI validation**.

## MVP scope, deliberate exclusions and commercial readiness

An important design decision was to build **a credible portfolio MVP rather than a superficially production-ready product**.

The scope includes deterministic rules, explicit file handling, useful audit artifacts, conversational explanation, regression tests and honest documentation. It intentionally does **not** include all controls required to handle real customer CRM exports.

| Deliberately excluded or limited | Why it matters |
| --- | --- |
| **SEC-001 sensitivity classification and manual approval** | Not implemented; therefore **synthetic data only** and no real customer-data processing |
| Full association completeness | A partial reference export cannot support missing-association conclusions |
| Freshness and original close-date reconciliation | Reliable checks require extract timestamps, original values and documented transformation rules |
| Production deployment, monitoring, CI and operational hardening | Local development success does not establish portable or reliable production operation |
| Customer-specific business rules and commercial validation | Real policies, demand, pricing and acceptance remain unverified |

These items are **documented, not forgotten**. The [Scope Decision Record (SDR-001)](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/decisions.md) explains the MVP boundary; the [commercial-readiness backlog](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/commercial-readiness-backlog.md) records deferred requirements and future evidence expectations. The [definition of done](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/definition-of-done.md) distinguishes portfolio acceptance from production clearance.

## What this project demonstrates

**Business analysis:** Translate a broad CRM data-quality concern into a concrete set of reviewable rules, while marking policy assumptions.

**Solution design:** Separate reliable, testable audit computation from AI-assisted communication.

**Integration:** Connect a file-upload API to a conversational tool and distinguish working from unsuccessful integration paths.

**Verification:** Use synthetic fixtures and automated regression tests to protect core behavior and failure handling.

**Delivery judgment:** Define a realistic MVP, document what is excluded, and preserve a traceable path to commercial readiness.

## Next steps

The remaining **Variant 1 portfolio acceptance work** is a final review of report wording and coverage disclosures, followed by evidence and case-study sign-off. This case study is therefore a substantive **Variant 1 draft**, not a declaration that every acceptance checkbox has been closed.

A separate **Variant 2** will explore the same synthetic CRM audit scenario as a ChatGPT Skill-based workflow. Only after both variants have been exercised against shared inputs will the portfolio compare accuracy, repeatability, explainability, setup and maintenance effort, and security boundaries.

---

**Explore the evidence:** [S02 repository](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor) · [Tests](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/tree/main/tests) · [Validation](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/validation.md) · [Security boundaries](https://github.com/bb-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/security.md)
