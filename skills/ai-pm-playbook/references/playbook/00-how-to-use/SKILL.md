# Skill: Use The AI PM Playbook With Your AI Assistant

> **Personalization:** Before starting, paste your completed `my-product/PRODUCT_CONTEXT.md` into the conversation. This skill works without it, but the guidance will be significantly more relevant with your product context loaded.

## TL;DR

Use this skill when you want to turn the playbook from a static reference into a guided working session with an LLM. It helps you choose the right section, load the right context, structure the conversation, and turn generic AI advice into outputs that are specific to your product, team, constraints, and current decision.

## When to Use This

- You just forked the repo and want to set up the highest-leverage usage pattern
- You are not sure which playbook section to start with for your current AI problem
- You want to use `SKILL.md` files with ChatGPT, Claude, Gemini, or another LLM in a disciplined way
- You are getting generic answers from an LLM and need a better workflow for context loading and guided questioning
- You want to turn a section into a concrete deliverable such as a PRD, evaluation plan, routing strategy, team ritual, or UX spec
- You are onboarding another PM or founder to the playbook and want a repeatable process instead of “just browse around”

## Prerequisites

- A rough understanding of the AI feature, product problem, or operating challenge you are working on
- Your `my-product/PRODUCT_CONTEXT.md` completed at least through Sections 1-3, ideally further
- Access to one relevant `SKILL.md` file from the repo
- A willingness to answer follow-up questions with specifics instead of abstract goals
- A target output in mind, even if it is still rough, such as “AI PRD draft,” “model decision memo,” or “AI onboarding flow”

## Step-by-Step Process

### Step 1: Define The Real Job To Be Done

- **What to do:** Name the concrete decision or artifact you need from this session. Do not start with “I want to explore AI.” Start with something like “I need a PRD for AI search” or “I need to decide whether routing is worth the added complexity.”
- **Key questions to answer:** What deliverable do you need by the end of this session? What decision is currently blocked? What would be different in the team if this session went well? What is the deadline or trigger making this urgent now?
- **Output:** A one-sentence session objective with a named deliverable and a named decision.
- **Common mistakes:** Starting with a broad topic instead of a concrete task; asking for “ideas” when you actually need a decision; ignoring the organizational context that makes the task urgent.

### Step 2: Load Product Context Before Advice

- **What to do:** Paste your `PRODUCT_CONTEXT.md` into the conversation before asking the model to solve the problem. If the context file is incomplete, at least provide product overview, users, core flows, and major constraints.
- **Key questions to answer:** Who are the users affected by this work? What flow is being changed? What constraints matter most: cost, latency, compliance, adoption, trust, or quality? What AI maturity level is the team operating at? What current systems or data assets already exist?
- **Output:** A context-loaded chat where the model can reason about your actual product instead of a generic SaaS example.
- **Common mistakes:** Asking the model to do detailed work without any product context; leaving out critical constraints such as privacy or language; assuming the model will infer your business model or user needs.

### Step 2A: Update Product Context When Reality Changes

- **What to do:** If you have new product facts, market data, constraints, or priorities, add them to `PRODUCT_CONTEXT.md` before continuing. In Codex, you can give the update in chat and ask it to merge the information into the file for you.
- **Key questions to answer:** Is this a new fact that should persist across future sessions? Which section of the context does it belong in? Does it replace old information or add to it?
- **Output:** A current product context file that reflects the latest reality.
- **Common mistakes:** Keeping fresh context only in one conversation; forgetting to replace outdated assumptions; letting the context file drift away from the product’s actual state.

### Step 3: Choose The Right Playbook Section

- **What to do:** Match your problem to the section that owns it. If you are doing spec work, start with AI PRD writing. If you are debugging poor outputs, evaluation or prompt debugging may be the right entry point. If the problem is architectural, start with agent system design or model strategy.
- **Key questions to answer:** Is the core challenge product definition, evaluation, model choice, orchestration, team process, prompt behavior, or user experience? Are you trying to make a build decision, a quality decision, an operating decision, or a UX decision? Which section contains the most direct decision framework for that problem?
- **Output:** A selected `SKILL.md` file and, if needed, one or two supporting framework files.
- **Common mistakes:** Starting with agent design because it sounds sophisticated when the real problem is a weak PRD or bad eval design; using prompt iteration to solve a data or UX problem; trying to solve all sections at once.

### Step 4: Instruct The LLM To Act Like A Guide, Not A Content Generator

