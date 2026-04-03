# AI Agent PRD Template

Use this template for tool-using, multi-step, or stateful AI agents where model behavior, uncertainty, fallback logic, evaluation quality, and action controls matter. Replace the bracketed examples with your own specifics.

---

## 1. PRD Summary

**Feature name:** [e.g., Conversational Property Search]  
**Owner:** [e.g., AI PM]  
**Status:** [e.g., Draft / In review / Approved]  
**Target release:** [e.g., Beta in Q3]  
**Primary user:** [e.g., Returning property seekers using mobile search]

**One-sentence summary:** [e.g., Let users describe property preferences in natural language and receive structured, explainable search results.]

---

## 2. Problem Statement

- **Current user problem:** [e.g., Users cannot express tradeoffs like budget + commute + school access through rigid filters alone.]
- **Why this matters now:** [e.g., Search abandonment is rising for users with complex queries.]
- **Current workaround:** [e.g., Users try multiple keyword searches or message agents directly.]
- **Why AI is the right lever:** [e.g., The problem requires interpreting messy natural language and translating it into structured search intent.]

---

## 3. Goals And Non-Goals

### Goals

- [e.g., Increase successful search sessions for users with complex intent]
- [e.g., Reduce time from first query to first high-intent listing view]
- [e.g., Produce responses that are relevant, grounded, and easy to refine]

### Non-goals

- [e.g., Replacing the standard filter-based search flow]
- [e.g., Answering legal, financial, or neighborhood-safety questions outside available data]
- [e.g., Supporting every language in v1]

---

## 4. User And Use Cases

**Primary persona:** [e.g., First-time renters who know lifestyle preferences but not exact filters]  
**Secondary persona:** [e.g., High-volume agents testing AI search on behalf of clients]

**Primary use cases:**
- [e.g., “Find a quiet 2+1 near the metro under X budget”]
- [e.g., “Show me family-friendly areas close to good schools and parks”]

**Out-of-scope use cases:**
- [e.g., “Which investment will appreciate fastest?”]
- [e.g., Requests that require private data or unsupported geographies]

---

## 5. Current Experience And Pain Points

- **Current flow:** [Describe the existing flow in 3-5 bullets]
- **Pain points:** [e.g., Rigid filters, ambiguous keywords, repeated reformulation, low trust in results]
- **Baseline metrics:** [e.g., search-to-listing-view rate, avg searches/session, current latency]

---

## 6. Proposed Experience

Describe the end-to-end user experience.

### Happy Path

1. [e.g., User enters a natural-language request]
2. [e.g., System extracts structured intent and runs search]
3. [e.g., User sees results plus an explanation of interpreted preferences]
4. [e.g., User refines or asks follow-up questions]

### Clarification Path

- [e.g., If budget or location is ambiguous, ask one narrow clarifying question before returning results]

### Low-Confidence Path

- [e.g., Show manual filter suggestions and a transparent message rather than overconfident summarization]

### Failure Path

- [e.g., Revert to standard search results with prefilled filters and a message that conversational interpretation was unavailable]

---

## 7. Agent Job Definition

**Primary agent job:** [e.g., Convert natural-language search intent into structured filters, run grounded search, and explain results]

**Subtasks:**
- [e.g., Intent extraction]
- [e.g., Ambiguity detection]
- [e.g., Tool selection or search execution]
- [e.g., Clarification question generation]
- [e.g., Response explanation generation]

**What the agent must not do:**
- [e.g., Invent listing facts]
- [e.g., Recommend neighborhoods using unsupported external knowledge]
- [e.g., Pretend uncertainty does not exist]

**What remains deterministic:**
- [e.g., Search execution, result ranking inputs, safety rules, available inventory]

---

## 8. Agent Workflow And Tool Boundaries

- **Workflow steps:** [e.g., Interpret request -> ask clarification if needed -> call search -> summarize grounded results]
- **Available tools or APIs:** [e.g., Search API, saved-search API, listing details API]
- **What each tool is allowed to do:** [e.g., Retrieve data only, no external side effects]
- **Actions that require user confirmation:** [e.g., Sending messages, saving searches, publishing content]
- **Handoff or escalation conditions:** [e.g., Unsupported legal advice, repeated low confidence, missing required data]

---

## 9. Model Strategy Rationale

- **Required capability:** [e.g., Multilingual intent understanding with low-latency generation]
- **Why this capability is needed:** [e.g., Queries are messy, implicit, and often multi-constraint]
- **Candidate model approach:** [e.g., Small model for extraction, stronger model for explanation]
- **Why not simpler alternatives:** [e.g., Rules alone fail on vague lifestyle preferences]
- **Known risks:** [e.g., Hallucinated interpretation of neighborhood traits]

---

## 10. Data, Grounding, And State Requirements

- **Structured data required:** [e.g., Listing metadata, location hierarchy, amenity tags]
- **Unstructured data required:** [e.g., Listing descriptions, prior query logs]
- **Grounding source:** [e.g., Returned listings only]
- **State or memory requirements:** [e.g., Preserve prior user constraints within a session, do not persist across sessions in v1]
- **Tool dependencies:** [e.g., Search API must return normalized structured filters]
- **Data limitations:** [e.g., Inconsistent amenity tagging in older inventory]
- **Localization constraints:** [e.g., Turkish-first output, English secondary]

---

## 11. Evaluation Strategy

