---
name: prototype-ui
description: Prototype a fuzzy UI surface to answer a product question.
---

# Prototype UI

Prototype UI answers a product question. It does not mean "make it prettier".

Use this before building when the surface is fuzzy, especially for search,
thinking, learning, feedback, workbench, or phone-first flows.

## Operating Principle

Name the thing being learned before drawing the screen.

If the product question is unclear, grill briefly before coding.

## Workflow

1. State the product question in one sentence.
2. Identify the user, job, and success signal.
3. Choose the lightest fidelity that can answer the question.
4. Build the smallest useful surface.
5. Use real-ish data, not lorem ipsum.
6. Make state visible when state is part of the question.
7. Run the prototype and test one target flow.
8. Capture the verdict: keep, kill, or iterate.

## Fidelity Choices

- Conversation sketch: use when the domain language is still unstable.
- Static wireframe: use when layout or information hierarchy is unclear.
- Clickable prototype: use when flow, sequence, or state is unclear.
- Real app slice: use when real data, feedback, auth, or device behaviour is the risk.

Prefer one thin vertical slice for product/workflow questions.

Use 2-3 materially different variants only when the question is visual or
layout-based. Variants must differ in structure, not just colour or copy.

## UI Heuristics

- First screen starts at the user's job, not an explanation.
- Put the primary input first for search, probe, or concierge surfaces.
- Show human labels before machine ids.
- Hide debug ids by default; keep them one tap or copy action away.
- For search and memory surfaces, show the top relevant chunks, not filenames.
- For thinking surfaces, show compact thought-sized chunks with a source trail nearby.
- Use phone/thumb constraints when the target surface is mobile.
- Use desktop density when the target surface is a private workbench or debug tool.
- Avoid global frameworks unless the project already uses one or the prototype is testing it.

## Continuum-Specific Defaults

- Favour "what is the user trying to think through?" over "what document is this from?"
- Treat long document excerpts as a smell; prefer thought cards or meaningful chunks.
- Preserve source trail, but keep it behind the human-readable result.
- If search results are technically correct but meaningless, add an extraction or
  summarisation step before polishing the UI.
- If two lenses or models return the same shape, vary the model or remove one.

## Fall Back To Grilling

Use grill-with-docs instead of coding when:

- The user/job/success cannot be stated in one sentence.
- The requested UI improvement is really a product-language problem.
- The next screen depends on unresolved domain terms.
- The prototype would only decorate unclear behaviour.

Ask one question at a time and provide a recommended answer.

## Output Shape

```text
Product question:
Prototype type:
What changed:
How to run:
Checks:
What we learned:
Suggested next step:
```
