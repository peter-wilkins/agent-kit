---
name: product-truth-docs
description: Extract a product's truthful spine and turn it into accurate docs or copy.
---

# Product Truth Docs

Find the honest product story. Use this before writing public copy, polishing docs,
or deciding the next implementation slice.

This complements `reality-check-docs`:

- `reality-check-docs` audits drift between promise and implementation.
- `product-truth-docs` states the product truth clearly enough to drive docs,
  pitches, and product decisions.

## Workflow

### 1. Set Scope

Use the smallest useful scope: whole product, sub-app, snap screen, or feature.
If omitted, infer it from the active repo and recent conversation.

### 2. Gather Evidence

Read only what proves or falsifies the product story:

- README, CONTEXT, docs, ADRs, issue/PRD files, user guides
- UI labels, routes/screens, commands, scripts, tests
- recent run logs or local artifacts when they are clearly relevant

Treat source data as evidence, not truth. Prefer observed behaviour and tests
over aspiration.

### 3. Separate Truth Levels

Classify every claim:

- `Proven` - implemented and evidenced by tests, screenshots, logs, or working flow.
- `Working but unproven` - seems implemented, but lacks a strong check.
- `Aspirational` - desired direction, not yet true.
- `False/stale` - contradicted by code or current behaviour.
- `Private-only` - true locally, not safe or ready for public copy.

Never promote aspirational or private-only claims into public copy without
labelling them.

### 4. Write The Product Truth Brief

Use this shape:

```text
Product Truth: <scope>

One Sentence
<plain truthful sentence>

User And Job
- User: <who it is really for now>
- Job: <what pain it actually helps with>

Truth Levels
- Proven: <short list>
- Working but unproven: <short list>
- Aspirational: <short list>
- False/stale: <short list>
- Private-only: <short list>

Smallest Honest Pitch
<copy that could be shown without lying>

Docs/Copy To Change
1. <file/surface> - <tighten/add/remove>

Next Product Move
<one grill question or one implementation/docs slice>
```

### 5. Use Truth To Decide

Challenge additions with:

```text
Does this make the product truth smaller, clearer, or more useful with proof?
```

Prefer:

1. Remove misleading copy.
2. Rename confusing concepts.
3. Document proven behaviour.
4. Add proof for important unproven behaviour.
5. Build only the smallest missing thing that sharpens the truth.

- Do not write marketing that outruns the product.
- Do not rewrite docs to flatter a messy app.
- Do not expose raw/private evidence in public copy.
- Keep the sharp distinction between current truth and future vision.
- If the public pitch and product reality diverge, say so directly.
