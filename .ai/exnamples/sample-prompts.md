# Sample Prompts

## Add Feature

```txt
Use .ai/workflows/add-feature.md.

Requirement:
Add optional `source` field to create payment API.
Existing clients must continue working.

Do not code yet.
Analyze current behavior and create a plan first.
```

## Modify Feature

```txt
Use .ai/workflows/modify-feature.md.

Requirement:
Change payment expiry calculation to support branch-specific expiry hours.
Default behavior must remain unchanged for branches without configuration.

Do not code yet.
```

## Bug Fix

```txt
Use .ai/workflows/bug-fix.md.

Bug:
Payment creation sometimes throws LazyInitializationException when reading customer tier prices.

Evidence:
<stack trace>

Do root cause analysis first.
Do not code yet.
```

## Review Implementation

```txt
Use .ai/workflows/review-implementation.md.

Review the current changes against this requirement:
<normalized requirement>

Check backward compatibility, regression risk, and missing tests.
```

## Continue After Plan Approval

```txt
The implementation plan is approved.

Implement only the approved changes.
Do not refactor unrelated code.
After implementation, review against the requirement and update tests.
```
