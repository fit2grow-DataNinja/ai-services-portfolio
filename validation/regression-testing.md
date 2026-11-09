# Portfolio regression-testing standard

**Purpose:** Ensure previously verified service behavior remains correct as new features and fixes are introduced.

## Policy
1. Before changing behavior, identify the working path that must remain supported.
2. Add a regression test for each new feature or fixed defect. Prefer a test that demonstrates the defect or missing feature before implementing the fix.
3. Run the focused tests and relevant broader suite after the change. Record actual outcomes, not assumed results.
4. Keep tests deterministic and isolated from running services when unit tests can mock external I/O. Add integration tests when actual boundaries need verification.
5. Use synthetic inputs until the service's required sensitivity, approval, and security controls are implemented and verified.
6. Store small shared fixtures in the service repository under `tests/fixtures/` **when reused**. Prefer inline/temporary data for one-off scenarios; avoid duplicating `samples/` demonstration datasets.
7. Preserve negative tests for missing inputs, malformed data, and security-related failures where applicable.
8. Add automated CI test execution when dependencies and environment requirements are reproducible. Until then, manual test evidence is acceptable if accurately recorded.

## Ownership
- **Portfolio repository:** this policy and the [service test layout template](../templates/service-test-layout.template.md).
- **Service repositories:** runnable tests, fixtures, execution commands, results, and milestone-specific acceptance criteria.
- **S02 example:** [adapter regression tests](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/tests/test_openwebui_adapter.py) and [fixture policy](https://github.com/fit2grow-DataNinja/s02-crm-data-quality-auditor/blob/main/tests/fixtures/README.md).

The portfolio repository is primarily documentation and governance; it does not require an empty executable `tests/` directory.
