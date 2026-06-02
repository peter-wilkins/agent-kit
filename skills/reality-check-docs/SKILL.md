---
name: reality-check-docs
description: Audit whether the actual app matches its docs, product language, and intended tight surface area. Use when the user asks whether app reality matches docs, mentions doc drift, feature sprawl, coherent app surface, product reality checks, or wants the next grilling/implementation slice.
---

# Reality Check Docs

Counterpart to `grill-with-docs`: first sharpen the intended app, then check
whether code, UI, tests, and workflows still match that intention.

1. **Documented promise** - what the app says it is for.
2. **App reality** - what the code/UI actually does.
3. **User surface** - what a human must understand to use it.
4. **Proof** - tests, screenshots, logs, or working flows.

## Workflow

### 1. Set Scope
Infer the smallest useful scope if omitted.

### 2. Read The Promise

Read only relevant docs first: `CONTEXT.md`, `README.md`, `docs/`, ADRs,
issues/PRDs/user guides, and app copy.

Extract the **Documented Promise**: user, core job, flows, non-goals,
safety/privacy rules, and intended surface area.

### 3. Inspect Reality
Inspect implementation and evidence: routes/screens/components,
handlers/state/storage, tests, screenshots/smoke runs, and run logs.

### 4. Compare

Classify findings:

- `Missing` - docs promise behaviour that is absent.
- `Extra` - app exposes behaviour not supported by docs or product intent.
- `Confused` - terminology, flows, or UI labels disagree.
- `Overbuilt` - implementation adds machinery without proof of improvement.
- `Underspecified` - app works, but docs do not explain the contract.
- `Unproven` - claim may be true, but tests/evidence are missing.
- `Good fit` - reality and docs agree.

### 5. Recommend Cuts Before Adds

Default order:

1. Delete or hide extra surface.
2. Rename confusing concepts.
3. Tighten docs to match proven behaviour.
4. Add tests/evidence for important claims.
5. Only then add missing features.

Challenge new features with:

```text
Does this make the app smaller, clearer, or more useful with proof?
```

For implementation top moves, name the lightest `AGENTS.md` workflow mode.

## Report Shape

```text
Reality Check: <scope>

Verdict: <one sentence>

Findings
1. [Severity] <type> - <short finding>
   Docs: <file/line>
   Reality: <file/line or observed evidence>
   Recommendation: <cut/tighten/test/add>

Coherence Score
- Surface area: <tight / spreading / bloated>
- Docs fit: <good / partial / stale>
- Proof: <good / weak / missing>

Top Move
<one next grill question or implementation slice, plus workflow mode if implementation>
```

Severity:

- `High` - user confusion, data loss risk, broken core promise, unsafe external action.
- `Medium` - stale docs, misleading UI, feature sprawl, missing proof.
- `Low` - cleanup, wording, polish.

## Guardrails

- Do not rewrite docs to excuse a messy app.
- Do not propose more architecture before checking for deletion.
- Use the result to choose the next grill or smallest implementation move.
- Impressive AI-built features only count as value if they support the core job.
- Keep raw personal data local; cite private files only in local/private reports.
- Inspect external services/accounts read-only unless explicitly approved.
