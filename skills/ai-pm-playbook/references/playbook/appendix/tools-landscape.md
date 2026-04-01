# Tools Landscape

This appendix is intentionally high level. The repo is not a vendor comparison site, and tools change too quickly for static “best tool” lists to age well.

Instead, use this landscape to understand which categories matter for AI PM decisions.

## Model Providers

Useful when you need:

- text generation
- reasoning
- multimodal input
- speech capabilities
- embedding or classification support

PM lens:

- quality in your target language and domain
- latency under real load
- pricing model
- support for grounding, structure, and safety controls

## Retrieval And Search Infrastructure

Useful when you need:

- document or knowledge retrieval
- hybrid search
- semantic recall plus deterministic filters

PM lens:

- freshness
- permission handling
- source quality
- observability of retrieval failures

## Evaluation And Observability Tools

Useful when you need:

- prompt or model comparison
- grader orchestration
- trace inspection
- latency and token monitoring

PM lens:

- whether the tool helps decisions, not just dashboards
- ability to segment by route, cohort, or failure category
- support for versioning and baseline comparison

## Workflow And Agent Orchestration Tools

Useful when you need:

- multi-step AI workflows
- tool orchestration
- traceability across steps

PM lens:

- how much complexity they add
- how transparent step behavior is
- whether they encourage overbuilding

## Internal Adoption And Workspace Tools

Useful when you need:

- AI copilots for teams
- prompt libraries
- workflow templates

PM lens:

- whether the tool fits real tasks
- how permissions and data exposure are handled
- whether usage data can be connected to adoption outcomes

## Practical Advice

- pick categories based on the problem you are solving
- avoid buying tools before your workflow and evaluation needs are clear
- prefer tools that improve visibility and decision quality, not only feature count
- remember that the product problem should choose the tool category, not the other way around
