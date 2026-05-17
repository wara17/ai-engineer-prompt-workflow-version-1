# Example Workflow Usage

## Scenario

You want to modify an existing Spring Boot API without breaking current clients.

## Step 1: Ask Copilot to Analyze

```txt
Use .ai/agent.md and .ai/workflows/modify-feature.md.

Requirement:
Add optional `source` field to create payment API.
Existing clients must continue working.

Analyze current behavior first.
Do not code yet.
```

## Step 2: Review AI Output

Check whether Copilot clearly separates:

- observed current behavior
- inferred behavior
- assumptions
- compatibility risks
- implementation plan
- test plan

## Step 3: Approve Implementation

```txt
The plan is approved.
Implement the changes.
Keep public API backward compatible.
Add regression tests.
```

## Step 4: Review

```txt
Use .ai/workflows/review-implementation.md.

Review the implementation against the normalized requirement.
```

## Step 5: Fix Issues If Needed

```txt
Fix only the review issues.
Do not refactor unrelated code.
Update tests if needed.
```
