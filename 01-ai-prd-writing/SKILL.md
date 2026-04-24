# Skill: Write An AI Agent PRD

> **Context:** In Codex, look for `my-product/PRODUCT_CONTEXT.md` in the current workspace first and use it as the default product context. If local file access is unavailable, ask the user to paste product context manually or use the bundled template. If you already have an agent prompt, tool list, or rough workflow sketch, include that too so the PRD can stay aligned with the actual agent behavior.

## TL;DR

Use this skill when you need to write or sharpen a PRD for an AI agent, not just a generic AI feature. It helps you define the user problem, narrow the agent's job, specify tool boundaries, design fallback behavior, define evaluation strategy and starter datasets, document review requirements, and produce a PRD that engineering and leadership can actually use to make decisions.

## When to Use This

- You are defining a new AI agent or tool-using workflow and need a production-ready PRD
- You have a rough concept or prototype, but the scope, tools, or launch bar are still vague
- Engineering is asking for more precision about behavior, metrics, evals, or fallback logic
- Leadership wants a clearer explanation of what the agent will actually do and how risk will be managed
- You are replacing a traditional PRD template that does not cover eval strategy, datasets, or human review
- You need to compare multiple agent directions using the same structure

## Prerequisites

- A rough feature concept or product problem statement
- A basic understanding of the affected user flow
- Current constraints on latency, budget, privacy, and risk tolerance
- Any existing prompts, workflow sketches, tool lists, or technical assumptions if they exist
- At least rough alignment on why this agent matters to the business and the user

## Step-by-Step Process

### Step 1: Name The User Problem And The Product Outcome

- **What to do:** Start the PRD with the user problem, not the agent pattern. Define who the user is, what job they are trying to get done, what is broken today, and what better outcome you want.
- **Key questions to answer:** Which user or persona is this for? What friction in the current flow is worth solving? What better decision, task, or outcome should the user get? Why is an agent the right lever instead of a deterministic UX change or a single bounded prompt? What business outcome matters if this works?
- **Output:** A clear problem statement, target user definition, and success framing grounded in user value.
- **Common mistakes:** Leading with "we will build an agent"; describing a capability instead of a problem; mixing user value with internal excitement about autonomy.

### Step 2: Define The Agent Job, Scope Boundary, And Tool Boundaries

- **What to do:** Describe exactly what the agent is responsible for, what it is allowed to do, what remains deterministic, and which tools or APIs it may call.
- **Key questions to answer:** What is the primary job of the agent? Which subtasks are in scope? Which actions require user confirmation? What requests should the agent refuse, clarify, or hand off? What tools are available, and what must remain under product control? If the agent disappeared tomorrow, what non-agentic flow would remain?
- **Output:** A scoped agent contract including in-scope behavior, out-of-scope behavior, tool boundaries, and confirmation rules.
- **Common mistakes:** Giving the agent an overly broad mandate; hiding scope ambiguity inside phrases like "assist the user"; failing to define which tool actions are permitted.

### Step 3: Specify The User Experience Across Happy Path And Failure Path

- **What to do:** Write the user-facing behavior, including not only the ideal flow but also ambiguity handling, low-confidence states, retries, fallbacks, and handoff experiences.
- **Key questions to answer:** What does the user see first? When should the agent ask a clarifying question? What happens when the agent is unsure or blocked by a tool? When should the user be shown manual controls instead of agent output? How will the product preserve trust after a poor result?
- **Output:** A UX behavior spec covering happy path, clarification path, low-confidence path, failure path, and human handoff path.
- **Common mistakes:** Writing only the best-case scenario; assuming fallback is an engineering detail; failing to specify whether the agent should answer, ask, defer, or hand off.

### Step 4: Define The Evaluation Strategy And Starter Dataset Plan

- **What to do:** Translate "good agent behavior" into a rubric, launch thresholds, and a first-pass dataset plan.
- **Key questions to answer:** What makes this agent helpful, trustworthy, and usable? Which dimensions matter most: task success, correctness, grounding, tool-use accuracy, state handling, fallback behavior, safety, latency? What blocker failures must never pass? What starter dataset should be created in CSV form? What should be judged by rules, graders, or humans?
- **Output:** An evaluation strategy with rubric dimensions, launch thresholds, grader approach, and starter dataset plan.
- **Common mistakes:** Using only business metrics; postponing eval design until after implementation; forgetting to name dataset sources and blocker cases.

