# Stakeholder Communication

AI progress is hard to communicate because the work is nonlinear. Teams can make major qualitative progress that barely changes a simple KPI, or they can finish implementation while still being far from trustworthy quality.

PMs need a better language for this.

## Communication Matrix

| Leadership question | Better PM response |
| --- | --- |
| “Is 80% accuracy good?” | “It depends on which task and error type. For low-risk suggestions it may be enough; for grounded customer answers it may not be.” |
| “When will it be done?” | “Build completion and quality confidence are separate. Here is where each stands.” |
| “Can’t we just make it better?” | “We can improve it, but the next lift likely trades against cost, latency, or scope. Here are the options.” |
| “Why did progress slow down?” | “We hit quality boundary work: edge cases, eval coverage, and fallback design. That is where production readiness lives.” |

## What To Report Regularly

- mission objective
- build progress
- quality confidence
- key risks
- cost and latency tradeoffs
- decision needed from stakeholders

Do not collapse those into one optimistic update.

## Realistic Use Scenarios

### Scenario 1: Conversational Search

Leadership hears “relevance is 82%.” A better update says: “Core structured queries are strong, but ambiguous lifestyle queries still cause silent constraint drops. Beta is viable only for a limited cohort unless we narrow scope.”

### Scenario 2: Internal Copilot

Leadership sees positive agent sentiment and assumes rollout is ready. A better update says: “Drafting speed improved, but policy-sensitive tickets still require stronger grounding validation before wider release.”

## Questions To Ask Your Engineering Team Before Communicating Upward

- What is genuinely better versus merely implemented?
- Which failure types remain the biggest risk?
- Are we clear on the next improvement step and its tradeoff?
- What decision from leadership would actually help right now?
- Which metric could be misunderstood without context?

## Anti-Patterns

### The Accuracy Theater Update

One number is presented without task context. What goes wrong: leaders draw the wrong conclusion.

### The Demo-Led Update

A great example stands in for broad readiness. What goes wrong: trust later drops when reality catches up.

### The Linear Timeline Fiction

Progress is communicated as if AI quality improves predictably by week. What goes wrong: setbacks look like failure instead of expected learning.

## Red Flags

- Stakeholders keep asking the same clarifying questions every update
- The team reports implementation without quality confidence
- Risks are discussed late because the team fears sounding negative
- Tradeoffs are implied, not stated directly
- Leadership requests keep bouncing because the real decision needed was never made explicit

## Bottom Line

Communicate AI progress with context, tradeoffs, and uncertainty. Leaders can handle nuance if you present it clearly. What they cannot work with is vague optimism.
