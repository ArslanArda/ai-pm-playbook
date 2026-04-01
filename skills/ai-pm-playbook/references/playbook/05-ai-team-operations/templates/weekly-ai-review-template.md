# Weekly AI Review Template

Use this for the standing weekly review of an AI initiative.

## 1. Mission Snapshot

- Mission: [e.g., Listing Description Agent Pilot]
- Week number: [e.g., Week 3]
- Overall status: [Green / Yellow / Red]
- Main decision this week: [e.g., keep retry loop or simplify]

## 2. Product Progress

- What shipped or changed this week:
  [e.g., added validator for unsupported amenities]
- What was learned:
  [e.g., one retry improves quality, second retry does not]

## 3. Quality Review

- Current eval score or pass rate: [e.g., 81% pass on stable benchmark]
- Biggest failure category: [e.g., generic filler]
- Blocker-level issues: [e.g., unsupported amenity hallucinations remain above threshold]

## 4. Cost And Latency Review

- Cost change vs. last week: [e.g., +12% due to retry path]
- P50 / P95 latency: [e.g., 4s / 9s]
- Main cost or latency driver: [e.g., large context passed into grader]

## 5. User / Operator Feedback

- Top positive signal: [e.g., agents publish faster on simple listings]
- Top friction signal: [e.g., low trust in image-derived suggestions]
- Complaints or flagged cases: [summarize]

## 6. Decisions Needed

- [e.g., tighten retry cap]
- [e.g., remove one attribute from pilot scope]
- [e.g., hold beta expansion]

## 7. Next Week Focus

- [e.g., improve grader specificity]
- [e.g., reduce fallback rate]
- [e.g., validate high-risk category manually]
