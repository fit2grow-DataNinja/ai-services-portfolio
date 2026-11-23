# Balázs Bogda
## Data Analytics & Applied AI Solutions Consultant

I combine business analysis and consulting experience with hands-on analytics, data quality, and applied AI implementation. I help organizations improve measurement, reporting, and operational workflows by translating business needs into practical, testable solutions.

**Budapest, Hungary** · [LinkedIn](https://www.linkedin.com/in/balazsbogda/)

## Profile

I have 6+ years of focused experience in data analytics, business intelligence, and digital measurement, backed by earlier business analysis and systems consulting roles. My work spans business requirements, data validation, analytics implementation, process improvement, and applied AI prototypes built with Python, APIs, and LLM integrations.

## What I bring

- **Business consulting and analysis:** requirements definition, process improvement, implementation support, and cross-functional delivery.
- **Data analytics and BI:** SQL, BigQuery, Power BI, Tableau, Looker Studio, KPI reporting, and customer analytics.
- **Data quality and measurement:** SQL-based validation, ETL data checks, GA4, event specifications, measurement audits, and web and app tracking.
- **Applied AI implementation:** Python, FastAPI, APIs, LLM integrations, and AI-assisted analytics and workflow prototypes.

## About this portfolio repository

This repository is the portfolio-level home for my business solutions. It lists the solutions and contains their use-case documents, portfolio architecture and governance, and documented improvement opportunities.

As the portfolio develops, reusable core systems and solution components may also be maintained here when their reuse is justified. Individual service implementations and their technical documentation are maintained in separate repositories linked from the relevant solution and use-case pages. This keeps the business context and use cases together at portfolio level while allowing each implementation to be documented and maintained independently.

## Documentation hierarchy

This portfolio is the showcase and navigation layer for the AI solutions I build. The solution repositories are the technical homes for their implementations and detailed project evidence.

The supporting knowledge and method are organized separately:

1. **AI Governance Frameworks** — reusable, source-grounded governance knowledge, framework notes, and governance methods. See the [AI Governance Frameworks repository](https://github.com/fit2grow-DataNinja/ai-governance-frameworks).
2. **Organizational Readiness** — a planned central repository for reusable ways to assess the capabilities an organization needs to support a specific AI use case.
3. **AI Enablement Method** — a planned central repository describing how governance knowledge, organizational readiness, and use-case requirements are brought together into an assessment and action plan.
4. **Applied use cases and implementations** — project-specific application of the method, with technical implementation, evidence, controls, limitations, and status documented in the relevant solution repositories. Portfolio case studies summarize the business context and link to the detailed project records.
5. **AI Services Portfolio** — this repository presents the built solutions and provides cross-project context and navigation; it is not a second technical home for their implementations.

The two planned repositories are not yet created. Until then, this README records the intended structure; it does not claim those materials or assessments are implemented.

## Portfolio solutions and use cases

### S02 — CRM Data Quality Auditor

A completed, two-variant **synthetic-data portfolio MVP** exploring how deterministic CRM data checks can be paired with AI-assisted explanations.

The portfolio use case describes the business problem, both solution approaches, available evidence, trade-offs, and limitations. The separate implementation repositories contain the technical source, tests, and implementation documentation.

- [S02 portfolio use case and comparison](case-studies/S02-crm-data-quality-auditor.md)
- [Portfolio service overview](services/S02.md)
- [Variant 1 — FastAPI and Open WebUI implementation](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor)
- [Variant 2 — ChatGPT Skill and Python implementation](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor-skill)

Both variants were completed for the defined synthetic-data scope. The shared synthetic case recorded 202 contacts, 121 deals, and 92 medium-severity missing-owner findings; those findings are review flags under a provisional rule, not confirmed business errors. Test and parity evidence is documented in the project records, with some execution and cross-user results reported by the project owner. Neither variant is production-ready, approved for customer CRM data, or commercially validated.

### AI-assisted A/B testing analysis and reporting

Originally developed an AI-supported approach for analyzing experimentation results and preparing structured reports, combining digital experimentation expertise with practical AI workflows. **Recreation is in progress**; this portfolio will be updated with the recreated project when it is ready to present.

## Separate learning project

### RAG MVP

A learning project exploring retrieval-augmented generation for knowledge management. It is intended to support my own knowledge management and to explore how the approach could extend to internal knowledge management within a company.

- [View the RAG MVP repository](https://github.com/fit2grow-DataNinja/rag-mvp)

## Selected consulting outcomes

At Fit2Grow, I have delivered analytics, BI, digital measurement, and process improvement work, including:

- Standardized digital measurement specifications across web, Android, and iOS, saving approximately 4–5 hours per specification in the original workflow.
- Implemented SQL-based quality checks on raw GA4 data in BigQuery and business-relevant ETL datasets.
- Documented ETL processes with version tracking and issue records to improve change traceability.

Selected clients: Columbus McKinnon EMEA · SolarKit Europe Ltd · BigFish Ltd

## Tools and methods

**Analytics and BI:** SQL, BigQuery, Power BI, Tableau, Looker Studio, GA4  
**Applied AI and implementation:** Python, FastAPI, APIs, LLM integrations, GitHub  
**Methods:** business analysis, requirements definition, data validation, digital measurement, experimentation, process improvement

## Portfolio approach

This portfolio is evolving through documented projects and learning. Further improvement opportunities are identified and recorded for consideration as new needs arise; they are not claims of implemented capabilities or committed work.

Across future solutions, selected architecture components and systems are intended to form a reusable core, while other components remain specific to each project. The boundary will be guided by demonstrated reuse and project needs, with shared components introduced when justified; this README does not imply that a shared core already exists.

Repositories document project scope, implementation, available validation evidence, and known limitations. Implemented behavior, test results, user-reported outcomes, and planned work are identified separately. Portfolio prototypes are not presented as production deployments or commercially validated services.
