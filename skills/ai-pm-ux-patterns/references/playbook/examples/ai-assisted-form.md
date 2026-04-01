# Example: AI-Assisted Form Flow

## Context

A complex property-listing form was being improved with AI autofill from uploaded photos, notes, and prior listing patterns. The challenge was making the form feel faster without making users fear hidden mistakes.

## Step 1: User Starts With Core Inputs

The user uploads photos and enters a few essential details.

The form immediately shows:

- what the user entered manually
- which sections the AI is preparing to help with

This keeps the user aware that autofill is assistive, not magical.

## Step 2: AI Draft State

As the AI works:

- empty fields show subtle “drafting suggestion” placeholders
- sections that are still pending display skeleton placeholders, not final-looking guesses

Important:

Pending states should never look identical to confirmed values.

## Step 3: Suggestion Review State

When suggestions appear:

- high-confidence suggestions are visually distinct but editable
- medium-confidence suggestions are highlighted for review
- low-confidence areas are left blank rather than guessed

Example:

- property type may be auto-suggested confidently
- balcony presence may be surfaced as “Confirm if this listing has a balcony”

## Step 4: Confirmation And Editing

Each AI-touched field supports:

- accept
- edit
- reject

The UI groups AI suggestions in one review section as well as inline within the form. This helps both quick-review users and detail-oriented users.

## Step 5: Final Publish Review

Before final submit:

- show a compact summary of AI-assisted fields
- surface any still-unconfirmed medium-confidence suggestions
- remind the user that the final listing reflects their approval

This preserves accountability and trust.

## Error And Fallback Behavior

If AI extraction fails:

- the form remains fully usable
- no broken empty AI module blocks progress
- helper copy may suggest which fields still need manual input

## Key UX Lessons

- AI autofill works best when suggestion state is visually distinct from confirmed state
- users need fast edit/reject controls, not just acceptance
- blank is often better than a low-confidence guess
- the form should remain usable even if the AI layer fails completely
