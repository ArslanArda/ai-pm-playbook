# Tool And MCP Design

Tool design is a product decision because tools define what the model can reliably know, do, and claim.

Poor tool design creates vague actions, high token usage, confusing failures, and silent trust problems. Good tool design narrows the model’s freedom where determinism matters and preserves flexibility where interpretation actually adds value.

## Tool vs. Prompt Decision Matrix

| Capability type | Keep in prompt when... | Make it a tool when... |
| --- | --- | --- |
| Formatting or rewriting | No live data or side effect is needed | Structured output must be validated externally |
| Retrieval | Context is static and small | Live, scoped, or permissioned data is required |
| Action execution | Never, if real action occurs | The system must call a real service or workflow |
| Deterministic policy checks | Never, if rules are strict | A rule or policy system should enforce the decision |
| Multi-source lookup | Small and cached | Multiple systems or permissions are involved |

Rule of thumb: if the model needs live data, causes a side effect, or must obey a precise schema, it probably belongs in a tool or deterministic layer.

## Tool Granularity: One Big Tool vs. Many Small Tools

### One big tool is better when:

- the task is conceptually one product action
- splitting would create routing noise
- the underlying system already exposes one stable operation

### Many smaller tools are better when:

- failure handling differs by step
- permissions or visibility differ by data source
- you need step-level observability and retry control

The PM question is not “what is more elegant?” It is “which boundary gives us the right combination of control, simplicity, and traceability?”

## Designing Schemas That Reduce Ambiguity

A good tool schema:

- uses product-language fields the model can map to reliably
- keeps required parameters explicit
- limits optional clutter
- avoids overlapping fields that invite confusion
- mirrors the user’s real intent structure when possible

Bad schemas cause the model to guess, omit, or misuse fields. That becomes a product quality issue because bad tool calls produce bad outcomes even if the model reasoning sounded plausible.

## PM-Level Principles For Tool Design

### 1. Make high-risk claims depend on grounded tools

If a user-facing answer depends on inventory status, pricing, policy, or account data, the system should call the authoritative source instead of reasoning from memory or stale context.

### 2. Keep product policy outside model discretion

Eligibility rules, pricing permissions, compliance checks, and escalation rules should not live only in prompts.

### 3. Design for failure visibility

Every important tool should fail in a way the product can react to cleanly. “Tool failed” is not enough. The system should know whether the failure is timeout, no result, permission denied, or invalid input.

## Realistic Use Scenarios

### Scenario 1: Marketplace Search

Search should be a tool, not a prompt behavior. The model interprets user intent, but the search system returns inventory truth. This keeps ranking, filtering, and result integrity grounded.

### Scenario 2: Support Copilot

Policy lookup should be a tool or deterministic retrieval layer. Drafting tone can stay in prompt logic. This prevents the assistant from inventing return-policy details while preserving flexible writing assistance.

## Questions To Ask Your Engineering Team

- Which user-facing claims should only be made if supported by authoritative tool output?
- Where are we relying on prompt behavior for something that should be deterministic?
- Which tool failures need distinct fallback behavior in the product?
- Are current schemas forcing the model to guess missing fields too often?
- Would splitting or combining tools improve traceability without creating routing noise?

## Anti-Patterns

### The Omniscient Tool

One tool does too many unrelated things. What goes wrong: token-heavy schemas, hard debugging, and vague failure states.

### The Prompt-Only Action

The model is asked to perform a real-world action conceptually without a reliable tool boundary. What goes wrong: false confirmations, silent failure, or policy violations.

### The Schema Maze

The tool requires many optional fields with overlapping meanings. What goes wrong: malformed calls, inconsistent arguments, and expensive prompt workarounds.

## Red Flags

- The model frequently asks for information the tool already has access to
- Tool failures are logged as one generic error type
- Users receive answers that sound grounded but were not actually tool-backed
- Schema docs are long because the interface is conceptually muddy
- The same product action can be triggered through multiple overlapping tools

## Bottom Line

Make tools represent real product actions and authoritative data boundaries. Keep prompts for interpretation and language generation. Keep policy, truth, and side effects where they can be validated.
