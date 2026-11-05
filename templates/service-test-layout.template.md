# Service test layout — template

Use this **guideline**, not a mandatory directory scaffold. Adapt to the service's language and test runner.

```text
service-repository/
  tests/
    test_<domain>.py          # deterministic business rules
    test_<api>.py             # API behavior
    test_<integration>.py     # adapters and integrations
    fixtures/
      README.md               # synthetic fixture policy
      <reused-fixtures>       # add only when justified
  samples/                    # optional larger synthetic demonstrations
  docs/
    definition-of-done.md     # milestone-specific acceptance criteria
```

## Expectations
- Protect a verified existing workflow before adding a new path.
- Add focused regression coverage for changed behavior and error handling.
- Prefer synthetic inline or temporary inputs for isolated tests.
- Add source-controlled fixture files only for reuse or stable examples.
- Record the test command, environment assumptions, and observed result.
- Never mark tests passed solely because they were committed.
- Do not commit real customer data, secrets, or sensitive exports.

See [portfolio definition of done](../governance/definition-of-done.md) and [regression-testing standard](../validation/regression-testing.md).
