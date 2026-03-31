# Personalization UX

AI personalization is powerful because it can reduce repeated effort and increase relevance. It is risky because remembered preferences can feel invisible, wrong, or intrusive.

## Personalization Spectrum

| Pattern | Benefit | Risk |
| --- | --- | --- |
| Explicit preference collection | Clear and user-controlled | More setup friction |
| Implicit learning from behavior | Lower friction | Can feel creepy or inaccurate |
| Hybrid preference model | Best balance when done well | Needs strong transparency and controls |

## Key UX Principles

- make remembered preferences inspectable
- let users edit or reset them
- explain why a preference affected a result when relevant
- avoid pretending to know more than the user shared

## Realistic Use Scenarios

### Scenario 1: Property Search

The product remembers that the user prefers commute-friendly districts and 2+1 homes. Helpful UX might surface “using your saved preferences” with an edit option. Creepy UX would silently optimize around that preference in unrelated contexts.

### Scenario 2: Internal Copilot

The assistant remembers that one support team prefers concise responses. Helpful if transparent. Harmful if it silently adopts a tone that no longer fits the current task.

## Questions To Ask Your Engineering Team And Designer

- Which preferences should be explicit versus learned?
- How will users see, edit, or clear remembered preferences?
- What is the privacy expectation in this product context?
- When should the product explain why a personalized result was shown?
- Which personalization behaviors risk feeling creepy rather than helpful?

## Anti-Patterns

### Invisible Personalization

The system changes behavior without telling the user. What goes wrong: surprises feel manipulative.

### Overconfident Memory

One past behavior becomes a durable preference. What goes wrong: the product feels stubborn or wrong.

### Preference Dump

The product forces too many setup questions upfront. What goes wrong: value is delayed and onboarding friction rises.

## Red Flags

- Users cannot inspect or reset remembered preferences
- Personalization explanations sound vague or unsettling
- The product remembers behavior that users would not expect to be stored
- Old preferences keep overriding new intent
- Privacy concerns surface in user feedback early

## Bottom Line

Personalization should reduce effort while increasing user control, not replace control with invisible memory. Helpful beats clever.
