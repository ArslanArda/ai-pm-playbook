# Prompt-To-Eval Pack For AI Agents

Use this when you already have an agent or system prompt and need to turn it into a usable evaluation package quickly.

The goal is to produce three artifacts from the prompt plus product context:

1. evaluation strategy
2. evaluator implementation spec
3. starter rubric dataset in CSV format

The important change: do not assume every agent should be graded with an LLM judge.

Some agents should be evaluated mainly with:

- rule-based checks
- an LLM-as-judge grader
- a hybrid stack that combines rules and grader logic
- human review only for the highest-risk dimensions

The prompt plus product context should tell you which evaluator shape fits the agent.

## Required Inputs

- the current agent or system prompt
- relevant product context
- any tool list or action list the agent can use
- optional sample conversations, logs, or failure examples

## What To Extract From The Prompt

Before writing the eval pack, extract:

- the main job the agent is trying to do
- the subtasks it implies
- any promised behaviors or quality claims
- any forbidden behaviors or safety rules
- any tool-use expectations
- any fallback or clarification behaviors

This becomes the raw material for the rubric and dataset.

## Step 0: Choose The Evaluator Mode

Before writing the pack, decide which evaluator type should own which part of the rubric.

### Default evaluator modes

#### Mode A: Rule-Based Evaluator

Best when the agent has explicit, checkable requirements such as:

- required JSON fields
- schema validity
- exact tool-call shapes
- known allowed or disallowed strings
- deterministic pass/fail rules

Typical examples:

- extraction agents
- routing classifiers
- format-constrained generators
- tool wrappers with explicit action constraints

#### Mode B: LLM-As-Judge Evaluator

Best when quality depends on interpretation and natural-language judgment such as:

- conversational naturalness
- relevance
- groundedness relative to provided context
- tone fit
- nuanced refusal quality

Typical examples:

- writing agents
- conversational practice agents
- summarization or explanation agents
- assistant responses where multiple outputs can be acceptable

#### Mode C: Hybrid Evaluator

Best when the agent has both deterministic and subjective quality requirements.

Typical examples:

- agents that must return strict JSON and also sound natural
- tool-using agents where tool trace correctness is rule-checkable but fallback quality is not
- assistants with hard safety boundaries plus softer UX quality goals

Recommended split:

- rules handle hard format and action constraints
- LLM grader handles judgment-heavy dimensions
- human review samples disagreement clusters or high-risk cases

#### Mode D: Human-Review-Primary Evaluator

Best when:

- the task is highly sensitive
- the rubric is still too fuzzy for consistent grading
- domain truth is hard to verify from the prompt alone
- launch risk is too high to over-trust automated evaluation

Use this as the primary mode temporarily, not as an excuse to avoid rubric design.

## Fast Decision Heuristic

Ask these in order:

1. Can the key failure be detected deterministically from the output or trace?
   If yes, start with rules.
2. Is the remaining quality mostly subjective but still rubric-able?
   If yes, add an LLM judge.
3. Would a grader mistake fluent but wrong behavior for success?
   If yes, tighten rules or require human review for that dimension.
4. Would a false pass create serious trust or compliance risk?
   If yes, keep a human in the loop at least during launch calibration.

## Output 1: Evaluation Strategy

The evaluation strategy should answer:

- What user-facing behaviors matter most?
- Which dimensions belong in the rubric?
- Which failures are blockers?
- Which parts can be checked by rules, humans, or graders?
- What launch thresholds matter?

Recommended structure:

1. Eval target summary
2. Rubric dimensions
3. Blocker failures
4. Scoring method by dimension
5. Dataset coverage plan
6. Launch thresholds

## Output 2: Evaluator Implementation Spec

Do not default this artifact to a grader prompt. First choose the evaluator mode, then produce the implementation artifact that fits it.

### Option A: Rule-Based Evaluator Spec

Use this when the main quality bar can be checked deterministically.

Recommended contents:

- input fields the checker receives
- exact validation rules
- pass/fail thresholds
- error codes
- any derived metrics to compute

Example shape:

```text
Evaluator type: rule_based

Inputs:
- user request
- agent output
- optional tool trace

Checks:
1. Output parses as valid JSON
2. Required keys are present
3. Disallowed content is absent
4. Tool call, if present, matches expected schema

Return JSON:
{
  "case_id": "...",
  "evaluator_type": "rule_based",
  "checks": {
    "valid_json": true,
    "required_keys_present": true,
    "disallowed_content_absent": true,
    "tool_schema_valid": true
  },
  "blocker_failure": false,
  "overall_pass": true,
  "rationale": "..."
}
```

