# Error And Hallucination UX

Bad AI outputs are inevitable. The UX question is whether the product handles them in a way that preserves enough trust for the user to continue.

## Recovery Model

| Error type | Better UX response |
| --- | --- |
| Minor formatting issue | Quiet correction or simple retry |
| Low-confidence interpretation | Transparent caveat and refinement option |
| Unsupported request | Clear scope boundary and alternate path |
| Hallucinated factual claim | Apology, correction path, stronger grounding or source display |

## Realistic Use Scenarios

### Scenario 1: Search Result Explanation

If the assistant implies a listing has a feature it does not have, the product should not just fail silently on the next query. It should make correction easy and ensure that future explanations stay grounded.

### Scenario 2: Support Copilot Draft

If the AI drafts a policy-inconsistent reply, the UX should show the source mismatch clearly to the agent and prevent one-click send.

## Questions To Ask Your Engineering Team

- Which error types are most visible to users?
- What signals tell us the output is likely hallucinated or unsupported?
- How can users correct the system quickly?
- When should the product show sources or evidence?
- What should the recovery state look like after a serious wrong answer?

## Anti-Patterns

### The Silent Wrong Answer

The system moves on without acknowledging or enabling correction. What goes wrong: trust decays invisibly.

### The Over-Disclaimer

The product floods every response with caution language. What goes wrong: usefulness drops and users tune out the warnings.

### The Dead-End Error

Users see a vague failure but no next step. What goes wrong: abandonment rises.

## Red Flags

- Users have no quick way to flag or correct bad outputs
- Serious wrong answers are treated like ordinary UI errors
- Source visibility exists only in technical logs
- Recovery UX is generic across very different error types
- The product does not distinguish between “unsure” and “wrong”

## Bottom Line

Trust is not preserved by hiding errors. It is preserved by handling them honestly, specifically, and with useful recovery paths.
