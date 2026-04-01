# Example AI PRD: Image-Based Listing Feature Detection

## 1. PRD Summary

**Feature name:** Listing Photo Feature Detection  
**Owner:** AI PM, Supply Quality  
**Status:** Draft for review  
**Target release:** Limited rollout in 6 weeks  
**Primary user:** Real estate agents creating listings; seekers consuming listing detail pages

**One-sentence summary:** Detect visual property features from listing photos to improve listing completeness, search filtering, and quality review without forcing agents to tag every detail manually.

## 2. Problem Statement

Agents frequently omit structured property attributes when creating listings, even when the feature is visible in the uploaded photos. This creates three downstream problems:

- seekers cannot filter reliably
- search relevance suffers because listing metadata is incomplete
- content quality teams spend manual time correcting obvious gaps

The opportunity is not full scene understanding. It is narrow visual detection of a limited set of commercially useful features such as balcony presence, elevator hints in building entrance shots, renovated kitchen indicators, furnished versus unfurnished state, and parking visibility where feasible.

This matters because incomplete metadata directly reduces listing quality and filter usefulness. AI is the right lever because image review at listing scale is too manual, but the product must be conservative where false claims could damage trust.

## 3. Goals And Non-Goals

### Goals

- Increase structured attribute completeness on newly created listings
- Reduce manual review burden for clearly detectable visual features
- Improve downstream search/filter usefulness for seekers

### Non-Goals

- Replacing all manual attribute entry by agents
- Detecting legally sensitive or subjective claims such as “luxury,” “safe,” or “high investment value”
- Auto-publishing all detections without confidence thresholds and review logic

## 4. User And Use Cases

**Primary persona:** Listing agents who want faster publishing with less form filling.  
**Secondary persona:** Quality operations analysts reviewing listing completeness.  
**Indirect user:** Property seekers relying on filters and attribute accuracy.

**Primary use cases:**

- detect that a listing likely has a balcony from one or more unit photos
- suggest that a kitchen appears renovated based on visible finishes
- identify that the space appears furnished for copy or metadata suggestion

**Out-of-scope use cases:**

- infer property value from visual cues
- certify structural safety or construction quality
- determine legal status from photos

## 5. Current Experience And Pain Points

Agents currently fill structured fields manually. Many skip optional fields or rush through them to publish faster. Quality reviewers later correct some listings, but coverage is inconsistent and expensive.

Baseline metrics:

- average publish time: 11 minutes
- listings missing 3+ optional attributes: 37%
- manual review touch rate for metadata quality: 18%

## 6. Proposed Experience

### Happy Path

1. Agent uploads photos during listing creation.
2. System analyzes images for a limited set of supported features.
3. Product presents suggested attributes with confidence labels, not silent auto-fill.
4. Agent accepts, edits, or rejects each suggestion before publish.

### High-Confidence Auto-Assist Path

For features with extremely high confidence and low downside if wrong, the system may pre-check suggested fields while still making them visible for confirmation.

### Uncertain Path

If confidence is moderate, the system surfaces a suggestion such as: “This listing may have a balcony. Confirm?” without applying it automatically.

### Failure Path

If no reliable features are detected, the upload flow continues normally and the user sees no broken or empty AI panel.

## 7. AI Task Definition

**Primary AI job:** Detect a bounded set of visually observable listing attributes from photos and convert them into product suggestions with confidence-aware handling.

**Supported attributes in v1:**

- balcony likely present
- furnished likely present
- renovated kitchen likely present
- parking visible in dedicated photo

**What the AI must not do:**

- assert a feature that is not visually verifiable
- infer legal or safety claims
- overwrite agent input without review
- generalize from weak evidence across unrelated photos

**What remains deterministic:**

- form structure
- publish flow
- attribute taxonomy
- confidence thresholds
- review rules

## 8. Model Strategy Rationale

The feature requires image classification and detection, not broad multimodal reasoning. The product choice is to prefer narrower, higher-confidence visual tasks over a broad model that “describes the home.” We are optimizing for trustworthy structured suggestions, not impressive language.

