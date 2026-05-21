# Role B: Analyst

## Your Job

Analyze how the system works TODAY before any changes.

## Responsibilities

✅ Understand current behavior  
✅ Document existing tests  
✅ Identify backward compatibility risks  
✅ Ask clarifying questions  
✅ Sign off when analysis complete  

## What You Do

### 1. Get the Requirement (From Step A)

You receive:
- Clear requirement
- Acceptance criteria
- Edge cases
- Requirement Owner's sign-off

### 2. Analyze Current Implementation

```
Questions to ask:
- Where is the relevant code?
- How does it work currently?
- What tests exist?
- What could break?
- Any hidden dependencies?
```

### 3. Study the Code

**Find the relevant files:**

```bash
# For payment example:
- Payment.java (entity)
- PaymentController.java (API)
- PaymentService.java (business logic)
- PaymentTest.java (tests)
- PaymentRepository.java (database)
```

**Understand the flow:**

```
User Request
  ↓
PaymentController.createPayment()
  ↓
PaymentService.createPayment()
  ↓
Validation
  ↓
Repository.save()
  ↓
Database
```

**Document current behavior:**

```markdown
# Current Implementation Analysis

## Payment Creation Flow

1. PaymentController receives POST /payments
2. Validates request (amount required, currency required)
3. PaymentService.createPayment(request)
4. Applies business logic (calculate fees, etc.)
5. Saves to database via PaymentRepository
6. Returns PaymentResponse

## Current Payment Entity

```java
public class Payment {
    private String id;
    private BigDecimal amount;
    private String currency;
    private LocalDateTime createdAt;
    // No 'source' field currently
}
```

## Current API Request

```json
{
  "amount": 100.00,
  "currency": "USD"
}
```

## Current API Response

```json
{
  "id": "payment_123",
  "amount": 100.00,
  "currency": "USD",
  "createdAt": "2026-05-21T10:30:00Z"
}
```

## Existing Tests

- PaymentTest.testCreatePaymentSuccess() ✓
- PaymentTest.testValidateAmountRequired() ✓
- PaymentTest.testValidateCurrencyRequired() ✓
- ... (10 total tests)

## Database Schema

```sql
CREATE TABLE payments (
    id VARCHAR(50) PRIMARY KEY,
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    created_at TIMESTAMP NOT NULL
)
```

## Backward Compatibility Status

- Old payments: Exist without 'source' field
- Old clients: Send requests without 'source'
- Old tests: Expect responses without 'source'
```

### 4. Ask Critical Questions

**About the change impact:**

- Q: "If we add 'source' field as optional, will old code still work?"
- Q: "Will old payments (without source) cause errors in new code?"
- Q: "Will new code that expects source field handle null gracefully?"

**About database:**

- Q: "Can we add new nullable column without migration?"
- Q: "Will old rows with null source cause issues?"
- Q: "Any database constraints that might break?"

**About tests:**

- Q: "Will old tests pass with new code?"
- Q: "Do old tests expect source field to NOT exist?"
- Q: "Will old test data work with new validation?"

**About API clients:**

- Q: "How many clients are currently using the API?"
- Q: "Do any clients depend on specific response fields?"
- Q: "If we add source to response, will old clients break?"

### 5. Identify Risks

```markdown
# Backward Compatibility Risk Analysis

## Risk 1: Old Payments Breaking
**Risk:** Old payments have no source field (NULL)
**Impact:** If new code requires source, old payments won't load
**Mitigation:** Make source optional, default to CREDIT_CARD
**Status:** ✅ Can be mitigated

## Risk 2: Old Tests Failing
**Risk:** Old tests check response and don't expect source field
**Impact:** Tests might fail when source appears
**Mitigation:** Old tests check exact fields, need to handle new field
**Status:** ✅ Will need test updates

## Risk 3: Old API Clients
**Risk:** Old clients might not handle new 'source' field in response
**Impact:** Older versions might ignore or break on new field
**Mitigation:** New fields usually ignored by old clients (safe)
**Status:** ✅ Low risk (additive change)

## Risk 4: Database Backward Compatibility
**Risk:** Old rows (without source) might cause queries to fail
**Impact:** Queries expecting source field would get NULL
**Mitigation:** Handle NULL in code (use default value)
**Status:** ✅ Can be mitigated
```

