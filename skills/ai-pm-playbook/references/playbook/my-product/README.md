# Product Context Setup

This directory is how you make the skill relevant to your actual product.

Most generic AI advice fails because it ignores context. The right model strategy for a B2C marketplace is different from the right model strategy for a regulated B2B workflow. The right fallback for an AI-generated listing description is different from the right fallback for a support copilot answering a customer in real time.

That is why the playbook includes a product context file. You fill it out once, then use it with the integrated skill or a relevant module `SKILL.md` to get guidance tailored to your product, users, team, constraints, and priorities.

## What This Directory Is For

Use this directory to create a local, private description of your product that Codex can read directly from the workspace.

The committed file is:

- [`PRODUCT_CONTEXT.template.md`](./PRODUCT_CONTEXT.template.md): the blank template with instructions and example depth

The local file you create is:

- `PRODUCT_CONTEXT.md`: your actual product context, kept local and ignored by Git

## How To Fill In `PRODUCT_CONTEXT.md`

1. Copy `PRODUCT_CONTEXT.template.md` to `PRODUCT_CONTEXT.md`.
2. Fill in the sections with your real product details.
3. Start with Sections 1-3 if you are short on time.
4. Add Sections 4-8 as your AI work becomes more concrete.

The template is deliberately structured so Codex can parse it quickly. Use plain language, but be specific. “We want better search” is weak. “Users struggle to express tradeoffs like commute vs. neighborhood quality in a keyword-only search flow” is useful.

## What To Include

The template asks for:

- product overview and business context
- core users and personas
- current product flows and pain points
- relevant AI/ML systems and data assets
- team structure and decision rights
- budget, latency, privacy, and localization constraints
- current AI priorities
- optional screen descriptions or screenshots

You do not need perfect answers. You need enough context for Codex to reason with the right constraints.

## How To Use It

When you are using Codex:

1. Keep `my-product/PRODUCT_CONTEXT.md` in the workspace.
2. Use the integrated `ai-pm-playbook` skill.
3. Let the skill read `my-product/PRODUCT_CONTEXT.md` directly instead of making you paste it manually each time.

Manual copy-paste is still the portable fallback for plain chat tools that cannot access local files. It should not be the default workflow inside Codex when the file already exists locally.

Typical tasks:

- write an AI PRD for conversational search
- choose a routing strategy for this product
- design an evaluation plan for a new feature
- review AI UX fallback behavior for a risky workflow

## Keep It Local

`PRODUCT_CONTEXT.md` is ignored by Git through [`./.gitignore`](./.gitignore) so you do not accidentally commit proprietary information.

The intended workflow is:

- keep the template in version control
- create your own local `PRODUCT_CONTEXT.md`
- keep updating it as your product evolves

If you need to share your context with colleagues, do it deliberately. Do not assume a public location is the right place for product-sensitive details.

## Practical Advice

- Update the file when a major AI initiative changes.
- Add metrics where possible. They anchor conversations.
- Be honest about constraints. The skill gives better advice when you include budget, latency, compliance, and team limitations.
- If you use screenshots in an environment that supports images, attach them alongside the text file rather than forcing everything into prose.
