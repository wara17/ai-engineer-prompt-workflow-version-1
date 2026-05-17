# GitHub Copilot Instructions

You are assisting with enterprise backend development in IntelliJ IDEA.

Follow the repository AI workflow in `.ai/agent.md`.

## Mandatory Behavior

Before implementation:

1. Normalize the requirement.
2. Analyze the current implementation.
3. Separate observed behavior from inferred behavior.
4. Create an implementation plan.
5. Identify backward compatibility risks.
6. Propose regression tests.

During implementation:

1. Make minimal changes.
2. Preserve existing behavior unless explicitly changed.
3. Avoid unrelated refactoring.
4. Keep public contracts stable.
5. Follow existing project style.
6. Reuse existing services, DTOs, repositories, mappers, utilities, and exception patterns.

After implementation:

1. Review the implementation against the normalized requirement.
2. List files changed.
3. Explain compatibility impact.
4. Generate or update unit/regression tests.
5. Mention any remaining risks.

## Spring Boot Guidance

- Keep controllers thin.
- Put business logic in services.
- Use transactions intentionally.
- Avoid accessing lazy-loaded entities outside transaction boundaries.
- Prefer constructor injection.
- Validate input at boundaries.
- Keep DTOs separate from entities.
- Avoid leaking internal exceptions to API responses.
- Do not change API contracts without explicit approval.

## Testing Guidance

Prioritize:

- Unit tests for service behavior
- Controller tests for request/response compatibility
- Repository tests only when query behavior is important
- Regression tests for previously working behavior
- Edge cases around nulls, invalid input, duplicates, permissions, and transaction rollback

## Do Not

- Do not rewrite large files unnecessarily.
- Do not change formatting across unrelated sections.
- Do not introduce new frameworks without approval.
- Do not remove existing tests.
- Do not assume unclear requirements.
- Do not claim behavior exists unless verified from code.
