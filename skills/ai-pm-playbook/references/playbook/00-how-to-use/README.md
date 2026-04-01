# How To Run The Playbook As A Skill

This reference explains how to operate the bundled playbook inside Codex.

The goal is not to browse documentation. The goal is to use the playbook as a working method that turns ambiguous AI PM questions into concrete outputs.

## The Core Idea

Most AI PM work is not blocked by lack of opinions. It is blocked by messy context.

You usually already know the broad questions:

- What should we build?
- Which model should we use?
- How should we evaluate it?
- When is a multi-agent system actually justified?
- What should users see when the model is uncertain?

The hard part is answering those questions for your specific product, team, data, and constraints. That is why each major section in the playbook has a `SKILL.md`. These files are structured so Codex can use them to guide the process step by step.

## Recommended Workflow

### 1. Load product context first

Read [`../my-product/README.md`](../my-product/README.md), then use `PRODUCT_CONTEXT.md` if it exists locally.

If the file does not exist yet, create it from `PRODUCT_CONTEXT.template.md` and fill in your:

- product overview
- user personas
- current flows and pain points
- AI maturity and team setup
- relevant constraints such as latency, privacy, and budget

Inside Codex, keep `my-product/PRODUCT_CONTEXT.md` in the workspace and let the skill read it directly. Manual paste is the fallback path for non-file-aware chat environments.

### 2. Pick the module that matches your current problem

Examples:

- writing a new AI feature spec: [`../01-ai-prd-writing/`](../01-ai-prd-writing/README.md)
- deciding how to evaluate outputs: [`../02-evaluation-design/`](../02-evaluation-design/README.md)
- choosing model strategy or routing: [`../03-model-strategy/`](../03-model-strategy/README.md)
- scoping an agent system: [`../04-ai-agent-system-design/`](../04-ai-agent-system-design/README.md)
- improving AI team operating rhythm: [`../05-ai-team-operations/`](../05-ai-team-operations/README.md)
- tightening prompt process: [`../06-prompt-engineering-for-pms/`](../06-prompt-engineering-for-pms/README.md)
- designing a better AI UX: [`../07-ai-ux-patterns/`](../07-ai-ux-patterns/README.md)

### 3. Use the section README only when orientation is needed

Use the README if you need the conceptual overview, the opinionated point of view, or the map of supporting framework files. Do not default to sending users away to browse docs when the skill can synthesize the content directly.

### 4. Use the `SKILL.md` for actual work

Use the section `SKILL.md` as the primary operating reference for the current job. The skill should read it, follow its structure, ask the necessary questions, and help produce a concrete output such as a PRD, evaluation plan, model strategy, or UX decision.

Inside Codex, the better workflow is:

- keep `my-product/PRODUCT_CONTEXT.md` in the workspace
- let the installed `ai-pm-playbook` skill read it from disk automatically
- pull in only the supporting module files that add signal
- use manual paste only if file access is unavailable

### 5. Pull in supporting files only when they add signal

The playbook is layered on purpose:

- `README.md`: what the topic is and how to think about it
- `SKILL.md`: guided workflow
- `frameworks/`: focused deep dives on specific decisions
- `templates/`: blank artifacts you can fill out
- `examples/`: realistic scenarios showing how the framework plays out in practice

If the work gets stuck, load one of the relevant framework or example files into context.

## What Good Usage Looks Like

Strong usage patterns:

- you load your product context
- you ask for a concrete deliverable
- you answer the skill’s questions with specific constraints
- you force a recommendation instead of settling for generic option lists
- you pressure-test the output with anti-patterns and quality checks

Weak usage patterns:

- you use the skill without product context
- you ask for “ideas” without naming a decision or artifact
- you accept generic output without pressure-testing it
- you treat the first draft as final

## How Deep To Go

Use the playbook in a layered way:

- If you need a fast answer in 10 minutes, use the `TL;DR`, the decision framework, and the checklist.
- If you are kicking off serious work, use the full `SKILL.md`.
- If you are preparing a team artifact, also use the related framework files and templates.
- If you are onboarding someone new, use the overview, one section README, and one example file first.

## A Practical Example

Say you are building conversational search for a marketplace.

1. Load `my-product/PRODUCT_CONTEXT.md`.
2. Use [`../01-ai-prd-writing/SKILL.md`](../01-ai-prd-writing/SKILL.md) as the primary working module.
3. Draft the AI PRD for conversational search step by step.
4. Pull in the example PRD from [`../01-ai-prd-writing/examples/conversational-search.md`](../01-ai-prd-writing/examples/conversational-search.md) if you need a realistic reference.
5. When the PRD starts getting specific about evals, load [`../02-evaluation-design/`](../02-evaluation-design/README.md).
6. When agent complexity appears, load [`../04-ai-agent-system-design/`](../04-ai-agent-system-design/README.md).

In practice, good AI PM work crosses sections. The playbook is modular so you can combine them without re-learning the whole system.
