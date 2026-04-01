---
name: ai-pm-playbook
description: Use when the user wants practical product-management guidance for AI-native products across PRDs, evals, model strategy, agent design, prompts, UX, and team operations as one integrated workflow.
---

# AI PM Playbook

Use this as the integrated skill for the AI PM Playbook.

This skill is intentionally broad because the underlying playbook is one operating system, not a set of isolated techniques. In real AI product work, PRD decisions affect eval design, prompt structure, routing, UX, and launch operations. Use this skill when those things need to work in sync.

## Read first

- `references/playbook/README.md`
- `references/playbook/00-how-to-use/README.md`
- `references/playbook/00-how-to-use/SKILL.md`

Personalization references:

- `references/playbook/my-product/README.md`
- `references/playbook/my-product/PRODUCT_CONTEXT.template.md`

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

1. Identify the real product problem and the concrete deliverable needed.
2. Look in the current workspace for `my-product/PRODUCT_CONTEXT.md` first. If it exists, read it and use it as default product context.
3. If `my-product/PRODUCT_CONTEXT.md` does not exist, check whether the user has another clearly named local product-context file in the workspace and use it if appropriate.
4. If no local product context file exists, fall back to `references/playbook/my-product/PRODUCT_CONTEXT.template.md` and ask the user to create or provide the missing context.
5. Only ask the user to paste the full product context manually when file access is not available or the context lives outside the current workspace.
6. Start from the closest primary module, but pull in adjacent modules when the task spans them.
7. Treat PRD, eval, prompts, model strategy, orchestration, UX, and rollout decisions as connected when they are connected in the user’s actual workflow.
8. Keep guidance practical, opinionated, and PM-oriented.

## Working rules

- Treat a workspace-local `my-product/PRODUCT_CONTEXT.md` as the preferred context source in Codex.
- Use manual copy-paste instructions only as the fallback path for non-file-aware LLM workflows.
- Do not keep modules artificially separate if the task clearly crosses boundaries.
- Prefer the relevant section `SKILL.md`, template, and one or two frameworks over bulk-loading everything at once.
- Do not drift into engineering tutorials unless the user explicitly asks.
