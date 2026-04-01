# Error And Hallucination UX

Bad AI outputs are inevitable. Generic error handling is optional.

The PM job is to decide which failures deserve quiet recovery, which deserve explicit correction, and which should block the action entirely. If you treat all AI failures like a spinner timeout, you will lose trust faster than your dashboards suggest.

## Default Doctrine

1. Quietly fix cosmetic issues. Do not quietly fix factual ones.
2. Ask for clarification only when the ambiguity changes the outcome materially.
3. If the AI could cause a user to act on wrong information, show evidence, correction, or both.
4. When in doubt, degrade to a narrower but reliable experience instead of a fluent wrong answer.

## Recovery Matrix

| Failure type | Typical signal | User-facing copy | UI action | Logging requirement | PM owner |
| --- | --- | --- | --- | --- | --- |
| Formatting or minor schema issue | Output parses after retry or auto-fix | No apology needed | Quiet retry or auto-correction | Count retry and corrected-output rate | Feature PM |
| Low-confidence interpretation | Confidence below threshold, high ambiguity score | "I may be missing part of what you want. Should I treat this as `rent` or `buy`?" | One targeted clarification or manual filter fallback | Track clarification prompts and abandonment after clarification | Feature PM |
| Unsupported request | Intent outside feature scope | "I can help narrow listings, but I can't assess neighborhood safety or legal risk." | Offer manual path or adjacent supported action | Track unsupported-intent categories | Feature PM plus policy owner |
| Hallucinated factual claim | Evidence mismatch, validator failure, user correction | "That was my mistake. I should not have stated that as a fact." | Remove claim, show grounded fields only, invite correction | Log claim type, source mismatch, and session context | PM plus trust/safety owner |
| High-risk policy conflict | Policy validator or reviewer flags the output | "I can't complete that safely here." | Block send or require human approval | Log blocked action and reason | PM plus policy owner |

## When To Apologize Versus Just Recover

### Apologize when

- the model stated a false fact
- the user could reasonably act on the wrong answer
- the system implied authority it did not have

### Do not apologize when

- the issue is a transient format problem invisible to the user
- a simple clarification is enough and no wrong claim was made
- the user asked for something the product clearly does not support

Over-apologizing makes the product sound fragile. Under-apologizing makes it sound evasive.

## Sample Error-State Copy

### Low-confidence interpretation

`I can run this search, but one part is unclear: should I treat 35,000 as monthly rent or purchase budget?`

### Unsupported request

`I can help narrow listings and compare features. I can't judge whether a neighborhood is safe or a legal document is valid.`

### Factual correction

`I was wrong to say this listing has a balcony. That detail is not confirmed in the listing data.`

### Graceful degradation

`I couldn't fill these fields confidently from the uploaded notes. I've left them blank so you can review them manually.`

## Realistic Use Scenarios

### Scenario 1: Search Result Explanation

If the assistant implies a listing has a sea view when the listing does not confirm it, the right UX is not a generic "something went wrong" toast. The product should:

- remove the unsupported claim
- show only grounded listing facts
- make correction easy
- log the hallucination category

### Scenario 2: Support Copilot Draft

If the AI drafts a policy-inconsistent refund promise, one-click send should disappear. The UI should show:

- the risky sentence
- the policy mismatch reason
- the approved fallback action or escalation path

## Decision Thresholds

Use explicit thresholds. These are defaults you can tune, but you need numbers.

- show one clarification prompt only if ambiguity confidence is below your threshold and retrieval would materially change
- if factual hallucination rate exceeds `2%` in a user-facing flow, add stronger grounding or narrow the feature promise before wider rollout
- if users abandon after clarification above `15%`, your clarification policy is too aggressive or too vague
- if more than `10%` of AI-assisted form fields are rejected, the suggestion UI or confidence thresholds need revision

## Questions To Ask Your Engineering Team

- Which failure types can we detect before the user sees them?
- What evidence or validator signal tells us a claim is unsupported?
- Which recovery states can stay silent, and which must be explicit?
- What is our threshold for asking a clarification question instead of continuing?
- If we degrade gracefully here, what narrower but still useful experience do we offer?

## Anti-Patterns

### The Silent Wrong Answer

What happens:

- the user moves forward based on an uncorrected false claim

Why it happens:

- the team optimizes for smoothness over trust

What to do instead:

- distinguish cosmetic errors from factual ones and require explicit correction for the latter

### The Over-Disclaimer

What happens:

- every response is wrapped in generic uncertainty text

Why it happens:

- the team is afraid of selective accountability

What to do instead:

- show caveats only when they change how the user should interpret the output

### The Dead-End Error

What happens:

- users see a failure state with no alternative action

Why it happens:

- fallback design was postponed until after launch

What to do instead:

- define the manual path, narrower path, or escalation path during product design

## Red Flags

- Users cannot correct bad outputs quickly
- Serious wrong answers are handled like ordinary loading failures
- Recovery copy does not change by failure type
- Clarification prompts are rising without a corresponding quality gain
- The team logs failure events but cannot map them to visible UX states

## Bottom Line

Trust is preserved when the product is specific about failure. The more harmful the AI mistake, the more specific the recovery should be.
