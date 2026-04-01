# How To Use This Playbook

This repository is designed to work in two modes at the same time:

- as a public reference you can browse on GitHub
- as a practical operating system you can use inside an LLM conversation

If you only read the markdown files, the repo should still be useful. But the highest-leverage workflow is different: personalize your product context once, then use the section `SKILL.md` files as guided working sessions with your AI assistant.

## The Core Idea

Most AI PM work is not blocked by lack of opinions. It is blocked by messy context.

You already know the broad questions:

- What should we build?
- Which model should we use?
- How should we evaluate it?
- When is a multi-agent system actually justified?
- What should users see when the model is uncertain?

The hard part is answering those questions for your specific product, team, data, and constraints. That is why each major section in this repo has a `SKILL.md`. These files are not just summaries. They are structured so an LLM can use them to guide you through the process step by step.

## The Recommended Workflow

### 1. Personalize the repo

Go to [`../my-product/`](../my-product/README.md).

Copy `PRODUCT_CONTEXT.template.md` to `PRODUCT_CONTEXT.md`, then fill in your:

- product overview
- user personas
- current flows and pain points
- AI maturity and team setup
- relevant constraints such as latency, privacy, and budget

If you only do one setup step in the whole repo, do this one.

If you are using Codex inside this repo, keep `my-product/PRODUCT_CONTEXT.md` in the workspace and let Codex read it directly. The manual paste workflow is mainly for generic LLM chats that cannot access local files.

If you have fresh product information later, you should also be able to type it in chat and ask Codex to merge it into `my-product/PRODUCT_CONTEXT.md` instead of manually rewriting the file each time.

### 2. Pick the section that matches your current problem

Examples:

- writing a new AI feature spec: [`../01-ai-prd-writing/`](../01-ai-prd-writing/README.md)
- deciding how to evaluate outputs: [`../02-evaluation-design/`](../02-evaluation-design/README.md)
- choosing model strategy or routing: [`../03-model-strategy/`](../03-model-strategy/README.md)
- scoping an agent system: [`../04-ai-agent-system-design/`](../04-ai-agent-system-design/README.md)
- improving AI team operating rhythm: [`../05-ai-team-operations/`](../05-ai-team-operations/README.md)
- tightening prompt process: [`../06-prompt-engineering-for-pms/`](../06-prompt-engineering-for-pms/README.md)
- designing a better AI UX: [`../07-ai-ux-patterns/`](../07-ai-ux-patterns/README.md)

### 3. Use the section README for orientation

Start with the README if you want the conceptual overview, the opinionated point of view, and the map of supporting framework files.

### 4. Use the `SKILL.md` for actual work

Open the section’s `SKILL.md`, then paste the full file into your LLM together with your `PRODUCT_CONTEXT.md`.

Your prompt can be simple:

> “Use this product context and this skill to guide me through the process for my feature.”

The LLM should then ask you the right questions, pressure-test your assumptions, and help you produce a concrete output such as a PRD, evaluation plan, model strategy, or UX decision.

For Codex specifically, the better workflow is:

- keep `my-product/PRODUCT_CONTEXT.md` in the repo
- let the installed `ai-pm-playbook` skill read it from disk automatically
- if priorities, constraints, or market context changes, ask Codex to update `my-product/PRODUCT_CONTEXT.md`
- only paste the file manually if you are working in a plain chat environment without file access

### 5. Pull in frameworks, templates, and examples as needed

The repo is layered on purpose:

- `README.md`: what the topic is and how to think about it
- `SKILL.md`: guided workflow
- `frameworks/`: focused deep dives on specific decisions
- `templates/`: blank artifacts you can fill out
- `examples/`: realistic scenarios showing how the framework plays out in practice

If your conversation gets stuck, add one of the relevant framework or example files to the LLM chat.

## How To Work With `SKILL.md` Files

Every `SKILL.md` follows the same pattern:

- `TL;DR`
- `When to Use This`
- `Prerequisites`
- `Step-by-Step Process`
- `Decision Framework`
- `Quality Checklist`
- `Anti-Patterns`
- `Adaptation Guide`

That structure is deliberate. It helps in three ways.

First, it keeps the content self-contained. You should not need to read five other files before using the skill.

Second, it gives the LLM a clear operating structure. Instead of free-form advice, the model has a workflow to follow.

Third, it gives you a clear review standard. The checklist and anti-patterns make it easier to spot shallow output before it causes downstream problems.

## What Good Usage Looks Like

Strong usage patterns:

- you include your product context
- you update the product context when important facts change
- you ask for a concrete deliverable
- you answer the model’s questions with specific constraints
- you push the model to recommend, not just brainstorm
- you ask it to show tradeoffs and failure modes

Weak usage patterns:

- you paste only the skill without context
- you keep fresh context only in one chat and never merge it into the product context file
- you ask for “ideas” without saying what problem matters
- you accept generic output without pressure-testing it
- you treat the model’s first draft as final

## Suggested Prompt Patterns

Use prompts like:

- “Guide me through this skill one step at a time. Ask only the questions you need to tailor the output.”
- “Challenge weak assumptions and give me a recommendation with rationale.”
- “Use the quality checklist at the end to review the output.”
- “Show me red flags and anti-patterns before we finalize.”

Avoid prompts like:

- “Give me a complete strategy” without context
- “What do you think about AI for my product?” without a decision to make
- “Write something good” without evaluation criteria

## How Deep To Go

Use the repo in a layered way:

- If you need a fast answer in 10 minutes, use the `TL;DR`, the decision framework, and the checklist.
- If you are kicking off serious work, use the full `SKILL.md`.
- If you are preparing a team artifact, also use the related framework files and templates.
- If you are onboarding someone new, point them to the README and one example file first.

## A Practical Example

Say you are building conversational search for a marketplace.

You would:

1. Fill out `my-product/PRODUCT_CONTEXT.md`.
2. Open [`../01-ai-prd-writing/SKILL.md`](../01-ai-prd-writing/SKILL.md).
3. Ask the LLM to guide you through an AI PRD for conversational search.
4. Pull in the example PRD from [`../01-ai-prd-writing/examples/conversational-search.md`](../01-ai-prd-writing/examples/conversational-search.md) if you want a realistic reference.
5. When the PRD starts getting specific about evals, open [`../02-evaluation-design/`](../02-evaluation-design/README.md).
6. When agent complexity appears, pull in [`../04-ai-agent-system-design/`](../04-ai-agent-system-design/README.md).

If your priorities or market constraints change midstream, update `my-product/PRODUCT_CONTEXT.md` before continuing so the next recommendations reflect the new reality.

In practice, good AI PM work crosses sections. The repo is modular so you can combine them without re-learning the whole system.

## Final Advice

Use the playbook to sharpen decisions, not to outsource judgment.

The best outcomes come when you treat the LLM as a demanding chief of staff: it should ask better questions, reveal hidden tradeoffs, and help you produce tighter artifacts faster. It should not replace your accountability for the product decisions themselves.

If you use the repo that way, it becomes much more than documentation. It becomes a repeatable working method.
