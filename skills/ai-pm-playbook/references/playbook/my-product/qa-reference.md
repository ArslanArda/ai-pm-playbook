# Product Context QA Reference

Use this when `my-product/PRODUCT_CONTEXT.md` is missing, stale, or too thin for a serious AI PM recommendation.

The goal is not to collect every possible fact. The goal is to ask the minimum useful questions about product UX, users, data, tools, and constraints so you can update `PRODUCT_CONTEXT.md` and make better decisions later.

## Minimum Question Set

Ask these first when time is limited:

1. What product are we talking about, and what business outcome matters most right now?
2. Who are the primary users, and what pain point are they struggling with?
3. Which current screen or workflow would an AI agent touch?
4. What should the agent help with, and what should it never do?
5. Which tools, APIs, or internal actions could the agent use?
6. What product data, logs, transcripts, or historical examples are available?
7. What are the main constraints: latency, privacy, localization, budget, or human review?
8. What would a clearly good result look like, and what failure would hurt trust most?
9. Who owns the decision and who will review quality after launch?
10. What is the current AI priority or blocked decision?

## Expanded Question Bank

Use these when the minimum set is not enough.

### Product And Users

- What is the product, and how does it make money?
- Which persona should this agent help first?
- What is the user's current workaround without AI?
- What user behavior or business metric would improve if this works?

### UX And Workflow

- In which exact screen or flow would the agent appear?
- What does the user see first?
- Can the agent ask clarifying questions, or must it answer immediately?
- What fallback should appear when the agent is unsure or blocked?
- Which actions require explicit user confirmation?

### Agent Scope And Tools

- What is the primary job of the agent?
- What subtasks are in scope?
- What requests are out of scope or should be handed off?
- Which tools or APIs can the agent call?
- What must stay deterministic or policy-controlled?

### Data And Grounding

- What structured data is available?
- What unstructured data is available?
- Which logs, support tickets, or conversation transcripts exist?
- Do we have labeled examples, QA reviews, or red-team cases already?
- What data is missing, stale, or low quality?

### Constraints And Risk

- What is the acceptable latency for this experience?
- Which privacy or compliance constraints matter?
- What languages or locales matter?
- What is the budget sensitivity?
- Which wrong behavior would be most damaging?

### Team And Operations

- Who owns the product decision?
- Who owns prompts, tool contracts, and quality?
- Who reviews flagged outputs or failures?
- How often can the team review eval results after launch?

## Mapping To `PRODUCT_CONTEXT.md`

Map answers into the template instead of storing raw interview notes:

- Product and business answers -> `1. Product Overview`
- Users and personas -> `2. Users & Personas`
- UX flow, screens, and pain points -> `3. Current Product Experience`
- Tools, models, data, and logs -> `4. Technical Landscape`
- Team and decision rights -> `5. AI Maturity & Team`
- Constraints and risk -> `6. Constraints & Context`
- Current priorities -> `7. Current AI Priorities`
- Screen details -> `8. Screenshots & Screen Descriptions`

## Update Rules

- Ask the shortest question set that can unblock the current decision.
- Prefer specific questions over broad prompts like "tell me about your product."
- Rewrite answers into durable prose inside `PRODUCT_CONTEXT.md`.
- Preserve useful existing context unless the user is replacing it.
- Keep unknowns explicit instead of inventing detail.
- If screenshots or mockups are discussed, summarize the relevant UX in the matching section.
