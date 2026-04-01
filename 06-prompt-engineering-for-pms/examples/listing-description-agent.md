# Example: Iterating A Listing Description Prompt Through Five Versions

## Context

A large real estate marketplace wanted an AI assistant that drafts listing descriptions from:

- structured listing data
- optional agent notes
- a small set of high-confidence image signals

The product promise was not “beautiful copy.” It was:

- faster listing creation for agents
- grounded descriptions that do not invent facts
- useful differentiation when the listing genuinely has differentiators
- Turkish-first output that still sounds local, not machine-translated

### Non-negotiables

- no invented amenities
- no neighborhood claims unless explicitly supported
- no visual claims from low-confidence image inference
- no salesy filler that makes plain listings sound fraudulent

### Review dimensions

| Dimension | How the team judged it |
| --- | --- |
| Factual grounding | Unsupported claims per 100 drafts |
| Specificity | Share of drafts with at least 2 concrete listing facts |
| Readability | Human reviewer score, 1-5 |

### Early baseline

The team reviewed 60 drafts per prompt version. Human reviewers scored each version on the same set of listing inputs.

| Version | Unsupported claims | Drafts with 2+ concrete facts | Readability |
| --- | --- | --- | --- |
| V1 | 18% | 32% | 4.4 |
| V2 | 7% | 35% | 3.6 |
| V3 | 9% | 71% | 4.0 |
| V4 | 3% | 64% | 3.8 |
| V5 | 2% | 76% | 4.2 |

The pattern mattered: every improvement created a different tradeoff.

## Version 1: "Write A High-Quality Listing Description"

### Prompt excerpt

```text
Write a high-quality real estate listing description using the provided listing data.
Make it compelling, clear, and attractive to potential buyers or renters.
```

### What the team hoped for

- polished descriptions fast
- acceptable drafts with minimal prompt work

### What actually happened

- outputs were readable
- many descriptions sounded interchangeable
- unsupported adjectives appeared even when the listing was plain
- some drafts implied amenities not present in the input

### Example bad output

> Modern and spacious apartment in a peaceful family-friendly area with comfortable living spaces and excellent amenities.

Problems:

- "peaceful family-friendly area" was unsupported
- "excellent amenities" was vague and invented
- nothing in the sentence helped the user understand the actual listing

### Product lesson

"High quality" is not a product instruction. It is empty aspiration disguised as direction.

## Version 2: Add Grounding Constraints

### Prompt excerpt

```text
Use only the facts provided in the listing input.
Do not mention amenities, neighborhood traits, or property details unless they are explicitly present.
If a detail is missing, omit it.
```

### What improved

- hallucinated amenities dropped sharply
- reviewers trusted the drafts more

### What regressed

- copy became dry
- many descriptions started sounding like compressed field lists
- plain listings became especially repetitive

### Example failure

> 2+1 apartment, 95 m2, on the 3rd floor. It has 1 bathroom and 1 balcony. The building age is 8.

Problems:

- grounded, but lifeless
- no prioritization of what mattered most
- barely better than reading structured metadata

### Product lesson

Grounding solved trust risk, but not usefulness. Safety alone did not create product value.

## Version 3: Add Structure And Differentiation Rules

### Prompt excerpt

```text
Write the description in 3 parts:
1. One-sentence summary
2. Two or three concrete highlights from the listing
3. One practical closing sentence

Mention at least two differentiating facts from the listing when they exist.
Avoid generic filler such as "ideal opportunity" or "modern living."
```

### What improved

- specificity improved materially
- bland openings dropped
- more drafts surfaced the features agents actually cared about

### What regressed

- some plain listings were forced into fake differentiation
- the model sometimes overused image hints to sound more distinctive

### Example failure

> The bright and airy layout stands out with an inviting feel, while the balcony adds a lifestyle-oriented touch.

Problems:

- "bright and airy" came from visual inference, not structured truth
- "lifestyle-oriented touch" is filler wearing a blazer