### Step 5: Document Model, Data, Context, And State Assumptions

- **What to do:** Record the assumptions the agent makes about model capability, data availability, grounding, localization, conversation state, and context quality.
- **Key questions to answer:** What model capabilities are required? What data or context must be available for acceptable performance? What structured inputs or tools are required? What conversation memory or state must persist across turns? What happens if required data is missing or stale?
- **Output:** A product-facing rationale for model class, data dependencies, grounding, and state requirements.
- **Common mistakes:** Treating model choice as purely technical; failing to define which data the agent depends on; assuming the model can infer missing context safely.

### Step 6: Design Human-In-The-Loop, Guardrails, And Review Requirements

- **What to do:** Decide where human oversight, deterministic checks, and product guardrails are necessary before launch or in production.
- **Key questions to answer:** Is human review required for safety, brand, legal, or trust reasons? Which outputs are too risky to publish automatically? What confidence or severity threshold should trigger review? Which actions require deterministic confirmation or policy checks? What is the operational burden if the agent underperforms?
- **Output:** A review policy and guardrail design tied to product risk.
- **Common mistakes:** Assuming humans will "check important outputs" without defining ownership or volume; leaving action controls implicit; adding manual review that destroys the business case.

### Step 7: Map Edge Cases And What Could Go Wrong

- **What to do:** Create a concrete taxonomy of failure modes, unsupported requests, adversarial inputs, state errors, and risky scenarios.
- **Key questions to answer:** What ambiguity will the agent encounter? Which edge cases are common in this domain? Which wrong actions are merely annoying versus trust-damaging or legally risky? What happens when a tool fails or the state is stale? What failure would generate the worst screenshot for leadership or social media?
- **Output:** An edge-case list and a "what could go wrong" section with mitigation logic.
- **Common mistakes:** Leaving edge cases to QA; listing generic risks without linking them to behavior; ignoring tool or state failures because the happy path feels more important.

### Step 8: Define Rollout, Observability, And Decision Gates

- **What to do:** State how the agent will be launched, monitored, and iterated. Agent PRDs should not end at "build v1."
- **Key questions to answer:** Will the launch be internal-only, beta, geography-limited, or persona-limited? What traces, dashboards, or review rituals will track quality after launch? What launch gate must be passed before wider rollout? What signals would cause rollback, prompt revision, or a switch to a more conservative fallback mode?
- **Output:** A launch and iteration plan with explicit gates, monitoring signals, and rollback triggers.
- **Common mistakes:** Treating launch as binary; assuming observability can be defined later; failing to name rollback triggers or trace review cadence.

## Decision Framework

Use this rubric to decide whether your agent PRD is ready to move forward.

| Dimension | Weak PRD | Acceptable PRD | Strong PRD |
| --- | --- | --- | --- |
| User problem clarity | Capability-first, vague problem | Clear problem, but weak prioritization | Concrete user pain and business rationale tied to one flow |
| Agent job and tool boundaries | "Agent helps" language, unclear actions | Core workflow defined, but some scope ambiguity remains | In-scope, out-of-scope, tool contracts, and confirmation rules are explicit |
| Evaluation strategy | Mostly business KPIs | Some quality criteria, weak dataset plan | Clear rubric, launch thresholds, grader approach, and starter dataset plan |
| Fallback design | Missing or hand-wavy | Basic fallback exists | Clarification, low-confidence, failure, and handoff paths are specified |
| Data and state assumptions | Hidden assumptions | Basic dependencies listed | Required context, memory, localization, and dependency risks are explicit |
| Guardrails and review | Not addressed | Mentioned, not operationalized | Review triggers, action controls, owners, and burden are clearly specified |
| Edge cases | Minimal | Some cases listed | Edge cases are prioritized by user risk, tool risk, and business impact |
| Launch and observability | "Ship and monitor" | Rollout noted | Launch gates, trace review, monitoring signals, and rollback conditions are defined |

