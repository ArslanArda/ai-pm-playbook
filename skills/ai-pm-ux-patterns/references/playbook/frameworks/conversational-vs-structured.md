# Conversational vs. Structured

Not every AI feature should be chat. The right interaction model depends on the shape of the task.

## Comparison Matrix

| Dimension | Conversational UI | Structured UI | Hybrid UI |
| --- | --- | --- | --- |
| Task specificity | Low to medium | High | Medium to high |
| User knows parameters | Not always | Usually yes | Partially |
| Number of parameters | Unclear or evolving | Known | Mixed |
| Error tolerance | Needs flexible recovery | Can enforce precision | Flexible start, precise finish |
| Best for | Exploration and refinement | Known workflows and forms | Complex tasks with both exploration and precision |

## Realistic Use Scenarios

### Scenario 1: Property Search

Chat works well for open-ended exploration. But once intent becomes clearer, structured filters or editable chips often improve control. That points to hybrid UX.

### Scenario 2: Refund Request Workflow

If the required parameters are known and policy-sensitive, structured UI is usually better than open chat. The AI can still assist within a more controlled interface.

## Questions To Ask Your Engineering Team And Designer

- Does the user know what to ask for in structured terms?
- Will users need to correct or refine multiple parameters quickly?
- Would chat create unnecessary ambiguity for this workflow?
- Which fields must be precise for the system to work safely?
- Could a hybrid design preserve both discovery and control?

## Anti-Patterns

### Chat Worship

Chat is used because it feels modern. What goes wrong: parameter-heavy tasks become slower and harder to correct.

### Form Worship

The team forces every AI feature into rigid inputs. What goes wrong: exploratory intent and nuance are lost.

### Hybrid Confusion

Chat and forms are combined without a clear role split. What goes wrong: users do not know where to act next.

## Red Flags

- Users keep restating parameters that a form could capture better
- Chat interface hides important state or applied constraints
- Structured UI forces users to know things they do not yet know
- Hybrid surfaces duplicate the same controls in confusing ways
- Correction flow feels harder than the original task

## Bottom Line

Choose the interaction model that best fits the task, not the one that makes the product look most “AI.” Hybrids are often strongest when exploration and precision both matter.
