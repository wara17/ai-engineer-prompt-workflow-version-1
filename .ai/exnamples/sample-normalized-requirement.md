# Sample Normalized Requirement

## Goal

Allow clients to optionally send a `source` value when creating a payment.

## In Scope

- Add optional `source` field to create-payment request DTO.
- Persist source if provided.
- Keep old requests valid.
- Return existing response format unchanged.

## Out of Scope

- No new endpoint.
- No change to payment calculation.
- No change to existing required fields.
- No change to existing response fields unless approved.

## Acceptance Criteria

1. Request without `source` still succeeds.
2. Request with valid `source` succeeds.
3. Source is stored when provided.
4. Existing tests continue to pass.
5. Regression test covers old request format.

## Backward Compatibility Requirements

- `source` must be nullable or optional.
- Existing clients must not be forced to send it.
- Existing response contract must not break.
