# Glossary

## Agent

An AI workflow that does more than one direct input-output step. It may plan, route, call tools, validate, retry, or hand off.

## Confidence

A signal used to decide whether the system should act, ask, defer, or hand off. Confidence only matters if it changes behavior.

## Fallback

The product behavior shown when the ideal AI path is unavailable, low-confidence, or wrong.

## Grounding

Constraining AI output to trusted context, sources, or system data instead of relying on model memory or inference alone.

## Hallucination

An unsupported or invented claim presented as if it were true.

## Human-In-The-Loop

Any design where a person reviews, confirms, edits, or overrides AI output before or after it is used.

## Intent Extraction

Turning natural-language input into a structured representation the product can act on.

## MCP

Model Context Protocol. In practical PM terms, think of it as a standardized way for models to access tools, data, or external capabilities through structured interfaces.

## Model Routing

Sending different requests or workflow steps to different models or model tiers based on complexity, risk, or cost logic.

## Prompt Injection

An attempt to manipulate the system’s instructions or safety boundaries through user-provided content.

## Retrieval

Fetching relevant information from external or internal sources so the model can respond with fresher, more grounded context.

## Silent Wrong Answer

A dangerous failure mode where the output sounds plausible and passes surface checks but is materially wrong.

## Tool

A structured capability the model can call to retrieve data or take an action.

## Trace

A step-by-step record of what an agent system did, including routing, tool use, latency, and validations.
