# Workflow: Modify Feature

Use when changing an existing feature.

## Main Risk

Feature modification can accidentally break existing users.

## Steps

1. Normalize requirement
2. Analyze current behavior
3. Identify existing contracts
4. Create compatibility-preserving plan
5. Implement approved changes
6. Review implementation
7. Generate/update regression tests

## Prompt

```txt
Use .ai/workflows/modify-feature.md.

Requirement:
<modification requirement>

Before coding:
- Identify current behavior.
- Identify behavior that must remain unchanged.
- Separate observed behavior from inferred behavior.
- Create implementation plan.
- Highlight backward compatibility risks.
```
