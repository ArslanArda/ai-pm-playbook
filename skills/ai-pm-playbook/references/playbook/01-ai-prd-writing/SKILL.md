# Skill: Write An AI PRD

> **Context:** In Codex, look for `my-product/PRODUCT_CONTEXT.md` in the current workspace first and use it as the default product context. If local file access is unavailable, ask the user to paste product context manually or use the bundled template.

## TL;DR

Use this skill when you need to write or sharpen a PRD for an AI-powered feature. It helps you define the user problem, narrow the AI task, specify quality and evaluation criteria, design fallback behavior, document edge cases, and produce a PRD that engineering and leadership can actually use to make decisions.

## When to Use This

- You are defining a new AI feature and need a production-ready PRD
- You have a rough concept or prototype, but the spec is still vague
- Engineering is asking for more precision about behavior, metrics, or fallback logic
- Leadership wants a clearer explanation of what the AI feature will actually do and how risk will be managed
- You are replacing a traditional PRD template that does not cover model behavior, evals, or failure handling
- You need to compare multiple AI feature directions using the same structure

## Prerequisites

- A rough feature concept or product problem statement
- A basic understanding of the affected user flow
- Current constraints on latency, budget, privacy, and risk tolerance
- Any existing prototypes, prompt drafts, or technical assumptions if they exist
- At least rough alignment on why this feature matters to the business and the user

## Step-by-Step Process

### Step 1: Name The User Problem And The Product Outcome

- **What to do:** Start the PRD with the user problem, not the AI approach. Define who the user is, what job they are trying to get done, what is broken today, and what better outcome you want.
- **Key questions to answer:** Which user or persona is this for? What friction in the current flow is worth solving? What better decision, task, or outcome should the user get? Why is AI the right lever instead of a deterministic UX change? What business outcome matters if this works?
- **Output:** A clear problem statement, target user definition, and success framing grounded in user value.
- **Common mistakes:** Leading with “we will use an LLM”; describing a capability instead of a problem; mixing user value with internal excitement about AI.

### Step 2: Define The AI Task Boundary

- **What to do:** Describe exactly what the AI system is responsible for and what remains deterministic or manual. Break the behavior into sub-jobs if needed.
- **Key questions to answer:** What is the AI generating, classifying, extracting, ranking, or summarizing? What decisions must remain under product control? What is explicitly out of scope for v1? What types of user requests should the AI refuse, clarify, or reroute? If the AI disappeared tomorrow, what non-AI flow would remain?
- **Output:** A scoped task definition including in-scope behavior, out-of-scope behavior, and the interface between AI and non-AI components.
- **Common mistakes:** Giving the AI an overly broad mandate; hiding scope ambiguity inside phrases like “assist the user”; treating agentic behavior as a feature rather than a set of bounded tasks.

### Step 3: Specify The User Experience Across Happy Path And Failure Path

- **What to do:** Write the user-facing behavior, including not only the ideal flow but also ambiguity handling, low-confidence states, retries, and fallback experiences.
- **Key questions to answer:** What does the user see first? When should the system ask a clarifying question? What happens when the AI is unsure? What happens when the output is partial? When should the user be shown manual controls instead of AI-generated output? How will the product preserve trust after a poor result?
- **Output:** A UX behavior spec covering happy path, clarification path, low-confidence path, and failure path.
- **Common mistakes:** Writing only the best-case scenario; assuming fallback is an engineering detail; failing to specify whether the system should answer, ask, defer, or hand off.

### Step 4: Define Quality Criteria And Evaluation Metrics

- **What to do:** Translate “good output” into observable criteria and measurable metrics. Cover both user-facing quality and operational performance.
- **Key questions to answer:** What does a good output look like in plain language? Which dimensions matter most: relevance, correctness, completeness, tone, structure, safety, latency? What quantitative thresholds matter for launch? What is the acceptable hallucination rate? What quality score, latency P50/P95, or human-review pass rate is required?
- **Output:** A quality rubric plus measurable launch and post-launch metrics.
- **Common mistakes:** Using only business metrics like conversion; defining “quality” too vaguely; setting no explicit launch threshold.

