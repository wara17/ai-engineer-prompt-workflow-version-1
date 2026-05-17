# AI Engineering Workflow Repository

A lightweight reusable workflow repository for IntelliJ IDEA + GitHub Copilot.

## Purpose

This repo helps teams use AI more safely during software development.

It is designed to:

- Reduce vibe coding
- Improve requirement understanding
- Standardize AI-assisted development
- Support enterprise backend development
- Support Spring Boot projects
- Preserve backward compatibility during feature modification

## Repository Structure

```txt
.
├── .ai
│   ├── agent.md
│   ├── project-summary.md
│   ├── skills
│   │   ├── analyze-current-behavior.md
│   │   ├── create-implementation-plan.md
│   │   ├── generate-unit-tests.md
│   │   ├── normalize-requirements.md
│   │   ├── review-implementation.md
│   │   └── root-cause-analysis.md
│   ├── workflows
│   │   ├── add-feature.md
│   │   ├── bug-fix.md
│   │   ├── modify-feature.md
│   │   └── review-implementation.md
│   ├── templates
│   │   ├── bug-report-template.md
│   │   ├── implementation-plan-template.md
│   │   ├── normalized-requirement-template.md
│   │   └── review-result-template.md
│   └── examples
│       ├── example-workflow-usage.md
│       ├── sample-feature.md
│       ├── sample-implementation-plan.md
│       ├── sample-normalized-requirement.md
│       ├── sample-prompts.md
│       └── sample-review-result.md
└── .github
    └── copilot-instructions.md
```

## How to Use With IntelliJ IDEA + GitHub Copilot

Copy the `.ai` and `.github` folders into your project root.

Then open GitHub Copilot Chat in IntelliJ IDEA and start with:

```txt
Use .ai/agent.md.

Analyze current implementation first.
Do not code yet.

Requirement:
<your requirement>
```

## Recommended Workflow

```txt
1. Normalize requirement
2. Analyze current behavior
3. Create implementation plan
4. Implement approved changes
5. Review implementation
6. Generate/update tests
```

## Feature Workflow

```txt
Use .ai/workflows/add-feature.md.

Requirement:
<feature requirement>

Analyze current behavior first.
Create an implementation plan before coding.
Preserve backward compatibility.
Generate regression tests.
```

## Modify Feature Workflow

```txt
Use .ai/workflows/modify-feature.md.

Requirement:
<modification requirement>

Before coding:
- identify current behavior
- identify behavior that must remain unchanged
- separate observed behavior from inferred behavior
- create implementation plan
- highlight backward compatibility risks
```

## Bug Fix Workflow

```txt
Use .ai/workflows/bug-fix.md.

Bug:
<bug description>

Evidence:
<logs, stack trace, screenshots, API response, or failed test>

Do root cause analysis first.
Do not code yet.
```

## Review Workflow

```txt
Use .ai/workflows/review-implementation.md.

Review the current implementation.

Check:
1. requirement coverage
2. backward compatibility
3. regression risk
4. missing tests
5. unnecessary changes
6. code quality
```

## Why This Works

Most AI coding mistakes happen because the AI starts coding before it understands:

- the current behavior
- the real requirement
- hidden compatibility constraints
- existing tests
- enterprise backend side effects

This workflow forces AI to slow down before implementation.

## Practical Rules

### Good Prompt

```txt
Use .ai/workflows/modify-feature.md.

Requirement:
When creating a payment, allow optional source field.
Existing clients must still work.

Analyze current behavior first.
Do not code yet.
```

### Bad Prompt

```txt
Add source to payment.
```

The bad prompt encourages vibe coding.

## Backward Compatibility Checklist

Before approving AI-generated code, check:

- Did API request fields remain compatible?
- Did API response fields remain compatible?
- Did validation become stricter?
- Did HTTP status codes change?
- Did database schema changes remain non-destructive?
- Did old tests still pass?
- Were regression tests added?

## Recommended Team Practice

For every non-trivial task, require Copilot to produce:

1. normalized requirement
2. current behavior analysis
3. implementation plan
4. compatibility review
5. test plan

Only then allow implementation.

## License

Use freely inside your projects.
