# Skill: Analyze Current Behavior

Use this skill before changing existing code.

## Purpose

Understand what the system currently does.

## Output Format

```md
## Files Reviewed

## Observed Current Behavior

## Existing Flow

## Existing API / Contract

## Existing Database Behavior

## Existing Tests

## Inferred Behavior / Assumptions

## Gaps / Unknowns

## Compatibility Risks
```

## Rules

- Only put verified code behavior under observed behavior.
- Put guesses under inferred behavior.
- Mention files/classes/methods reviewed.
- Identify side effects and dependencies.
- Look for existing tests before proposing new tests.

## Prompt

```txt
Use .ai/skills/analyze-current-behavior.md.

Analyze the current implementation for this requirement.
Do not code yet.

Requirement:
<requirement>
```
