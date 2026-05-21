# Main Orchestrator: A-H Sequential Workflow

## Purpose

Control the complete flow from requirement to deployment with explicit checkpoints and Q&A at each step.

## How to Start

```
Use this orchestrator for new features, bug fixes, or modifications.

Feature/Task: [Your feature name]

Start with Step A below.
```

## Complete Workflow Flow

### STEP A: Requirement Owner (Clarify Requirement)

**Load:** `.ai/sequential-workflow/roles/role-a-requirement-owner.md`

```
Feature: [Your feature]

Clarify the requirement.
Ask clarifying questions until you understand completely.
Document decisions.

When done, Role A signs off: ✅ APPROVED
```

**What to get from Role A:**
- Clear requirement
- Acceptance criteria
- Edge cases considered
- Sign-off document

---

### STEP B: Analyst (Analyze Current Behavior)

**Load:** `.ai/sequential-workflow/roles/role-b-analyst.md`

```
Requirement (from Step A): [Reference requirement]

Analyze the current implementation.
Understand how it works now.
Identify backward compatibility risks.
Ask questions about existing behavior.

When done, Role B signs off: ✅ APPROVED
```

**What to get from Role B:**
- Current behavior analysis
- Existing tests documented
- Backward compatibility risks
- Sign-off document

---

### STEP C: Architect (Create Implementation Plan)

**Load:** `.ai/sequential-workflow/roles/role-c-architect.md`

```
Requirement (from Step A): [Reference]
Current Behavior (from Step B): [Reference]

Create a detailed implementation plan.
Identify files/classes to change.
Propose the approach.
GetPreview approval from Role A & B.

When done, get sign-offs:
- ✅ Architect approves
- ✅ Requirement Owner approves
- ✅ Analyst approves
```

**What to get from Role C:**
- Implementation plan
- Files to modify
- No hidden side effects
- Approval from A & B

---

### STEP D: Developer (Implement Code)

**Load:** `.ai/sequential-workflow/roles/role-d-developer.md`

```
Implementation Plan (from Step C): [Reference]

Write code according to the plan.
Follow the plan exactly.
Don't add extra features.
Verify code compiles.
Do basic manual testing.

When done, sign off: ✅ APPROVED
```

**What to get from Role D:**
- Implemented code
- All files compile
- Basic tests pass
- Code follows plan

---

### STEP E: Developer/Tester (Write Unit Tests)

**Load:** `.ai/sequential-workflow/roles/role-e-tester.md`

```
Implementation (from Step D): [Reference]

Write comprehensive unit tests.
Test happy path, error cases, edge cases.
Ensure code coverage >80%.
Verify old tests still pass (no regression).

When done, sign off:
- ✅ Tests passing: [count]/[count]
- ✅ Coverage: [%]
- ✅ No regression
```

**What to get from Role E:**
- Unit tests written
- Tests all passing (100%)
- Coverage >80%
- Old tests still pass
- Test report

---

### STEP F: Reviewer (Code Review & Approvals)

**Load:** `.ai/sequential-workflow/roles/role-f-reviewer.md`

```
Implementation (from Step D): [Reference]
Tests (from Step E): [Reference]

Review the code quality.
Check test coverage.
Verify backward compatibility.
Get approval from:
  - ✅ Reviewer (code quality)
  - ✅ Requirement Owner (meets requirements)
  - ✅ Analyst (no regression)

When done, all approve: ✅ APPROVED
```

**What to get from Role F:**
- Code review comments resolved
- All approvals collected
- A & B sign-off
- Ready to commit

---

### STEP G: Developer (Create Git Commit)

**Load:** `.ai/sequential-workflow/roles/role-g-committer.md`

```
Code Review Approved (from Step F): ✅

Create a clean git commit.
Write clear commit message.
Stage the files.
Commit to your feature branch.

When done, sign off: ✅ APPROVED
```

**What to get from Role G:**
- Git commit created
- Clear commit message
- Ready to push
- Commit reference

---

### STEP H: DevOps (Push to Repository)

**Load:** `.ai/sequential-workflow/roles/role-h-devops.md`

```
Commit (from Step G): [Reference commit]

Push code to repository.
Create Pull Request.
Wait for CI/CD checks to pass.
Merge to main when ready.

When done, sign off: ✅ COMPLETE
```

**What to get from Role H:**
- Code pushed
- PR created
- CI/CD passing
- Ready to merge

---

## ✅ Checkpoint Status Template

Use this to track progress:

```markdown
# Feature: [Feature Name]

## Status Report

### Step A: Requirement Owner
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- Requirement: [Clear statement]
- Approver: [Name]
- Date: [Date]

### Step B: Analyst
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- Current Behavior: [Summary]
- Risks: [Any risks identified]
- Approver: [Name]
- Date: [Date]

### Step C: Architect
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- Plan: [Summary]
- Approvals: A ✅ B ✅ C ✅
- Date: [Date]

### Step D: Developer (Implementation)
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- Files Changed: [Count]
- Compiles: ✅
- Basic Tests: ✅
- Date: [Date]

### Step E: Tester (Unit Tests)
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- Tests Written: [Count]
- Tests Passing: ✅ [Count]/[Count]
- Coverage: [%]
- Regression: ✅ No
- Date: [Date]

### Step F: Reviewer (Code Review)
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- Approvals: Reviewer ✅ A ✅ B ✅
- Issues: [Any issues resolved]
- Date: [Date]

### Step G: Committer (Git Commit)
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- Commit: [Commit SHA]
- Message: [Clear message]
- Date: [Date]

### Step H: DevOps (Push to Repo)
- Status: ⏳ IN PROGRESS / ✅ APPROVED / ❌ NEEDS REVISION
- PR: [PR URL]
- CI/CD: ✅ All passing
- Merged: YES / NO
- Date: [Date]

## Overall Status

- Complete: [Steps completed]/8
- Next Step: Step [X]
```