### Step 5: Document Model, Data, And Context Assumptions

- **What to do:** Record the assumptions the feature makes about model capability, data availability, grounding, localization, and context quality. This is not an engineering implementation section; it is the product rationale for those dependencies.
- **Key questions to answer:** What kind of model capability is required: generation, extraction, multimodal reasoning, low-latency dialogue? What data or context must be available for acceptable performance? What structured inputs are required? What localization or language constraints matter? What happens if required data is missing or stale?
- **Output:** A product-facing rationale for model class, context sources, and critical data dependencies.
- **Common mistakes:** Treating model choice as purely technical; failing to define which data the feature depends on; assuming the model can infer missing context safely.

### Step 6: Design Human-In-The-Loop And Review Requirements

- **What to do:** Decide where human oversight is necessary before launch or in production. Be explicit about whether humans review every output, sampled outputs, flagged outputs, or none.
- **Key questions to answer:** Is human review required for safety, brand, legal, or trust reasons? Which outputs are too risky to publish automatically? What confidence or severity threshold should trigger review? Who reviews flagged cases, and how quickly? What is the operational burden if the AI underperforms?
- **Output:** A human-review policy and escalation design tied to product risk.
- **Common mistakes:** Assuming humans will “check important outputs” without defining ownership or volume; forgetting to estimate review load; adding manual review that destroys the business case.

### Step 7: Map Edge Cases And What Could Go Wrong

- **What to do:** Create a concrete taxonomy of failure modes, unsupported requests, adversarial inputs, and risky scenarios. This section should make the team less surprised later.
- **Key questions to answer:** What kinds of ambiguity will the feature encounter? What edge cases are common in this domain? Which wrong answers are merely annoying versus trust-damaging or legally risky? What happens when the user asks for something unsupported? What failure would generate the worst screenshot for leadership or social media?
- **Output:** An edge-case list and a “what could go wrong” section with mitigation logic.
- **Common mistakes:** Leaving edge cases to QA; listing generic risks without linking them to behavior; ignoring adversarial or weird inputs because the happy path feels more important.

### Step 8: Define Rollout, Monitoring, And Decision Gates

- **What to do:** State how the feature will be launched, monitored, and iterated. AI PRDs should not end at “build v1.”
- **Key questions to answer:** Will the launch be internal-only, beta, geography-limited, or persona-limited? What dashboards or review rituals will track quality after launch? What launch gate must be passed before wider rollout? What signals would cause rollback, prompt revision, or a switch to a fallback-heavy mode?
- **Output:** A launch and iteration plan with explicit gates and monitoring signals.
- **Common mistakes:** Treating launch as binary; assuming monitoring can be defined later; failing to name rollback triggers.

## Decision Framework

Use this rubric to decide whether your PRD is ready to move forward.

| Dimension | Weak PRD | Acceptable PRD | Strong PRD |
| --- | --- | --- | --- |
| User problem clarity | Capability-first, vague problem | Clear problem, but weak prioritization | Concrete user pain and business rationale tied to one flow |
| AI task definition | “AI helps” language, unclear boundary | Core task defined, but some scope ambiguity remains | In-scope, out-of-scope, and clarification cases are explicit |
| Quality definition | Mostly business KPIs | Some output quality criteria | Clear rubric plus measurable thresholds for launch |
| Fallback design | Missing or hand-wavy | Basic fallback exists | Clarification, low-confidence, failure, and non-AI paths are specified |
| Data and model assumptions | Hidden assumptions | Basic dependencies listed | Required context, localization, and dependency risks are explicit |
| Human review | Not addressed | Mentioned, not operationalized | Review triggers, owners, and burden are clearly specified |
| Edge cases | Minimal | Some cases listed | Edge cases are prioritized by user risk and business impact |
| Launch plan | “Ship and monitor” | Rollout noted | Launch gates, monitoring signals, and rollback conditions are defined |

Default rule:

- If two or more dimensions are still in the “Weak PRD” column, do not treat the document as launch-shaping.
- If the PRD is strong on user problem and weak on quality definition, pause and fix quality before architecture debates.
- If the PRD is strong on behavior but weak on fallback, the team will underestimate trust risk.

