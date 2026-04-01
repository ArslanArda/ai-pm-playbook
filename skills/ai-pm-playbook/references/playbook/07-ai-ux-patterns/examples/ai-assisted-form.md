# Example: AI-Assisted Form Flow

## Scenario

A real estate listing form was being upgraded with AI autofill based on:

- uploaded property photos
- short freeform agent notes
- repeated patterns from prior listings

The business goal was speed. The product risk was silent wrong data.

Launch targets:

- reduce median time-to-publish from `12` minutes to under `8.5`
- keep AI-suggested field rejection under `10%`
- keep factual correction tickets from agents below baseline

## The Product Rule

The PM wrote one hard default before any UI design:

`Blank is better than a confident wrong field.`

That one rule drove the whole flow.

## Step 1: Clear Assistive Framing

After photo upload and core details, the form showed:

- user-entered fields in standard style
- AI-preparing fields with dotted placeholders
- a small label: `AI suggestions are drafts until you approve them`

The team explicitly refused to prefill the entire form invisibly in the background. That would have looked faster and been harder to trust.

## Step 2: Draft State That Does Not Pretend To Be Final

Pending AI sections showed skeleton rows and section labels such as:

- `Drafting property details`
- `Checking visible amenities`
- `Preparing description suggestion`

No pending state used the final field style. This mattered because earlier tests showed users mistook grey placeholder text for committed values.

## Step 3: Confidence-Based Suggestion Design

The UI separated suggestions into three states:

| Confidence band | UX treatment | Example |
| --- | --- | --- |
| High | Pre-filled but marked `AI draft`, easy to edit | `Property type: Apartment` |
| Medium | Highlighted review card with explicit confirmation control | `Balcony: Please confirm` |
| Low | Left blank with optional hint | `Heating type: not filled` |

The thresholds were product choices:

- high confidence above `0.92`
- medium confidence `0.75 - 0.92`
- below `0.75`, do not auto-suggest inline

Those cutoffs were tuned to agent tolerance, not model vanity metrics.

## Step 4: Review Controls That Match Real Behavior

Every AI-touched field supported:

- `Accept`
- `Edit`
- `Reject`

And the form also provided a sidebar review module:

`12 AI suggestions ready for review`

This let fast users review in bulk and cautious users inspect inline.

### Example field copy

- high confidence: `AI draft based on photos and notes`
- medium confidence: `Needs your review before publish`
- rejected state: `You chose not to use this suggestion`

## Step 5: Final Publish Gate

Before publish, the form displayed:

- number of AI-assisted fields used
- number of suggestions still unreviewed
- one hard block on medium-confidence unreviewed fields in critical categories

Critical categories:

- price
- room count
- listing type
- availability status

The PM explicitly blocked auto-publish if any critical medium-confidence field stayed unresolved.

## What The Team Tried First And Rejected

The first prototype auto-filled nearly every detectable field and marked them with a tiny sparkle icon.

Why it failed:

- rejection rate hit `18%`
- agents were unsure which values came from AI versus previous listing memory
- publish confidence dropped even when the form was technically faster

The second version reduced automation and made provenance visible. Time-to-publish improved less dramatically, but trust improved enough to keep the feature.

## Beta Metrics

| Metric | Before AI assist | Beta week 2 |
| --- | --- | --- |
| Median time-to-publish | `12.1 min` | `8.7 min` |
| AI-suggested field rejection rate | n/a | `8.6%` |
| Critical-field correction after publish | baseline `4.2%` | `4.5%` |
| Description suggestion usage | n/a | `63%` |

The small rise in post-publish correction was acceptable, but it triggered closer monitoring on price and room count fields.

## Fallback Behavior

If extraction failed:

- the form remained fully usable
- failed sections said `Couldn't draft this reliably`
- manual input remained primary

No broken AI card was allowed to block publish.

## What This Example Teaches

### 1. Autofill should look assistive, not magical

The fastest-looking design was not the safest or most trusted.

### 2. Confidence thresholds are a product choice

The right threshold is the one users will tolerate, not the one that makes the model look busiest.

### 3. Critical fields need stricter review than descriptive fields

You can accept more automation on listing description than on price or room count. Treating them equally is lazy UX.