Default rule:

- If two or more dimensions are still in the "Weak PRD" column, do not treat the document as launch-shaping.
- If the PRD is strong on user problem and weak on evaluation strategy, pause and fix eval design before architecture debates.
- If the PRD is strong on behavior but weak on fallback or review rules, the team will underestimate trust risk.

## Quality Checklist

- [ ] Does the PRD name a specific user problem rather than an AI capability?
- [ ] Does it define exactly what the agent is responsible for and what it is not?
- [ ] Does it define which tools, actions, and confirmations are allowed?
- [ ] Does it specify the user experience for low-confidence, failed, or blocked agent behavior?
- [ ] Does it include an evaluation strategy with rubric dimensions and launch thresholds?
- [ ] Does it describe a starter dataset plan for the agent?
- [ ] Does it document critical data, grounding, localization, and state assumptions?
- [ ] Does it state whether human review is required and when?
- [ ] Does it include a prioritized list of edge cases and risky scenarios?
- [ ] Does it define rollout scope, monitoring signals, and rollback conditions?

## Anti-Patterns

### 1. The Demo PRD

- **Description:** The spec reads like a polished demo narrative rather than a product document. It emphasizes impressive behavior and skips evals, fallbacks, or messy constraints.
- **Why it happens:** Early excitement and stakeholder pressure reward aspirational storytelling.
- **What to do instead:** Write the PRD around user value, acceptable quality, and operational reality. Add a "what could go wrong" section before socializing the doc broadly.

### 2. The Capability Proxy

- **Description:** The PRD says the agent should "help the user" without defining the actual jobs, tool calls, or boundaries.
- **Why it happens:** Teams confuse broad product ambition with usable specification.
- **What to do instead:** Break the behavior into narrow, testable jobs and define where the agent should clarify, defer, or hand off.

### 3. The Tool Contract Gap

- **Description:** The agent can call tools or take actions, but the PRD never states what those actions require or what must remain deterministic.
- **Why it happens:** Teams treat tool design as an implementation detail.
- **What to do instead:** Specify tool boundaries, action permissions, and user confirmation rules inside the PRD.

### 4. The Hidden Eval Debt

- **Description:** The team plans to "measure later," so the PRD has no rubric, dataset plan, or blocker failure list.
- **Why it happens:** Evaluation feels like a downstream concern.
- **What to do instead:** Define the evaluation strategy and starter dataset plan before launch planning.

### 5. The Invisible Fallback

- **Description:** The PRD assumes the system will "fail gracefully," but no graceful behavior is actually defined.
- **Why it happens:** Fallbacks feel secondary during early planning.
- **What to do instead:** Specify what the user sees when the agent is unsure, unavailable, incomplete, blocked, or wrong. Treat fallback behavior as part of the feature, not an exception case.

### 6. The Hidden Human Cleanup

- **Description:** The product only works because humans are expected to correct agent mistakes, but the PRD never names the review path or operational burden.
- **Why it happens:** Manual review sneaks in informally during pilots and becomes invisible in documentation.
- **What to do instead:** State exactly what gets reviewed, by whom, at what volume, and whether that workload is sustainable.

## Adaptation Guide

### Assistive vs. Autonomous Agents

Assistive agents should specify where the user remains in control and how to correct output quickly. Autonomous or action-taking agents need much stronger confirmation rules, rollback logic, and review requirements.

### Internal Copilots vs. Customer-Facing Agents

Internal copilots can tolerate more review and iteration. Customer-facing agents need stronger fallback behavior, trust repair, and explicit user-facing constraints.

### Single-Agent vs. Multi-Step Workflows

Single-agent flows still need explicit scope and eval design. Multi-step workflows need clearer tool boundaries, state assumptions, and observability because failures can occur at several points.

### Text vs. Voice vs. Multimodal Agents

Text agents need strong rubric and grounding design. Voice agents need latency budgets, interruption handling, and handoff logic. Multimodal agents need explicit confidence thresholds and wrong-action safeguards.
