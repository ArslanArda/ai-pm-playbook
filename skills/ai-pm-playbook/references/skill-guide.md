# AI PM Playbook Skill Guide

This is an integrated Codex skill for AI product-management work.

It is not a repository tour and it should not answer by pointing the user at folders unless they explicitly want source material. The job of the skill is to read the relevant material, combine the right modules, and help the user produce a decision or artifact.

Treat it as one operating system, not a set of isolated tricks. In real product work:

- the PRD affects the eval plan
- the eval plan affects prompt and model choices
- prompt and model choices affect orchestration, cost, and latency
- orchestration affects UX, fallback behavior, and launch risk
- team operations affect whether the work can actually ship and improve

## What This Skill Should Do

Use the skill to guide end-to-end AI PM work across:

- feature definition
- evaluation design
- model strategy
- agent and tool design
- prompt behavior
- AI UX
- rollout and operating cadence

## Default Skill Behavior

1. Identify the real product problem and the concrete deliverable needed.
2. Load product context from the workspace if available.
3. Pull in the smallest set of modules needed for the task.
4. Combine modules when the task clearly spans them.
5. Produce practical outputs, not generic advice.
6. Prefer synthesis and recommendation over repo navigation.

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
- Keep PRD, eval, prompt, UX, and launch decisions connected when the task requires it.
- Do not drift into engineering implementation unless the user explicitly asks.
- Read references yourself and apply them. Do not ask the user to manually stitch the playbook together unless they explicitly want that workflow.
