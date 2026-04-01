---
name: ai-pm-playbook
description: Use when the user needs end-to-end AI product-management help across PRDs, evals, model strategy, agent design, prompts, UX, and team operations, especially when those decisions need to stay aligned in one workflow.
---

# AI PM Playbook

Use this as one integrated Codex skill for AI PM work.

This skill is intentionally broad because the underlying playbook is one operating system, not a set of isolated techniques. In real AI product work, PRD decisions affect eval design, prompt structure, routing, UX, and launch operations. Use this skill when those things need to work in sync.

Do not treat this skill like a document index or a repo tour. Read the needed references yourself, synthesize the answer, and help the user produce a concrete artifact, recommendation, or next-step plan.

## Read first

- `references/skill-guide.md`
- `references/product-context-workflow.md`
- `references/module-map.md` when routing across modules is unclear

## Load modules as needed

Use these bundled playbook areas together when the task requires it:

- PRD writing: `references/playbook/01-ai-prd-writing/`
- evaluation design: `references/playbook/02-evaluation-design/`
- model strategy: `references/playbook/03-model-strategy/`
- agent system design: `references/playbook/04-ai-agent-system-design/`
- team operations: `references/playbook/05-ai-team-operations/`
- prompt engineering: `references/playbook/06-prompt-engineering-for-pms/`
- AI UX: `references/playbook/07-ai-ux-patterns/`
- appendix: `references/playbook/appendix/`

## Default workflow

1. Identify the real product problem and the concrete deliverable or blocked decision.
2. Look in the current workspace for `my-product/PRODUCT_CONTEXT.md` first. If it exists, read it and use it as default product context.
3. If `my-product/PRODUCT_CONTEXT.md` does not exist, check whether the user has another clearly named local product-context file in the workspace and use it if appropriate.
4. If no local product context file exists, fall back to `references/playbook/my-product/PRODUCT_CONTEXT.template.md` and ask the user to create or provide the missing context.
5. Only ask the user to paste the full product context manually when file access is not available or the context lives outside the current workspace.
6. Start from the closest primary module, but pull in adjacent modules when the task spans them.
7. Treat PRD, eval, prompts, model strategy, orchestration, UX, and rollout decisions as connected when they are connected in the user’s actual workflow.
8. Produce a concrete output: a draft artifact, a recommendation with rationale, a decision framework, or a prioritized next-step plan.
9. Keep guidance practical, opinionated, and PM-oriented.

## Working rules

- Treat a workspace-local `my-product/PRODUCT_CONTEXT.md` as the preferred context source in Codex.
- Use manual copy-paste instructions only as the fallback path for non-file-aware LLM workflows.
- Do not keep modules artificially separate if the task clearly crosses boundaries.
- Prefer the relevant section `SKILL.md`, template, and one or two frameworks over bulk-loading everything at once.
- Use bundled references as working input, not as a substitute for actually helping the user.
- Prefer delivering the answer over telling the user which files to browse.
- Do not default to “open this doc” or “read that section” when you can extract and apply the content directly.
- Do not drift into engineering tutorials unless the user explicitly asks.
