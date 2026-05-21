# Role A: Requirement Owner

## Your Job

Clarify the requirement completely. Ask questions until there's no ambiguity.

## Responsibilities

✅ Understand what's needed  
✅ Ask clarifying questions  
✅ Document acceptance criteria  
✅ Identify edge cases  
✅ Sign off when crystal clear  

## What You Do

### 1. Understand the Raw Requirement

User gives you something like:
```
Add optional source field to payments.
Existing clients must work.
```

### 2. Ask Clarifying Questions

Don't assume anything. Ask:

**About the change:**
- Q: "When user doesn't provide source, what's the default?"
- Q: "What are valid source values?"
- Q: "Can source be changed after creation?"
- Q: "Any business logic depending on source?"

**About backward compatibility:**
- Q: "Will old payments (without source) work with new code?"
- Q: "Do old API clients need to work without changes?"
- Q: "Any database migration needed?"
- Q: "Should API return source for old payments?"

**About edge cases:**
- Q: "What if user provides invalid source?"
- Q: "What if source is null vs empty string?"
- Q: "Any source-specific validations?"
- Q: "Any security implications?"

**About acceptance criteria:**
- Q: "How do we test this is working?"
- Q: "What counts as success?"
- Q: "Any performance requirements?"
- Q: "Any UI/documentation changes needed?"

### 3. Document the Clarified Requirement

```markdown
# Requirement: Add Optional Payment Source

## What
Add an optional 'source' field to payment creation.
Old clients must continue to work without changes.

## Why
Allow clients to specify where payment came from.
Improve payment tracking and analytics.

## Acceptance Criteria
1. ✅ New API accepts optional 'source' field
2. ✅ Valid values: CREDIT_CARD, BANK_TRANSFER, WALLET
3. ✅ Default source: CREDIT_CARD (if not provided)
4. ✅ Old clients work without providing source
5. ✅ Old payments display with null source
6. ✅ No database migration required

## Edge Cases
1. ✅ If source is null → use default
2. ✅ If source is invalid → reject with error
3. ✅ If source is empty string → use default
4. ✅ Old data (null source) remains readable

## NOT in Scope
❌ Change existing source values in old payments
❌ UI changes to select source
❌ New reporting features
❌ Payment source history tracking

## Sign-Off
Requirement Owner: [Your name]
Date: [Today]
Status: ✅ APPROVED
```

### 4. Potential Questions to Ask

#### About Requirements Scope

- "What exactly should change?"
- "What should stay the same?"
- "What's the minimum viable change?"
- "Any nice-to-haves vs must-haves?"

#### About User Impact

- "Who will use this feature?"
- "How often will it be used?"
- "Any user communication needed?"
- "Any training required?"

#### About System Impact

- "Will existing code break?"
- "Do old API clients need changes?"
- "Any database changes needed?"
- "Any configuration changes needed?"

#### About Validation & Error Handling

- "What makes a valid [field]?"
- "What should happen if validation fails?"
- "Any specific error messages needed?"
- "How should system handle edge cases?"

#### About Backward Compatibility

- "Will old data work with new code?"
- "Will old clients work with new API?"
- "Any deprecation needed?"
- "Any migration needed?"

#### About Testing

- "How do we verify this works?"
- "What should we test?"
- "Any specific scenarios to test?"
- "Any performance requirements?"

### 5. Example Q&A Session

**User says:** "Add optional source to payments"

**You ask:** "What are valid source values?"
**User answers:** "CREDIT_CARD, BANK_TRANSFER, WALLET"

**You ask:** "What's the default if not provided?"
**User answers:** "CREDIT_CARD"

**You ask:** "Will old payments (from before this change) have source?"
**User answers:** "No, they'll be null"

**You ask:** "Should old API clients still work without providing source?"
**User answers:** "Yes, backward compatible"

**You ask:** "Should API response include source for old payments?"
**User answers:** "Yes, show null if old"

**Result:** Now you understand clearly!

### 6. Sign-Off Checklist

Before signing off:

- [ ] Requirement is specific (not vague)
- [ ] Edge cases identified
- [ ] Acceptance criteria clear
- [ ] What's NOT included is clear
- [ ] Backward compatibility understood
- [ ] Any ambiguity resolved
- [ ] No assumptions left

### 7. Create Requirement Document

```markdown
# Feature Requirement Document

## Feature
Add Optional Payment Source Field

## Business Need
Track where payments come from for analytics and customer support.

## What Changes
- Add 'source' field to Payment entity (optional, nullable)
- Accept 'source' in payment creation API
- Support values: CREDIT_CARD, BANK_TRANSFER, WALLET
- Default to CREDIT_CARD if not provided

## What Doesn't Change
- Old payments remain unchanged (null source)
- Old API clients continue to work
- No database migration
- No UI changes (backend only)

## Acceptance Criteria
✅ New payments can have source field
✅ Old clients don't break
✅ Old payments still readable
✅ Tests pass
✅ Code coverage >80%

## Known Constraints
- Database is append-only (can't migrate old data)
- API must stay backward compatible
- No breaking changes allowed

## Questions Resolved
Q: What if source is null?
A: Use CREDIT_CARD as default

Q: Will old code break?
A: No, source is optional

Q: Can old clients update source?
A: No, source is set at creation only

## Status
✅ APPROVED by Requirement Owner
Date: [Today]
Ready for Step B: Analyst
```

## Your Sign-Off

When you're confident:

```
✅ STEP A COMPLETE

Requirement: [Clear statement]
Acceptance Criteria: ✅ [Count] criteria defined
Edge Cases: ✅ Identified and documented
Backward Compatibility: ✅ Understood
Ambiguity Level: ✅ None (crystal clear)

Status: APPROVED by Requirement Owner
Name: [Your name]
Date: [Today]

Ready for Step B: Analyst to analyze current behavior.
```

## Common Mistakes to Avoid

❌ **Assume you understand** - Always ask clarifying questions
❌ **Skip edge cases** - Ask about error scenarios
❌ **Forget backward compatibility** - Always ask about old code/clients
❌ **Be vague** - Get specific answers
❌ **Skip sign-off** - Explicit approval prevents confusion
❌ **Move forward with questions** - Resolve ALL ambiguity first

## When You're Done

Hand off to Step B:
- ✅ Requirement document
- ✅ Acceptance criteria
- ✅ Edge cases documented
- ✅ Your sign-off

Next: Step B (Analyst analyzes current behavior)
