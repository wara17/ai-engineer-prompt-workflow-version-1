# Testing & Coverage Skill

This skill provides guidance on unit test coverage metrics, line coverage, branch coverage, and acceptance criteria (AC) validation for pull requests.

## Overview

When reviewing or creating a PR, ensure comprehensive test coverage reporting including:
- Unit test count and results
- Line coverage metrics (goal: ≥80%)
- Branch coverage metrics (goal: ≥75%)
- Acceptance criteria validation (goal: 100%)

## Unit Test Coverage Metrics

### 1. Unit Test Count
Track the total number of tests:
```
✅ Total Tests: [count]
✅ Passed: [count]
❌ Failed: [count]
⏭️ Skipped: [count]
```

**Requirement:**
- All tests must pass (0 failures)
- No skipped tests in production code
- Skipped tests must have documented reason

### 2. Line Coverage
Percentage of code lines executed by tests.

```
📊 Line Coverage: 85% (Goal: ≥80%)
   Lines Executed: 170 / 200
   Lines Not Covered: 30
```

**Coverage Thresholds by Layer:**
```
Service Layer:     ≥85%  (core business logic)
Controller Layer:  ≥75%  (endpoint routing)
Repository Layer:  ≥70%  (data access)
Utility/Helper:    ≥90%  (reusable functions)
```

**How to Improve:**
- Write unit tests for each service method
- Test both happy path and error cases
- Use mock objects for dependencies
- Cover all conditional branches

### 3. Branch Coverage
Percentage of conditional branches (if/else, switch, etc.) covered by tests.

```
📊 Branch Coverage: 78% (Goal: ≥75%)
   Branches Covered: 35 / 45
   Branches Not Covered: 10
```

**What to Test:**
```
if (condition) {
  // True branch
  // False branch
}

switch (value) {
  case A: // Test A
  case B: // Test B
  default: // Test default
}

ternary ? // Test both sides
```

**Common Missing Branches:**
- Exception handling paths
- Null/empty checks
- Edge case conditions
- Fallback logic

### 4. Acceptance Criteria (AC) Validation

Each PR must verify that all acceptance criteria pass.

```
## ✅ Acceptance Criteria Results

| AC ID | Requirement | Status | Test Case | Evidence |
|-------|-------------|--------|-----------|----------|
| AC-1 | User can register with email | ✅ PASS | UserRegistrationTest.testRegisterNewUser | Line 45-67 |
| AC-2 | Email format validation | ✅ PASS | UserRegistrationTest.testInvalidEmail | Line 68-75 |
| AC-3 | Password encryption | ✅ PASS | UserRegistrationTest.testPasswordEncrypted | Line 76-85 |
| AC-4 | Duplicate email rejected | ✅ PASS | UserRegistrationTest.testDuplicateEmail | Line 86-95 |
```

**AC Validation Process:**
1. Read AC from issue/task
2. Write unit test that verifies AC
3. Ensure test fails before implementation
4. Implement feature
5. Ensure test passes
6. Document in PR description

## Tools & Configuration

### JaCoCo Maven Configuration
```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.8</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
        <execution>
            <id>jacoco-check</id>
            <goals>
                <goal>check</goal>
            </goals>
            <configuration>
                <rules>
                    <rule>
                        <element>PACKAGE</element>
                        <excludes>
                            <exclude>*Test</exclude>
                        </excludes>
                        <limits>
                            <limit>
                                <counter>LINE</counter>
                                <value>COVEREDRATIO</value>
                                <minimum>0.80</minimum>
                            </limit>
                        </limits>
                    </rule>
                </rules>
            </configuration>
        </execution>
    </executions>
</plugin>
```

### Run Tests with Coverage
```bash
# Generate coverage report
mvn clean test jacoco:report

# View HTML report
open target/site/jacoco/index.html

# Check coverage enforcement
mvn jacoco:check
```

### GitHub Actions Integration
```yaml
name: Test Coverage Check
on: [pull_request]

jobs:
  coverage:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: '17'
      - run: mvn clean test jacoco:report
      - run: mvn jacoco:check
```

## Test Coverage Report Template

Use this template in PR descriptions:

```markdown
## 📊 Test Coverage Report

### Unit Test Results
- Total Tests: 25
- Passed: 25 ✅
- Failed: 0
- Skipped: 0
- Execution Time: 2.34s

### Line Coverage
```
Coverage: 87% (Goal: ≥80%)
Lines Executed: 432 / 496
Lines Not Covered: 64
```

### Branch Coverage
```
Coverage: 82% (Goal: ≥75%)
Branches Covered: 58 / 71
Branches Not Covered: 13
```

### Acceptance Criteria Verification

| AC ID | Requirement | Status | Test File | Lines |
|-------|-------------|--------|-----------|-------|
| AC-1 | Users can login with email | ✅ | LoginServiceTest.java | 34-56 |
| AC-2 | Invalid credentials rejected | ✅ | LoginServiceTest.java | 57-72 |
| AC-3 | JWT token generated | ✅ | LoginServiceTest.java | 73-89 |
| AC-4 | Token expires after 24h | ✅ | JwtTokenTest.java | 45-68 |

### Coverage Gaps
- ❌ Error handling in retry logic (3 branches)
  - Status: Acceptable (rare edge case)
  - Reason: Requires external service mock

### Summary
✅ All tests passing
✅ Line coverage meets minimum (87% ≥ 80%)
✅ Branch coverage meets minimum (82% ≥ 75%)
✅ All ACs verified and passing
✅ No regressions detected
```

## Before PR Merge Checklist

- [ ] All unit tests pass (0 failures)
- [ ] Line coverage ≥ 80% (service layer ≥ 85%)
- [ ] Branch coverage ≥ 75%
- [ ] All acceptance criteria verified (100%)
- [ ] No skipped tests without reason
- [ ] Coverage report attached to PR
- [ ] Code reviewer approved
- [ ] No regressions in existing tests
- [ ] Documentation updated

## Common Issues & Solutions

### Issue: Line coverage below 80%
**Solution:**
1. Identify uncovered lines: `target/site/jacoco/index.html`
2. Write unit tests for those lines
3. Test both happy path and error cases
4. Re-run: `mvn clean test jacoco:report`

### Issue: Branch coverage below 75%
**Solution:**
1. Find uncovered branches in JaCoCo report
2. Write tests for each branch:
   - If/else → test both conditions
   - Switch → test each case
   - Exception paths → test throws
3. Update test coverage report

### Issue: AC not testable
**Solution:**
1. Break AC into smaller, testable criteria
2. Create integration tests if needed
3. Use test fixtures and mocks
4. Document testing approach in PR

### Issue: False negatives in coverage
**Solution:**
1. Exclude generated code from coverage
2. Exclude test utilities and helpers
3. Focus on business logic coverage
4. Don't over-test trivial getters/setters

## References

- **JaCoCo Documentation:** https://www.jacoco.org/
- **Test Coverage Best Practices:** https://testing.googleblog.com/
- **Acceptance Criteria Guide:** BDD-style AC writing
