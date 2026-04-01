# Example AI PRD: Conversational Search For A Property Marketplace

## 1. PRD Summary

**Feature name:** Conversational Search Assistant  
**Owner:** AI PM, Search Experience  
**Status:** Draft for cross-functional review  
**Target release:** Closed beta in 8 weeks  
**Primary user:** Mobile-first property seekers struggling with filter-heavy search

**One-sentence summary:** Allow users to describe what they want in natural language, translate that intent into structured search filters, and return grounded search results with transparent explanations and follow-up refinement.

## 2. Problem Statement

Users with complex housing preferences struggle to use the current keyword-and-filter search flow. They can filter by price, rooms, district, and a few amenities, but they cannot easily express tradeoffs such as “quiet area but still close to the metro” or “good for a family, not too old, and walkable to parks.”

Today those users either:

- run multiple search attempts
- use vague keywords that return noisy results
- abandon search after a few unproductive reformulations
- contact agents early to ask exploratory questions the product should have helped with

This matters because search abandonment is highest among users with multi-constraint, higher-intent needs. AI is the right lever because the hard part is not search execution. It is understanding messy language, surfacing ambiguity, and translating intent into usable constraints without pretending to know facts the marketplace does not have.

## 3. Goals And Non-Goals

### Goals

- Increase successful search sessions for users who start with natural-language queries
- Reduce time from first query to first meaningful listing view
- Improve user trust by showing how the system interpreted the request
- Enable multi-turn refinement without forcing the user back into a blank search box

### Non-Goals

- Replacing the standard search flow for all users in v1
- Recommending neighborhoods using unsupported external knowledge
- Providing financial, legal, or investment advice
- Persisting long-term conversational memory across sessions

## 4. User And Use Cases

**Primary persona:** First-time renters and buyers who know lifestyle preferences but do not know how to express them in filters.  
**Secondary persona:** Repeat seekers comparing areas with multiple tradeoffs.

**Primary use cases:**

- “I need a 2+1 near the metro in Kadikoy under 40,000 TL, preferably in a quieter street.”
- “Show me family-friendly places near good schools on the Anatolian side.”
- “I work in Levent and want a short commute, but I do not want to pay premium center prices.”

**Out-of-scope use cases:**

- “Which district will appreciate most over five years?”
- “Is this neighborhood safe for women at night?” when no verified source exists
- “Find me places similar to my friend’s house” without product context to ground the request

## 5. Current Experience And Pain Points

Current search requires users to combine rigid filters with keyword hacks. Users often enter free-text phrases in a keyword field that was designed for listing title fragments, not lifestyle intent. Internal logs show that sessions with three or more reformulations are more likely to end without a listing contact.

Baseline metrics:

- search-to-listing-view rate: 42%
- listing-view-to-contact rate: 3.4%
- average searches per session for complex queries: 4.8
- search latency P50: 1.2s using standard filters only

## 6. Proposed Experience

### Happy Path

1. User enters a natural-language request in the search bar or search assistant entry point.
2. System extracts structured intent from the request.
3. Marketplace search runs on structured constraints only.
4. User sees standard search results plus a short explanation such as: “Showing 2+1 apartments in Kadikoy under 40,000 TL, prioritizing metro access and quieter streets where available.”
5. User can refine with follow-up prompts like “show newer buildings” or “wider budget if closer to the metro.”

### Clarification Path

If the query contains a major ambiguity that materially affects results, the system asks one focused clarification before running the full response. Example: “Do you want to rent or buy?” or “Is your budget monthly rent or total purchase price?”

### Low-Confidence Path

If the system cannot reliably infer a soft preference such as “quiet” or “family-friendly,” it still returns grounded results but labels the limitation. Example: “I can filter by rooms, budget, and district. For ‘quiet,’ I’m prioritizing listings away from major roads where we have that signal, but this is approximate.”

### Failure Path

If model inference fails or times out, the user is returned to standard results with any safely extracted structured fields preserved. The system says: “We could not fully interpret your request, but we applied the filters we could detect.”

## 7. AI Task Definition

**Primary AI job:** Extract structured search intent from natural-language input and generate a brief grounded explanation of how the request was interpreted.

**Subtasks:**

- detect rent versus buy
- extract location, room count, budget, property type, and amenities
- detect whether clarification is needed
- rewrite the interpreted request into concise explanation copy

**What the AI must not do:**

