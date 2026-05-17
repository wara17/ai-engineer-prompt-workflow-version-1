# Skill: Generate Unit Tests

Use this skill after or during implementation planning.

## Purpose

Generate meaningful tests, especially regression tests.

## Output Format

```md
## Test Scope

## Existing Tests Reviewed

## Test Cases

| Case | Purpose | Expected Result |
|---|---|---|

## Suggested Test Files

## Test Data

## Notes
```

## Rules

- Cover new behavior.
- Cover old behavior to prevent regression.
- Include edge cases.
- Match the existing project's test style.
- Avoid brittle tests that depend on unrelated internals.

## Prompt

```txt
Use .ai/skills/generate-unit-tests.md.

Generate or update tests for this requirement:

<requirement>

Include regression tests for existing behavior.
```
