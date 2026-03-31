# Product Context

> Fill in each section below. Be specific. The more detail you provide, the more personalized your playbook experience will be. Paste this entire file into your LLM conversation along with any `SKILL.md` file to get tailored guidance.
>
> You do not need to fill every section on day one. Start with the essentials (Sections 1-3) and expand as needed.

---

## 1. Product Overview

**Product name:** [e.g., HomeFinder]  
**One-line description:** [e.g., A real estate marketplace connecting property seekers with agents and listings across Turkey]  
**Domain/vertical:** [e.g., Real estate marketplace, B2C + B2B]  
**Website/app:** [e.g., web + iOS + Android]  
**Stage:** [e.g., Growth stage — 2M monthly active users, 500K+ listings]  
**Business model:** [e.g., Subscription revenue from real estate agents + premium listing fees + lead generation]

---

## 2. Users & Personas

Describe your 2-4 primary user personas. For each persona:

**Persona 1: [Name/Role]**
- Who they are: [e.g., First-time home buyers, 25-35, urban, mobile-first]
- Primary goal: [e.g., Find an affordable apartment in a specific neighborhood]
- Key pain points: [e.g., Overwhelmed by listings, cannot tell which are real, do not understand pricing]
- AI relevance: [e.g., Would benefit from conversational search, personalized recommendations, price analysis]

**Persona 2: [Name/Role]**
- Who they are: [e.g., Real estate agents managing 50+ listings]
- Primary goal: [e.g., Get more leads and close deals faster]
- Key pain points: [e.g., Writing unique listing descriptions is time-consuming, responding to inquiries is slow]
- AI relevance: [e.g., Would benefit from automated listing descriptions, AI-assisted lead qualification, smart response suggestions]

[Add more personas as needed]

---

## 3. Current Product Experience

Describe the core product flows most relevant to AI features.

**Core flow 1: [Flow name]**
- Description: [e.g., Property search — user enters criteria, browses listings, filters, views details, contacts agent]
- Current pain points: [e.g., Keyword search is rigid, users struggle to express complex preferences like "quiet neighborhood near good schools"]
- Current metrics: [e.g., 40% search-to-listing-view rate, 3% listing-to-contact rate, avg 4.2 searches per session]

**Core flow 2: [Flow name]**
- Description: [e.g., Listing creation — agent uploads photos, fills property details, writes description, publishes]
- Current pain points: [e.g., Description writing takes 15-20 minutes per listing, quality is inconsistent, many descriptions are copy-pasted]
- Current metrics: [e.g., 12 min avg time to publish, 30% of descriptions are under 50 words]

[Add more flows as needed]

---

## 4. Technical Landscape

**Current AI/ML features (if any):**
- [e.g., Basic recommendation engine based on collaborative filtering]
- [e.g., Image moderation for listing photos — rule-based, not AI]
- [List what exists, its maturity, and known limitations]

**AI models/providers in use:**
- [e.g., OpenAI GPT-4o for conversational features, GPT-4o-mini for classification tasks]
- [e.g., No models in production yet — evaluating options]

**Key infrastructure:**
- [e.g., Backend: Python/FastAPI, hosted on AWS]
- [e.g., Database: PostgreSQL + Elasticsearch for search]
- [e.g., No vector database yet]
- [Only include what is relevant to AI product decisions, not your entire stack]

**Data assets relevant to AI:**
- [e.g., 5M historical listings with structured metadata]
- [e.g., 200K user search queries per day — logged but not labeled]
- [e.g., Customer support chat logs — 50K conversations/month]
- [What data do you have that could train, fine-tune, or evaluate AI features?]

---

## 5. AI Maturity & Team

**AI maturity level:** [Pick one and elaborate]
- Exploring: [No AI features in production, researching possibilities]
- Experimenting: [Running pilots or POCs, 1-2 AI features in limited release]
- Scaling: [Multiple AI features in production, dedicated AI resources]
- Optimizing: [AI is core to the product, sophisticated eval/monitoring in place]

**Team structure:**
- Product team: [e.g., 1 AI PM, 2 general PMs, 1 designer]
- Engineering: [e.g., 4 backend engineers, 2 with ML experience, 1 data engineer]
- Data science: [e.g., No dedicated DS team — engineers handle model integration]
- Total people who touch AI features: [e.g., ~6 people]

**AI decision-making:**
- Who decides which AI features to build? [e.g., PM proposes, VP Product approves]
- Who decides which model to use? [e.g., Engineering lead recommends, PM approves based on cost/quality tradeoff]
- Who owns prompt quality? [e.g., PM owns the criteria, engineers implement and iterate]

---

## 6. Constraints & Context

**Budget constraints:**
- [e.g., $2K/month API budget for AI features]
- [e.g., No budget for fine-tuning infrastructure — cloud API only]
- [e.g., Budget is flexible if we can prove ROI]

**Latency requirements:**
- [e.g., Search responses must return within 3 seconds]
- [e.g., Listing description generation can be async — up to 30 seconds is fine]
- [List latency expectations per feature or flow]

**Compliance & privacy:**
- [e.g., KVKK compliance required — user data cannot leave Turkey]
- [e.g., Company policy requires human review for customer-facing AI content]
- [e.g., PII in user queries must be stripped before sending to external models]

**Language & localization:**
- [e.g., Primary language is Turkish — all AI outputs must be in Turkish]
- [e.g., Turkish NLP has unique challenges: agglutinative morphology, limited Turkish training data in many models]
- [e.g., Bilingual support needed — Turkish primary, English secondary]

**Competitive landscape:**
- [e.g., Main competitors: Competitor A (market leader, no AI features visible), Competitor B (recently launched AI search)]
- [e.g., AI could be a key differentiator in our market — competitors are behind]
- [Where do you stand versus competitors on AI adoption?]

---

## 7. Current AI Priorities (Optional)

What are you currently working on or planning?

- [e.g., Launching conversational search as the next major feature — currently in design phase]
- [e.g., Exploring AI-generated listing descriptions to reduce agent workload]
- [e.g., Evaluating whether to build an internal AI copilot for customer support]
- [List your current or next AI initiatives]

---

## 8. Screenshots & Screen Descriptions (Optional)

If you want more personalized guidance, describe key screens or attach screenshots when you paste this into your LLM conversation.

**Screen 1: [Screen name]**
- What it shows: [e.g., Search results page — list of property cards with photo, price, location, size]
- Key elements: [e.g., Filter sidebar on left, sort dropdown, map toggle, 20 results per page]
- Known issues: [e.g., No way to express complex preferences, filters are too rigid]

**Screen 2: [Screen name]**
- What it shows: [e.g., Listing detail page — photos, description, property details, agent contact form]
- Key elements: [e.g., Photo carousel, AI-generated description planned, similar listings section]
- Known issues: [e.g., Descriptions are often low quality, no neighborhood context]

[If your LLM supports images, you can attach actual screenshots instead of writing detailed descriptions. This file stays text-only for GitHub compatibility.]
