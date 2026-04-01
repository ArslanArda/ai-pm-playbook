# Example: AI Onboarding Flow

## Scenario

A marketplace launched an AI search assistant for logged-in mobile users. The team knew the biggest risk was not first-run confusion. It was overexpectation.

If users treated the assistant like a general local expert, the product would fail immediately on:

- neighborhood safety questions
- investment advice
- unsupported listing facts

The onboarding goal was therefore narrow:

- get the user to one successful first task
- define the feature boundary in under `20` seconds
- teach correction and manual fallback early

Initial rollout targets:

- onboarding completion above `65%`
- first successful AI-assisted search above `45%`
- first-session abandonment after AI handoff below `18%`

## The Bad Version The Team Rejected

The first draft looked impressive and underperformed.

### What it showed

- a large hero message saying `Ask me anything about homes`
- animated examples across buying, renting, pricing, and neighborhood advice
- a long disclaimer hidden behind `Learn more`

### What went wrong in testing

- `31%` of users asked unsupported neighborhood or legal questions in their first session
- first-query disappointment was high because the hero message implied broad expertise
- users did not discover the manual filters after a weak answer

The lesson was simple: broad promise creates narrow patience.

## The Shipped Flow

### Screen 1: Contract, Not Hype

Headline:

`Describe the home you want. I'll turn it into a search you can refine.`

Supporting copy:

`Best for: combining budget, area, room count, and must-have features in one request.`

Secondary line:

`Not for: legal advice, neighborhood safety claims, or facts not shown in listing data.`

This screen deliberately reduced ambition. That was the right trade.

### Screen 2: One Easy First Win

Starter chips:

- `2+1 rental under 35,000 in Kadikoy`
- `family-friendly homes near metro in Atasehir`
- `show me listings with parking and balcony`

The PM blocked open-ended freeform as the first-run default. The goal was guided success, not maximum expression.

### Screen 3: Interpreted Request Review

Before results, the UI showed editable interpretation chips:

- `For rent`
- `Kadikoy`
- `2+1`
- `Budget: up to 35,000`

And one soft preference chip:

- `Near metro`

Helper copy:

`Check these before I search. You can edit or remove any item.`

This screen mattered because it converted invisible AI reasoning into visible user control.

### Screen 4: First Result State

When the search succeeded, the UI showed:

- results grid
- short AI summary
- an always-visible `Edit search` action
- a `Use filters instead` link beneath the summary

Summary copy example:

`I searched for rentals in Kadikoy up to 35,000 and kept "near metro" as a preference, not a hard filter.`

That last clause reduced surprise later.

### Screen 5: Failure Or Low-Confidence State

If the interpretation was weak, the product did not show a vague apology. It used one of two states.

#### Retrieval-critical ambiguity

`Before I search: should I treat 35,000 as monthly rent or purchase budget?`

#### Unsupported request

`I can help narrow listings, but I can't judge whether an area is safe or a good investment.`

In both cases the manual path remained one tap away.

## Review Metrics After Beta Week 1

| Metric | Target | Actual |
| --- | --- | --- |
| Onboarding completion | `65%` | `72%` |
| First successful AI-assisted search | `45%` | `49%` |
| Unsupported first query rate | below `20%` | `14%` |
| Abandonment after AI handoff | below `18%` | `16%` |

## What Still Failed

- some users still read `family-friendly` as a guaranteed neighborhood judgment
- the `Use filters instead` path was underused on smaller screens
- a few starter chips implied too much confidence about soft preferences

The PM response was not to broaden the feature promise. It was to tighten chip copy and make the fallback path more visible.

## What This Example Teaches

### 1. Onboarding should define the contract, not celebrate the model

The rejected version was exciting and strategically wrong.

### 2. First-run AI should expose interpretation, not hide it

Editable chips did more for trust than any generic disclaimer.

### 3. Narrower promise beats broader disappointment

The best onboarding copy in AI products often sounds less magical than marketing wants.
