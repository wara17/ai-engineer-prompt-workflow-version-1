# Role C: Architect

## Your Job

Create a detailed implementation plan that both Role A (Requirement Owner) and Role B (Analyst) approve.

## Responsibilities

✅ Design the solution  
✅ Identify files to change  
✅ Verify no side effects  
✅ Create detailed plan  
✅ Get approval from A & B  
✅ Sign off when approved  

## What You Do

### 1. Get Previous Work

You receive:
- Clear requirement (from Step A)
- Current behavior analysis (from Step B)
- Backward compatibility concerns (from Step B)
- Requirement Owner approval (Step A)
- Analyst approval (Step B)

### 2. Design the Solution

**Ask yourself:**

- "What files need to change?"
- "What's the minimal change needed?"
- "Will this break anything?"
- "Are there alternative approaches?"
- "Is this the best approach?"

### 3. Create Implementation Plan

```markdown
# Implementation Plan: Add Optional Payment Source

## Overview
Add optional 'source' field to payment system.
Minimal changes for maximum compatibility.

## Design Decision
Add new field, make optional, default to CREDIT_CARD.
No database migration (nullable column).
No breaking changes to API.

## Files to Modify

### 1. Payment.java (Entity)
**Change:** Add source field
```java
public class Payment {
    private String id;
    private BigDecimal amount;
    private String currency;
    private String source;  // NEW FIELD
    private LocalDateTime createdAt;
    
    // Getters/setters for source
    public String getSource() { return source; }
    public void setSource(String source) { this.source = source; }
}
```

### 2. PaymentRequest.java (DTO)
**Change:** Add source as optional field
```java
public class PaymentRequest {
    @NotNull
    private BigDecimal amount;
    
    @NotNull
    private String currency;
    
    @Nullable  // NEW: Optional field
    @ValidSource  // NEW: Custom validation
    private String source;
}
```

### 3. PaymentValidator.java (Validation)
**Change:** Add source validation
```java
public class PaymentValidator {
    private static final List<String> VALID_SOURCES = 
        Arrays.asList("CREDIT_CARD", "BANK_TRANSFER", "WALLET");
    
    public void validatePayment(PaymentRequest request) {
        validateAmount(request.getAmount());
        validateCurrency(request.getCurrency());
        validateSource(request.getSource());  // NEW
    }
    
    private void validateSource(String source) {
        if (source != null && !VALID_SOURCES.contains(source)) {
            throw new InvalidSourceException("Invalid source: " + source);
        }
    }
}
```

### 4. PaymentService.java (Business Logic)
**Change:** Apply default source if not provided
```java
public class PaymentService {
    public Payment createPayment(PaymentRequest request) {
        Payment payment = new Payment();
        payment.setAmount(request.getAmount());
        payment.setCurrency(request.getCurrency());
        // NEW: Set source with default
        payment.setSource(request.getSource() != null ? 
                         request.getSource() : "CREDIT_CARD");
        
        return repository.save(payment);
    }
}
```

### 5. PaymentTest.java (Unit Tests)
**Change:** Add source field tests
- Test with source provided
- Test without source (default applied)
- Test invalid source (rejected)
- Test backward compatibility (old tests still pass)

### 6. Database Schema
**Change:** Add nullable column
```sql
-- Add new column (non-breaking, backward compatible)
ALTER TABLE payments ADD COLUMN source VARCHAR(50);

