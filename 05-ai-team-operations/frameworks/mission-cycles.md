# Mission Cycles

AI work benefits from mission cycles because the team needs time-boxed focus without pretending everything can be predicted upfront.

This playbook recommends 6-week cycles for substantial AI initiatives:

- long enough to run discovery, build, and evaluation loops
- short enough to force prioritization and visible learning

## Anatomy Of A 6-Week Mission

```mermaid
flowchart LR
    A["Week 0: Mission brief"] --> B["Week 1-2: Build + baseline eval"]
    B --> C["Week 3-4: Iterate + narrow scope"]
    C --> D["Week 5: Validate launch or learning"]
    D --> E["Week 6: Demo, retro, carryover decision"]
```

## What Good Mission Scope Looks Like

A strong mission answers one of these:

- Can we ship this feature to a defined cohort safely?
- Can we prove that this AI approach beats the current workflow?
- Can we learn enough to reject or commit to the next investment?

Weak mission scope sounds like:

- “improve search with AI”
- “build an agent”
- “explore prompt engineering”

## Weekly Rhythm

- **Kickoff:** align on mission question, scope, success metrics, and risks
- **Weekly checkpoint:** review quality signals, cost, blockers, and scope pressure
- **End-of-cycle review:** decide ship, extend, simplify, or stop

## Handling Scope Creep

AI missions attract new ideas constantly:

- “we should also add memory”
- “maybe this needs retrieval”
- “can we add a grader too?”

Use this rule:

- if the new work is required to answer the mission question, it stays
- if it is interesting but non-blocking, move it to next-cycle candidates

## Realistic Use Scenarios

### Scenario 1: Conversational Search Beta

Mission question: can we launch to 5% of mobile users with acceptable relevance, latency, and fallback behavior?

### Scenario 2: Internal Support Copilot

Mission question: can agents reduce response-drafting time without policy-consistency regression?

## Questions To Ask Your Engineering Team

- What is the minimum technical scope needed to answer the mission question?
- Which risks need validation within this cycle rather than later?
- What would make the mission unshippable even if implementation finishes?
- Which experiments are valuable, but not mission-critical?
- What would justify simplifying scope mid-cycle?

## Anti-Patterns

### The Endless Discovery Mission

The team keeps expanding the question. What goes wrong: learning feels active, but no decision gets easier.

### The Shipping Theater Mission

The team commits to launch optics before quality confidence exists. What goes wrong: demo success masks operational risk.

### The Scope-By-Excitement Pattern

New ideas enter because they are interesting. What goes wrong: the mission loses focus and no core question is answered well.

## Red Flags

- No one can state the mission question in one sentence
- Weekly reviews drift into tactical debugging only
- Success criteria are purely build-based
- New AI capabilities are being added without clear relation to the mission goal
- Carryover decisions happen implicitly rather than explicitly

## Bottom Line

Scope the mission around a decision, not just a deliverable. AI teams need a cycle structure that can absorb uncertainty without becoming directionless.
