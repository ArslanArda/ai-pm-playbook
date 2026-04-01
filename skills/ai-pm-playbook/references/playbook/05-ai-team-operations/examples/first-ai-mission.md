# Example: Running Your Team’s First 6-Week AI Mission

## Context

A marketplace product team wanted to run its first serious AI mission around conversational search. The organization had enthusiasm but no strong AI operating model yet.

Team:

- 1 PM
- 1 designer
- 3 engineers
- 1 analytics partner
- occasional support input

Mission question:

Can we ship a safe closed beta for conversational search that improves complex-query sessions without damaging trust?

## Mission Brief Excerpt

The PM wrote a short brief before kickoff. The useful part was not the prose. It was the forced choices.

| Field | Decision |
| --- | --- |
| Target user | Logged-in mobile users with at least one prior saved search |
| Mission question | Can we justify a closed beta for conversational search? |
| Success metrics | complex-query success rate, fallback recovery rate, P95 latency |
| Launch blockers | hallucinated listing facts above `2%`; silent constraint-drop above `5%`; P95 latency above `4.5s` |
| Non-goals | neighborhood advice, voice input, cross-session memory, English launch |
| Review ritual | weekly AI review every Tuesday with PM, eng, design, analytics |
| End-of-cycle decision | no-go, closed beta, or broader rollout |

## Week 0: Mission Brief

The PM created a brief with:

- one target cohort: logged-in mobile users
- one mission question
- three success criteria: relevance, latency, fallback quality
- explicit non-goals: neighborhood expertise, memory, and voice input

This mattered because early stakeholder requests already included “while you are at it, could it also recommend districts?” The brief gave the PM cover to say no.

## Week 1: Build Progress Looked Good, Confidence Did Not

The intent extraction pipeline worked in demos. Search explanations sounded promising. Leadership felt positive.

The PM kept the weekly review grounded by separating:

- implementation progress: ahead of plan
- quality confidence: still low, especially on ambiguous queries

This prevented the classic mistake of reporting the project as “70% done” when the hardest product questions were still unresolved.

### Weekly review agenda

The team used the same agenda every week:

1. last week's decision and what changed
2. scorecard against launch blockers
3. top `5` failure examples from live or eval traffic
4. cost and latency snapshot
5. scope-change requests and whether they were accepted or rejected

That rhythm stopped the meeting from becoming status theater.

## Week 2: The First Real Quality Shock

Initial evals showed the system often dropped one user constraint silently. It sounded coherent while being directionally wrong.

What the PM did:

- elevated silent constraint drop as the top blocker category
- removed lower-priority experiments from scope
- asked engineering to expose extracted-intent traces in the review dashboard

Why it mattered:

Without a structured mission review, the team might have kept polishing response copy instead of fixing the real issue.

### Metrics snapshot

| Metric | Week 1 | Week 2 |
| --- | --- | --- |
| Eval pass rate | `61%` | `64%` |
| Silent constraint-drop | `11%` | `13%` |
| Fallback recovery rate | `71%` | `70%` |
| P95 latency | `3.8s` | `4.0s` |

The pass rate looked like progress. The blocker metric got worse. That is why the team separated "looks better" from "is safer to launch."

## Week 3: Scope Creep Pressure

Leadership asked whether the assistant could also:

- answer neighborhood-quality questions
- support English queries
- help schedule tours

The PM used the mission brief to respond:

- neighborhood advice: out of scope due to weak grounding
- English: important, but not required to answer the current mission question
- scheduling: valuable later, but adds routing complexity and risk

This was the week where the mission framework proved its value. It made “not now” defensible.

### What leadership heard versus what the team knew

Leadership heard:

- "The assistant is basically working."

The team knew:

- the happy path was working
- the ambiguous-query path still risked confident wrong retrieval
- the launch blockers were not met

That gap is normal in AI work. The PM's job is to make it visible without sounding like the team is stalling.

## Week 4: Weekly AI Review Changed The Roadmap

The weekly review surfaced that clarification questions were overused. Users were abandoning after getting slowed down for non-critical ambiguities.

The PM and team decided:

- ask clarifying questions only for ambiguity that changes retrieval materially
- handle soft preferences through transparent approximation instead

This decision came from ritualized review, not intuition. The team could point to:

- clarification frequency
- abandonment after clarification
- sample session review

### Decision log excerpt

| Decision | Why |
| --- | --- |
| Stop clarifying on soft preferences | abandonment after clarification was `19%` |
| Keep clarification for listing type ambiguity | retrieval changed materially without it |
| Delay English support | no evidence it changed the mission outcome this cycle |

## Week 5: Launch Gate Debate

Implementation was nearly complete, but quality on one edge-case segment remained weak: typo-heavy district names and colloquial abbreviations.

The DACI setup mattered here.

- PM drove the quality assessment
- engineering contributed constraint and feasibility context
- product lead approved the limited-cohort beta decision

The team did not pretend the feature was “done.” They chose a narrower launch:

- 5% of traffic
- logged-in users only
- clear fallback to standard search

### Launch gate table

| Gate | Threshold | Week 5 result | Decision |
| --- | --- | --- | --- |
| Hallucinated listing facts | below `2%` | `1.4%` | pass |
| Silent constraint-drop | below `5%` | `4.7%` | pass, but watch |
| P95 latency | below `4.5s` | `4.2s` | pass |
| Fallback recovery rate | above `80%` | `78%` | fail for broad launch |

This was the key moment. The team had enough to justify a limited beta, but not enough to pretend the feature was ready for everyone.

## Week 6: Demo, Retro, Carryover

The end-of-cycle review asked three questions:

1. Did we answer the mission question?
2. What remains too weak for broader launch?
3. What belongs in the next cycle versus a later roadmap bucket?

Answer:

- yes, a closed beta was justified
- no, broad rollout was not yet justified
- next cycle should focus on ambiguous-location handling and multilingual readiness

## What Worked

- one clear mission question
- explicit non-goals
- weekly review centered on quality and trust, not just delivery
- DACI clarity for launch decisions

## What Almost Went Wrong

- demo excitement nearly masked unresolved quality risks
- scope creep nearly pulled in unrelated capabilities
- explanation-copy polish could have distracted from deeper intent issues

## Carryover Brief For The Next Cycle

The PM did not write "keep improving quality." That would have been lazy.

Carryover priorities:

- reduce fallback recovery gap from `78%` to above `82%`
- improve typo-heavy district handling
- validate whether English support matters for the target cohort
- keep the same non-goals unless beta evidence changes them

That preserved momentum without widening the mission by default.

## Lessons Learned

### 1. Your first AI mission should answer one hard question well

Breadth is the enemy early.

### 2. Build progress and quality confidence must be reported separately

This single habit prevented false optimism more than anything else.

### 3. Weekly review should change decisions, not just update status

The best meeting in the cycle was the one that caused the team to simplify clarification logic.

### 4. A narrower launch is often the correct success case

The mission succeeded because it enabled a defensible beta, not because it forced a larger rollout than quality allowed.
