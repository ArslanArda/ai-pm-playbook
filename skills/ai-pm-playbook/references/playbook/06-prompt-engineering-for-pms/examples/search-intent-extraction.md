# Example: Iterating A Search Intent Extraction Prompt

## Scenario

A Turkish property marketplace wanted to replace rigid keyword search with conversational query interpretation. The first release goal was narrow:

- extract structured intent before retrieval
- support messy mobile Turkish
- avoid silent constraint loss
- keep clarification prompts below annoyance threshold

Team:

- 1 PM
- 2 backend engineers
- 1 applied AI engineer
- 1 analyst

Timeline:

- 4 weeks from prototype to closed beta decision

Initial output schema:

- `listing_type`
- `budget_min`
- `budget_max`
- `location`
- `room_count`
- `amenities`
- `soft_preferences`
- `ambiguity_flag`
- `notes`

Launch blockers:

- silent material constraint-drop rate above `5%`
- incorrect listing-type inference above `3%`
- clarification prompt rate above `18%`
- malformed JSON above `1%`

Initial eval set:

- `240` queries
- `80` clean explicit queries
- `70` typo-heavy or shorthand mobile queries
- `50` multi-intent or contradictory queries
- `40` soft-preference-heavy queries

## Version Scorecard

| Version | Exact-field accuracy | Silent material constraint drop | Clarification prompt rate | Malformed JSON | Decision |
| --- | --- | --- | --- | --- | --- |
| V1 | `78%` | `14%` | `4%` | `0%` | Too guessy |
| V2 | `81%` | `7%` | `29%` | `0%` | Too interruptive |
| V3 | `85%` | `6%` | `15%` | `0%` | Close, but unstable on multi-intent |
| V4 | `88%` | `4.8%` | `14%` | `0.4%` | Beta-eligible on logic, weak on localized shorthand |
| V5 | `91%` | `3.9%` | `13%` | `0.4%` | Ship to closed beta |

## Version 1: Straight Extraction

### Prompt excerpt

```text
Extract structured search intent from the user's query.
Return JSON with listing_type, budget, location, room_count, amenities, and ambiguity_flag.
If a field is not present, use null.
```

### What looked good

- clean queries parsed well
- schema stayed simple
- latency was low

### What failed

- the model guessed too often
- soft preferences were mixed with hard filters
- material constraints were dropped without warning

### Failure examples

| Query | Bad behavior |
| --- | --- |
| `sessiz bir yerde 2+1 kiralik max 35 bin kadikoy civari` | Interpreted `sessiz` as mandatory neighborhood filter instead of soft preference |
| `kiralik ama uygun satilik da olabilir, atasehir 3+1` | Collapsed two intents into one clean rental result without ambiguity flag |
| `ümraniye tarafı 30 civarı` | Guessed a rental budget in thousands without currency or listing type evidence |

### What the PM changed

The PM stopped calling this an extraction problem and reframed it as a product risk problem: the worst failure was not "missing nuance." It was confident wrong retrieval.

## Version 2: Add Ambiguity Rules

### Prompt diff

```text
Mark fields unknown when not clearly present.
Set ambiguity_flag=true when listing_type or budget meaning is unclear.
Do not guess district when multiple candidates fit.
```

### What improved

- fewer silent wrong assumptions
- listing-type errors dropped
- district guessing was reduced

### What got worse

- the model became overly cautious
- clarification prompts spiked on non-critical ambiguity
- users got interrupted for preferences that should not block retrieval

### Failure examples

| Query | Bad behavior |
| --- | --- |
| `metroya yakin 2+1 kiralik besiktas civari` | Asked for clarification even though `metroya yakin` should be a soft preference |
| `aileye uygun, kadikoy ama moda da olur` | Marked the whole query ambiguous rather than extracting a primary location with soft preference notes |

## Version 3: Separate Retrieval-Critical Ambiguity From Soft Preference Ambiguity

The PM made the product rule explicit:

- ask only if ambiguity changes retrieval materially
- treat adjectives like `sessiz`, `aileye uygun`, and `metroya yakin` as soft preferences
- prefer one-pass extraction whenever retrieval can still proceed safely

