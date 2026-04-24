---
name: ai-pm-playbook
description: Use when the user needs agent-centered AI product-management help across orchestration, tools, evals, prompts, UX, and launch decisions, especially when agent design has to stay aligned with product scope and quality.
---

# AI PM Playbook

Use this as an agent-centered Codex skill for AI PM work.

Short version: this is a strong AI PM judgment system for AI agents, not a general AI build guide.

The center of gravity is agent and tool design, not generic product planning. Use it when the user is designing an AI workflow that may involve orchestration, routing, tools, guardrails, evals, prompt behavior, fallback UX, and launch decisions.

This skill still bundles adjacent PM material because agent work gets worse when task definition, quality bars, or fallback rules are vague. PRD writing is included as supporting material for agent scope, task boundaries, human review, and launch gates, not as a generic standalone PRD assistant.

Do not treat this skill like a document index or a repo tour. Read the needed references yourself, synthesize the answer, and help the user produce a concrete artifact, recommendation, or next-step plan.

## Artifact Menu

Use this skill to produce one of these default outputs:

- `architecture memo`: whether the workflow should be non-agentic, single-agent, or multi-step, with rationale
- `agent PRD`: product requirements for an AI agent including scope, tools, evals, datasets, fallback behavior, and launch gates
- `agent instruction pack`: decision-backed single-agent or multi-agent instructions including tool boundaries, shared rules, and fallback behavior
- `eval plan`: evaluation strategy, rubric, grader approach, and starter dataset plan
- `launch review`: decision-ready review of launch blockers, risks, and rollout readiness
- `fallback design`: user-facing fallback, escalation, and human-review behavior

## First Session Fast Path

Use one of these prompts on the first working session:

1. "Here is my workflow and product context. Should this stay prompt-only, become a single agent, or become a multi-step system?"
   Expected output: `architecture memo`
2. "Here is my agent or system prompt. Turn it into an evaluation strategy, grader prompt, and starter CSV rubric dataset."
   Expected output: `eval plan`
3. "Help me write an agent PRD for this workflow, including tools, fallback behavior, human review, eval strategy, and launch criteria."
   Expected output: `agent PRD`
4. "Review this agent design before launch and tell me the top trust, fallback, and evaluation risks."
   Expected output: `launch review`
5. "I do not have product context written yet. Ask me the minimum questions needed and update `my-product/PRODUCT_CONTEXT.md`."
   Expected output: `product context update`
6. "Here is the agent I want. Decide whether it should be single-agent or multi-agent, define the needed tools, and write the production-ready instruction set."
   Expected output: `agent instruction pack`

## When Not To Use This Skill

Do not use this skill as the primary tool when:

- the task is SDK setup, framework integration, or code implementation
- the task is low-level model research, training, or fine-tuning strategy
- the request is broad ideation with no product context or blocked decision
- the feature is non-AI or mostly deterministic
- the user needs an engineering tutorial more than a product decision

## Read first

- `references/skill-guide.md`
- `references/product-context-workflow.md`
- `references/module-map.md` when routing across modules is unclear
- `references/playbook/my-product/qa-reference.md` when product context is missing, thin, or stale

## Load modules as needed

Use these bundled playbook areas together when the task requires it. Start from agent system design by default unless the user is clearly doing a different primary task.

- agent system design: `references/playbook/04-ai-agent-system-design/`
- model strategy: `references/playbook/03-model-strategy/`
- evaluation design: `references/playbook/02-evaluation-design/`
- prompt engineering: `references/playbook/06-prompt-engineering-for-pms/`
- AI UX: `references/playbook/07-ai-ux-patterns/`
- PRD writing: `references/playbook/01-ai-prd-writing/` for agent scope, fallback behavior, human review, launch criteria, and edge cases
- team operations: `references/playbook/05-ai-team-operations/`
- appendix: `references/playbook/appendix/`

## Default workflow