## 🔄 Loop-Back Rules

If issues found, loop back:

| Found In | Issue Type | Loop Back To |
|----------|------------|-------------|
| Step B | Can't understand current behavior | Step A (clarify requirement) |
| Step C | Can't create plan | Step A or B (clarify more) |
| Step D | Code doesn't match plan | Step C (update plan) |
| Step E | Tests fail | Step D (fix bugs) |
| Step F | Code quality issues | Step D (fix code) |
| Step F | Regression risk | Step B or E (verify) |
| Step G | Issues with commit | Step F (review again) |
| Step H | CI/CD fails | Appropriate earlier step (fix) |

## 📋 Key Questions Each Role Should Ask

### Role A - Requirement Owner
- [ ] What exactly needs to change?
- [ ] Why do we need this?
- [ ] What are acceptance criteria?
- [ ] What should NOT change?
- [ ] Any edge cases?

### Role B - Analyst
- [ ] How does it work currently?
- [ ] What tests exist?
- [ ] What could break?
- [ ] Do old clients need to work?
- [ ] Any database considerations?

### Role C - Architect
- [ ] What files need to change?
- [ ] Will this affect other parts?
- [ ] Is the approach optimal?
- [ ] Any alternative approaches?
- [ ] Do A & B agree with this plan?

### Role D - Developer
- [ ] Did I follow the plan?
- [ ] Does it compile?
- [ ] Does basic testing pass?
- [ ] Is code clean?
- [ ] Any unexpected issues?

### Role E - Tester
- [ ] Are all scenarios tested?
- [ ] Is coverage adequate?
- [ ] Do old tests pass?
- [ ] Are edge cases covered?
- [ ] Any regression detected?

### Role F - Reviewer
- [ ] Is code quality acceptable?
- [ ] Are tests adequate?
- [ ] Is backward compatibility preserved?
- [ ] Do A & B agree with this?
- [ ] Ready to commit?

### Role G - Committer
- [ ] Is commit message clear?
- [ ] Is commit atomic?
- [ ] Are only intended files included?
- [ ] Any unwanted changes?
- [ ] Ready to push?

### Role H - DevOps
- [ ] Is PR created?
- [ ] Is CI/CD passing?
- [ ] Any merge conflicts?
- [ ] Ready to merge?
- [ ] Any deployment risks?

## 🎯 Success Criteria

### You Know Step A is Done When:
✅ Requirement is crystal clear  
✅ No ambiguity remains  
✅ Acceptance criteria defined  
✅ Role A has signed off  

### You Know Step B is Done When:
✅ Current behavior fully understood  
✅ Existing tests documented  
✅ Backward compatibility risks identified  
✅ Role B has signed off  

### You Know Step C is Done When:
✅ Implementation approach is clear  
✅ Files to modify identified  
✅ Role A & B have approved plan  
✅ Role C has signed off  

### You Know Step D is Done When:
✅ Code written per plan  
✅ Code compiles without errors  
✅ Basic functionality works  
✅ Role D has signed off  

### You Know Step E is Done When:
✅ 10+ unit tests written  
✅ All tests passing (100%)  
✅ Coverage >80%  
✅ Old tests still pass (no regression)  
✅ Role E has signed off  

### You Know Step F is Done When:
✅ Code review completed  
✅ No quality issues  
✅ Role A approved (meets requirements)  
✅ Role B approved (no regression)  
✅ Role F approved (code quality)  
✅ All three have signed off  

### You Know Step G is Done When:
✅ Git commit created  
✅ Commit message is clear  
✅ Only intended files included  
✅ Role G has signed off  

### You Know Step H is Done When:
✅ Code pushed to repository  
✅ PR created (if using PR workflow)  
✅ CI/CD checks passing  
✅ PR merged to main  
✅ Deployment complete  
✅ Role H has signed off  

## 🎉 Workflow Complete!

When Step H is done:

```
✅ COMPLETE: Feature [Name] deployed successfully

Timeline:
- Step A: [Date] [Duration]
- Step B: [Date] [Duration]
- Step C: [Date] [Duration]
- Step D: [Date] [Duration]
- Step E: [Date] [Duration]
- Step F: [Date] [Duration]
- Step G: [Date] [Duration]
- Step H: [Date] [Duration]

Total time: [Hours]

All approvals: ✅ COMPLETE
All tests: ✅ PASSING
Deployment: ✅ SUCCESSFUL
```

## 💡 Pro Tips

✅ **Don't skip steps** - Each one prevents problems  
✅ **Ask questions early** - Clarification is cheaper than rework  
✅ **Document decisions** - Keep track of why, not just what  
✅ **Get sign-offs** - Explicit approval prevents misunderstandings  
✅ **Loop back quickly** - If confused, go back to clarify  
✅ **Test thoroughly** - The more tests, the fewer production bugs  
✅ **Clear commits** - Good commit messages help future debugging  
✅ **Communication** - Keep team updated on progress  

## Ready to Start?

```
Feature: [Your feature name here]

Start with Step A!
```

Good luck! 🚀