# System Prompt Design

A production system prompt should have structure, not just content.

## Core Anatomy

| Component | Why it matters | Product impact if missing |
| --- | --- | --- |
| Role / persona | Sets the assistant’s job and posture | Behavior drifts or becomes inconsistent |
| Behavioral constraints | Defines what the assistant must not do | Unsafe or over-helpful output appears |
| Output format | Tells the model how to structure the response | UI breaks or responses become inconsistent |
| Fallback / refusal rules | Defines behavior under uncertainty or unsupported requests | Confident guessing or vague failure |
| Few-shot examples | Anchors style or schema behavior | Inconsistent execution on edge patterns |
| Reasoning guidance | Shapes how carefully the model handles tasks | May affect accuracy, latency, and verbosity |

## PM View Of Each Component

Role is not about personality. It is about product function.

Behavioral constraints are where product policy enters the prompt.

Output format is a UI contract.

Fallback rules define the user experience of uncertainty.

Examples are teaching aids, not substitutes for rules.

Reasoning guidance should be used carefully because it can affect both quality and latency.

## Realistic Use Scenarios

### Scenario 1: Listing Description Agent

Without explicit grounding constraints, the prompt may produce more persuasive but less accurate copy. The product impact is trust loss in listings.

### Scenario 2: Search Intent Extractor

Without explicit output schema, downstream search logic receives inconsistent fields and the feature appears flaky even if interpretation quality is decent.

## Questions To Ask Your Engineering Team

- Does each prompt section map to a clear product need?
- Which component is currently doing too much work?
- Are examples masking weak instruction design?
- What part of the prompt most affects latency?
- Which fallback rules belong in prompt versus deterministic validation?

## Anti-Patterns

### Persona Overload

The prompt spends many tokens on tone and identity. What goes wrong: product rules get diluted.

### Format By Hope

The team expects the model to infer structure. What goes wrong: outputs vary and UI handling becomes brittle.

### Constraint Burial

Critical safety or grounding rules are buried deep in prose. What goes wrong: the model underweights them.

## Red Flags

- The prompt is one long paragraph
- Output structure is partially specified
- Few-shot examples contradict the stated rules
- Refusal behavior is absent or vague
- Performance issues exist, but no one knows which prompt section is responsible

## Bottom Line

A system prompt should read like a well-structured behavior contract. If the prompt is messy, the product behavior will usually be messy too.
