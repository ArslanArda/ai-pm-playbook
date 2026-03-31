# DACI For AI

AI work creates decision ambiguity fast. PMs, engineers, designers, data people, and leaders all have valid inputs, but input is not the same as ownership.

DACI works well for AI teams because it clarifies:

- who drives the work
- who approves the decision
- who contributes expertise
- who must stay informed

## Common AI Decisions And Recommended DACI Mapping

| Decision | Driver | Approver | Contributors | Informed |
| --- | --- | --- | --- | --- |
| Feature scope and user problem | PM | Product lead | Design, engineering | Leadership |
| Model choice | Engineering lead | PM or product lead | Data, infra, finance if needed | Leadership |
| Prompt strategy | PM | PM | Engineering, design, ops | Team |
| Evaluation rubric | PM | PM | Engineering, ops, QA | Leadership if high risk |
| Launch gate | PM | Product lead or GM | Engineering, support, legal if needed | Broader team |
| Quality veto on borderline launch | PM + accountable leader | Product lead or GM | Engineering, ops, legal | Team |

Adjust the table to your context, but do not leave these decisions ownerless.

## Pre-Filled DACI Template

Use this as a starting point:

- **Decision:** [e.g., Whether to launch conversational search beta]
- **Driver:** [e.g., AI PM]
- **Approver:** [e.g., VP Product]
- **Contributors:** [e.g., Search eng lead, design lead, support ops]
- **Informed:** [e.g., Sales, exec staff, CX]

## Realistic Use Scenarios

### Scenario 1: Prompt Quality Conflict

PM wants stricter groundedness; engineering wants broader helpfulness. DACI clarifies that PM drives the product behavior decision, engineering contributes technical constraints, and the approver breaks true deadlock.

### Scenario 2: Borderline Launch Quality

Eval scores are close, but complaint risk is unclear. DACI prevents last-minute escalation chaos by making the launch approver and veto path explicit in advance.

## Questions To Ask Your Engineering Team

- Which AI decisions feel slow because ownership is unclear?
- Are we treating contribution as implicit approval?
- Who can block launch on quality grounds today?
- Which decisions need one owner even if many people contribute?
- Where do we need a stronger tie-break mechanism?

## Anti-Patterns

### Shared Ownership Everywhere

Everything is collaborative. What goes wrong: decisions drift and conflicts surface late.

### Technical Default Ownership

Engineering owns the model and quietly ends up owning the product behavior too. What goes wrong: user-facing tradeoffs lose product accountability.

### Executive Surprise

Leaders are informed only when a decision is already politically loaded. What goes wrong: approvals slow down and trust drops.

## Red Flags

- Teams argue about who “should decide” during the decision itself
- Prompt, eval, and launch decisions have different owners every week
- Quality concerns surface, but no one knows who has veto authority
- Contributors expect approval rights that were never defined
- Decisions get revisited because ownership was unclear

## Bottom Line

AI work is too cross-functional for implicit ownership. Use DACI to turn collaboration into clear decision flow, not slower consensus theater.
