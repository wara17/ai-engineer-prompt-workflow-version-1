# Project Summary

Use this file to summarize the target project before asking Copilot to implement changes.

## Project Type

Enterprise backend application.

## Primary Stack

- Java / Kotlin
- Spring Boot
- REST API
- JPA / Hibernate
- SQL database
- Unit tests / integration tests
- IntelliJ IDEA
- GitHub Copilot

## Engineering Priorities

1. Correctness
2. Backward compatibility
3. Maintainability
4. Clear service boundaries
5. Test coverage
6. Low-risk implementation
7. Minimal unrelated changes

## Common Backend Concerns

- API contract compatibility
- Transaction behavior
- Database migration safety
- DTO / entity mapping correctness
- Exception handling
- Validation rules
- Logging without exposing sensitive data
- Performance impact
- Idempotency
- Regression tests

## Backward Compatibility Policy

When modifying existing features:

- Do not remove existing fields unless explicitly approved.
- Do not rename API fields unless explicitly approved.
- Do not change HTTP status codes unless explicitly approved.
- Do not change database schema destructively.
- Do not change existing business behavior unless required.
- Keep old behavior working while adding new behavior where possible.

## AI Collaboration Style

Prefer asking the AI to analyze and plan first.

Recommended first prompt:

```txt
Use .ai/agent.md.

Analyze current implementation first.
Do not code yet.

Requirement:
<write requirement here>

Please return:
1. normalized requirement
2. observed current behavior
3. inferred behavior / assumptions
4. implementation plan
5. backward compatibility risks
6. test plan
```
