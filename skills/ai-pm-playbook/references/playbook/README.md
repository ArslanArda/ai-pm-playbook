# AI PM Playbook

> A practical playbook for product managers building AI-native products.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-blue.svg)](./CONTRIBUTING.md)
[![GitHub stars](https://img.shields.io/badge/stars-welcome-black.svg)](#)

AI engineering is flooded with code samples, benchmark charts, framework tutorials, and hot takes. AI product management is not. Most PMs shipping AI features still have to invent their own operating system from scratch: how to write an AI PRD, how to define evaluation criteria, how to choose a model strategy, how to scope an agent system, how to explain quality tradeoffs to leadership, and how to design fallback behavior when the model is uncertain.

This repository exists to close that gap. It is a practical, opinionated, open-source playbook for PMs building AI-native products in the real world. The content is based on production-style product work: ambiguous user intent, budget constraints, latency budgets, unreliable outputs, stakeholder pressure, and the constant need to make defensible tradeoffs quickly.

This is not a coding repo. You will not find SDK walkthroughs, sample apps, or model-integration code here. You will find reusable PM frameworks, decision guides, checklists, templates, realistic examples, and `SKILL.md` files designed to work directly with any modern LLM assistant.

## Who This Is For

This playbook is for:

- Product managers shipping AI features into existing products
- AI product leads building the operating system for AI delivery
- Founders building AI-native products and making product/model tradeoffs themselves
- PMs transitioning from traditional SaaS or marketplace work into AI-heavy roles

If you are deciding what to build, how to scope it, how to evaluate it, how to explain it, and how to improve it after launch, this repo is for you.

## What Makes This Different

- **Based on production experience, not theory.** The frameworks assume you have real users, real constraints, and real pressure to ship.
- **AI-consumable by design.** Every major section includes a `SKILL.md` file you can paste into ChatGPT, Claude, Gemini, or another LLM to get guided through the process.
- **Personalized to your product.** Fill out [`my-product/PRODUCT_CONTEXT.template.md`](./my-product/PRODUCT_CONTEXT.template.md), save it as `PRODUCT_CONTEXT.md`, and your conversations become materially more useful. In Codex, the integrated skill can read that file directly from the workspace.
- **Opinionated, not vague.** The playbook makes recommendations and explains when to deviate.
- **No code.** This is pure product thinking: markdown, templates, diagrams, checklists, and examples.

## Quick Start

1. Fork this repository.
2. Copy [`my-product/PRODUCT_CONTEXT.template.md`](./my-product/PRODUCT_CONTEXT.template.md) to `my-product/PRODUCT_CONTEXT.md` and fill in your product context.
3. Use the repo in the way that fits your environment:
   - in Codex, keep `my-product/PRODUCT_CONTEXT.md` in the workspace and let the integrated skill read it directly
   - in generic LLM chat tools, paste the relevant `SKILL.md` together with `my-product/PRODUCT_CONTEXT.md`

If you only have 15 minutes, start with:

- [`00-how-to-use/README.md`](./00-how-to-use/README.md)
- [`my-product/README.md`](./my-product/README.md)
- [`01-ai-prd-writing/SKILL.md`](./01-ai-prd-writing/SKILL.md)

## Use With Codex Skills

This repo now also includes a self-contained Codex skill under [`skills/`](./skills/).

That means you can use the playbook in two ways:

- as a normal GitHub-readable playbook
- as one installable Codex skill that wraps the full playbook content

The installable skill lives here:

- [`skills/ai-pm-playbook`](./skills/ai-pm-playbook/)

See [`skills/README.md`](./skills/README.md) for installation examples.

When used inside Codex, the skill is designed to look for `my-product/PRODUCT_CONTEXT.md` in the active workspace before asking for manual context input.

## Playbook Sections

| Section | What it covers |
| --- | --- |
| [`00-how-to-use`](./00-how-to-use/README.md) | How to navigate the repo, personalize it, and use `SKILL.md` files with an LLM assistant |
| [`01-ai-prd-writing`](./01-ai-prd-writing/README.md) | How to write AI PRDs that specify behavior, evals, fallback logic, and failure handling |
| [`02-evaluation-design`](./02-evaluation-design/README.md) | How to design evaluation systems for AI outputs, graders, datasets, and error analysis |
| [`03-model-strategy`](./03-model-strategy/README.md) | Model selection, routing, and cost-latency-quality tradeoffs as product decisions |
| [`04-ai-agent-system-design`](./04-ai-agent-system-design/README.md) | Agent architecture decisions from a PM perspective: orchestration, tools, guardrails, and failure modes |
| [`05-ai-team-operations`](./05-ai-team-operations/README.md) | How AI-native teams run missions, rituals, decision rights, and stakeholder communication |
| [`06-prompt-engineering-for-pms`](./06-prompt-engineering-for-pms/README.md) | Prompt work as product specification, with iteration, testing, versioning, and debugging frameworks |
| [`07-ai-ux-patterns`](./07-ai-ux-patterns/README.md) | UX patterns specific to AI features: latency, fallbacks, confidence, conversational interfaces, and personalization |
| [`appendix`](./appendix/glossary.md) | Glossary, reading list, and tool landscape for AI PMs |

## How To Use This Playbook

There are three practical ways to use the repo:

### 1. Browse it on GitHub

Use the section READMEs, frameworks, templates, and examples as reference material while you work. This is the fastest path if you already know what problem you are solving and need sharper thinking or a reusable artifact.

### 2. Use it with your AI assistant

This is the mode the repo is optimized for.

Start by filling out your product context in `my-product/PRODUCT_CONTEXT.md`. Then open any `SKILL.md` file and paste both documents into a chat with your preferred LLM. Ask the model to guide you through the process for your team, your feature, and your constraints.

The structure is deliberate. Each `SKILL.md` tells the model:

- when the skill should be used
- what prerequisites to gather
- which questions to ask you
- what output to produce at each step
- how to make the core decision
- how to self-review the result
- what anti-patterns to avoid

That means the file is not just documentation. It is a reusable operating prompt for PM work.

### 3. Fork it and adapt it for your team

You can use the repo as the baseline for your internal AI PM playbook. Add your own examples, replace generic templates with your operating formats, and tailor the frameworks to your compliance, budget, and organizational constraints.

## Why This Matters

AI product work breaks many default PM habits.

In a traditional feature, the specification usually defines deterministic behavior. In an AI feature, the spec has to define acceptable ranges of behavior, evaluation criteria, fallback logic, escalation paths, and the boundary between “smart enough to ship” and “too risky to expose.” The PM is not just deciding what screen to build. The PM is deciding what uncertainty is acceptable, what failure modes are tolerable, and what tradeoff is worth making.

That is why the repo is intentionally opinionated. A vague AI strategy is not a strategy. “We’ll test a few prompts and see” is not an operating model. “We need higher accuracy” is not a useful direction unless you specify for whom, on which tasks, at what latency, at what cost, and with what fallback behavior.

This playbook helps you turn those blurry instincts into concrete product decisions.

## Contributing

Contributions are welcome. Read [`CONTRIBUTING.md`](./CONTRIBUTING.md) before opening a PR. The short version:

- add substance, not filler
- keep the repo tool-agnostic and code-free
- favor decision frameworks over generic advice
- use realistic examples with actual constraints and tradeoffs
- preserve the section structure and `SKILL.md` format

## About The Author

This playbook is written from the perspective of an AI Product Manager with 5+ years of product experience and current hands-on work leading AI initiatives at a large real estate platform. The underlying experience includes shipping conversational search, computer vision features, voice agents, content generation systems, and multi-agent workflows in production-like environments where latency, cost, trust, and adoption all mattered.

If you use the playbook and improve it for your own team, contribute back. The repo gets better when more PMs add what actually worked.
