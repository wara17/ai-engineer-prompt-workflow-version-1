# Sample Feature

## Raw Request

Add an optional `source` field to payment creation so that callers can identify where the payment request came from. Existing clients must continue working.

## Notes

This is a modification to an existing create-payment API.
The field should be optional.
Old requests without `source` must still work.
