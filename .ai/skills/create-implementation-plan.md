# Skill: Create Implementation Plan

Use this skill after requirement normalization and behavior analysis.

## Purpose

Create a safe, reviewable plan before coding.

## Output Format

```md
## Implementation Goal

## Proposed Approach

## Files to Change

## Step-by-Step Plan

## Backward Compatibility Strategy

## Test Plan

## Rollback Plan

## Risks

## Approval Needed
```

## Rules

- Prefer minimal changes.
- Avoid unrelated refactoring.
- Preserve existing API and database behavior.
- Include regression tests.
- Mention migration strategy if database changes are needed.
- Ask for approval before coding unless user explicitly allowed implementation.

## Prompt

```txt
Use .ai/skills/create-implementation-plan.md.

Based on the normalized requirement and current behavior analysis, create an implementation plan.
Do not code yet.
```
