# Role D: Developer (Implementation)

## Your Job

Write code according to the implementation plan from Step C.

## Responsibilities

✅ Follow the plan exactly  
✅ Write clean code  
✅ Verify code compiles  
✅ Do basic testing  
✅ Sign off when done  

## What You Do

### 1. Get Implementation Plan (From Step C)

You receive:
- Detailed implementation plan
- Files to modify
- Approach to use
- Backward compatibility requirements
- Approvals from A, B, and C

### 2. Follow the Plan Step-by-Step

**Never deviate from the plan!**

```
If the plan says:
✓ Modify 6 files
✗ Don't add extra files

If the plan says:
✓ Add source field
✗ Don't add other fields

If the plan says:
✓ Make source optional
✗ Don't make it required
```

### 3. Implement Each File

**File 1: Payment.java (Entity)**

```java
public class Payment {
    private String id;
    private BigDecimal amount;
    private String currency;
    private String source;  // NEW FIELD
    private LocalDateTime createdAt;
    
    // Constructor
    public Payment() {
    }
    
    // Getters and Setters
    public String getId() {
        return id;
    }
    
    public void setId(String id) {
        this.id = id;
    }
    
    public BigDecimal getAmount() {
        return amount;
    }
    
    public void setAmount(BigDecimal amount) {
        this.amount = amount;
    }
    
    public String getCurrency() {
        return currency;
    }
    
    public void setCurrency(String currency) {
        this.currency = currency;
    }
    
    public String getSource() {  // NEW GETTER
        return source;
    }
    
    public void setSource(String source) {  // NEW SETTER
        this.source = source;
    }
    
    public LocalDateTime getCreatedAt() {
        return createdAt;
    }
    
    public void setCreatedAt(LocalDateTime createdAt) {
        this.createdAt = createdAt;
    }
}
```

**File 2: PaymentRequest.java (DTO)**

```java
public class PaymentRequest {
    @NotNull(message = "Amount is required")
    private BigDecimal amount;
    
    @NotNull(message = "Currency is required")
    private String currency;
    
    @Nullable  // NEW: Optional field
    private String source;
    
    // Constructors
    public PaymentRequest() {
    }
    
    public PaymentRequest(BigDecimal amount, String currency) {
        this.amount = amount;
        this.currency = currency;
    }
    
    // Getters and Setters
    public BigDecimal getAmount() {
        return amount;
    }
    
    public void setAmount(BigDecimal amount) {
        this.amount = amount;
    }
    
    public String getCurrency() {
        return currency;
    }
    
    public void setCurrency(String currency) {
        this.currency = currency;
    }
    
    public String getSource() {  // NEW GETTER
        return source;
    }
    
    public void setSource(String source) {  // NEW SETTER
        this.source = source;
    }
}
```

**File 3: PaymentValidator.java (Validation)**

```java
public class PaymentValidator {
    private static final List<String> VALID_SOURCES = 
        Arrays.asList("CREDIT_CARD", "BANK_TRANSFER", "WALLET");
    
    public void validatePayment(PaymentRequest request) throws ValidationException {
        validateAmount(request.getAmount());
        validateCurrency(request.getCurrency());
        validateSource(request.getSource());  // NEW
    }
    
    private void validateAmount(BigDecimal amount) throws ValidationException {
        if (amount == null) {
            throw new ValidationException("Amount is required");
        }
        if (amount.compareTo(BigDecimal.ZERO) <= 0) {
            throw new ValidationException("Amount must be greater than zero");
        }
    }
    
    private void validateCurrency(String currency) throws ValidationException {
        if (currency == null || currency.trim().isEmpty()) {
            throw new ValidationException("Currency is required");
        }
    }
    
    private void validateSource(String source) throws ValidationException {  // NEW METHOD
        // Source is optional, but if provided must be valid
        if (source != null && !source.trim().isEmpty()) {
            if (!VALID_SOURCES.contains(source)) {
                throw new ValidationException(
                    "Invalid source. Valid sources: " + VALID_SOURCES);
            }
        }
    }
}
```

**File 4: PaymentService.java (Business Logic)**

```java
public class PaymentService {
    private PaymentRepository repository;
    private PaymentValidator validator;
    
    public PaymentService(PaymentRepository repository, PaymentValidator validator) {
        this.repository = repository;
        this.validator = validator;
    }
    
    public Payment createPayment(PaymentRequest request) throws ValidationException {
        // Validate input
        validator.validatePayment(request);
        
        // Create payment entity
        Payment payment = new Payment();
        payment.setId(UUID.randomUUID().toString());
        payment.setAmount(request.getAmount());
        payment.setCurrency(request.getCurrency());
        
        // NEW: Set source with default
        String source = request.getSource();
        if (source == null || source.trim().isEmpty()) {
            source = "CREDIT_CARD";  // Default
        }
        payment.setSource(source);
        
        payment.setCreatedAt(LocalDateTime.now());
        
        // Save to database
        return repository.save(payment);
    }
    
    public Payment getPaymentById(String id) {
        return repository.findById(id).orElse(null);
    }
}
```

