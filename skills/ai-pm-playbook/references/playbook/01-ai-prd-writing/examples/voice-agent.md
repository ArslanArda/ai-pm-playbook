# Example AI PRD: Real-Time Voice Leasing Assistant

## 1. PRD Summary

**Feature name:** Voice Leasing Assistant  
**Owner:** AI PM, Lead Qualification  
**Status:** Draft for design and engineering review  
**Target release:** Pilot with one call center team in 10 weeks  
**Primary user:** Inbound rental callers seeking basic property information

**One-sentence summary:** Handle high-volume inbound rental calls for simple qualification and scheduling tasks using a real-time voice assistant that can answer grounded questions, collect intent, and hand off to a human when confidence or policy limits require it.

## 2. Problem Statement

The call center receives a large volume of repetitive inbound calls asking basic questions:

- Is the property still available?
- What is the rent?
- Can I schedule a viewing?
- Is it furnished?
- Which district is it in?

Human agents spend disproportionate time on simple qualification and scheduling work, while more complex or high-value conversations suffer from longer wait times.

AI is the right lever because the interaction is conversational, repetitive, and time-sensitive. But voice raises a higher bar than text because latency, interruption handling, and conversational control directly affect whether the experience feels usable or broken.

## 3. Goals And Non-Goals

### Goals

- Deflect simple inbound calls that ask grounded, repetitive questions
- Reduce agent load on low-complexity inquiries
- Collect contact details and viewing intent for qualified leads
- Hand off smoothly when the call exceeds the assistant’s safe scope

### Non-Goals

- Replacing human agents for negotiation or complex objection handling
- Providing legal, financial, or unverifiable property advice
- Handling emotionally charged complaint calls in v1
- Supporting open-ended long-form sales conversations

## 4. User And Use Cases

**Primary persona:** Renters calling from mobile after viewing a listing.  
**Secondary persona:** Internal leasing team receiving transferred leads.

**Primary use cases:**

- confirm listing availability
- answer grounded questions from listing data
- collect preferred viewing time
- capture caller contact info and reason for interest

**Out-of-scope use cases:**

- negotiation on rent or deposit
- policy exceptions
- complaints about prior agent interactions
- speculative advice such as “is this a good investment”

## 5. Current Experience And Pain Points

Current inbound phone flow routes most calls to human agents or queues. During peak periods, wait times increase and simple questions consume time that senior agents should spend on qualified prospects.

Baseline metrics:

- average wait time during peak: 96 seconds
- percentage of calls that are repetitive information requests: estimated 43%
- agent-handled call completion time for simple info requests: 3.5 minutes

## 6. Proposed Experience

### Happy Path

1. Caller hears a short, clear greeting that explains the assistant can answer listing questions and help schedule viewings.
2. Assistant asks which listing or area the caller is asking about.
3. Assistant answers grounded questions from listing data and can collect missing qualification details.
4. If the user wants a viewing, assistant offers available scheduling windows or records a callback request.
5. Assistant confirms next steps and ends the call cleanly.

### Interruption And Turn-Taking Path

The assistant must allow the caller to interrupt naturally. If the caller starts speaking, the assistant stops within a tight budget and shifts to listening mode rather than finishing a scripted sentence.

### Low-Confidence Path

If the assistant is uncertain about the listing reference or the answer is not grounded in available data, it should say so directly and either ask a narrow follow-up or transfer the call.

### Handoff Path

If the caller asks out-of-scope questions, repeats a misunderstood request, or shows frustration, the assistant transfers to a human agent with a short call summary.

## 7. AI Task Definition

**Primary AI job:** Conduct short, grounded voice conversations for listing-related Q&A, basic qualification, and scheduling assistance while maintaining natural turn-taking and safe escalation.

**Subtasks:**

- speech recognition and intent capture
- listing identification
- grounded answer generation
- slot collection for scheduling or contact details
- interruption handling
- frustration and handoff detection

**What the AI must not do:**

- improvise answers beyond available listing or process data
- continue talking over the caller
- trap the caller in repeated clarification loops
- pretend to have scheduled something if downstream confirmation has not happened

