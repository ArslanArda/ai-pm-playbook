# Skill: Design Better UX For AI Features

> **Context:** In Codex, look for `my-product/PRODUCT_CONTEXT.md` in the current workspace first and use it as the default product context. If local file access is unavailable, ask the user to paste product context manually or use the bundled template.

## TL;DR

Use this skill when you need to make user experience decisions for an AI-powered feature. It helps you decide how to handle latency, confidence, fallbacks, human review, interface style, and personalization so the feature feels useful and trustworthy rather than flashy or brittle.

## When to Use This

- You are designing or refining the UX of an AI feature
- The AI works technically, but user trust or usability is weak
- You need to decide between chat, form, or hybrid interaction
- Low-confidence behavior and fallback UX are unclear
- Users need review or correction controls
- You are introducing AI personalization and want the experience to feel helpful, not invasive

## Prerequisites

- A defined feature or user flow
- Known latency characteristics or at least latency expectations
- Some understanding of likely failure or low-confidence states
- Any early user feedback if available

## Step-by-Step Process

### Step 1: Define The User’s Mental Model

- **What to do:** Decide what users should understand about the AI’s role and limits.
- **Key questions to answer:** Is this assistant advisory, assistive, or acting automatically? What should users expect it to know? What should they expect to verify?
- **Output:** A clear UX positioning statement.
- **Common mistakes:** Letting the interface imply more capability than the product actually has.

### Step 2: Design The Happy Path And The Failure Path Together

- **What to do:** Map both what happens when the AI works and what happens when it is uncertain, wrong, or unavailable.
- **Key questions to answer:** What should the user see when confidence is low? What fallback should appear? When should the system ask versus act?
- **Output:** A state map with happy, low-confidence, and failure paths.
- **Common mistakes:** Designing fallback later; overusing generic error messages.

### Step 3: Match Interface Pattern To Task

- **What to do:** Choose conversational, structured, or hybrid interaction based on task shape.
- **Key questions to answer:** Is the task open-ended or parameterized? Does the user know what to ask for? Is correction easy in this interface?
- **Output:** An interface recommendation.
- **Common mistakes:** Using chat by default because it feels AI-native.

### Step 4: Set Review And Control Boundaries

- **What to do:** Decide where the user or a human operator should confirm, edit, or override the AI.
- **Key questions to answer:** Which actions are reversible? Which mistakes are costly? How much control is needed for trust without destroying speed?
- **Output:** A control model.
- **Common mistakes:** Automating too aggressively on high-risk actions; adding review where it creates pointless friction.

### Step 5: Tune Messaging For Confidence, Errors, And Personalization

- **What to do:** Write the product behavior for uncertainty, explanation, and memory or preference signals.
- **Key questions to answer:** How transparent should the feature be about limitations? How do we recover trust after a bad output? How do we explain remembered preferences without sounding invasive?
- **Output:** Messaging and UX rules.
- **Common mistakes:** Hiding uncertainty or oversharing internal model caveats.

### Step 6: Review Against Trust, Speed, And Clarity

- **What to do:** Evaluate the UX against the three big user-facing dimensions.
- **Key questions to answer:** Does it feel fast enough? Does it help users understand what happened? Does it keep trust when the AI is imperfect?
- **Output:** A UX decision review.
- **Common mistakes:** Optimizing one dimension at the expense of the others without noticing.

## Decision Framework

| UX symptom | First design area to inspect |
| --- | --- |
| Users feel confused | Mental model and onboarding |
| Users abandon during waiting | Latency UX |
| Users distrust outputs | Confidence, source, and fallback design |
| Users fight the interface | Conversational vs. structured pattern fit |
| Users fear automation | Human-in-the-loop and confirmation boundaries |

## Quality Checklist

- [ ] Is the AI’s role clear to the user?
- [ ] Are happy path and failure path both designed explicitly?
- [ ] Does the interaction model match the task shape?
- [ ] Are confirmation and override controls placed where they matter?
- [ ] Is low-confidence behavior visible and graceful?
- [ ] Does the latency treatment match the actual response time?
- [ ] Are error and recovery messages trust-preserving?
- [ ] Does personalization feel useful and transparent?

## Anti-Patterns

### 1. The Chat-By-Default Pattern

- **Description:** Every AI feature gets a conversation box whether the task needs it or not.
- **Why it happens:** Chat feels like the obvious AI interface.
- **What to do instead:** Match the interface to task structure and correction needs.

### 2. The Invisible Uncertainty Pattern

- **Description:** The product hides low confidence behind polished language.
- **Why it happens:** Teams fear exposing weakness.
- **What to do instead:** Show calibrated transparency and useful fallback choices.

### 3. The Human Review Tax

- **Description:** Human confirmation is added everywhere.
- **Why it happens:** It feels safer.
- **What to do instead:** Add review only where risk and irreversibility justify it.

### 4. The Generic Error State

- **Description:** AI failure falls back to a vague error toast.
- **Why it happens:** Failure design was deferred.
- **What to do instead:** Design domain-specific fallback behavior.

### 5. The Creepy Memory Reveal

- **Description:** Personalization appears without explanation or control.
- **Why it happens:** Teams optimize for delight without privacy sensitivity.
- **What to do instead:** Show preference use transparently and let users edit or opt out.

## Adaptation Guide

### Consumer Search And Discovery

Prioritize latency, trust, and easy refinement.

### Internal Productivity Tools

Users can tolerate more complexity if the system is transparent and editable.

### High-Risk Or Irreversible Actions

Favor stronger review, clearer confidence messaging, and more conservative fallback behavior.
