# Skill: Design An AI Agent System

> **Context:** In Codex, look for `my-product/PRODUCT_CONTEXT.md` in the current workspace first and use it as the default product context. If local file access is unavailable, ask the user to paste product context manually or use the bundled template.

## TL;DR

Use this skill when your AI feature has become multi-step enough that prompt-only thinking is no longer sufficient. It helps you decide whether you even need an agent system, choose the simplest viable architecture, define tool boundaries, set guardrails and fallbacks, and specify the observability and cost controls required before launch.

## When to Use This

- You are deciding whether a feature should stay single-step or become agentic
- The team wants to split work across multiple tools, prompts, or specialist agents
- A current AI workflow is becoming hard to debug because multiple steps are hidden inside one prompt
- You need a product-facing architecture recommendation, not just an engineering sketch
- You are scoping guardrails, fallback chains, or human handoff for an agentic experience
- Cost or latency is rising because the workflow is growing in complexity

## Prerequisites

- A defined user problem or feature concept
- A rough description of the current or proposed AI workflow
- Known user-facing latency expectations
- At least rough constraints on cost, compliance, and risk tolerance
- Some understanding of what tools, data sources, or APIs the system may need

## Step-by-Step Process

### Step 1: Confirm That The Product Problem Actually Requires Orchestration

- **What to do:** Ask whether the feature truly needs multi-step reasoning, routing, or tool use, or whether the team is reaching for agent language too early.
- **Key questions to answer:** What specific user value requires multiple coordinated steps? Could one bounded prompt with a few deterministic helpers solve this? Which part of the workflow cannot be expressed reliably in a simpler pattern? What breaks if you keep the system non-agentic?
- **Output:** A clear statement of why an agent system is justified or why it is not.
- **Common mistakes:** Starting from architecture fashion instead of user need; calling a normal tool-using assistant “multi-agent” without reason; using orchestration to compensate for a weak product definition.

### Step 2: Decompose The Workflow Into Product-Critical Jobs

- **What to do:** Break the end-to-end interaction into distinct jobs such as triage, intent extraction, retrieval, execution, validation, response generation, and handoff.
- **Key questions to answer:** Which steps are deterministic versus probabilistic? Which steps are high-risk if wrong? Which steps need specialization? Which steps must remain visible to the user? Which steps could fail independently?
- **Output:** A workflow map with named steps and product significance for each.
- **Common mistakes:** Treating the whole flow as one blob; decomposing into too many abstract micro-steps; failing to separate retrieval, execution, and explanation.

### Step 3: Choose The Smallest Architecture That Can Do The Job

- **What to do:** Decide between single-agent, simple pipeline, router pattern, parallel fan-out, or iterative refinement based on task complexity, tool count, latency budget, and isolation needs.
- **Key questions to answer:** Do you need specialization across tasks or just sequencing? Does the flow require independent failure handling by step? Is the latency budget compatible with multiple model hops? Will context windows become too large if everything stays in one prompt?
- **Output:** A recommended architecture pattern with explicit rationale.
- **Common mistakes:** Choosing multi-agent because it sounds scalable; ignoring the latency cost of every extra hop; missing the value of simple deterministic routing.

### Step 4: Define Tool Boundaries And Product Contracts

- **What to do:** Decide what becomes a tool, what stays in prompt logic, what stays deterministic, and how granular tool interfaces should be.
- **Key questions to answer:** Which capabilities need structured access to live data or actions? What must be reliable enough to deserve deterministic enforcement? Is one broad tool easier for the model, or does it hide too many failure states? What schema design minimizes ambiguity and token waste?
- **Output:** A tool map with product rationale for each boundary.
- **Common mistakes:** Turning every subtask into a tool; making tools so broad that observability disappears; letting the model improvise where product policy should be fixed.

### Step 5: Design Guardrails, Fallbacks, And Escalation Paths

- **What to do:** Define what the system checks before acting, after acting, and before responding to the user. Include low-confidence handling and human handoff where relevant.
- **Key questions to answer:** What inputs should be blocked or rerouted? Which outputs must be validated? What should happen when a tool fails, returns partial data, or conflicts with policy? When is user trust better served by asking, deferring, or handing off?
- **Output:** A guardrail and fallback design tied to specific workflow steps.
- **Common mistakes:** Treating guardrails as only a safety topic; adding validation with no user-facing fallback; relying on hidden retries that make latency unpredictable.

### Step 6: Set Cost And Latency Budgets Before The System Grows

- **What to do:** Put explicit limits on model hops, context size, response length, and retry behavior so the workflow does not quietly become too expensive or too slow.
- **Key questions to answer:** What latency is acceptable for this user experience? Which steps can be asynchronous? Which steps require the stronger model, and which do not? What is the acceptable cost per conversation or task? Which retries are worth paying for?
- **Output:** Budget constraints that shape architecture choices.
- **Common mistakes:** Discussing cost after launch; assuming better quality always justifies slower flows; ignoring how repeated retries compound both latency and spend.

### Step 7: Specify Observability And Review Rituals