1. Identify the real product problem and the concrete deliverable or blocked decision.
2. Look in the current workspace for `my-product/PRODUCT_CONTEXT.md` first. If it exists, read it and use it as default product context.
3. If `my-product/PRODUCT_CONTEXT.md` does not exist, check whether the user has another clearly named local product-context file in the workspace and use it if appropriate.
4. If the context file is missing or too thin for a serious recommendation, use `references/playbook/my-product/qa-reference.md` to ask targeted questions about product UX, users, data, tools, constraints, and AI priorities.
5. If no local product context file exists, fall back to `references/playbook/my-product/PRODUCT_CONTEXT.template.md`, use the QA reference to collect missing inputs, and create `my-product/PRODUCT_CONTEXT.md`.
6. Only ask the user to paste the full product context manually when file access is not available or the context lives outside the current workspace.
7. If the user provides fresh product information or asks to update product context, treat that as an edit request for `my-product/PRODUCT_CONTEXT.md`.
8. When updating product context, merge the new information into the right sections, preserve useful existing details, and normalize the content into the template structure instead of dumping raw notes.
9. If the context file does not exist yet and the user provides product details, create `my-product/PRODUCT_CONTEXT.md` from the bundled template and fill it with the provided information.
10. Default to `references/playbook/04-ai-agent-system-design/` when the task involves orchestration, tool use, routing, or multi-step AI behavior.
11. When the user asks for an agent instruction, first decide whether the workflow should stay bounded as a single agent or split into multiple agents, even if the user already has a preferred architecture in mind.
12. Use `references/playbook/04-ai-agent-system-design/frameworks/agent-instruction-pack.md` when the output should be a production-ready single-agent or multi-agent instruction set.
13. Define tool boundaries before writing the instruction text: what tools exist, who may call them, what each tool is for, and which actions need validation, approval, or escalation.
14. Pull in prompt engineering when the main challenge is writing stable behavior contracts, but keep architecture and tool-boundary decisions primary.
15. Pull in PRD writing only when the agent design needs clearer task boundaries, fallback behavior, human review rules, rollout logic, or launch criteria.
16. Treat eval, prompts, model strategy, orchestration, UX, and rollout decisions as connected when they are connected in the user’s actual workflow.
17. Produce a concrete output: a draft architecture memo, agent PRD, agent instruction pack, eval plan, launch review, fallback design, system recommendation, or prioritized next-step plan.
18. Keep guidance practical, opinionated, and PM-oriented.

## Working rules

- Treat a workspace-local `my-product/PRODUCT_CONTEXT.md` as the preferred context source in Codex.
- Use manual copy-paste instructions only as the fallback path for non-file-aware LLM workflows.
- If the user says new product facts out loud in chat and wants them remembered, update `my-product/PRODUCT_CONTEXT.md` directly.
- Preserve the structured template and rewrite terse notes into clean, durable context.
- Ask a follow-up question only when the user’s update is too ambiguous to place safely.
- Start from agent design, then pull in adjacent modules only where they sharpen the decision.
- If the user asks for an agent instruction or system prompt, do not jump straight to text generation; first decide the architecture, jobs, and tool boundaries.
- If the user asks for a multi-agent workflow, challenge whether specialization, context isolation, tool separation, or failure isolation actually justify it.
- For multi-agent outputs, produce shared rules plus agent-specific instructions with explicit handoff and final-answer ownership.
- Treat PRD material as support for task boundary and launch quality, not as the default frame for every request.
- Do not keep modules artificially separate if the task clearly crosses boundaries.
- Prefer the relevant section `SKILL.md`, template, and one or two frameworks over bulk-loading everything at once.
- Use bundled references as working input, not as a substitute for actually helping the user.
- Prefer delivering the answer over telling the user which files to browse.
- Do not default to “open this doc” or “read that section” when you can extract and apply the content directly.
- Do not drift into engineering tutorials unless the user explicitly asks.
