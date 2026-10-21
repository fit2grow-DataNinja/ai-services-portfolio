# RAG MVP reference architecture

Status: Existing verified setup + planned features, per owner-provided design

## Verified on development Mac

Git repository; Python 3.11.5 and `.venv/`; Podman runs; Open WebUI container launched and accessible at `http://localhost:3000`; application data in named Podman volume `open-webui`; bound to loopback (`127.0.0.1`).

## Planned, not yet verified

Markdown ingestion/metadata, LlamaIndex backend, persistent Chroma, embeddings and retrieval, evidence inspection/citations/abstention, sensitivity filtering before hosted model calls, incremental indexing, tests/evaluation dataset, Open WebUI-to-backend integration, Compose deployment.

## Intended RAG flow

Markdown -> discover/parse metadata -> chunk with source references -> sensitivity policy -> approved embeddings/index -> user query via Open WebUI/FastAPI -> retrieve/filter evidence -> hosted model if allowed -> cited answer or abstention.

## Open questions

Integration/API contract and citation rendering; exact embedding/generation models; sensitivity metadata policy; retrieval baseline and metrics; handling of updates/deletions; licensing and data handling. Chroma remains embedded unless separation has a demonstrated benefit.

## Future company requirements

Authentication, authorization, document-level permissions, tenant isolation, audit logs, operational monitoring, incident response, backup and security review.

This reference is not evidence that the RAG application is complete.
