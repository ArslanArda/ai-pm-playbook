# Personalize The Playbook

This directory is how you make the playbook relevant to your actual product.

Most generic AI advice fails because it ignores context. The right model strategy for a B2C marketplace is different from the right model strategy for a regulated B2B workflow. The right fallback for an AI-generated listing description is different from the right fallback for a support copilot answering a customer in real time.

That is why this repo includes a product context file. You fill it out once, then use it with any `SKILL.md` file in the repository to get guidance tailored to your product, users, team, constraints, and priorities.

## What This Directory Is For

Use this directory to create a local, private description of your product that you can paste into LLM conversations or let Codex read directly from your workspace.

The committed file is:

- [`PRODUCT_CONTEXT.template.md`](./PRODUCT_CONTEXT.template.md): the blank template with instructions and example depth
- [`qa-reference.md`](./qa-reference.md): a guided question set you can use to interview a team and fill or update the context file

The local file you create is:

- `PRODUCT_CONTEXT.md`: your actual product context, kept local and ignored by Git

## How To Fill In `PRODUCT_CONTEXT.md`

1. Copy `PRODUCT_CONTEXT.template.md` to `PRODUCT_CONTEXT.md`.
2. Fill in the sections with your real product details.
3. Start with Sections 1-3 if you are short on time.
4. Add Sections 4-8 as your AI work becomes more concrete.
5. If you do not know what to write yet, use [`qa-reference.md`](./qa-reference.md) and answer the minimum useful questions first.

The template is deliberately structured so an LLM can parse it quickly. Use plain language, but be specific. “We want better search” is weak. “Users struggle to express tradeoffs like commute vs. neighborhood quality in a keyword-only search flow” is useful.

## What To Include

The template asks for:

- product overview and business context
- core users and personas
- current product flows and pain points
- agent-relevant UX surfaces and action constraints
- relevant AI/ML systems and data assets
- tools, APIs, and logs an agent could use
- team structure and decision rights
- budget, latency, privacy, and localization constraints
- current AI priorities
- optional screen descriptions or screenshots

You do not need perfect answers. You need enough context for an LLM to reason with the right constraints.

## How To Use It

When you want help from an LLM:

1. Open your completed `PRODUCT_CONTEXT.md`.
2. Open the relevant section’s `SKILL.md`.
3. Paste both into the conversation.
4. Ask the model to guide you through that process for your product.

If your context is incomplete:

1. Open [`qa-reference.md`](./qa-reference.md).
2. Answer the shortest set of questions needed for the current decision.
3. Rewrite those answers into `PRODUCT_CONTEXT.md`.
4. Use the updated context file for the actual working session.

When you are using Codex in this repository:

1. Keep `my-product/PRODUCT_CONTEXT.md` in the workspace.
2. Use the integrated `ai-pm-playbook` skill or the playbook files normally.
3. Codex should read `my-product/PRODUCT_CONTEXT.md` directly instead of making you paste it manually each time.
4. If you have fresh product context, new market input, or new priorities, you should be able to type that update in chat and ask Codex to merge it into `my-product/PRODUCT_CONTEXT.md`.

Manual copy-paste is still the portable fallback for generic LLM chat tools. It should not be the default workflow inside Codex when the file already exists locally.

Example prompts:

- “Use this product context and this skill to help me write an AI PRD for conversational search.”
- “Guide me through model routing decisions for this product.”
- “Act as my AI PM copilot and walk me through the evaluation design process.”
- “Update my product context with this new information and use it for later feature discovery work.”
- “Add this fresh market context to `my-product/PRODUCT_CONTEXT.md` before we brainstorm new AI features.”
- “Ask me the minimum questions needed to update `my-product/PRODUCT_CONTEXT.md` for an AI agent workflow.”

## Keep It Local

`PRODUCT_CONTEXT.md` is ignored by Git through [`./.gitignore`](./.gitignore) so you do not accidentally commit proprietary information to a public repo.

The intended workflow is:

- commit the template
- create your own local `PRODUCT_CONTEXT.md`
- keep updating it as your product evolves

If you need to share your context with colleagues, do it deliberately. Do not assume a public fork is the right place for product-sensitive details.

## Practical Advice

- Update the file when a major AI initiative changes.
- Add metrics where possible. They anchor conversations.
- Be honest about constraints. The model gives better advice when you include budget, latency, compliance, and team limitations.
- If you use screenshots in an LLM that supports images, attach them alongside the text file rather than forcing everything into prose.
- In Codex, you should not need to manually maintain the file for every small change. You can give fresh context in chat and ask Codex to merge it into `PRODUCT_CONTEXT.md`.

This one file is the highest-leverage setup step in the entire repo. It turns the playbook from a static reference into a personalized working system.
