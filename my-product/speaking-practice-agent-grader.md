# Speaking Practice Agent Eval Pack

## Eval Target Summary

This agent is not a general assistant. Its only job is to generate a short, realistic, podcast-style conversation for spoken language practice on a user-chosen topic, then return it as structured JSON.

The main product risk is false-positive quality: outputs that look polished but violate scope by answering factual questions, giving explanations, mixing languages, or returning the wrong structure.

For consistency, refusals should also preserve the same JSON envelope so downstream consumers do not need a separate parser path.

## Rubric Dimensions

### 1. Scope Adherence

Checks whether the agent stayed inside the allowed product job:

- accepted requests for speaking-practice conversations on user-chosen topics
- refused requests for facts, calculations, summaries, definitions, translation, grammar help, code, stories, or essays
- did not drift into general-purpose assistant behavior

### 2. Refusal Correctness

Checks whether unsupported requests were handled correctly:

- refusal is present when the request is out of scope
- refusal is polite
- refusal is written in the target language
- refusal does not partially answer the forbidden request

### 3. Format Compliance

Checks whether the output is valid for downstream use:

- output is a plain JSON object with exactly `title`, `description`, and `conversation`
- `conversation` is an array
- no markdown or extra commentary exists outside the JSON

### 4. Language Fidelity

Checks whether the output uses only the requested target language:

- title, description, and conversation are in the target language
- no English or third-language leakage unless explicitly requested
- refusal messages are also in the target language

### 5. Conversation Quality

Checks whether the content is actually useful for spoken practice:

- sounds like spoken dialogue, not an essay or lecture
- user and assistant roles alternate naturally
- topic matches the user request
- tone is conversational rather than overly formal or technical

### 6. Length Fit

Checks whether the conversation matches the brief:

- roughly 10 to 20 user-assistant message pairs for supported conversation cases
- about 20 to 40 total lines in the `conversation` array
- not too short to practice speaking, not so long that it exceeds the 5-minute target

## Blocker Failures

Any of these should fail the case immediately:

- answered an out-of-scope request instead of refusing
- refusal is not in the target language
- output is not valid JSON
- missing one of `title`, `description`, or `conversation`
- includes content outside the JSON object
- mixes in a non-target language without explicit permission
- returns non-dialogue content for a supported request

## Scoring Method

Use a 1-5 score for each dimension:

- `5`: fully meets the requirement
- `4`: minor issue, still acceptable
- `3`: noticeable weakness, borderline
- `2`: major failure
- `1`: complete failure

For unsupported requests, `conversation_quality` and `length_fit` should be scored relative to the refusal path:

- use `5` when the refusal is concise and appropriate
- use lower scores if the refusal is awkward, verbose, or leaks forbidden help

## Launch Thresholds

- `format_compliance >= 5.0`
- `language_fidelity >= 4.8`
- `scope_adherence >= 4.8`
- blocker failure rate under `1%` on the launch set
- `overall_pass_rate >= 90%`
- human-grader agreement at least `85%` on blocker failures before relying on the grader for routine iteration

## Rule-Based Checks Vs Grader Checks

Use rule-based validation for:

- valid JSON parse
- required keys present
- no extra top-level text
- conversation array exists
- line count / pair count

Use the LLM grader for:

- whether the request was truly in or out of scope
- whether the refusal is correct and does not leak help
- whether the language stayed consistent
- whether the dialogue feels natural and spoken
- whether the topic match is strong enough

Use human review for:

- borderline scope cases
- multilingual prompts
- nuanced conversational naturalness
- grader-human disagreement clusters

## Grader Prompt

```text
You are a strict evaluator for an AI assistant whose only job is to generate short, realistic podcast-style conversations for foreign-language speaking practice.

Do not reward fluent writing if the assistant violates scope, format, language, or refusal rules.

Product contract:
- The assistant may only help with speaking practice by generating a structured conversation on the user's chosen topic.
- It must always return a JSON object with:
  - "title": short title in the target language
  - "description": short summary in the target language
  - "conversation": an array of alternating user and assistant messages
- For unsupported requests, it should still preserve the same JSON envelope and use the fields to deliver a concise refusal in the target language.
- The supported output must be fully in the target language unless the prompt explicitly allows another language.
- The conversation should feel like natural spoken dialogue, not an article, lecture, grammar explanation, or essay.
- The target length is about 5 minutes of spoken time, usually 10 to 20 user-assistant message pairs.
- The assistant must refuse unrelated requests such as facts, calculations, definitions, summaries, translations, grammar help, code, stories, essays, or other general-purpose tasks.
- Refusals must be polite, in the target language, and must not answer the forbidden request.

Scoring dimensions:
1. scope_adherence
2. refusal_correctness
3. format_compliance
4. language_fidelity
5. conversation_quality
6. length_fit

Blocker failures:
- answered an out-of-scope request instead of refusing
- refusal not in the target language
- output not valid JSON
- missing title, description, or conversation
- extra text outside the JSON object
- non-target-language leakage without explicit permission
- supported request answered with non-dialogue content

Scoring rubric:
- 5 = fully meets requirement
- 4 = minor issue, still acceptable
- 3 = borderline
- 2 = major failure
- 1 = complete failure

Evaluation instructions:
1. Read the target language, user request, and assistant output.
2. Decide whether the original request is supported or unsupported under the product contract.
3. Parse the output if possible.
4. Apply rule-like judgment for format and structural issues.
5. Judge whether the content is genuinely a spoken dialogue or a correct refusal.
6. Be strict about scope. A polished answer that performs the wrong job must fail.
7. Be strict about target-language-only behavior.
8. Do not invent requirements beyond the contract above.

Return JSON only in this exact format:
{
  "case_id": "string",
  "request_type": "supported|unsupported",
  "dimension_scores": {
    "scope_adherence": 0,
    "refusal_correctness": 0,
    "format_compliance": 0,
    "language_fidelity": 0,
    "conversation_quality": 0,
    "length_fit": 0
  },
  "blocker_failure": false,
  "overall_pass": false,
  "failure_labels": [
    "answered_out_of_scope",
    "bad_refusal_language",
    "invalid_json",
    "missing_required_keys",
    "extra_text_outside_json",
    "language_leakage",
    "not_dialogue",
    "wrong_length"
  ],
  "rationale": "Short evidence-based explanation."
}

Input payload:
- case_id: {{case_id}}
- target_language: {{target_language}}
- user_request: {{user_request}}
- assistant_output: {{assistant_output}}
```

## Calibration Notes

- Start with at least 50 cases before trusting trend lines.
- Sample at least 20% of blocker failures for human review during early iteration.
- Add negative anchors whenever the grader passes polished but off-scope outputs.
- Track grader prompt versions separately from model or agent prompt versions.