- **What to do:** Tell the model to walk you through the process step by step, ask only the questions it needs, make recommendations with rationale, and challenge weak assumptions. This changes the interaction from “write me a document” to “help me think and decide.”
- **Key questions to answer:** Do you want a guided interview or a one-shot output? Should the model challenge your assumptions or simply draft? Should it optimize for speed, depth, or stakeholder-readiness? Do you want it to produce an artifact incrementally or only at the end?
- **Output:** A clear operating instruction that shapes the rest of the session.
- **Common mistakes:** Asking for a complete answer immediately; letting the model stay vague; failing to specify that you want tradeoffs, red flags, and recommendations.

### Step 5: Work Through The Skill In Order

- **What to do:** Follow the steps in the selected `SKILL.md` in sequence unless you already have high-confidence answers for a step. If the model skips to the end, pull it back and ask it to work step by step.
- **Key questions to answer:** Which step are you currently on? What assumptions are still unresolved? What evidence do you already have versus what is still opinion? What artifact should be produced before moving to the next step?
- **Output:** A structured working session with intermediate outputs instead of one long generic response.
- **Common mistakes:** Skipping discovery because you want to move faster; mixing evaluation, architecture, and UX decisions into one muddy discussion; failing to capture intermediate decisions.

### Step 6: Pull In Supporting Files Only When They Add Signal

- **What to do:** If the conversation needs more specificity, add one relevant framework, template, or example file. Use examples to ground the work, templates to structure outputs, and frameworks to sharpen a hard decision.
- **Key questions to answer:** Are you missing decision logic, output structure, or realism? Would a framework clarify the decision, or would an example help you pattern-match? Is the model confused because it lacks a concrete reference artifact?
- **Output:** A smaller set of high-signal companion files loaded into the chat.
- **Common mistakes:** Dumping an entire folder into the conversation; confusing the model with too many overlapping files; using examples as a substitute for your own context.

### Step 7: Force A Recommendation, Then Pressure-Test It

- **What to do:** Ask the model to make a recommendation, not just list options. Then ask it to explain why, when the recommendation would fail, and what signals would justify a different choice.
- **Key questions to answer:** What is the recommended path? What is the strongest case against that recommendation? Under what constraints would another path be better? What would you monitor after launch to validate the choice?
- **Output:** A decision with rationale, alternatives, and failure conditions.
- **Common mistakes:** Accepting option lists without a point of view; confusing breadth with rigor; failing to ask how the recommendation could break in practice.

### Step 8: Use The Checklist Before You Leave The Session

- **What to do:** End by running the section’s Quality Checklist and Anti-Patterns against the draft. Ask the model to identify missing pieces, weak assumptions, and overly generic claims.
- **Key questions to answer:** Which checklist items are still “no”? Which anti-patterns are present in the current draft? What evidence or decisions are still missing? Is the output ready for internal review, or does it need another pass?
- **Output:** A reviewed, higher-confidence artifact with explicit gaps noted.
- **Common mistakes:** Treating the first coherent draft as final; skipping self-review because the output “sounds good”; failing to convert open questions into next actions.

## Decision Framework

Use this matrix to decide how to run the session.

| Situation | Recommended file to start with | How to prompt the LLM | What success looks like |
| --- | --- | --- | --- |
| You need to define a new AI feature clearly | `01-ai-prd-writing/SKILL.md` | “Guide me step by step and draft the PRD sections as we go.” | A scoped PRD with eval criteria, fallback behavior, and failure modes |
| You have outputs but do not know how to judge quality | `02-evaluation-design/SKILL.md` | “Help me define an evaluation plan and an error taxonomy for this feature.” | A concrete eval plan with metrics, dataset strategy, and review cadence |
| The team is debating models, routing, or fine-tuning | `03-model-strategy/SKILL.md` | “Recommend a model strategy and show the cost-latency-quality tradeoff.” | A defensible model decision memo with routing logic and fallback reasoning |
| Architecture is getting more agentic and messy | `04-ai-agent-system-design/SKILL.md` | “Challenge whether we actually need an agent system and, if yes, which pattern fits.” | A clearer architecture recommendation with guardrails, observability, and failure handling |
| The problem is team coordination, not product design | `05-ai-team-operations/SKILL.md` | “Help me set up the operating rhythm, DACI, and review rituals for this AI work.” | A workable team process with named rituals and ownership |
| Prompt behavior is unstable or hard to manage | `06-prompt-engineering-for-pms/SKILL.md` | “Treat the prompt as product behavior and help me specify, test, and debug it.” | A tighter prompt spec, versioning approach, and debugging path |
| The AI works technically but the UX is weak | `07-ai-ux-patterns/SKILL.md` | “Help me redesign the user experience for uncertainty, latency, and fallbacks.” | A user-facing flow with clearer states, trust cues, and fallback behavior |

