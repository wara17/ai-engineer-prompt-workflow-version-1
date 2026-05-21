# Sequential Role Workflow (A-H)

Complete workflow system from requirement to deployment with checkpoints and Q&A at each stage.

## 🎯 Workflow Overview

```
A: Requirement Owner
   ↓ (Q&A until OK)

B: Analyst  
   ↓ (Q&A until OK)

C: Architect
   ↓ (Q&A until OK)

D: Developer (Implement)
   ↓ (Q&A until OK)

E: Developer/Tester (Unit Tests)
   ↓ (Q&A until OK)

F: Reviewer (Code Review + A & B Sign-off)
   ↓ (Q&A until OK)

G: Developer (Commit)
   ↓ (Q&A until OK)

H: DevOps (Push to Repo)
   ↓ DONE!
```

## 📁 Structure

```
.ai/sequential-workflow/
├── README.md                    (This file)
├── orchestrator.md              (Main workflow controller)
├── roles/
│   ├── role-a-requirement-owner.md
│   ├── role-b-analyst.md
│   ├── role-c-architect.md
│   ├── role-d-developer.md
│   ├── role-e-tester.md
│   ├── role-f-reviewer.md
│   ├── role-g-committer.md
│   └── role-h-devops.md
└── skills/
    ├── skill-a-clarify-requirement.md
    ├── skill-b-analyze-current-behavior.md
    ├── skill-c-create-implementation-plan.md
    ├── skill-d-implement.md
    ├── skill-e-generate-unit-tests.md
    ├── skill-f-review-implementation.md
    ├── skill-g-commit.md
    └── skill-h-push-to-repo.md
```

## 🚀 Quick Start

### To Start A New Feature

```
Use .ai/sequential-workflow/orchestrator.md

Feature: Add optional payment source field

Start with Step A.
```

### Step-by-Step Flow

**STEP A - Requirement Owner**
```
Use .ai/sequential-workflow/roles/role-a-requirement-owner.md

Feature: [Your feature]

Clarify the requirement.
Ask clarifying questions until requirement is crystal clear.
Sign off when OK.
```

**STEP B - Analyst**
```
Use .ai/sequential-workflow/roles/role-b-analyst.md

Requirement (from Step A): [Reference]

Analyze current behavior.
Ask questions about existing implementation.
Sign off when clear.
```

**STEP C - Architect**
```
Use .ai/sequential-workflow/roles/role-c-architect.md

Requirement (from Step A): [Reference]
Current Behavior (from Step B): [Reference]

Create implementation plan.
Get approval from A & B before coding.
```

**STEP D - Developer (Implement)**
```
Use .ai/sequential-workflow/roles/role-d-developer.md

Implementation Plan (from Step C): [Reference]

Write code according to plan.
Verify compilation and basic functionality.
```

**STEP E - Developer/Tester**
```
Use .ai/sequential-workflow/roles/role-e-tester.md

Implementation (from Step D): [Reference]

Write unit tests.
Ensure code coverage >80%.
Verify old tests still pass.
```

**STEP F - Reviewer**
```
Use .ai/sequential-workflow/roles/role-f-reviewer.md

Implementation (from Step D): [Reference]
Tests (from Step E): [Reference]

Review code quality.
Get approval from Role A & B.
Sign off when OK.
```

**STEP G - Developer (Commit)**
```
Use .ai/sequential-workflow/roles/role-g-committer.md

Code Review Approved (from Step F): ✅

Create clean commit message.
Stage and commit code.
```

**STEP H - DevOps (Push)**
```
Use .ai/sequential-workflow/roles/role-h-devops.md

Commit (from Step G): [Reference]

Push to repository.
Create PR.
Monitor CI/CD.
Merge when approved.
```

## ✨ Key Principles

✅ **Sequential** - Each step builds on previous  
✅ **Approval-based** - Move forward only when approved  
✅ **Question-driven** - Each role asks clarifying questions  
✅ **Loop-back** - If issues found, go back to fix  
✅ **Sign-offs** - Each role signs off completion  
✅ **Templates** - Use provided templates and checklists  

## 📊 Status Tracking

### Template for Each Step

```markdown
### STEP A: Requirement Owner

Requirement:
[Clear, specific requirement]

Q&A Summary:
- [Question 1]: [Answer]
- [Question 2]: [Answer]
- [Question 3]: [Answer]

Status: ✅ APPROVED by Requirement Owner
Date: [Date]
Approver: [Name]
```

