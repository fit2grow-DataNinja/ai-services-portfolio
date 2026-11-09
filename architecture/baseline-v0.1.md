# Architecture baseline v0.1

Status: Approved design baseline; implementation partly planned | 2026-10-21

## Principles
P1. Each service is an independently testable module with explicit inputs/outputs and errors.
P2. Deterministic calculations and validations remain in tested code/SQL; AI interprets and documents results.
P3. Client customization is configuration-first; core code changes are exceptions.
P4. Backend enforces validation, sensitivity rules, outbound model access, and security controls. UI is not a security boundary.
P5. Avoid infrastructure proliferation. Justify additions/replacements through change control.

## Approved components and boundaries
- Python 3.11.5 initially; FastAPI as the standard service API (AC-001 approved).
- One modular FastAPI application initially, with separately testable service modules (D-002 approved).
- Open WebUI as default conversational UI; another UI only with explicit business justification (D-003 approved).
- Podman on development Mac; Docker-compatible, Compose-based deployment target; compatibility still to test.
- Python/SQL business logic and reusable skills.
- LlamaIndex for RAG only when relevant; embedded persistent Chroma for vector retrieval only when needed.
- Markdown as initial knowledge source, additional source types as service requirements justify.
- Hosted OpenAI API initially proposed for models; exact models, data handling, costs and EU processing must be verified before selection.
- Git for source versioning. No additional workflow orchestration platform initially.

## Logical flow
Open WebUI -> FastAPI boundary -> reusable service module / optional RAG module -> configured source adapters -> validated business deliverable. Model calls pass through backend policy enforcement. Source data, indexes, secrets and configuration remain separate from container images.

## Two delivery dimensions
Technology: shared client-platform skill OR technical application (when necessary).
Operations: client-operated with maintenance/advisory OR provider-managed with recurring deliverables.
The same business methodology can support multiple delivery forms; portability is a goal, not yet demonstrated.

## S02-specific validation update (2026-10-26)

The S02 synthetic-data pilot verified a local FastAPI audit endpoint and Open WebUI Workspace Tool attachment-to-multipart adapter. This resolves one narrow integration question, **not** platform-wide compatibility or production readiness. The hosted-model chat flow has **not** implemented SEC-001 outbound approval controls; only synthetic data is approved for this test. Technical details belong to the [S02 repository](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/architecture.md) after its documentation branch is merged.

## Known implementation gaps
Broader Open WebUI/FastAPI compatibility, citations, Compose portability, cross-platform behavior, authentication/authorization, tenant isolation, logging, monitoring, backup, secrets management, licensing, and EU deployment need validation appropriate to the customer context.

## Security
Fail closed on absent/invalid sensitivity metadata; prohibit unapproved sensitive content in outbound embedding/generation calls; treat retrieved content as untrusted; avoid leaks through logs/errors/citations. Multi-user and company deployment requires separate security review.

## Sensitive-data tagging and manual approval — planned requirement
Client-sensitive data is intended to be identified with sensitivity tags. When a proposed operation involves tagged sensitive data, the workflow must hold the affected operation for manual review/approval before any otherwise-restricted external disclosure or processing. This is a **planned control, not an implemented or tested capability**.

- Enforce tagging and approval decisions in the backend, not only in the UI.
- Missing, invalid, or uncertain sensitivity metadata must fail closed; absence of a tag alone does not establish that data is safe.
- Check relevant outbound pathways separately, including embedding and generation, as applicable.
- Approval must be scoped to the data and proposed use, with an auditable decision; rejection blocks the operation. An approval cannot waive legal, contractual, or other mandatory restrictions.
- Minimize sensitive content in logs, review requests, and approval records.
- **Unresolved design scope:** whether manual approval is required only for external model/provider transmission or for local access/processing as well; who may approve; tag taxonomy and inheritance; approval validity, revocation, and storage; operational impact.
- Any new UI, approval service, storage component, or infrastructure needed for implementation requires a separate architecture change notice and explicit approval. No additional component is approved by recording this requirement.
- This portfolio-level statement does **not** change the separate RAG-MVP repository or assert that its implementation has been updated.

## Change rule
Do not silently introduce or replace an infrastructure component. Create an Architecture Change Notice with business reason, existing-component alternatives, operational/security/cost impacts, and explicit decision.