### Product lesson

Differentiation instructions are dangerous when they are not paired with strict grounding discipline.

## Version 4: Tighten Image Signal Rules

### Prompt excerpt

```text
Use image-derived details only when they are marked HIGH_CONFIDENCE.
If a visual detail is uncertain, omit it.
Do not infer quality, luxury level, or neighborhood character from images.
```

### What improved

- speculative claims dropped again
- content-ops reviewers trusted the drafts enough to use them as real starting points

### What regressed

- some drafts became too minimal when listings were plain and image signals were sparse
- safe output sometimes felt unhelpful

### Example failure

> The apartment offers a 2+1 layout with a balcony and standard building features.

Problems:

- technically safe
- practically useless
- too weak to save agent time

### Product lesson

Safety without value still fails the product test. The team now had something shippable for trust, but not yet something agents would consistently prefer.

## Version 5: Replace Sales Tone With User-Value Framing

### Prompt excerpt

```text
Prefer practical value framing over sales adjectives.
Describe who the property may suit only when that suggestion is clearly supported by actual facts.
If the listing is plain, be concrete rather than promotional.

Good:
"The separate kitchen and 2+1 layout may suit couples or small families who want a more defined living arrangement."

Bad:
"Ideal for modern living."
```

### What improved

- drafts felt more useful than promotional
- specificity stayed strong
- hallucination rate stayed low
- reviewer confidence improved because the output sounded grounded and intentional

### What still needed attention

- premium listings still converged on similar phrasing
- some agents wanted a more premium tone than the prompt allowed
- the team still needed listing-segment-specific tone policies later

### Example approved-style output

> This 2+1 apartment offers a separate kitchen, balcony, and 95 m2 interior space. The layout may suit couples or small families who want a more defined living arrangement rather than an open-plan home. Located on the 3rd floor in an 8-year-old building, it presents a practical option for buyers focused on usable space and standard daily comfort.

Why it worked:

- every claim was grounded
- the description explained value without inventing prestige
- the tone felt helpful instead of robotic

## What Changed In The Product, Not Just The Prompt

The biggest gains did not come from better wording taste. They came from clarifying the product contract:

- the system should save time, not impersonate a copywriter
- the draft should be trustworthy enough to edit, not perfect enough to publish raw
- unsupported neighborhood and amenity claims are worse than plain language
- user value framing is better than generic sales tone

That is why PM ownership mattered. The engineers could improve the prompt mechanics, but the PM had to define what the draft was supposed to be good at.

## Final Approved Prompt Spec

### Behavior rules

- use only provided structured facts, notes, and high-confidence image signals
- never invent amenities, location traits, or luxury cues
- prefer practical usefulness over promotional language
- mention differentiators only when supported by actual facts
- if the listing is plain, write a plain but still useful description

### Output structure

1. one-sentence summary
2. two or three grounded highlights
3. one practical closing sentence

### Launch gate

The team agreed they would not expand rollout unless:

- unsupported claims stayed below 3% in review samples
- at least 70% of drafts contained 2+ concrete listing facts
- average reviewer score stayed above 4.0

## What We Still Would Not Ship

Even after Version 5, the team would still block publication in these cases:

- the listing has too little usable data and the draft becomes empty filler
- the model tries to infer neighborhood quality from weak evidence
- image signals are low-confidence but the text still sounds visual
- luxury inventory needs brand-level tone that the generic prompt cannot support

## Final Takeaways

### 1. The useful prompt was a behavior spec, not a prettier paragraph

The real gains came from grounding rules, structure, and product-specific value framing.

### 2. Every prompt improvement created a new tradeoff

Grounding reduced hallucination. Then tone flattened. Differentiation improved. Then speculation rose. Good prompt work is controlled tradeoff management, not linear polish.

### 3. The PM contribution was not wordsmithing

The PM clarified the product promise: trustworthy, useful, time-saving drafts. Once that became explicit, the prompt improved faster.
