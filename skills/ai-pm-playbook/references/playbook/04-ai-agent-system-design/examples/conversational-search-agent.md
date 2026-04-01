# Example: Conversational Search Agent For A Property Marketplace

## Scenario

A large property marketplace wanted to launch a conversational search entry point for logged-in mobile users. The team had:

- 1 AI PM
- 1 product designer
- 3 backend engineers
- 1 search engineer
- 1 data analyst

Timeline: 8 weeks to closed beta.

Constraints:

- search response needed to feel usable within 5 seconds P95
- budget could support production inference, but only if cost per search stayed close to premium search-session economics
- the system had to stay grounded in marketplace inventory
- soft lifestyle traits such as “quiet” or “family-friendly” were only partially supported by structured data

The original proposal was a multi-agent architecture with:

- a planner agent
- an intent agent
- a neighborhood expert agent
- a search agent
- a response agent

The PM rejected that initial direction.

## Why The Team Simplified First

The user problem was not “we need many intelligent specialists.” The user problem was “users cannot express complex housing intent through rigid filters.” The key product risks were:

- misunderstanding user intent
- sounding too confident about unsupported neighborhood claims
- introducing too much latency for a search experience

That pointed to a simpler design:

```mermaid
flowchart LR
    A["User message"] --> B["Triage and scope check"]
    B --> C["Intent extraction"]
    C --> D["Marketplace search"]
    D --> E["Response composer"]
    E --> F["Output validator"]
```

This was technically multi-step, but not genuinely multi-agent in the “specialist society” sense. The PM framed it as a bounded search pipeline, not a generalized agent.

## Step-By-Step Design Walkthrough

### Step 1: Triage And Scope Check

The first step determined whether the request belonged in conversational search at all.

Examples:

- “2+1 near Marmaray under 35k” stayed in the search flow
- “Which neighborhood is the best investment?” was out of scope
- “Can I book a tour for tomorrow?” routed away from search and into contact or scheduling flows

**Decision made:** use deterministic routing rules for common off-domain intents instead of asking the model to improvise.

**Reasoning:** search trust mattered more than conversational freedom. If the assistant tried to answer unsupported real-estate advice questions, it would create authority the product could not back up.

### Step 2: Intent Extraction

This step used a smaller, faster model to extract:

- listing type: rent or sale
- location
- budget
- room count
- amenities
- soft preferences
- ambiguity flags

**Decision made:** split intent extraction from final response generation.

**Reasoning:** the team needed a clean, inspectable artifact showing what the system believed the user meant. That improved debugging and enabled deterministic search execution.

### Step 3: Search Execution

Marketplace search stayed deterministic. The AI did not rank listings directly. It translated intent into structured constraints and let the existing search system do the retrieval.

**Decision made:** keep inventory truth, filters, and ranking out of the model.

**Reasoning:** search quality was already a mature platform capability. The model’s job was to interpret messy user language, not replace ranking or invent relevance logic.

### Step 4: Response Composition

The response composer generated:

- a short explanation of how the query was interpreted
- a compact summary of applied filters
- optional clarification suggestions

**Decision made:** use a stronger generation model only for this step, not for the whole pipeline.

**Reasoning:** explanation quality mattered for trust, but the higher-cost model was not needed for simple extraction or search execution.

### Step 5: Output Validation

The final validator checked:

- whether the explanation mentioned unsupported claims
- whether critical extracted constraints were dropped
- whether format matched UI expectations

**Decision made:** validate before rendering, and fallback to a simpler explanation if validation failed.

**Reasoning:** a polished but slightly hallucinated explanation would damage trust faster than a plain one.

## What Went Wrong In Early Iteration

### Problem 1: Clarification Loops

The first design asked clarifying questions too often. Users asking “quiet 2+1 near metro” were frequently asked to clarify secondary preferences before seeing any results.

**Why it happened:** the ambiguity detector treated too many soft preferences as blockers.

**Fix:** only block on ambiguity that materially changed retrieval, such as missing rent-vs-buy or unclear budget units. Soft preferences moved into “approximate interpretation” language instead.

### Problem 2: The “Neighborhood Expert” Fantasy

The original concept included a specialist agent for neighborhood reasoning. In practice, the product did not have strong, verified neighborhood-level data for claims about quietness, school quality, or family-friendliness.

**Why it happened:** the team confused aspirational user value with available product truth.

**Fix:** remove the expert agent concept. The product now says when a lifestyle preference is only weakly approximated from available data.

### Problem 3: Cost Creep From Verbose Search Context

Early prompts sent large chunks of listing metadata into response generation.

**Why it happened:** the team wanted the explanation to feel rich and “aware.”

**Fix:** pass only the top structured facts needed for explanation, not full search payloads. This reduced both tokens and inconsistent wording.

## Why The Final Pattern Worked

The chosen pipeline balanced product needs:

- enough step separation for debugging
- deterministic control over inventory truth
- limited model use where flexibility mattered
- acceptable latency for search UX

It was not the most ambitious architecture. It was the most defensible one.

## Lessons Learned

### 1. Search products usually need orchestration discipline more than agent creativity

Interpretation, retrieval, validation, and explanation matter. Autonomous “reasoning” matters much less.

### 2. If your data cannot support a claim, do not create an agent whose job is to make that claim elegantly

This is a common AI PM trap. Better language does not fix missing truth.

### 3. Clarification is expensive

A clarifying question is a product decision, not a UX nicety. Ask only when the answer materially changes the path.

### 4. A step boundary is valuable when it makes debugging or policy control easier

The separation between extraction and response generation paid off because the team could inspect what the system thought the user wanted.

## Transferable Takeaway

For marketplace search, start with a bounded pipeline:

- triage
- extract
- retrieve
- compose
- validate

Only add more agent specialization if a specific step proves too broad, too risky, or too hard to improve inside that structure.
