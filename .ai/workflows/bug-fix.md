# Workflow: Bug Fix

Use when fixing incorrect behavior.

## Steps

1. Normalize the bug report
2. Reproduce or reason from evidence
3. Perform root cause analysis
4. Create fix plan
5. Implement minimal fix
6. Add regression test
7. Review fix

## Prompt

```txt
Use .ai/workflows/bug-fix.md.

Bug:
<bug description>

Evidence:
<logs, stack trace, screenshots, API response, or test failure>

Do root cause analysis first.
Do not code until the root cause and fix plan are clear.
```
