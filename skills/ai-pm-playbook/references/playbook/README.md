# AI PM Playbook

> A practical operating system for product managers shipping AI features.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-blue.svg)](./CONTRIBUTING.md)
[![GitHub stars](https://img.shields.io/badge/stars-welcome-black.svg)](#)

There is no shortage of AI engineering content. There is still a shortage of AI product judgment.

Most PMs shipping AI features are not blocked by model access. They are blocked by questions like:

- What exactly is the AI responsible for versus the product?
- What quality bar is good enough for launch?
- When should the system ask, act, fall back, or disclose uncertainty?
- When is routing worth it?
- What should leadership hear when quality is improving in one segment and regressing in another?

This repository exists for those questions.

It is a practical, opinionated, markdown-only playbook for PMs building AI-native products. No SDK walkthroughs. No framework boilerplate. No “10 trends in AI.” Just product artifacts, decision frameworks, examples, checklists, and AI-consumable `SKILL.md` files built around real production tensions: latency, hallucination risk, weak grounding, cost creep, scope blur, stakeholder pressure, and launch decisions under uncertainty.

## What This Playbook Will Tell You To Do

This repo is not neutral. The defaults are deliberate.

- Start with the product job, not the model.
- Write the fallback path at the same time as the happy path.
- Separate build progress from quality confidence.
- Stay prompt-first longer than most teams do.
- Avoid multi-agent unless a bounded pipeline clearly fails.
- Treat prompts as product behavior, not hidden implementation.
- Do not ship a fluent wrong answer when a plain fallback would protect trust better.

If you disagree with one of those defaults, good. The repo is designed to make the tradeoff explicit, not pretend every path is equally sensible.

## Who This Is For

This playbook is for:

- Product managers shipping AI features into existing products
- AI product leads building the operating system for AI delivery
- Founders making product, model, and launch tradeoffs directly
- PMs moving from traditional SaaS or marketplace work into AI-heavy product areas

If you are deciding what to build, how to scope it, how to evaluate it, how to explain it, and how to improve it after launch, this repo is for you.

## What Makes This Different

- **It treats AI product work as a decision system, not a collection of tricks.** The sections are designed to work together: PRD, evals, prompts, model strategy, UX, and team operations.
- **It is built for real product constraints.** The examples assume ambiguous user intent, weak data, partial grounding, budget limits, and leadership pressure.
- **It is AI-consumable by design.** Every major section has a `SKILL.md` file that can guide a serious working session with an LLM.
- **It is personalized.** Fill out [`my-product/PRODUCT_CONTEXT.template.md`](./my-product/PRODUCT_CONTEXT.template.md), save it as `PRODUCT_CONTEXT.md`, and the playbook becomes materially more useful. In Codex, the integrated skill reads that file directly.
- **It is code-free on purpose.** This repo is about product thinking, not implementation frameworks.

## Start Here

1. Fork this repository.
2. Copy [`my-product/PRODUCT_CONTEXT.template.md`](./my-product/PRODUCT_CONTEXT.template.md) to `my-product/PRODUCT_CONTEXT.md`.
   If you do not know what to write yet, use [`my-product/qa-reference.md`](./my-product/qa-reference.md) and answer the minimum useful questions first.
3. Fill in at least Sections 1-3.
4. Choose the section closest to your current bottleneck.
5. Use the relevant `SKILL.md` with your product context to produce a concrete artifact.

If you only have 15 minutes, start with:

- [`00-how-to-use/README.md`](./00-how-to-use/README.md)
- [`my-product/README.md`](./my-product/README.md)
- [`01-ai-prd-writing/SKILL.md`](./01-ai-prd-writing/SKILL.md)

## A Good First-End-To-End Workflow

If you are planning a new AI feature, the most useful sequence is usually:

1. [`01-ai-prd-writing`](./01-ai-prd-writing/README.md): define the user problem, task boundary, failure modes, fallback behavior, and launch criteria
2. [`02-evaluation-design`](./02-evaluation-design/README.md): define the rubric, eval set, and error taxonomy
3. [`03-model-strategy`](./03-model-strategy/README.md): decide whether prompt-first, routing, or model adaptation is justified
4. [`07-ai-ux-patterns`](./07-ai-ux-patterns/README.md): design how the experience behaves under latency, ambiguity, and failure
5. [`05-ai-team-operations`](./05-ai-team-operations/README.md): run the work with explicit review rituals and launch gates

That is the real thesis of the repo: AI PM work becomes much easier when those decisions stop living in separate conversations.

## Playbook Sections

| Section | What it covers |
| --- | --- |
| [`00-how-to-use`](./00-how-to-use/README.md) | How to run the playbook as a disciplined workflow instead of passive reading |
| [`01-ai-prd-writing`](./01-ai-prd-writing/README.md) | AI PRDs with behavior definition, evals, fallback logic, edge cases, and rollout thinking |
| [`02-evaluation-design`](./02-evaluation-design/README.md) | Rubrics, graders, eval sets, error analysis, and launch-confidence design |
| [`03-model-strategy`](./03-model-strategy/README.md) | Prompt-first vs buy vs build, routing logic, and cost-latency-quality tradeoffs |
| [`04-ai-agent-system-design`](./04-ai-agent-system-design/README.md) | When agent systems are justified, how to bound them, and how to keep them observable |
| [`05-ai-team-operations`](./05-ai-team-operations/README.md) | Mission cycles, DACI, review rituals, adoption, and stakeholder communication |
| [`06-prompt-engineering-for-pms`](./06-prompt-engineering-for-pms/README.md) | Prompt work as product behavior definition, with versioning, review, testing, and debugging |
| [`07-ai-ux-patterns`](./07-ai-ux-patterns/README.md) | Latency UX, low-confidence handling, hybrid interfaces, trust recovery, and personalization |
| [`appendix`](./appendix/glossary.md) | Glossary, reading list, and tool landscape |

## Use It On GitHub Or In Codex

There are two practical modes.

### 1. GitHub-readable playbook

Use the READMEs, frameworks, templates, and examples as reference material while you work.

### 2. Installable Codex skill

This repo also ships as one integrated Codex skill under [`skills/`](./skills/README.md).

That skill is designed to:

- read `my-product/PRODUCT_CONTEXT.md` from the workspace
- route across PRD, eval, model, prompt, UX, and ops modules as needed
- update product context when you give fresh facts in chat
- help produce concrete deliverables instead of only pointing at docs

The installable skill lives here:

- [`skills/ai-pm-playbook`](./skills/ai-pm-playbook/)

## What You Should Expect From This Repo

This repo should help you produce:

- a tighter AI PRD
- a stronger evaluation plan
- a more defensible model decision
- a simpler agent architecture
- a clearer fallback design
- a better operating cadence for AI work

It should not give you false comfort.

If a feature is underspecified, it should make that obvious. If a launch gate is weak, it should make that uncomfortable. If a team is hiding behind demo quality, it should make that visible.

That is the point.

## Flagship Examples

If you want the best sense of the repo’s point of view, start with:

- [`04-ai-agent-system-design/examples/conversational-search-agent.md`](./04-ai-agent-system-design/examples/conversational-search-agent.md)
- [`02-evaluation-design/frameworks/eval-data-strategy.md`](./02-evaluation-design/frameworks/eval-data-strategy.md)
- [`06-prompt-engineering-for-pms/examples/listing-description-agent.md`](./06-prompt-engineering-for-pms/examples/listing-description-agent.md)

These show the style the repo aims for: concrete constraints, product judgment, tradeoffs, and explicit failure handling.

## Contributing

Contributions are welcome. Read [`CONTRIBUTING.md`](./CONTRIBUTING.md) before opening a PR. The short version:

- add substance, not filler
- keep the repo tool-agnostic and code-free
- favor decision frameworks over generic advice
- use realistic examples with constraints and tradeoffs
- preserve the section structure and `SKILL.md` format

## About The Author

This playbook is written from the perspective of an AI Product Manager with 5+ years of product experience and current hands-on work leading AI initiatives at a large real estate platform. The underlying experience includes conversational search, computer vision features, voice agents, content generation systems, and multi-step AI workflows where latency, cost, trust, and adoption all mattered at once.

If you use the playbook and improve it for your own team, contribute back. The best AI PM practices still spread too slowly, and they get better when they are pressure-tested in public.