## 9. Data And Context Requirements

- labeled photo set for each target attribute
- examples of both positive and negative cases
- enough variation across lighting, device quality, and room angle
- mapping from image signals to supported taxonomy values

Known limitation: some features are genuinely hard to infer reliably from photos alone. For example, “renovated” is subjective and can drift toward style judgment. We therefore limit the attribute to “kitchen appears recently renovated” and treat it as a suggestion only until quality stabilizes.

## 10. Success Metrics And Evaluation Criteria

### Business Metrics

- reduce average publish time by 10%
- increase structured attribute completeness by 15% on supported fields

### AI Quality Metrics

- precision >= 95% for any attribute that is auto-prechecked
- recall >= 70% for surfaced suggestions on supported attributes
- false positive rate <= 3% on balcony detection
- false positive rate <= 5% on furnished detection

### Operational Metrics

- image analysis P95 <= 8s in background during photo upload
- agent rejection rate tracked per attribute
- manual-review escalation rate <= 10% of analyzed listings

## 11. Confidence Threshold Design

This is the core PM tradeoff.

- **High confidence:** Auto-precheck suggestion, but still show editable confirmation
- **Medium confidence:** Show suggestion card, require explicit user confirmation
- **Low confidence:** Do not surface the attribute

The threshold is not the same for every attribute. Balcony false positives are more harmful because they materially affect seeker expectations and filter trust. Furnished false positives are also harmful, but slightly easier for an agent to catch during review. “Renovated kitchen” has the highest subjectivity, so the launch threshold is stricter and suggestion-only.

## 12. False Positive vs. False Negative Tradeoff

The product should prefer false negatives over false positives for seeker-facing attributes. Missing a balcony tag is less harmful than falsely tagging a listing as having one. The exception is low-risk internal review signals, where surfacing a broader set for human review can be acceptable.

## 13. Fallback Behavior

If image analysis fails:

- listing creation continues normally
- no broken AI UI is shown
- user can still enter fields manually

If image quality is too poor:

- the system should not guess
- a neutral helper message may prompt the agent to fill missing fields manually

## 14. Human-In-The-Loop Design

Human review is not used for every listing. Instead:

- agents confirm or reject suggestions during publish
- quality ops review a sample of accepted suggestions in beta
- high-disagreement attributes are held back from wider rollout

This keeps the workflow useful without creating an unsustainable review queue.

## 15. Edge Cases And Failure Modes

- photos are heavily edited or filtered
- the same room is shown repeatedly, hiding key features
- balcony is implied through outdoor view but not actually visible
- furniture belongs to staging rather than the property
- kitchen photos are too dark for reliable inference
- parking appears nearby but does not belong to the listing

## 16. What Could Go Wrong

The biggest risk is silent trust erosion in filters. If users repeatedly see balcony-tagged listings with no actual balcony, the value of structured search drops beyond this feature alone.

Another risk is agent annoyance. If the system generates too many low-quality suggestions, agents will stop paying attention and the assistant becomes noise. We will detect this through rejection rates, attribute-specific precision, and publish-dropoff analysis.

## 17. Launch Plan

- launch type: 20% of new listing creation flow for selected agencies
- launch gate: high-confidence precision target met on offline eval and first-week shadow mode
- monitoring plan: precision sample review, agent acceptance/rejection rate, publish-time change, downstream filter usage
- rollback trigger: any seeker-facing attribute exceeds false positive threshold for 3 consecutive daily samples

## 18. Open Questions

- Should supported attributes differ between rental and sale inventory?
- Do we surface “why we suggested this” previews to increase agent trust?
- Is “renovated kitchen” too subjective for v1 and better moved to later release?

## 19. Lessons Embedded In This PRD

This PRD deliberately avoids the temptation to make the model “describe the property.” The product value comes from conservative, useful structure, not broad visual storytelling. Confidence thresholds and false-positive discipline are the backbone of that decision.
