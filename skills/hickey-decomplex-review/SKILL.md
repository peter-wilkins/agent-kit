---
name: hickey-decomplex-review
description: Find tangled/complected concepts in a plan, schema, architecture, or product workflow and split them into simpler independent records, policies, and interfaces before implementation. Use when the user mentions Hickey, simple not easy, decomplex, complected, tangled, untangle, separate concerns, or asks for a pre-implementation architecture sanity check.
---

# Hickey Decomplex Review

Use before implementing a plan that is growing records, schemas, services,
drivers, permissions, workflows, or UI.

Longer note: https://continuumkit.org/blog/the-hickeyian-way/

Core question:

```text
What things have been tied together that can vary independently?
```

## Workflow

### 1. Scope
Name the smallest scope under review: a schema, command, feature, runtime slice,
workflow, or product surface.

### 2. Concepts And Forces

Extract nouns and forces:
- identity, state, time/history, values/data
- effects, policy, implementation, platform
- UI/interface, proof/tests, permissions/grants, recovery

### 3. Complections

Look for records, classes, commands, or docs combining independent axes:
- reachability plus implementation
- requirement plus grant
- permission plus approval
- operation plus driver
- safety policy plus capability
- proof plus implementation
- UI state plus domain state
- current state plus history

```text
Can this vary independently from the thing it is inside?
```

If yes, propose a split.

### 4. Data Boundaries

When a split is real, name the data records first. Keep behaviour behind simple
interfaces.

Good pattern:

```text
GraphEdge
ImplementationBinding
CapabilityRequirement
CapabilityGrant
SafetyPolicy
ProofClaim
```

Bad pattern:

```text
Provider { kind, driver, safety, grant, tests, UI, setup, execution }
```

### 5. Enforcement

For safety-sensitive designs, ask:

```text
Who enforces this, and what stops bypass?
```

Policies without runtime enforcement are documentation only. Name the broker,
sandbox, driver wrapper, ledger, or test that provides proof.

### 6. Report

Use this shape:

```text
Hickey Decomplex Review: <scope>

Verdict
<one sentence>

Already Simple
- <good split>

Complected / At Risk
1. <tangled concept> - <why tangled> -> <split>

Next Slice
<one small record/schema/test/docs change>
```

## Guardrails

- Do not split for elegance alone. Split when concepts vary independently or
  enforcement/proof needs a clean boundary.
- Do not turn every review into a framework rewrite.
- Prefer deleting fields before adding records.
- For Zod/schema work, print the proposed schema and get Peter's approval before
  coding.
- Capture resolved terminology in project docs when useful.
