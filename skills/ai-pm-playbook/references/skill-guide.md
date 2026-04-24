# AI PM Playbook Skill Guide

This is an agent-centered Codex skill for AI product-management work.

Short version: it is a PM judgment system for AI agents, not a general AI build guide.

It is not a repository tour and it should not answer by pointing the user at folders unless they explicitly want source material. The job of the skill is to read the relevant material, combine the right modules, and help the user produce a decision or artifact.

Treat it as one operating system, not a set of isolated tricks. The primary lens is agent and tool design, but the surrounding PM decisions still matter. In real product work:

- the PRD affects the eval plan
- the eval plan affects prompt and model choices
- prompt and model choices affect orchestration, cost, and latency
- orchestration affects UX, fallback behavior, and launch risk
- team operations affect whether the work can actually ship and improve

## What This Skill Should Do

Use the skill to guide end-to-end AI PM work across:

- agent and tool design
- evaluation design
- model strategy
- prompt behavior
- AI UX
- scoped product requirements for agent behavior
- rollout and operating cadence

Preferred artifacts:

- architecture memo
- agent PRD
- agent instruction pack
- eval plan
- launch review
- fallback design

## Default Skill Behavior

1. Identify the real product problem and the concrete deliverable needed.
2. Load product context from the workspace if available.
3. If product context is missing or weak, use `references/playbook/my-product/qa-reference.md` to gather the minimum useful context before making strong recommendations.
4. Start from agent system design by default when the task involves orchestration, tool use, or multi-step AI behavior.
5. If the user asks for an agent instruction or prompt, decide first whether the workflow should be single-agent or multi-agent instead of taking the requested architecture for granted.
6. Define tool boundaries and caller-specific tool rules before writing the instruction text.
7. Pull in the smallest supporting set of modules needed for the task.
8. Use PRD material only when it sharpens task boundary, fallback behavior, review rules, edge cases, or launch gates.
9. Combine modules when the task clearly spans them.
10. Produce practical outputs, not generic advice.
11. Prefer synthesis and recommendation over repo navigation.
12. If the user provides new product facts and wants them remembered, update the local product context file as part of the workflow.

## When Not To Use

This skill is usually the wrong primary tool when the task is:

- SDK or framework implementation
- low-level model training or fine-tuning research
- broad ideation with no concrete product decision
- non-AI product work

## Product Context Rule

Inside Codex, a local `my-product/PRODUCT_CONTEXT.md` file is the preferred source of truth.

Use this order:

1. `my-product/PRODUCT_CONTEXT.md` in the current workspace
2. another clearly named local product context file if one exists
3. `references/playbook/my-product/PRODUCT_CONTEXT.template.md` if the file does not exist yet
4. manual paste only when file access is unavailable

## Working Style

- Be opinionated, but explain tradeoffs.
- Favor reusable artifacts over abstract brainstorming.
- Keep agent design, eval, prompt, UX, and launch decisions connected when the task requires it.
- Treat agent instructions as decision-backed behavior contracts, not isolated prompt-writing exercises.
- Use PRD thinking to tighten agent scope and quality bars, not to drift into generic product-spec writing.
- Do not drift into engineering implementation unless the user explicitly asks.
- Read references yourself and apply them. Do not ask the user to manually stitch the playbook together unless they explicitly want that workflow.
- When product context changes, keep the local context file current so later tasks benefit automatically.
