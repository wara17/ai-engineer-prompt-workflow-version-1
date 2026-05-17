# Skill: Root Cause Analysis

Use this skill for bug fixes.

## Purpose

Find the real cause before changing code.

## Output Format

```md
## Bug Summary

## Reproduction Steps

## Expected Behavior

## Actual Behavior

## Evidence

## Suspected Root Cause

## Confirmed Root Cause

## Fix Options

## Recommended Fix

## Regression Tests
```

## Rules

- Do not patch symptoms only.
- Use logs, stack traces, tests, and code evidence.
- Separate suspected root cause from confirmed root cause.
- Add regression tests that fail before the fix and pass after the fix.

## Prompt

```txt
Use .ai/skills/root-cause-analysis.md.

Analyze this bug before coding:

<bug description>

Separate suspected and confirmed root cause.
Do not implement yet.
```