- invent listing facts
- claim neighborhood qualities unless grounded in internal signals
- answer unsupported advisory questions
- rank results independently of marketplace search logic

**What remains deterministic:**

- inventory retrieval
- hard filters
- ranking
- final result set
- policy enforcement

## 8. Model Strategy Rationale

The required capability is low-latency natural-language understanding in Turkish with short-form response generation. A lighter model can likely handle extraction and ambiguity classification, while explanation copy may use the same or a slightly stronger model if needed. The key product decision is to keep the AI responsible for interpretation and explanation, not search truth.

We are explicitly not using the model to answer “which listing is best” or “which area is safest,” because the data required for those claims is incomplete and trust damage would be high.

## 9. Data And Context Requirements

- structured listing metadata: price, location, rooms, size, building age, amenities
- location hierarchy data
- search logs for common query patterns
- optional road-noise or main-road proximity signals where available

Known limitation: soft lifestyle traits like “quiet” and “family-friendly” are only partially supported by current structured data. The PRD therefore requires transparent wording whenever those traits are approximated rather than verified.

## 10. Success Metrics And Evaluation Criteria

### Business Metrics

- +7% search-to-listing-view rate for conversational sessions
- +5% listing-view-to-contact rate for sessions that use at least one follow-up refinement

### AI Quality Metrics

- intent extraction accuracy >= 92% on golden set
- clarification-needed precision >= 80%
- response relevance score >= 4.3/5 on human review sample
- hallucination rate on explanation copy <= 1.5%

### Operational Metrics

- P50 latency <= 2.5s
- P95 latency <= 5.0s
- fallback rate <= 4%

## 11. Quality Rubric

A good response:

- captures the main hard constraints correctly
- does not overstate soft-preference understanding
- makes it obvious how the query was interpreted
- returns results that feel directionally right to the user
- provides a clear next step for refinement

A bad response:

- silently drops an important user constraint
- sounds confident about unsupported neighborhood traits
- asks unnecessary clarification questions that break flow
- returns an explanation that is polished but not grounded in retrieved results

## 12. Fallback Behavior

Clarify only when ambiguity changes the search path meaningfully. Do not ask a follow-up for every soft preference. If the model is uncertain about secondary preferences, return results with a transparent caveat instead of blocking the session.

Fallback hierarchy:

1. primary intent extraction path
2. retry with narrower extraction prompt
3. preserve obvious fields and show standard results
4. if nothing usable is extracted, return user to standard search without pretending success

## 13. Human-In-The-Loop Design

No per-request human review is planned because the interaction is real-time and high-volume. Instead, the team will use:

- pre-launch human eval sets
- daily sampled conversation review during beta
- flagged-session review for high complaint or low-confidence cases

Ops burden must stay below 30 flagged-session reviews per day during beta or the launch plan needs adjustment.

## 14. Edge Cases And Failure Modes

- user mixes buy and rent language in one request
- user uses district nicknames or misspellings
- user asks for contradictory constraints such as “central but very cheap and very large”
- user asks follow-up without enough context: “show the newer ones” after switching category
- no listings match the interpreted constraints
- explanation copy implies a soft preference is guaranteed when it is only approximated

## 15. What Could Go Wrong

The biggest trust risk is silent misinterpretation. If the model drops “near the metro” or misreads a budget, the results may still look plausible but be wrong. We will detect this through golden-set evals, live complaint tagging, and mismatch analysis between user query and clicked results.

Another risk is clarification overuse. If the system asks too many questions, it will feel slower and less helpful than ordinary search. Beta analysis will track clarification frequency, abandonment after clarification, and downstream conversion.

## 16. Launch Plan

- launch type: closed beta to 5% of logged-in mobile users
- launch gate: must pass eval thresholds, Turkish-language review, and latency targets for 7 consecutive days in staging
- monitoring plan: daily review of quality sample, latency, fallback rate, clarification frequency, and user complaints
- rollback trigger: hallucination rate > 3% for two consecutive days or clarification abandonment > baseline by 20%

## 17. Open Questions

- Should the interpreted query explanation appear above results or as an editable chip row?
- Do we store conversation state across a single session only, or across app restarts?
- Is an explicit “switch to standard filters” control required in every conversational session?

## 18. Lessons Embedded In This PRD

The key design decision is that the assistant interprets intent but does not pretend to be a real estate advisor. That keeps the feature useful without crossing into unsupported authority. The PRD is also explicit that soft preferences are approximate, which prevents the most damaging form of AI overconfidence in this domain.
