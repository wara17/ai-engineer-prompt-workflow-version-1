# Skill: Review Implementation

Use this skill after implementation.

## Purpose

Check whether the implementation satisfies the requirement safely.

## Output Format

```md
## Review Summary

## Requirement Coverage

| Requirement | Status | Evidence |
|---|---|---|

## Backward Compatibility Review

## Code Quality Review

## Test Coverage Review

## Regression Risk

## Issues Found

## Recommended Fixes

## Final Verdict
```

## Status Values

- Pass
- Partial
- Fail
- Not Verified

## Rules

- Compare against normalized requirement.
- Check that old behavior still works.
- Check public contracts.
- Check tests.
- Do not approve implementation without evidence.

## Prompt

```txt
Use .ai/skills/review-implementation.md.

Review the implementation against the normalized requirement.
Check backward compatibility and regression risks.
```
