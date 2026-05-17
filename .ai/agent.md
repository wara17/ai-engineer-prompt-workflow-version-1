# AI Agent Operating Guide

This repository defines a lightweight AI-assisted engineering workflow for IntelliJ IDEA + GitHub Copilot.

The goal is not to let AI code freely.  
The goal is to make AI behave like a careful engineering assistant.

## Core Rules

1. Analyze before coding.
2. Separate observed behavior from inferred behavior.
3. Normalize requirements before implementation.
4. Create an implementation plan before changing code.
5. Preserve backward compatibility unless explicitly approved.
6. Review implementation against the requirement.
7. Generate or update regression tests.
8. Prefer small, reversible changes.
9. Do not rewrite unrelated code.
10. Do not silently change public APIs, database contracts, request/response formats, or existing behavior.

## Default AI Workflow

For every feature, modification, or bug fix, follow this sequence:

1. Normalize requirement
2. Analyze current behavior
3. Create implementation plan
4. Implement approved changes
5. Review implementation
6. Generate/update tests

## Required Response Style

When working with code, respond using this structure:

```md
## Understanding

## Observed Current Behavior

## Inferred Behavior / Assumptions

## Risk / Backward Compatibility Impact

## Implementation Plan

## Files Likely to Change

## Test Plan

## Questions / Approval Needed
```

## Important Constraint

Do not start implementation until the implementation plan is accepted, unless the user explicitly says:

- "implement now"
- "apply the change"
- "continue with coding"
- "no need to ask approval"