### Option B: LLM-As-Judge Prompt

Use this when the evaluator must interpret quality rather than only validate structure.

Minimum inputs:

- user request
- prior state or conversation context if relevant
- tool traces or tool outputs if relevant
- final agent response
- expected behavior or scenario notes

Use a grader prompt shape like this:

```text
You are a strict evaluator for an AI agent.

Your job is to judge whether the agent behavior meets the rubric below.
Do not reward fluent wording if the behavior is incorrect, unsupported, unsafe, or missing key constraints.

Rubric dimensions:
1. Task success
2. Correctness and grounding
3. Tool-use accuracy
4. Fallback or clarification behavior
5. Safety and policy compliance

For each case:
- read the user request, prior state, tool traces, and final response
- score each dimension from 1-5
- flag any blocker failure as true or false
- provide a short rationale citing the evidence

Return JSON with:
{
  "case_id": "...",
  "dimension_scores": {
    "task_success": 0,
    "correctness_grounding": 0,
    "tool_use_accuracy": 0,
    "fallback_behavior": 0,
    "safety_policy": 0
  },
  "blocker_failure": false,
  "overall_pass": false,
  "rationale": "..."
}
```

Adjust the dimensions to fit the actual agent.

### Option C: Hybrid Evaluator Spec

Use this when both rules and an LLM grader are needed.

Recommended contents:

- which dimensions are rule-owned
- which dimensions are grader-owned
- how blocker failures are combined
- when human review overrides automated scoring

Example shape:

```text
Evaluator type: hybrid

Rule-owned checks:
- valid_json
- required_fields_present
- tool_call_schema_valid

Grader-owned dimensions:
- task_success
- groundedness
- fallback_quality

Aggregation logic:
- any failed rule-owned blocker => overall fail
- otherwise run grader and require minimum dimension thresholds
- send borderline or disagreement cases to human review
```

### Option D: Human Review Rubric

Use this when automation is not yet trustworthy enough.

Recommended contents:

- reviewer instructions
- dimensions and scoring anchors
- blocker definitions
- sampling policy
- adjudication process when reviewers disagree

## What To Choose By Agent Type

Use these as defaults, then override if the prompt suggests otherwise:

| Agent type | Default evaluator |
| --- | --- |
| Structured extraction or classification | Rule-based |
| Natural-language generation with open-ended quality | LLM-as-judge |
| Tool-using assistant with hard constraints plus soft UX quality | Hybrid |
| Sensitive, fuzzy, or hard-to-ground workflow | Human-review-primary |

## Output 3: Starter CSV Dataset

Use CSV because it is simple, reviewable, and easy to extend.

Recommended columns:

```text
case_id,segment,user_input,prior_state,available_tools,expected_behavior,primary_rubric_dimensions,blocker_failure,notes
```

Use the starter set to cover:

- common requests
- ambiguous requests
- missing-information cases
- unsupported requests
- tool failure or unavailable-data cases
- state carryover cases
- high-risk or trust-sensitive cases

See [`../examples/agent-rubric-dataset.csv`](../examples/agent-rubric-dataset.csv) for a simple example.

## Copyable Request Pattern

Use a prompt like this with an LLM:

```text
Use this product context and this agent prompt to generate:
1. an evaluation strategy
2. the right evaluator implementation for this agent
3. a starter CSV rubric dataset

First decide whether this agent should be evaluated mainly with rules, an LLM judge, a hybrid evaluator, or human review.
Do not default to LLM-as-judge unless the agent behavior actually requires judgment-heavy grading.
Make the eval product-facing, not purely technical.
Call out blocker failures, launch thresholds, and the difference between rule-based checks, grader checks, and human review.
For the dataset, cover common, edge, adversarial, and trust-sensitive scenarios.
```

## Quality Bar

The eval pack is strong enough to start with when:

- the rubric reflects real user value
- blocker failures are explicit
- the chosen evaluator type matches the actual agent behavior
- the evaluator artifact has a structured response format
- the CSV covers more than happy-path cases
- the outputs can drive launch or iteration decisions
