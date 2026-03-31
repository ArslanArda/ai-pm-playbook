# Build vs. Buy vs. Prompt

This decision is usually framed too simply. The real question is not “should we fine-tune?” It is “what is the cheapest, fastest, most maintainable way to reach the quality bar for this product job?”

## Decision Matrix

| Factor | Prompt-first recommendation | Buy / external capability recommendation | Build / custom adaptation recommendation |
| --- | --- | --- | --- |
| Data availability | Limited labeled data | Some external domain fit exists | Strong proprietary data exists |
| Quality requirement | Good enough with clear instructions | Needs specialized capability fast | Requires domain-specific lift beyond prompt-only |
| Latency constraints | Acceptable on general models | Vendor can meet specialized latency need | You can support infra and optimization burden |
| Budget | Lower upfront cost preferred | Pay-for-capability acceptable | Larger long-term investment justified |
| Team capability | Limited ML specialization | Integration team is strong | Team can manage training/eval lifecycle |
| Time-to-ship | Need fastest learning loop | Need fast specialized launch | Willing to invest for longer-term advantage |

## Recommended Default

Start prompt-first unless you have clear evidence it cannot meet the quality bar. Buy specialized capability before building custom adaptation unless proprietary advantage or domain constraints clearly justify ownership.

## When Prompt-First Is Right

### Scenario 1: Conversational Search Interpretation

You need strong intent extraction and grounded response behavior, but the task can be improved significantly through prompt design, context structure, and evaluation. Prompt-first is usually the right baseline.

### Scenario 2: Internal Content Summaries

If the task is bounded and internal, prompt quality and retrieval quality often matter more than custom modeling.

## When Buying Is Right

### Scenario 1: Voice Or Vision Capability You Need Quickly

If a vendor can provide robust real-time speech or domain-ready OCR faster than you can build it, buying is often the pragmatic choice.

### Scenario 2: Compliance Or Localization Support Exists Externally

If a provider is already stronger in your target language or domain format, buying may reduce risk faster than building.

## When Building Is Right

### Scenario 1: Proprietary High-Value Domain Data

You have enough domain examples and repeated task volume that custom adaptation could materially improve quality and economics over time.

### Scenario 2: Strategic Differentiation Depends On It

The capability is core enough that external sameness becomes a product ceiling, and the team can support the lifecycle.

## Questions To Ask Your Engineering Team

- Have we proven prompt and context improvements are insufficient?
- Do we actually have enough high-quality data for custom adaptation?
- What ongoing maintenance burden would a custom path create?
- Could an external capability close the gap fast enough for the product timeline?
- What would success look like that justifies moving beyond prompt-first?

## Anti-Patterns

### Build For Prestige

You pursue custom adaptation because it sounds strategic. What goes wrong: cost and complexity rise without clear product lift.

### Buy As A Shortcut Around Product Clarity

You purchase specialized capability before the task and quality bar are well defined. What goes wrong: integration happens faster than learning.

### Prompt Blame

You blame “the model” before improving inputs, context, or evaluation. What goes wrong: the team escalates complexity prematurely.

## Red Flags

- No one can articulate why prompt-first is insufficient
- Data quality is assumed rather than verified
- The main argument for building is future flexibility
- The team lacks a plan for ongoing eval and retraining
- Vendor choice is being driven by sales narrative rather than feature needs

## Bottom Line

Prompt-first is the default. Buy when it gets you specialized quality or speed faster. Build only when you have the data, the need, and the organizational discipline to make custom adaptation worthwhile.
