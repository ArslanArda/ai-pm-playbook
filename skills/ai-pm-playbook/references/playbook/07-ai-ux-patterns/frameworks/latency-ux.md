# Latency UX

Users do not experience latency only as time. They experience it as uncertainty, lack of control, and broken expectation.

## Practical Latency Thresholds

- **<1s:** feels instant
- **1-3s:** usually acceptable with lightweight progress signal
- **3-10s:** needs streaming, progressive disclosure, or visible staged progress
- **>10s:** should usually shift to async, background, or clearly staged workflow

## Pattern Map

| Latency range | Recommended UX |
| --- | --- |
| <1s | Minimal transition, keep flow tight |
| 1-3s | Spinner or subtle loading state |
| 3-10s | Streaming response, progressive disclosure, skeleton states |
| >10s | Async handoff, notifications, draft generation, background processing |

## Realistic Use Scenarios

### Scenario 1: AI Search Summary

Results should appear progressively or with partial grounding rather than a blank wait if the response takes 4-5 seconds.

### Scenario 2: Listing Description Drafting

If generation takes 20 seconds, do not trap the user on a frozen screen. Let them continue editing the listing while the draft prepares asynchronously.

## Questions To Ask Your Engineering Team

- What are P50 and P95 latency targets for this feature?
- Which steps can be streamed or shown progressively?
- Can part of the experience be rendered before the full AI output is ready?
- Is the current loading state honest about what is happening?
- Should this workflow become async rather than pretending to be real-time?

## Anti-Patterns

### Spinner Abuse

Long waits are hidden behind an indefinite spinner. What goes wrong: users feel the product is stuck or unreliable.

### Fake Streaming

The UI streams text that is not meaningfully useful yet. What goes wrong: motion creates the illusion of progress without real value.

### Real-Time Pretending

An async-worthy task is forced into synchronous UX. What goes wrong: frustration and abandonment rise.

## Red Flags

- P95 latency is far higher than the UX pattern implies
- Users cannot tell whether the system is working or stuck
- Long waits are frequent, but no background pattern exists
- Streaming text often gets rewritten heavily before finishing
- Teams talk about latency only as infrastructure, not as UX

## Bottom Line

Design for the latency you actually have, not the latency you wish you had. Honest, useful waiting experiences protect trust far better than pretending the response is faster than it is.
