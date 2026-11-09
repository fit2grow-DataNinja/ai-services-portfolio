# Portfolio definition of done

**Status:** Working portfolio-wide completion standard.

Apply these criteria to every meaningful service feature, fix, integration, or milestone. A completed milestone is **not** a claim that the service is production-ready or commercially validated.

## Service change completion checklist
- [ ] Scope, expected behavior, exclusions, and acceptance criteria are explicit.
- [ ] Implementation respects the service's approved architecture and decisions.
- [ ] Automated tests cover new behavior and protect existing behavior against regression.
- [ ] Tests use synthetic or otherwise explicitly approved non-sensitive data; reusable fixtures are source-controlled where justified.
- [ ] Relevant tests have actually been run and their commands/results recorded. Unexecuted tests must not be reported as passed.
- [ ] Relevant failure paths and invalid inputs are checked; known limitations are documented.
- [ ] Security and privacy gates required for the intended data and environment have been implemented and verified. A synthetic-data milestone does not waive a future production gate.
- [ ] The service's own status and validation documentation reflect the outcome, evidence, and outstanding work.
- [ ] Portfolio status is updated **only** when a portfolio-level milestone, priority, active service, or standard changes.

## Portfolio-level completion checklist
- [ ] The cross-service change has an explicit purpose and scope.
- [ ] The authoritative portfolio document or reusable template is updated and linked.
- [ ] Any architecture change follows the existing approval/change-control process.
- [ ] Cross-service reuse is demonstrated before extracting shared implementation into a common core.
- [ ] Portfolio status records the completed governance or portfolio milestone without copying service-level implementation details.

## Regression-testing convention
See [Regression testing](../validation/regression-testing.md) and [Service test layout template](../templates/service-test-layout.template.md).

## Service-specific acceptance criteria
Each service owns its concrete definition of done for current milestones. For S02, see [S02 definition of done](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/docs/definition-of-done.md). Service-specific criteria take precedence for technical behavior while remaining subject to portfolio-wide governance and security requirements.