## Quality Checklist

- [ ] Does the PRD name a specific user problem rather than an AI capability?
- [ ] Does it define exactly what the AI is responsible for and what it is not?
- [ ] Does it specify the user experience for low-confidence or failed outputs?
- [ ] Does it include feature-specific quality criteria beyond business KPIs?
- [ ] Does it define measurable launch thresholds such as quality score, hallucination rate, or latency targets?
- [ ] Does it document critical data, grounding, or localization assumptions?
- [ ] Does it state whether human review is required and when?
- [ ] Does it include a prioritized list of edge cases and risky scenarios?
- [ ] Does it contain a “what could go wrong” section with mitigation logic?
- [ ] Does it define rollout scope, monitoring signals, and rollback conditions?

## Anti-Patterns

### 1. The Demo PRD

- **Description:** The spec reads like a polished demo narrative rather than a product document. It emphasizes impressive behavior and skips reliability, fallbacks, or messy constraints.
- **Why it happens:** Early excitement and stakeholder pressure reward aspirational storytelling.
- **What to do instead:** Write the PRD around user value, acceptable quality, and operational reality. Add a “what could go wrong” section before socializing the doc broadly.

### 2. The Capability Proxy

- **Description:** The PRD says the feature should “act like an assistant” or “help the user find what they need” without defining the actual tasks.
- **Why it happens:** Teams confuse broad product ambition with usable specification.
- **What to do instead:** Break the behavior into narrow, testable tasks and define where the AI should clarify, defer, or hand off.

### 3. The KPI-Only Spec

- **Description:** Success is defined only through conversion, retention, CTR, or engagement metrics.
- **Why it happens:** PMs are used to business metrics and postpone AI quality metrics.
- **What to do instead:** Add feature-level quality measures such as relevance, correctness, hallucination rate, compliance, or human-review pass rate.

### 4. The Invisible Fallback

- **Description:** The PRD assumes the system will “just fail gracefully,” but no graceful behavior is actually defined.
- **Why it happens:** Fallbacks feel secondary during early planning.
- **What to do instead:** Specify what the user sees when the model is unsure, unavailable, incomplete, or wrong. Treat fallback behavior as part of the feature, not an exception case.

### 5. The Hidden Human Cleanup

- **Description:** The product only works because humans are expected to correct AI mistakes, but the PRD never names the review path or the operational burden.
- **Why it happens:** Manual review sneaks in informally during pilots and becomes invisible in documentation.
- **What to do instead:** State exactly what gets reviewed, by whom, at what volume, and whether that workload is sustainable.

### 6. The Edge-Case Debt

- **Description:** Ambiguous inputs, multilingual queries, adversarial requests, or missing-data scenarios are postponed until late testing.
- **Why it happens:** Teams over-focus on the happy path to preserve momentum.
- **What to do instead:** Prioritize the top edge cases early and define product behavior for each one in the PRD.

## Adaptation Guide

### B2B vs. B2C

For B2B products, emphasize workflow reliability, auditability, human review, and account-level variance. For B2C products, emphasize trust, latency, user education, and graceful fallback when the AI is wrong.

### Startup vs. Enterprise

Startups can accept more ambiguity if the PRD still nails the user problem and launch gate. Enterprises should write stronger review, governance, compliance, and escalation sections because ambiguity gets expensive quickly in larger organizations.

### Text vs. Vision vs. Voice

Text features need strong quality rubrics and source/fallback design. Vision features need explicit confidence thresholds and false positive versus false negative tradeoffs. Voice features need latency budgets, interruption handling, turn-taking rules, and escalation logic.

### Assistive vs. Autonomous Features

Assistive features should specify where the user remains in control and how to correct AI output quickly. Autonomous features need much stronger failure handling, rollback logic, confidence thresholds, and human intervention rules.

### Early-Stage Exploration vs. Scaled Production

In exploration, the PRD can note open questions as long as launch gates are explicit. In scaled production, open questions should be narrower and tied to follow-up experiments rather than core behavior ambiguity.