**What remains deterministic:**

- allowed workflows
- scheduling availability source
- handoff rules
- compliance scripts

## 8. Latency Budget

Voice is only acceptable if the system feels responsive.

- time to first audio response target: <= 800ms
- interruption response target: stop speaking within 300ms of caller speech detection
- grounded answer generation target: <= 1.5s for routine listing questions

If the system cannot meet these budgets reliably, the UX must shift from “natural assistant” expectations to a more constrained call automation pattern. This is a product decision, not just an infrastructure problem.

## 9. Model Strategy Rationale

The required capability is real-time speech interaction with short-turn grounded dialogue. The product is not optimizing for eloquence. It is optimizing for fast, accurate, limited-scope assistance. That means the design should favor shorter turns, explicit grounding, and aggressive handoff rather than broad conversational ambition.

## 10. Data And Context Requirements

- live listing availability and metadata
- scheduling rules and office hours
- supported scripts for greeting, disclaimer, and handoff
- known call intents and common objections from call logs

Known limitation: listing data freshness may lag. The assistant must avoid overpromising and, when data freshness is uncertain, default to callback or human transfer rather than false certainty.

## 11. Success Metrics And Evaluation Criteria

### Business Metrics

- deflect 20% of simple inbound calls from human agents
- reduce peak wait time by 25%
- maintain or improve qualified viewing bookings per inbound lead

### AI Quality Metrics

- grounded-answer accuracy >= 95% on supported intents
- call intent classification accuracy >= 92%
- handoff precision >= 85% for calls that genuinely require humans
- caller interruption recovery success >= 90%

### Operational Metrics

- median time to first audio <= 800ms
- interruption response <= 300ms
- call abandonment during assistant flow does not exceed human baseline by more than 5%

## 12. Fallback And Handoff Behavior

Handoff is part of the product, not an exception.

Trigger handoff when:

- the caller asks out-of-scope questions twice
- the assistant fails to ground an answer
- repeated interruption or frustration is detected
- a scheduling or identity step cannot be completed cleanly

When handing off, the assistant must summarize:

- listing or area in question
- user intent
- any collected contact details
- why the handoff occurred

## 13. Human-In-The-Loop Design

During pilot, human agents review a daily sample of completed calls and all failed handoffs. This is not to manually approve every response. It is to validate grounded accuracy, interruption quality, and escalation behavior before scaling.

## 14. Edge Cases And Failure Modes

- caller references a listing unclearly or with a colloquial nickname
- multiple people are speaking in the background
- caller code-switches between languages mid-call
- assistant answers too slowly and gets interrupted repeatedly
- caller asks compound questions across pricing, availability, and negotiation
- downstream scheduling API fails after verbal confirmation has started

## 15. What Could Go Wrong

The highest-risk failure is false confidence delivered in a human-sounding voice. In text, users can reread and spot issues. In voice, a wrong answer can sound authoritative and damage trust faster.

Another major risk is poor turn-taking. Even correct answers feel unusable if the assistant speaks too long, fails to stop when interrupted, or keeps asking redundant clarifications. Pilot reviews will score not just answer correctness but conversational control.

## 16. Launch Plan

- launch type: pilot for one inbound queue during business hours
- launch gate: latency targets and supported-intent accuracy thresholds met in simulation plus internal dogfood
- monitoring plan: daily call sample review, handoff reason analysis, caller drop-off, booking completion, latency dashboard
- rollback trigger: grounded-answer accuracy below threshold for two daily samples or interruption complaints exceed target threshold

## 17. Open Questions

- Should the assistant identify itself as AI in the first sentence or first two sentences?
- Is bilingual support required in pilot or only after supported-intent quality stabilizes?
- Should the assistant offer callback scheduling before human handoff if wait times are high?

## 18. Lessons Embedded In This PRD

This PRD is intentionally conservative. The assistant is designed to handle narrow, high-volume, grounded calls. That is the right starting point for voice. If the team tries to expand scope before the latency and handoff experience are solid, the product will feel worse than a queue.
