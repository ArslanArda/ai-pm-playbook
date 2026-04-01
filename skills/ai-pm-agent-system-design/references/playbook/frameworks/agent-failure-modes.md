# Agent Failure Modes

Agent systems fail in recurring ways. If you name the patterns early, you can design better mitigations, dashboards, and escalation rules before users discover them for you.

## Failure Taxonomy

| Failure mode | Severity | Detection method | Mitigation strategy |
| --- | --- | --- | --- |
| Infinite or excessive loops | High | Retry count, trace duration, repeated step signatures | Hard retry caps, stop conditions, fallback response |
| Context overflow | High | Token-limit warnings, truncation logs, degraded quality on long sessions | Context pruning, summaries, step isolation |
| Tool hallucination | High | Claimed tool call without matching trace, invalid action result | Strict tool verification, response grounding |
| Cascading failures | High | One upstream failure correlates with multiple downstream errors | Step isolation, explicit abort logic, fallback chain |
| Silent wrong answer | Critical | Human review, user complaints, mismatch analysis | Grounding checks, higher-risk validation, clearer uncertainty messaging |
| Latency spikes | Medium to high | P95/P99 latency, trace bottleneck analysis | Parallelize where possible, reduce hops, timeout policy |
| Partial completion | Medium | User task incomplete but no explicit failure surfaced | Completion checks, user confirmation, clearer end states |
| Guardrail false positives | Medium | High block/reroute rate on valid requests | Threshold tuning, allowlist logic, review samples |
| Misrouting | Medium to high | Route accuracy audit, downstream correction patterns | Better classifier, deterministic rules for common intents |
| Tool timeout or stale data | Medium to high | Tool error logs, freshness checks | Timeout fallback, stale-data messaging, retry rules |

## Why This Matters To PMs

Each failure mode has different product consequences.

- Silent wrong answers damage trust.
- Latency spikes damage usability.
- Guardrail false positives damage adoption.
- Partial completion damages task success and user confidence.

If you treat them all as generic “quality issues,” you will prioritize poorly.

## Realistic Use Scenarios

### Scenario 1: Conversational Search

Misrouting a search query into a support flow is annoying, but silently dropping “must be pet-friendly” from a search interpretation is worse because the results look plausible. That means silent wrong answer deserves stronger mitigation than route elegance.

### Scenario 2: Content Generation

An iterative review loop that retries too aggressively may improve surface quality slightly while doubling cost and latency. In that case, excessive loops are the bigger product problem than occasional imperfect wording.

## Designing For Graceful Degradation

For each failure mode, define:

- what the system does internally
- what the user sees
- whether the task should retry, clarify, hand off, or stop
- what gets logged for review

The user experience of failure is part of the product strategy.

## Questions To Ask Your Engineering Team

- Which failure modes are already visible in traces today?
- Which failures are currently silent from the user’s perspective?
- Which failure types are most expensive versus most trust-damaging?
- What can we validate deterministically before returning a result?
- What is the fallback behavior for each high-severity failure mode?

## Anti-Patterns

### The Single Failure Bucket

Everything is labeled as “agent error.” What goes wrong: prioritization becomes impossible and fixes stay generic.

### The Invisible Wrong Answer

Only hard failures are measured. What goes wrong: the most damaging behavior, plausible-but-wrong output, remains hidden until complaints pile up.

### The Retry Reflex

The system retries many failures automatically. What goes wrong: costs and latency rise while user-facing clarity often gets worse.

## Red Flags

- The team talks about failures mostly through anecdotes
- High-severity failures lack explicit user-facing fallback behavior
- There is no separation between harmless and trust-damaging errors
- Failure taxonomy exists but is not mapped to monitoring or review
- The product sounds confident even after a validation miss

## Bottom Line

Name the failure modes early, rank them by user harm and business risk, and design mitigations before rollout. Agent systems do not fail randomly. They fail in patterns, and those patterns are product-manageable if you treat them that way.
