# Codex Skills

This repo includes self-contained Codex skills under [`skills/`](./).

These are installer-friendly wrappers around the playbook content, packaged so a Codex skill installer can copy a single skill directory from GitHub and still have the referenced material it needs.

## Available Skills

| Skill path | What it covers |
| --- | --- |
| [`skills/ai-pm-playbook`](./ai-pm-playbook/) | Router skill for choosing the right AI PM playbook section |
| [`skills/ai-pm-prd-writing`](./ai-pm-prd-writing/) | AI PRDs, launch gates, fallback behavior, and edge cases |
| [`skills/ai-pm-evaluation-design`](./ai-pm-evaluation-design/) | Rubrics, eval sets, grader workflows, and error analysis |
| [`skills/ai-pm-model-strategy`](./ai-pm-model-strategy/) | Prompt-first vs buy vs custom, routing, and tradeoffs |
| [`skills/ai-pm-agent-system-design`](./ai-pm-agent-system-design/) | Single vs multi-agent, tools, guardrails, and observability |
| [`skills/ai-pm-team-operations`](./ai-pm-team-operations/) | Mission cadence, DACI, rituals, adoption, and stakeholder updates |
| [`skills/ai-pm-prompt-engineering`](./ai-pm-prompt-engineering/) | Prompt specs, review, versioning, and debugging |
| [`skills/ai-pm-ux-patterns`](./ai-pm-ux-patterns/) | Latency UX, confidence, fallbacks, control, and personalization |

## Install From GitHub

If you already have Codex and its skill installer available locally, install one skill at a time from this repo.

Example:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo ArslanArda/ai-pm-playbook \
  --path skills/ai-pm-prd-writing
```

Or install multiple related skills together:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo ArslanArda/ai-pm-playbook \
  --path skills/ai-pm-playbook skills/ai-pm-prd-writing skills/ai-pm-evaluation-design
```

After installation, restart Codex if the skills do not appear immediately.

## Design Notes

- Each skill is self-contained.
- The wrapper `SKILL.md` is intentionally concise for good triggering and context hygiene.
- The original playbook section content is bundled under each skill’s `references/` directory.
- The top-level playbook folders remain the primary authoring source. The `skills/` copies are for Codex distribution.