### Prompt diff

```text
Only set ambiguity_flag=true when uncertainty changes which listings should be retrieved.
Extract soft preferences separately instead of blocking retrieval for them.
Do not ask a clarification question for style or lifestyle preferences alone.
```

### What improved

- clarification rate fell from `29%` to `15%`
- search sessions moved faster
- soft-preference queries became much more usable

### What still failed

- multi-intent phrasing remained unstable
- the model sometimes picked a secondary intent because it sounded more explicit

### Example regression

Query:

`kiralik bakiyorum ama satilik da mantikliysa goster, kartal deniz manzarali`

Bad output:

- `listing_type = sale`
- `ambiguity_flag = false`

The model locked onto the more explicit second clause even though the first clause stated the primary job.

## Version 4: Add Primary Intent Priority

### Prompt diff

```text
When the query includes multiple intents, extract the primary actionable intent first.
Record secondary intent in notes if relevant.
If two materially different intents are equally weighted, set ambiguity_flag=true.
```

### What improved

- multi-intent stability improved sharply
- fewer contradictory retrievals reached the user
- PM and engineering now had a rule they could review together

### Score impact

- silent material constraint-drop rate fell below the `5%` launch blocker
- clarification prompt rate stayed acceptable
- malformed JSON rose slightly because `notes` handling became more complex

### Review artifact

| Slice | Before V4 | After V4 |
| --- | --- | --- |
| Multi-intent accuracy | `61%` | `82%` |
| False ambiguity on soft preferences | `17%` | `9%` |
| JSON compliance | `100%` | `99.6%` |

### Remaining problem

Turkish shorthand still hurt recall:

- `2+1`
- `b.sehir`
- `kadkoy`
- suffix-heavy forms like `kadikoyde`, `besiktastan`

## Version 5: Add Language-Specific Guidance

### Prompt diff

```text
Normalize common Turkish property shorthand and typos when strongly supported:
- room notation like 1+1, 2+1, 3+1
- common district abbreviations
- agglutinative suffix variation on known locations

Do not overfit to one abbreviation list. When evidence is weak, keep the field unknown.
```

### What improved

- typo-heavy query performance improved
- room-count extraction became more stable
- the model stayed conservative on truly weak location evidence

### Review sample

| Query | V4 behavior | V5 behavior |
| --- | --- | --- |
| `kadkoy 2+1 kiralk 35e kadar` | `location = null` | `location = Kadikoy` |
| `b.sehir 3+1 satlik` | `room_count = null` | `room_count = 3+1` |
| `besiktastan yurume mesafesi 1+1` | lost location | extracted `Besiktas` plus soft note |

## Final Approved Prompt Skeleton

```text
You extract structured search intent for a property marketplace before retrieval.

Priority order:
1. Do not drop material constraints.
2. Do not guess fields that change retrieval materially.
3. Prefer one-pass extraction over clarification unless ambiguity changes retrieval.

Treat lifestyle or desirability phrases as soft_preferences unless they change retrieval materially.
When multiple intents exist, choose the primary actionable intent and record the secondary intent in notes.

Normalize common Turkish shorthand and suffix variation when evidence is strong.
If evidence is weak, keep the field unknown.

Return valid JSON with:
- listing_type
- budget_min
- budget_max
- location
- room_count
- amenities
- soft_preferences
- ambiguity_flag
- notes
```

## What Still Would Not Ship

Even after V5, the team kept three classes out of the beta promise:

- neighborhood quality questions like `guvenli semt olsun`
- truly contradictory dual-intent finance queries
- deeply conversational follow-ups that depended on memory beyond the current turn

Those were not prompt polish issues. They were scope issues.

## Lessons Learned

### 1. Good extraction prompts encode product logic, not just parsing logic

The winning change was not "understand Turkish better." It was "only interrupt the user when ambiguity changes retrieval."

### 2. Thresholds prevent endless prompt tweaking

Once the team set explicit blockers, it became obvious which failures mattered and which ones could wait for later iterations.

### 3. Localization is not edge polish

In this product, shorthand and typo-heavy Turkish was mainstream traffic. Treating it as a later improvement would have made the feature feel broken on day one.