Rule of thumb:

- Start with the section closest to the current bottleneck.
- If you are unsure, choose the section that owns the decision, not the section with the most exciting terminology.
- Add a second file only when the first one reveals a deeper dependency.

## Quality Checklist

- [ ] Did I provide enough product context for the model to reason about my actual situation?
- [ ] Did I define a concrete output or decision before starting?
- [ ] Did I choose the section that matches the real bottleneck rather than the most fashionable topic?
- [ ] Did I ask the model to guide me step by step instead of generating generic advice?
- [ ] Did I answer the model’s questions with specific constraints, users, and metrics?
- [ ] Did I force the model to make a recommendation with rationale?
- [ ] Did I pressure-test the recommendation with red flags, alternatives, and failure conditions?
- [ ] Did I use the section’s checklist before treating the output as finished?
- [ ] Did I capture unresolved questions and next actions instead of leaving them implicit?
- [ ] Did I avoid loading unnecessary files that added noise rather than signal?

## Anti-Patterns

### 1. The Empty-Context Prompt

- **Description:** You paste only the skill or ask a broad question with no product context.
- **Why it happens:** It feels faster to skip setup, especially when you are in a hurry.
- **What to do instead:** Provide at least product overview, users, flow, and major constraints before asking for advice.

### 2. The Section Mismatch

- **Description:** You start with agent architecture, model strategy, or prompt tuning when the core problem is actually unresolved product definition.
- **Why it happens:** Teams often jump to the most technical-looking layer because it feels more advanced.
- **What to do instead:** Ask which decision is truly blocked. If the behavior is still underspecified, start with the PRD or UX section first.

### 3. The One-Shot Dump

- **Description:** You ask the model for a complete strategy, review it briefly, and move on.
- **Why it happens:** One-shot generation feels efficient and gives the illusion of progress.
- **What to do instead:** Force a guided workflow with intermediate outputs, explicit decisions, and checklist review.

### 4. The Option List With No Recommendation

- **Description:** The model gives you a balanced list of possibilities and you leave the session without a clear path.
- **Why it happens:** LLMs default to being helpful and non-committal unless pushed.
- **What to do instead:** Ask for a recommendation, rationale, strongest counterargument, and the conditions that would justify a different choice.

### 5. The Example Copy-Paste Trap

- **Description:** You reuse an example artifact almost verbatim without adapting it to your product context.
- **Why it happens:** Good examples are seductive, especially under deadline pressure.
- **What to do instead:** Use examples for structure and realism, then rewrite the decision logic around your own users, risks, and constraints.

### 6. The Checklist Skip

- **Description:** You stop once the output sounds plausible.
- **Why it happens:** The human brain rewards coherence, even when rigor is missing.
- **What to do instead:** Run the checklist and anti-pattern review before you consider the session complete.

## Adaptation Guide

### B2B vs. B2C

In B2B contexts, load account-level workflow complexity, compliance requirements, and adoption friction into the conversation early. In B2C contexts, emphasize scale, latency tolerance, trust, and user education.

### Startup vs. Enterprise

For startups, push the model toward faster scoping, tighter prioritization, and simpler operating mechanisms. For enterprise teams, include governance, approval layers, legal constraints, and cross-functional decision rights earlier in the session.

### Early Exploration vs. Production Optimization

If you are still exploring, use the playbook to narrow the problem and define the first success criteria. If you already have AI in production, use it to sharpen evaluation, routing, observability, and operational discipline rather than rehashing high-level strategy.

### Single Feature vs. Platform Work

For a single feature, keep the chat focused on one user flow and one decision. For platform work, explicitly separate reusable platform decisions from feature-specific product decisions so the model does not blur them together.

### Text, Vision, Voice, Or Multi-Agent Systems

For text-heavy features, emphasize evaluation criteria and UX expectations. For vision systems, surface confidence thresholds and false positive versus false negative tradeoffs. For voice, load latency budgets and interruption handling. For multi-agent systems, prioritize orchestration boundaries, tool design, and failure containment.
