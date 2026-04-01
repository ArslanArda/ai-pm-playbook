# PM Data Rituals

AI PMs need data rituals because build progress alone tells you very little about whether the product is improving.

## Recommended Ritual Cadence

| Frequency | Attendees | Agenda | Output |
| --- | --- | --- | --- |
| Daily 15 min | PM, eng lead, relevant operator | Review flagged outputs, latency spikes, blocker failures | Immediate actions and bug triage |
| Weekly 45-60 min | PM, engineering, design, ops, analytics | Quality trends, cost review, routing/fallback review, user feedback | Weekly decision log |
| End of cycle 60-90 min | Full mission team + stakeholders as needed | Evaluate mission outcome, quality confidence, carryover proposals | Ship/extend/stop decision |

## Daily Ritual

Look at:

- flagged outputs
- complaint clusters
- validation failures
- major latency regressions

The goal is not deep analysis. It is to catch obvious issues early.

## Weekly Ritual

Look at:

- eval trend changes
- top error categories
- token and cost movement
- fallback and handoff rate
- user feedback patterns

This is where PMs decide whether the roadmap should change, not just whether bugs need fixes.

## Cycle-Level Ritual

Ask:

- what did we prove?
- what is still too weak to ship?
- what got better but still lacks confidence?
- what should be simplified rather than extended?

## Realistic Use Scenarios

### Scenario 1: Search Feature

Daily review catches a spike in fallback rate after a prompt change. Weekly review reveals the real issue: ambiguous location handling regressed specifically for Turkish misspellings.

### Scenario 2: Internal Copilot

Weekly review shows drafting quality is fine, but adoption is weak because agents do not trust account-state references. The roadmap shifts toward transparency work instead of prompt tuning.

## Questions To Ask Your Engineering Team

- Which metrics genuinely drive decisions, and which are just interesting?
- What failure signals should appear in the daily review?
- Can we segment metrics by route, feature state, or user cohort?
- What trend would justify rollback or stricter gating?
- Which rituals currently exist but are not changing any decisions?

## Anti-Patterns

### Dashboard Tourism

People scan charts but no decision follows. What goes wrong: data review becomes ceremonial.

### Build Status Dominance

AI review meetings get overtaken by sprint delivery updates. What goes wrong: quality signals become secondary until late.

### Anecdote Override

One memorable demo or failure dominates the conversation. What goes wrong: trend data loses authority.

## Red Flags

- The PM cannot say what the daily ritual is for
- Weekly review has no standing agenda
- Cost review happens only when finance asks
- User feedback is discussed without trace or eval context
- The team does not separate blocker failures from minor quality issues

## Bottom Line

Install a small number of disciplined rituals tied to concrete decisions. AI PM work improves faster when the team reviews the right signals at the right cadence.
