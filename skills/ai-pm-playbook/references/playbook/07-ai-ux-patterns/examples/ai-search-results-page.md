# Example: AI Search Results Page

## Context

A marketplace added conversational search on top of a traditional results page. The UX challenge was to combine:

- open-ended intent capture
- grounded results
- transparent interpretation
- graceful fallback when the AI was unsure

## Screen State 1: Initial Entry

The page opens with:

- a prominent natural-language search input
- suggested starter prompts under the field
- a visible link to standard filters for users who prefer structured search

Key design choice:

The product does not force users into conversation. It offers conversational search as a faster route for complex intent.

## Screen State 2: Loading / Interpreting

If response time is expected to take 3-5 seconds:

- show skeleton result cards immediately
- show a short interpretation chip row such as “Budget,” “Location,” “Room count” as those are parsed
- avoid an empty spinner-only page

Why this works:

Users see progress in a product-relevant form, not just motion.

## Screen State 3: Streaming Or Progressive Results

As soon as the system has grounded filters:

- show initial result cards
- show “interpreted your request as…” summary above the results
- allow users to edit or remove interpreted chips directly

This creates a hybrid interaction:

- conversation for initial capture
- structured controls for refinement

## Screen State 4: Final Result State

Above the result grid:

- one-sentence explanation of what was applied
- clear chips for interpreted constraints
- a “switch to standard filters” option

On each card:

- no invented summary claims
- only grounded listing data

## Screen State 5: Low-Confidence State

If the system is unsure about a soft preference like “quiet”:

- show normal grounded results
- include a small explanation such as “Quiet area is approximate based on available signals”
- offer filter suggestions instead of pretending certainty

## Screen State 6: Error Or Fallback State

If conversational interpretation fails:

- preserve any safely extracted fields
- show standard results if possible
- display a message like “We could not fully interpret your request. You can refine the filters below.”

This is far better than a dead-end error state because it preserves user momentum.

## Key UX Lessons

- hybrid search UX is usually stronger than pure chat for marketplaces
- interpretation transparency matters more than clever copy
- fallback should keep the user moving, not bounce them out of the flow
- AI-generated language should explain, not replace, inventory truth