-- No migration needed (defaults to NULL)
-- Old rows: source will be NULL
-- New rows: source will be set based on input
```

## Implementation Order

1. Add source field to Payment entity
2. Add source to PaymentRequest DTO
3. Add source validation to PaymentValidator
4. Update PaymentService to handle source
5. Write unit tests
6. Verify old tests still pass
7. Add backward compatibility tests

## Backward Compatibility Strategy

**For old payments (already in database):**
- source will be NULL
- Reading old payments: source = NULL is OK
- Displaying old payments: show NULL or use default

**For old API clients:**
- They don't send source → Optional for them
- They get source in response → Usually safe (ignored)
- They don't break → Additive change (safe)

**For old tests:**
- All 10 existing tests must pass
- No changes required to old test code
- New tests verify source handling
- New tests verify backward compatibility

## Test Plan

### New Tests (12 total)

**Happy Path (4 tests):**
- Create payment with source = CREDIT_CARD
- Create payment with source = BANK_TRANSFER
- Create payment with source = WALLET
- Create payment without source (default applied)

**Error Cases (3 tests):**
- Reject invalid source
- Handle NULL source (use default)
- Handle empty string source (use default)

**Backward Compatibility (2 tests):**
- Old test payment works (no source field)
- Old data retrieved correctly (NULL source)

### Existing Tests (10 tests)
- All should still pass (no changes needed)
- Verify no regression

## No Breaking Changes

✅ Old payments still readable (NULL source is OK)  
✅ Old API clients still work (source is optional)  
✅ Old database works (schema change is additive)  
✅ Old tests still pass (no modifications required)  

## Risks Mitigated

| Risk | Mitigation |
|------|----------|
| Old payments break | source is nullable |
| Old clients break | source is optional in request |
| Old tests fail | old tests don't need to know about source |
| Unexpected side effects | minimal change, only adds new field |

## Alternative Approaches Considered

❌ **Option 1: Make source required**
- REJECTED: Would break old clients

❌ **Option 2: Migrate all old payments to have source**
- REJECTED: Complex database migration, unnecessary

✅ **Option 3: Make source optional, default to CREDIT_CARD** (SELECTED)
- SELECTED: Backward compatible, minimal changes, meets requirements

## Cost/Benefit

- **Cost:** 5-6 hours development + testing
- **Benefit:** Required feature for payment tracking
- **Risk:** Very low (backward compatible)
- **Confidence:** High (straightforward change)

## Dependencies

- None (independent feature)
- No external service calls
- No third-party library updates

## Database Schema Evolution

```sql
-- Before
CREATE TABLE payments (
    id VARCHAR(50) PRIMARY KEY,
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    created_at TIMESTAMP NOT NULL
);

-- After (fully backward compatible)
CREATE TABLE payments (
    id VARCHAR(50) PRIMARY KEY,
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    source VARCHAR(50),  -- NEW: nullable, defaults to NULL
    created_at TIMESTAMP NOT NULL
);

-- No migration script needed
-- Old rows: source = NULL
-- New rows: source = provided value or default
```

## Code Quality

- Follows existing code style
- Unit tests included (>80% coverage)
- No code duplication
- Clear variable names
- No hardcoded values outside config

## Deployment

- No special deployment steps
- Database change is backwards compatible
- No feature flags needed (optional by default)
- Immediate rollout possible

## Sign-Off Requirements

Before proceeding to implementation:

- [ ] Requirement Owner (A) reviews and approves plan
- [ ] Analyst (B) reviews and confirms backward compatibility
- [ ] Architect (C) confirms plan is complete and clear

## Status
✅ Plan complete and ready for approval
```

### 4. Get Approvals

**From Role A (Requirement Owner):**

```
Does this plan meet your requirement?
1. Add optional source field ✓
2. Accept source in API ✓
3. Default to CREDIT_CARD ✓
4. Backward compatible ✓

Approve? ✅ YES
```

**From Role B (Analyst):**

```
Does this plan address backward compatibility risks?
1. Old payments won't break ✓
2. Old API clients work ✓
3. Old tests pass ✓
4. No database migration ✓

Approve? ✅ YES
```

**From You (Architect):**

```
Are you confident this plan will work?
1. Design is sound ✓
2. All files identified ✓
3. No hidden side effects ✓
4. Backward compatible ✓

Ready to proceed? ✅ YES
```

### 5. Your Sign-Off

```
✅ STEP C COMPLETE

Implementation Plan:
- Files to modify: 6 files
- New tests needed: 12 tests
- Backward compatible: ✅ YES
- Database migration: ❌ NONE NEEDED
- Estimated effort: 5-6 hours

Approvals:
- ✅ Role A (Requirement Owner) approved
- ✅ Role B (Analyst) approved
- ✅ Role C (Architect) approved

Status: APPROVED
Architect: [Your name]
Date: [Today]

Ready for Step D: Developer implements code.
```

## Your Checklist

Before signing off:

- [ ] Plan addresses all requirements
- [ ] Plan respects backward compatibility risks
- [ ] All files to modify identified
- [ ] No unexpected side effects
- [ ] Alternative approaches considered
- [ ] Role A approval obtained
- [ ] Role B approval obtained
- [ ] Confidence in plan completeness

## When You're Done

Hand off to Step D:
- ✅ Detailed implementation plan
- ✅ List of files to modify
- ✅ Database changes (if any)
- ✅ Test plan
- ✅ Approvals from A & B
- ✅ Your sign-off

Next: Step D (Developer implements code)
