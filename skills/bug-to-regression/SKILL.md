---
name: bug-to-regression
description: Recreate a bug report or vague user complaint as a concrete failing case, using the Dev phone first for mobile/PWA issues when available, write the smallest useful regression test, fix the root cause, and verify the original flow. Use when a user reports a bug and asks to debug/fix it, says to recreate an issue, turn a bug report into a regression test, prevent a bug coming back, or build a bug-to-test-to-fix feedback loop.
---

# Bug To Regression

Turn "this is broken" into proof, then code.

## Rule

Do not start by patching. First build a pass/fail loop that proves the user-visible bug or the closest reachable failure seam.

For mobile/PWA bugs, "recreate" means try the Dev phone first when it is available. The phone is the primary reproduction surface; desktop/headless tests are the regression proxy after the real phone behavior is understood.

If no credible loop can be built, say exactly why and add temporary diagnostics or a focused issue instead of guessing.

## Workflow

### 1. Build Bug Packet

Collect the smallest useful packet:

- Symptom, expected behavior, actual behavior.
- User/device/env, route, account mode, feature flags, build hash.
- Repro steps, even if partial.
- Evidence: logs, screenshots text, crash reports, request IDs, recent deploy/commit, user data shape.
- Impact: data loss, security/privacy, blocked work, annoyance.

If underspecified, infer a minimal problem statement and list unknowns. Ask only if missing info makes reproduction impossible or destructive.

### 2. Recreate

Prefer fast deterministic loops:

1. Existing failing test or command.
2. Unit/service test at boundary where behavior diverges.
3. API/database smoke script.
4. Dev phone flow for mobile/PWA/device bugs, using `adb`, Chrome remote debugging, app text/DOM, logs, storage, network status, and button taps where possible.
5. Headless browser/device flow with text assertions.
6. Targeted instrumentation with removable `[DEBUG-...]` tags.
7. Human-in-the-loop only when device/platform behavior cannot be automated.

The loop must fail for the reported bug before the fix, or clearly explain why this seam is the best proxy.

#### Dev Phone Repro

When a Dev phone is plugged in:

- Identify device with `adb devices -l`.
- Keep it awake if appropriate; do not wipe data unless the user explicitly asked.
- Inspect foreground app/origin before assuming the user is on staging/prod.
- Prefer text evidence: DOM text, console errors, request failures, storage keys, auth/session state, and app logs.
- Use screenshots/video only when the bug is visual/layout and text evidence is insufficient.
- Record exact app URL/origin, installed PWA package/scope when relevant, build hash, and account mode.
- After fixing, repeat the same phone flow, then add a durable automated test or explain the proxy seam.

### 3. Rank Hypotheses

Write 3-5 falsifiable hypotheses before editing:

```text
If [cause], then [probe] should show [signal].
```

Check recent diffs and config drift when bug is regression-like. For library/platform behavior, verify docs or current examples instead of relying on memory.

### 4. Write Regression Test

Add the narrowest test that would have caught this bug:

- Put it at the same layer as the failure boundary.
- Assert user-visible behavior or contract, not implementation trivia.
- Include stale state, ordering, auth/session, offline, duplicate-click, or race conditions when that is the bug shape.
- For UI bugs, prefer text/DOM/network assertions over screenshots unless layout itself is the bug.
- If the only viable check is manual, write a tiny script or checklist and explain why automation is not credible yet.

Watch the test fail before fixing unless the bug only reproduces in prod/device state. If it cannot be made red, state that explicitly.

### 5. Fix Small

Patch the root cause with the smallest coherent change.

Avoid broad cleanup while the bug loop is red. Capture unrelated cleanup as issue/backlog.

Preserve user data. Do not clear storage, reset DBs, or change external services unless the user explicitly asked or approved.

### 6. Disprove

Before declaring done, try to break the fix:

- Run original repro/proxy loop.
- Run adjacent cases: logged out/logged in, refresh, second device, stale cache, denied permission, network failure, duplicate action.
- Re-read the diff as a skeptical reviewer: did it hide the symptom, overfit test data, or move state drift elsewhere?
- If the change touched shared code, run broader focused tests for nearby callers.

### 7. Ship Evidence

Final report must include:

- Root cause in one sentence.
- Dev phone reproduction result for mobile/PWA bugs, or why it was skipped.
- Regression test path/name and what it proves.
- Fix summary.
- Commands/checks run.
- Remaining risk or manual check, if any.

If using issue tracker, update issue with actual root cause, test evidence, and shipped commit before closing.

## Good Patterns To Steal

- **Bug packet first**: collect symptom, expected/actual, repro, impact, evidence.
- **Diagnosis-first**: prove before patch; tiny deterministic loop beats broad speculation.
- **Adversarial pass**: try to disprove the proposed fix before shipping.
- **No self-grade when risky**: ask for independent review or run an existing review skill for high-impact changes.
- **Circuit breaker**: after repeated non-repro attempts, stop and ask for a log, trace, debug report, or permission for temporary instrumentation.

## Output Shape

```text
Bug packet: ...
Repro loop: ...
Root cause: ...
Regression test: ...
Fix: ...
Checks: ...
Manual check: ...
```
