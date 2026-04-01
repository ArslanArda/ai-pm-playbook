# Codex Skills

This repo ships one public, self-contained Codex skill:

- [`skills/ai-pm-playbook`](./ai-pm-playbook/)

The design is intentional. The playbook is one integrated operating system for AI PM work, not a set of independent tactics. PRD writing, eval design, model strategy, prompts, agent design, UX, and team operations often need to be handled together in one workflow.

So the public skill package exposes one primary skill and bundles the full playbook inside its `references/` directory.

When this skill is used inside a workspace that contains `my-product/PRODUCT_CONTEXT.md`, Codex should read that file directly and use it as the default product context. Manual copy-paste remains the fallback for plain chat environments without file access.

## Install From GitHub

If you already have Codex and its skill installer available locally, install the single integrated skill from this repo.

Example:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo ArslanArda/ai-pm-playbook \
  --path skills/ai-pm-playbook
```

After installation, restart Codex if the skills do not appear immediately.

## Design Notes

- The wrapper `SKILL.md` is intentionally concise for good triggering and context hygiene.
- The full playbook is bundled under `skills/ai-pm-playbook/references/playbook/`.
- The top-level playbook folders remain the primary authoring source. The bundled skill references are the distribution copy.
