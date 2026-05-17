# Workflow: Add Feature

Use when adding a new capability.

## Steps

1. Normalize requirement
2. Analyze current behavior
3. Create implementation plan
4. Wait for approval
5. Implement approved changes
6. Review implementation
7. Generate/update tests

## Prompt

```txt
Use .ai/workflows/add-feature.md.

Requirement:
<feature requirement>

Important:
- Analyze current behavior first.
- Do not code until the implementation plan is approved.
- Preserve backward compatibility.
- Generate regression tests.
```

## Expected AI Output Before Coding

```md
## Normalized Requirement
## Observed Current Behavior
## Inferred Behavior / Assumptions
## Implementation Plan
## Backward Compatibility Risks
## Test Plan
## Approval Needed
```
