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

## Known implementation gaps

Open WebUI/FastAPI compatibility, citations, Compose portability, cross-platform behavior, authentication/authorization, tenant isolation, logging, monitoring, backup, secrets management, licensing, and EU deployment need validation appropriate to the customer context.

## Security

Fail closed on absent/invalid sensitivity metadata; prohibit unapproved sensitive content in outbound embedding/generation calls; treat retrieved content as untrusted; avoid leaks through logs/errors/citations. Multi-user and company deployment requires separate security review.

## Change rule

Do not silently introduce or replace an infrastructure component. Create an Architecture Change Notice with business reason, existing-component alternatives, operational/security/cost impacts, and explicit decision.
