# Documentation standards

Status: Proposed convention

Use Markdown, descriptive kebab-case filenames, stable service IDs (`S01`, etc.) and decision IDs (`AC-001`, `D-002`, etc.). Record status, date, owner when known, assumptions, evidence, open questions, and next validation step.

Distinguish: **agreed decision**, **verified implementation**, **planned implementation**, **hypothesis**, and **external evidence**. An architecture approval is not proof of a running deployment. Do not copy private client data or secrets into the portfolio repository.

For external claims record source URL, publisher, publication/update date if available, date accessed, exact claim, scope/limitations, and confidence. Recheck time-sensitive vendor, pricing, security, and regulatory claims before a commercial proposal.

Keep client-specific configurations, data, credentials, and deliverables separate from generic portfolio templates. Use change requests for any new infrastructure component or component replacement.

## Repository ownership and single source of truth

Maintain a hub-and-spoke repository hierarchy: this portfolio repository owns cross-service strategy, governance, approved architecture and service catalog; each service repository owns its implementation, tests, runbooks and service-specific technical documentation. Every component and document must have one authoritative home. Other repositories link to it rather than copying it. Keep cross-repository links reciprocal where useful.

Prefer service-local code until a shared capability is demonstrated in at least two solutions. Treat a potential `ai-services-core` repository as a future option, **not an approved or existing component**. Do not extract utilities or introduce shared runtime dependencies solely in anticipation of reuse. Any extraction affecting the approved architecture must follow architecture change control.

**Mandatory solution-readiness checkpoint:** Whenever a new service/solution reaches a working, verified milestone, explicitly remind the project owner to revisit the `ai-services-core` approach. Review candidate common functions, integrations, tests and documentation; identify duplication and ownership; decide to retain locally, link to existing shared material, or propose extraction through change control. Record the outcome, including a decision to defer, in the decision log and relevant service documentation.
