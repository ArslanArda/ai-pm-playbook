# Contributing

Thanks for contributing to `ai-pm-playbook`.

This repository is intentionally narrow: practical product-management frameworks for AI-native products. The fastest way to make a useful contribution is to add something a PM could use next week in a real product review, roadmap discussion, evaluation design session, or launch decision.

## Contribution Principles

- **No code.** Keep contributions to markdown, Mermaid diagrams, templates, and checklists.
- **Write for PMs, not engineers.** Engineering context is welcome when it affects product decisions, but avoid implementation tutorials.
- **Be opinionated.** Make a recommendation, explain why, and include when to deviate.
- **Use realistic examples.** Favor real estate, marketplace, e-commerce, travel, fintech, and support workflows over generic chatbot examples.
- **Optimize for reuse.** Someone should be able to copy the framework, template, or skill into their own workflow immediately.
- **Respect the `SKILL.md` contract.** These files are meant to be pasted into an LLM, so structure matters.

## What Good Contributions Look Like

Strong additions usually include:

- a clear PM problem statement
- a concrete decision framework, matrix, or rubric
- examples of when to use the framework
- anti-patterns and red flags
- questions a PM should ask their engineering or data partners
- realistic constraints such as latency, budget, compliance, or operational readiness

Weak additions usually sound like:

- “it depends” without structure
- abstract essays about AI transformation
- engineering implementation details without PM decisions attached
- shallow summaries that repeat common AI advice

## Section Structure

If you add a new top-level section, keep it self-contained and consistent:

```text
section-name/
├── README.md
├── SKILL.md
├── frameworks/
├── templates/        # if needed
└── examples/         # if needed
```

Every major section should work independently. Someone should be able to land on that folder and understand what it is for without reading the whole repo.

## Skill Wrappers

This repo also ships Codex-installable skills under [`skills/`](./skills/README.md).

If you change content in the main playbook folders, keep the matching bundled content under the related `skills/<skill-name>/references/` directory in sync. The wrapper skill files should stay concise; the heavier reference material belongs under `references/`.

## `SKILL.md` Requirements

Every `SKILL.md` must include:

- `TL;DR`
- `When to Use This`
- `Prerequisites`
- `Step-by-Step Process`
- `Decision Framework`
- `Quality Checklist`
- `Anti-Patterns`
- `Adaptation Guide`

Write the “Key questions to answer” so an LLM can ask them directly and use the answers to personalize guidance. Treat the file as both documentation and a reusable operating prompt.

## Writing Standards

- Write in direct, practical language.
- Prefer short paragraphs and clear bullets.
- Cut filler.
- Use Mermaid for flowcharts and decision trees when a visual structure helps.
- Keep internal links relative and working.
- If you use metrics, make them specific enough to be useful.
- If you use examples, include what went wrong and what changed.

## File-Specific Expectations

### Framework files

Each framework should include:

- a decision matrix, rubric, or Mermaid decision flow
- at least two realistic usage scenarios
- at least three anti-patterns
- three to five questions for engineering
- a red flags section

### Example files

Each example should include:

- a realistic scenario with team, constraints, and timeline
- the full decision walkthrough
- tradeoffs and reasoning
- what failed or changed during the process
- lessons learned

### Templates

Templates should be immediately usable. Include short bracketed examples so a PM knows what “good” looks like without turning the template into a filled-out document.

## How To Submit

1. Fork the repo.
2. Create a branch.
3. Make your changes.
4. Sanity-check internal links and Mermaid diagrams.
5. Open a PR with:
   - what you added
   - why it belongs in the playbook
   - what PM problem it solves

## Suggested PR Checklist

- [ ] The contribution is code-free
- [ ] The content is written for PMs
- [ ] Recommendations are explicit and defensible
- [ ] Anti-patterns and tradeoffs are included
- [ ] Internal links work
- [ ] Mermaid syntax is valid
- [ ] The content adds something specific that was missing

If you are unsure whether something fits, open an issue first and describe the PM problem you want to solve.
