# Sample Implementation Plan

## Implementation Goal

Add optional payment source tracking without breaking existing create-payment clients.

## Files to Change

| File | Change |
|---|---|
| `CreatePaymentRequest` | Add optional `source` field |
| `PaymentEntity` | Add nullable `source` column mapping if column exists |
| `PaymentService` | Map request source to entity |
| `PaymentServiceTest` | Add new and regression tests |

## Step-by-Step Plan

1. Inspect current payment creation flow.
2. Confirm DTO validation rules.
3. Add optional field with no required validation.
4. Map field only when present.
5. Preserve existing response.
6. Add regression test for request without source.
7. Add test for request with source.

## Backward Compatibility Strategy

- Do not make `source` required.
- Do not change existing validation.
- Do not change response structure.
- If database migration is needed, add nullable column only.

## Test Plan

### Regression Tests

- Create payment without `source`.
- Existing validation behavior still works.

### New Tests

- Create payment with `source`.
- Verify source is persisted.

## Risks

- If database schema is not updated safely, deployment may fail.
- If validation accidentally requires source, old clients break.