- **What to do:** Decide what you will log, measure, and review so the system is debuggable and improvable after launch.
- **Key questions to answer:** Which step-level metrics matter most? How will you inspect traces for failed sessions? Which failures need daily review versus weekly trend analysis? What signals indicate routing drift, tool unreliability, or model misuse?
- **Output:** An observability plan connected to PM review rituals.
- **Common mistakes:** Logging only end-to-end success; omitting step-level token and latency data; failing to tie dashboards to actual decision-making rituals.

### Step 8: Produce An Architecture Recommendation And Decision Memo

- **What to do:** Summarize the recommended pattern, why it fits, what alternatives were rejected, and what assumptions must hold true for the design to work.
- **Key questions to answer:** Why is this architecture simpler or safer than the alternatives? What must be validated before broader rollout? What future conditions would justify adding more orchestration? What is the rollback or simplification path if the design underperforms?
- **Output:** A concise architecture decision memo suitable for product and engineering review.
- **Common mistakes:** Ending with a diagram but no recommendation; failing to document rejected alternatives; leaving critical assumptions implicit.

## Decision Framework

Use this scorecard before choosing a more complex design.

| Question | If answer is mostly “no” | If answer is mostly “yes” |
| --- | --- | --- |
| Does the task genuinely require multiple distinct AI jobs? | Prefer single-agent or prompt-plus-tools | Consider pipeline or specialized agents |
| Do different steps need different prompts, tools, or failure handling? | Keep logic unified | Consider router or multi-step pipeline |
| Will one prompt hit context or control limits? | Keep it simple | Split steps or isolate memory |
| Is latency budget tight and user-facing? | Avoid multiple model hops | Use extra hops only where quality gain is clear |
| Would a bad decision in one step benefit from isolation and explicit validation? | Simple flow may be enough | Add step boundaries and validation |
| Can the team observe and maintain a more complex system? | Do not overbuild | Complexity may be justified |

Default rule:

- If fewer than three questions land in the “yes” column, do not start with a multi-agent design.
- If the only reason for complexity is “future flexibility,” reject it.
- If specialization clearly improves quality or failure isolation on a high-risk step, complexity may be justified.

## Quality Checklist

- [ ] Did we prove that the product problem requires orchestration rather than a simpler pattern?
- [ ] Did we map the workflow into distinct jobs with clear product meaning?
- [ ] Did we choose the smallest architecture that can deliver the required behavior?
- [ ] Did we define what is deterministic, what is tool-based, and what is model-driven?
- [ ] Did we specify input validation, output validation, and user-facing fallback behavior?
- [ ] Did we set latency and cost budgets before locking the design?
- [ ] Did we define observability at the step level, not just end-to-end?
- [ ] Did we document handoff or escalation conditions where trust risk is high?
- [ ] Did we record the assumptions under which this architecture remains the right choice?
- [ ] Did we note what would trigger simplification, expansion, or rollback later?

## Anti-Patterns

### 1. The Architecture Theater Pattern

- **Description:** The team adopts planners, routers, and specialist agents mainly because they sound advanced.
- **Why it happens:** “Agentic” language creates pressure to look technically ambitious.
- **What to do instead:** Start from the user problem and justify each added layer with a specific gain in quality, control, or maintainability.

### 2. The Single-Prompt Blob

- **Description:** Too many responsibilities are hidden inside one huge prompt, making behavior hard to debug and govern.
- **Why it happens:** It feels faster than designing explicit step boundaries.
- **What to do instead:** Split high-risk or high-ambiguity jobs into visible steps when it improves control or observability.

### 3. The Tool Explosion

- **Description:** Every minor capability becomes its own tool, creating routing confusion and token waste.
- **Why it happens:** Teams equate modularity with quality.
- **What to do instead:** Group tools around stable product actions and data domains, not arbitrary internal abstractions.

### 4. The Hidden Retry Maze

- **Description:** The system quietly retries prompts, tools, or models multiple times without a clear product rule.
- **Why it happens:** Engineers try to improve apparent success rates without revisiting UX tradeoffs.
- **What to do instead:** Define retry logic, latency budgets, and user-facing fallback behavior explicitly in the product design.

### 5. The Black-Box Launch

- **Description:** The system ships without step-level traces, token visibility, or routing diagnostics.
- **Why it happens:** Teams focus on capability first and assume observability can be added later.
- **What to do instead:** Treat logging, traceability, and review rituals as part of the launch scope, not a follow-up task.

## Adaptation Guide

### Search And Retrieval Products

Bias toward simple pipelines with strong grounding and deterministic search execution. The model should interpret, explain, and refine, not invent inventory truth.

### Content Generation Products

Iterative refinement patterns can be valuable, but only if review loops measurably improve quality and the latency/cost tradeoff still makes sense for the workflow.

### Internal Copilots

Human handoff is usually built-in, which allows somewhat more ambitious drafting behavior. Still, guardrails and observability matter because bad suggestions damage adoption quickly.

### Voice Agents

Latency and interruption handling are dominant. Avoid architectures that depend on too many serial model hops unless the user experience can tolerate them.

### Early-Stage Teams vs. Mature AI Teams

Early-stage teams should strongly prefer simpler patterns they can observe and maintain. Mature teams can justify more orchestration, but only with disciplined eval, cost controls, and trace review already in place.