**File 5: PaymentResponse.java (Response DTO)**

```java
public class PaymentResponse {
    private String id;
    private BigDecimal amount;
    private String currency;
    private String source;  // NEW FIELD
    private LocalDateTime createdAt;
    
    public PaymentResponse(Payment payment) {
        this.id = payment.getId();
        this.amount = payment.getAmount();
        this.currency = payment.getCurrency();
        this.source = payment.getSource();  // NEW
        this.createdAt = payment.getCreatedAt();
    }
    
    // Getters (for JSON serialization)
    public String getId() { return id; }
    public BigDecimal getAmount() { return amount; }
    public String getCurrency() { return currency; }
    public String getSource() { return source; }  // NEW
    public LocalDateTime getCreatedAt() { return createdAt; }
}
```

**File 6: Database Schema Migration**

```sql
-- Add source column (non-breaking change)
-- Can be run safely even if column already exists
ALTER TABLE payments ADD COLUMN source VARCHAR(50) DEFAULT NULL;
```

### 4. Compile and Verify

```bash
# Compile
mvn clean compile

# Expected: BUILD SUCCESS
```

### 5. Run Basic Tests

```bash
# Run old tests (should all pass - no regression)
mvn test -Dtest=PaymentTest

# Expected: ✅ All 10 existing tests pass
```

### 6. Manual Smoke Test

```java
// Quick manual test
PaymentRequest request = new PaymentRequest();
request.setAmount(new BigDecimal("100.00"));
request.setCurrency("USD");
request.setSource("CREDIT_CARD");

PaymentService service = new PaymentService(repo, validator);
Payment payment = service.createPayment(request);

System.out.println(payment.getSource());  // Should print: CREDIT_CARD

// Test default source
PaymentRequest request2 = new PaymentRequest();
request2.setAmount(new BigDecimal("50.00"));
request2.setCurrency("USD");
request2.setSource(null);  // No source provided

Payment payment2 = service.createPayment(request2);
System.out.println(payment2.getSource());  // Should print: CREDIT_CARD (default)
```

### 7. Documentation

```markdown
# Implementation Summary

## Files Modified
1. ✅ Payment.java - Added source field
2. ✅ PaymentRequest.java - Added source parameter
3. ✅ PaymentValidator.java - Added source validation
4. ✅ PaymentService.java - Applied default source
5. ✅ PaymentResponse.java - Included source in response
6. ✅ Database schema - Added source column

## Verification
- ✅ Code compiles without errors
- ✅ Old tests pass (10/10)
- ✅ Basic manual smoke tests pass
- ✅ Default source applied correctly
- ✅ Validation works for invalid sources
- ✅ Backward compatible (old payments work)

## What's Ready
- ✅ All code implemented per plan
- ✅ Code follows existing style
- ✅ No breaking changes
- ✅ Ready for unit testing (Step E)
```

## Your Checklist

Before signing off:

- [ ] Followed implementation plan exactly
- [ ] All 6 files modified as planned
- [ ] Code compiles without errors
- [ ] Old tests pass (no regression)
- [ ] Basic manual tests pass
- [ ] Default source working correctly
- [ ] Invalid source rejected correctly
- [ ] Code follows existing style
- [ ] No extra changes beyond plan

## Your Sign-Off

```
✅ STEP D COMPLETE

Implementation:
- Files modified: 6
- Code compiles: ✅ YES
- Old tests passing: ✅ 10/10 (no regression)
- Basic smoke tests: ✅ PASSED

What's Implemented:
1. ✅ Added source field to Payment entity
2. ✅ Added source parameter to API
3. ✅ Added source validation
4. ✅ Apply default source (CREDIT_CARD)
5. ✅ Include source in response
6. ✅ Database schema updated

Quality Checks:
- Compiles: ✅ NO ERRORS
- Old tests: ✅ NO REGRESSION
- Manual tests: ✅ PASSED
- Code style: ✅ FOLLOWS CONVENTIONS

Status: APPROVED by Developer
Developer: [Your name]
Date: [Today]

Ready for Step E: Generate unit tests.
```

## Common Issues & Solutions

**❌ Code won't compile**
- Check imports are correct
- Check syntax (semicolons, brackets)
- Check type names match

**❌ Old tests fail**
- Don't modify old tests
- Check if source is truly optional
- Make sure default is applied

**❌ Source not being set**
- Check PaymentService applies default
- Check getSource() getter exists
- Check setter is public

## When You're Done

Hand off to Step E:
- ✅ Implemented code
- ✅ All files compiled
- ✅ Old tests passing
- ✅ Basic manual tests passing
- ✅ Your sign-off

Next: Step E (Tester writes comprehensive unit tests)
