# Skill: Normalize Requirements

Use this skill before implementation.

## Purpose

Convert vague or conversational requirements into clear engineering requirements.

## Input

A raw feature, bug, or modification request.

## Output Format

```md
## Raw Requirement

## Normalized Requirement

### Goal

### In Scope

### Out of Scope

### Acceptance Criteria

### Backward Compatibility Requirements

### Open Questions

### Assumptions
```

## Rules

- Do not invent behavior.
- Separate confirmed details from assumptions.
- Convert vague words into testable conditions.
- Identify API, database, UI, and behavior impact.
- Preserve existing behavior unless the requirement explicitly changes it.

## Prompt

```txt
Use .ai/skills/normalize-requirements.md.

Normalize this requirement before coding:

<requirement>

Return acceptance criteria and backward compatibility concerns.
Do not implement yet.
```