### 6. Document Current Test Coverage

```markdown
# Current Test Analysis

## Existing Tests (10 tests)

### Happy Path Tests
- ✓ testCreatePaymentSuccess()
- ✓ testPaymentCreatedWithCorrectAmount()
- ✓ testPaymentCreatedWithCorrectCurrency()

### Validation Tests
- ✓ testAmountIsRequired()
- ✓ testCurrencyIsRequired()
- ✓ testNegativeAmountRejected()

### Integration Tests
- ✓ testPaymentSavedToDatabase()
- ✓ testPaymentRetrievedFromDatabase()
- ✓ testPaymentCanBeRetrievedById()
- ✓ testMultiplePaymentsCreated()

## Coverage
- Line coverage: 82%
- Branch coverage: 78%
- Method coverage: 95%

## What's NOT Tested
- Concurrent payment creation (thread safety)
- Very large amounts
- Unusual currencies
```

### 7. Create Analysis Document

```markdown
# Current Behavior Analysis

## Feature: Add Optional Payment Source

### Current State

**What exists:**
- Payment entity with: id, amount, currency, createdAt
- PaymentController with POST /payments endpoint
- PaymentService with createPayment() business logic
- 10 unit tests covering happy path and validation
- Database schema with 4 columns

**What's missing:**
- No 'source' field in entity
- No 'source' parameter in API
- No 'source' validation
- No source-related tests

### Backward Compatibility Analysis

**Old payments (existing data):**
- Will have NULL source
- Must continue to work with new code
- Should display as null or use default

**Old API clients (existing integrations):**
- Don't send 'source' (optional for them)
- May or may not handle 'source' in response
- Must not break when exposed to new field

**Old tests (existing test suite):**
- 10 existing tests must continue passing
- No regression allowed
- Tests should not require 'source' field

### Risks Identified

| Risk | Severity | Mitigation |
|------|----------|----------|
| Old payments have NULL source | Medium | Handle NULL gracefully |
| Old tests might fail | Medium | Make source optional, not required |
| Old clients might break | Low | New fields usually ignored safely |
| Database queries fail on NULL | Medium | Query code handles NULL |

### Recommendations

1. Make 'source' field optional (nullable)
2. Use default value "CREDIT_CARD" when not provided
3. Update all 10 existing tests to verify source handling
4. Add new backward compatibility tests
5. Test with real old payment data

## Status
✅ Analysis complete
Backward compatibility: ✅ Possible with precautions
Ready for Step C: Architect creates implementation plan
```

### 8. Your Checklist

Before signing off:

- [ ] Studied current code files
- [ ] Understood the current flow
- [ ] Reviewed existing tests (10 tests)
- [ ] Identified all backward compatibility risks
- [ ] Asked clarifying questions about impacts
- [ ] No critical risks remain unknown
- [ ] Confidence in current behavior understanding

## Your Sign-Off

When analysis is complete:

```
✅ STEP B COMPLETE

Current Behavior Analysis:
- Implementation: ✅ Understood
- Flow: ✅ Documented
- Existing tests: ✅ 10 tests documented
- Backward compatibility risks: ✅ Identified

Key Findings:
1. Old payments have NULL source (must be handled)
2. Old tests must continue passing
3. Old API clients should not break
4. Database changes are safe (additive)

Risks Identified: [List them]
Mitigations: [How to address]

Backward Compatibility: ✅ FEASIBLE

Status: APPROVED by Analyst
Name: [Your name]
Date: [Today]

Ready for Step C: Architect creates implementation plan.
```

## When You're Done

Hand off to Step C:
- ✅ Current behavior documentation
- ✅ Existing test inventory
- ✅ Backward compatibility analysis
- ✅ Risks and mitigations
- ✅ Your sign-off

Next: Step C (Architect creates implementation plan)