- **Primary eval question:** [e.g., Does the agent interpret intent correctly, use tools accurately, and recover gracefully when uncertain?]
- **Rubric dimensions:** [e.g., task success, correctness, grounding, tool-use accuracy, fallback behavior, safety]
- **What is rules-based:** [e.g., JSON format checks, required confirmation before actions]
- **What is grader-based:** [e.g., relevance, explanation quality, fallback appropriateness]
- **What is human-reviewed:** [e.g., trust-sensitive blocker cases, sampled customer-facing outputs]
- **Launch thresholds:** [e.g., >= 90% pass on blocker-free cases, 0 unsafe action-taking cases]

---

## 12. Starter Dataset Plan

- **Dataset sources:** [e.g., historical search logs, support transcripts, PM-written edge cases]
- **Coverage segments:** [e.g., common requests, ambiguous requests, unsupported asks, tool failures, multilingual cases]
- **Starter CSV schema:** [e.g., case_id, segment, user_input, prior_state, available_tools, expected_behavior, primary_rubric_dimensions, blocker_failure, notes]
- **Initial target size:** [e.g., 50-100 cases before beta]
- **Owner:** [e.g., AI PM with QA partner]

---

## 13. Success Metrics And Evaluation Criteria

### Business Metrics

- [e.g., +8% search-to-listing-view rate for conversational sessions]
- [e.g., +5% listing-to-contact conversion among qualified sessions]

### AI Quality Metrics

- [e.g., Intent extraction accuracy >= 90% on golden set]
- [e.g., Response relevance score >= 4.2/5 from grader + human spot checks]
- [e.g., Hallucination rate <= 2% on grounded responses]
- [e.g., Clarification necessity precision >= 80%]
- [e.g., Tool-use accuracy >= 95% on action-free flows]
- [e.g., Unsafe or unauthorized action rate = 0 in launch eval set]

### Operational Metrics

- [e.g., P50 latency <= 2.5s]
- [e.g., P95 latency <= 5s]
- [e.g., AI service fallback rate <= 4%]

---

## 14. Quality Rubric

Define what “good” means in plain language.

- **Relevant:** [e.g., The response reflects the user’s stated constraints]
- **Correct:** [e.g., No invented listing facts or unsupported claims]
- **Tool-accurate:** [e.g., The agent calls the right tool with the right intent]
- **Complete enough:** [e.g., Covers the major constraints without bloating]
- **Transparent:** [e.g., Makes uncertainty visible when interpretation is partial]
- **Actionable:** [e.g., Helps the user take the next step]

---

## 15. Guardrails And Fallback Behavior

- **When to clarify:** [e.g., Missing budget, conflicting location constraints]
- **When to show manual UI instead:** [e.g., Low confidence or unsupported request]
- **When to retry with a fallback model or flow:** [e.g., Primary model timeout]
- **When action confirmation is required:** [e.g., Before sending messages or making account changes]
- **Deterministic guardrails:** [e.g., No external actions without validated parameters]
- **What the user sees:** [Write the exact product behavior, not a technical note]

---

## 16. Human-In-The-Loop Design

- **Human review needed?:** [Yes / No / Sampled / Flagged only]
- **Review triggers:** [e.g., High-risk output categories, low confidence, policy-sensitive cases]
- **Reviewer role:** [e.g., Ops team, support team, content moderation team]
- **Operational burden estimate:** [e.g., 2% of sessions expected to require review]

---

## 17. Observability And Review Rhythm

- **Trace or log requirements:** [e.g., User input, tool call chosen, tool result, final answer, fallback trigger]
- **Review cadence:** [e.g., Daily launch review, weekly eval review, monthly dataset refresh]
- **Top dashboards:** [e.g., blocker failure rate, fallback rate, tool error rate, latency]

---

## 18. Edge Cases And Failure Modes

List the high-priority cases.

- [e.g., User asks for unsupported advice such as investment returns]
- [e.g., Query mixes multiple intents in one sentence]
- [e.g., Inventory does not match stated constraints]
- [e.g., User asks follow-up questions that depend on stale conversation state]
- [e.g., Model output format breaks UI expectations]
- [e.g., Agent selects the wrong tool or attempts an unauthorized action]

---

## 19. What Could Go Wrong

- [e.g., The system sounds confident while misreading a critical constraint]
- [e.g., Clarification loops create friction and increase abandonment]
- [e.g., The business impact looks good overall but trust drops for power users]
- [e.g., Human review volume is too high for the team to sustain]
- [e.g., The agent takes or suggests an action without sufficient confirmation]

For each major risk, note:
- why it matters
- how it will be detected
- what mitigation will be used

---

## 20. Launch Plan

- **Launch type:** [e.g., Internal alpha, invite-only beta, geography-limited rollout]
- **Launch gate:** [e.g., Must pass eval thresholds and legal review]
- **Monitoring plan:** [e.g., Daily dashboard review for quality, latency, fallback rate]
- **Rollback triggers:** [e.g., Hallucination rate above threshold for 2 consecutive days]

---

## 21. Open Questions

- [e.g., Do we need a persistent conversation state across sessions?]
- [e.g., Should the clarification question appear before or after initial results?]
- [e.g., Is bilingual output required for beta or only after launch?]

---

## 22. Appendix

- Related dashboards: [link or description]
- Related research: [link or description]
- Related prompts or eval docs: [link or description]
