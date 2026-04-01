# Example: Iterating A Listing Description Prompt Through Five Versions

## Context

A marketplace team wanted an AI assistant that drafts listing descriptions from structured listing data, optional agent notes, and a small set of high-confidence image signals.

Requirements:

- grounded in real listing facts
- clear and useful, not generic
- Turkish-first
- no invented amenities or neighborhood claims

The team tracked three review dimensions:

- factual grounding
- specificity
- readability

## Version 1: “Write A High-Quality Listing Description”

### What changed

The initial prompt mostly asked the model to write a compelling listing description using available listing data.

### What improved

- outputs were readable
- drafts felt polished

### What regressed or failed

- generic filler was common
- unsupported adjectives appeared
- some outputs implied amenities not present in the structured data

### Lesson

“High quality” is not a product instruction. It is an empty aspiration.

## Version 2: Add Grounding Constraints

### What changed

The prompt added:

- use only provided listing facts
- do not mention unsupported amenities
- avoid neighborhood claims unless explicitly supplied

### What improved

- hallucinated amenities dropped
- factual reliability improved

### What regressed or failed

- copy became dry and repetitive
- many descriptions sounded interchangeable

### Lesson

Constraint clarity helped, but the prompt still lacked a standard for what good specificity looked like.

## Version 3: Add Structure And Differentiation Guidance

### What changed

The team added explicit structure:

- opening summary sentence
- 2-3 concrete property highlights
- close with practical use-case framing

It also added:

- mention at least two differentiating facts from the listing
- avoid generic filler phrases

### What improved

- specificity improved
- bland openings dropped
- readability stayed acceptable

### What regressed or failed

- some outputs forced awkward differentiation when the listing itself was plain
- the model occasionally over-interpreted image signals to create “distinctive” details

### Lesson

Differentiation instructions need grounding discipline attached to them or the model will get creative in the wrong places.

## Version 4: Tighten Image Signal Rules

### What changed

The prompt clarified:

- image-derived features may be used only if marked high confidence
- if a detail is uncertain, omit it rather than decorate the description

### What improved

- speculative visual claims dropped sharply
- trust in drafts improved among content ops reviewers

### What regressed or failed

- some drafts became too minimalist when image input was sparse

### Lesson

The prompt was now safer, but it still needed a better way to make plain listings sound useful without sounding empty.

## Version 5: Add User-Value Framing Instead Of Generic Sales Tone

### What changed

The team replaced vague “compelling” language with:

- describe who this property is likely suitable for only if supported by actual facts
- prefer practical value framing over sales adjectives

Example:

- instead of “ideal for modern living”
- use “the separate kitchen and two-room layout may suit small families or couples needing a home office,” only if those facts are supported

### What improved

- outputs felt more helpful than promotional
- specificity remained strong
- hallucination rate stayed low

### What still needed attention

- luxury listings still tended to get overly similar phrasing
- some agents wanted a more premium tone than the current prompt allowed

## Final Prompt Design Takeaways

### 1. The big gains came from defining behavior, not adding more adjectives

Grounding rules, structure, and differentiation logic mattered more than style words.

### 2. The prompt became better when the PM clarified the product promise

The goal was not “beautiful copy.” It was “trustworthy, useful, time-saving draft output.”

### 3. Every improvement created a new tradeoff

Grounding improved but tone flattened. Differentiation improved but speculation rose. That is why prompt iteration needs explicit evaluation dimensions, not taste-based review.
