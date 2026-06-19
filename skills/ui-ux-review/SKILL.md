---
name: ui-ux-review
description: Socratic UI/UX review for product screens and flows.
disable-model-invocation: true
---

# UI/UX Review

## Mode

This is a UX grilling skill, not a passive checklist.

Challenge the screen by asking what the user is trying to do, what the app makes obvious, what it hides, and where the user's eye/thumb naturally goes. Give a recommended answer with each question. If code or screenshots can answer the question, inspect them instead of asking.

## Core Heuristics

- Primary job first: the most urgent user work belongs above slow setup/configuration.
- Obvious paths beat clever hiding: core actions should not rely only on a burger menu.
- No amateur floating: avoid controls that hover over unrelated content, collide with lists, or look detached from the screen's structure.
- Mobile first, not mobile only: check narrow mobile, touch landscape/tablet when relevant, and desktop.
- Thumb reach matters: common mobile actions should be reachable without precision taps.
- Eye path matters: headings, counts, and primary actions should support fast scanning.
- Minimize mode confusion: make it clear whether the user is reviewing, editing, creating, searching, or doing work.
- Reduce clicks for common work; allow extra clicks for rare/destructive work.
- Keep state visible but quiet: loading, stale/offline, empty, and error states should not blank useful context.
- Repeated controls should be consistent across screens unless a strong user-job reason says otherwise.

## Workflow

1. Identify the user and job.
   - Who is on this screen?
   - What are they trying to finish now?
   - What is the next likely action after success or failure?

2. Grill the information architecture.
   - Is this one surface or two?
   - Is urgent work mixed with setup?
   - Are important actions hidden in global navigation?
   - Would a first-time user know where to go?

3. Walk the flow.
   - Count taps/clicks for the main job.
   - Find backtracking, hidden branches, and dead ends.
   - Check whether review/decision moments naturally offer follow-up actions.

4. Inspect the UI.
   - Use real app screens when practical.
   - Check mobile and desktop layouts.
   - Look for overlap, cramped text, unstable controls, weak hierarchy, and confusing labels.

5. Decide or create issues.
   - If the product decision is unclear, keep grilling one question at a time.
   - If the decision is clear, update docs or create focused issues.
   - If implementation is requested, build the smallest complete slice and verify it.

## Socratic Question Shape

Ask one question at a time:

```text
Question: [specific UI/product decision]

Recommended answer: [clear recommendation]

Why: [short UX reason]
```

## Review Output Shape

When asked for a review rather than a grill:

- Findings
- Flow Friction
- Suggested Fixes
- Checks Run
- Open Product Questions

Lead with the highest-impact user problems. Include route/screen and viewport when known.