Repeat this pattern for steps B-H.

## 🎯 When Each Step Is Complete

| Step | Complete When |
|------|---------------|
| **A** | Requirement is crystal clear, no ambiguity |
| **B** | Current behavior fully understood |
| **C** | Plan approved by A & B, implementation clear |
| **D** | Code compiles, basic tests pass |
| **E** | All tests passing, coverage >80%, no regression |
| **F** | Code approved by reviewer, A & B sign-off |
| **G** | Commit created, message clear, ready to push |
| **H** | PR created, CI/CD passing, ready to merge |

## 🔄 Loop-Back Rules

If issues found:

| Found In | Go Back To | Fix |
|----------|-----------|-----|
| Step B | Step A | Clarify requirement again |
| Step C | Step A or B | Understand requirement/behavior better |
| Step D | Step C | Update plan |
| Step E | Step D | Fix implementation bugs |
| Step F | Step D or E | Fix code or tests |
| Step G | Step E or F | Fix issues before commit |
| Step H | Step G | Update commit before push |

## 📝 Example: Payment Source Feature

### Flow in Action

```
STEP A: 
Q: "When source is null, what's the default?"
A: "Use CREDIT_CARD as default"
Status: ✅ Approved

STEP B:
Q: "Do old payments have source field?"
A: "No, it's new"
Q: "Can we add it as optional?"
A: "Yes, make it nullable"
Status: ✅ Approved

STEP C:
Plan:
1. Add source field to Payment entity (nullable)
2. Update PaymentController to accept source
3. Add validation for valid sources
4. Update tests
Approval: ✅ A & B approved

STEP D:
Implemented and compiled successfully.
Status: ✅ Ready for testing

STEP E:
12 tests written:
- 4 happy path
- 3 error cases
- 3 edge cases
- 2 backward compatibility
All passing: ✅ 12/12
Status: ✅ Approved

STEP F:
Code review passed.
A & B sign-off: ✅
Status: ✅ Approved

STEP G:
Commit: "feat: Add optional payment source field"
Status: ✅ Ready to push

STEP H:
PR created and CI/CD passing.
Ready to merge: ✅
Status: ✅ COMPLETE
```

## 🤝 Team Communication

At each step, communicate clearly:

```
STEP X COMPLETE

[What was done]
[Key findings]
[Decisions made]
[What to do next]

✅ Approved by: [Name]
Date: [Date]

Next: STEP Y
```

## 📋 Checklists by Role

**Role A - Requirement Owner**
- [ ] Requirement is specific
- [ ] No ambiguity
- [ ] Edge cases considered
- [ ] Acceptance criteria clear

**Role B - Analyst**
- [ ] Current behavior understood
- [ ] Backward compatibility risks identified
- [ ] Existing tests documented
- [ ] Dependencies identified

**Role C - Architect**
- [ ] Implementation approach clear
- [ ] File/class changes identified
- [ ] No side effects on other parts
- [ ] Plan approved by A & B

**Role D - Developer**
- [ ] Code follows plan
- [ ] Compiles without errors
- [ ] Basic manual testing passed
- [ ] Code style consistent

**Role E - Tester**
- [ ] All new scenarios tested
- [ ] Error cases covered
- [ ] Edge cases covered
- [ ] Old tests still pass (no regression)
- [ ] Coverage >80%

**Role F - Reviewer**
- [ ] Code quality acceptable
- [ ] Tests adequate
- [ ] Backward compatibility preserved
- [ ] A & B approve

**Role G - Committer**
- [ ] Commit message clear
- [ ] Commit is atomic
- [ ] Only intended files included

**Role H - DevOps**
- [ ] PR created
- [ ] CI/CD passing
- [ ] Ready to merge

## 💡 Tips for Success

✅ **Clarify first, code later** - Don't rush to implementation  
✅ **Document decisions** - Keep track of Q&A and approvals  
✅ **Test thoroughly** - Edge cases and regression tests matter  
✅ **Communication** - Clear handoffs between roles  
✅ **Loop-back early** - If confused, go back to clarify  
✅ **Sign-offs** - Make approvals explicit  

## 🚀 Start Your First Workflow

```
Use .ai/sequential-workflow/orchestrator.md

Feature: [Your feature here]

Start with Step A!
```

Happy coding! 🎉
