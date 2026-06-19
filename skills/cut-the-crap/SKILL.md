---
name: cut-the-crap
description: Grill-style audit for deleting dead code and abandoned experiments.
disable-model-invocation: true
---

# Cut The Crap

Find code that is no longer earning its place and get it deleted.

## When To Use

- Abandoned experiments (e.g. a transcription runtime that never shipped)
- Features superseded by a different approach
- Backend code from a previous product shape that no longer reflects the domain
- Config, env vars, or routes with no live callers
- Dead UI paths, hidden screens, or disabled feature flags that were never re-enabled
- Duplicated utilities where one version won

## Workflow

### 1. Set Scope

Name the area: a directory, service, feature, or the whole repo.
If omitted, start with the backend, then frontend services, then UI.

### 2. Identify Candidates

Look for:
- Files/functions with no callers (`rg` for imports and usages)
- Feature flags or env vars that are always false/disabled
- Comments like "TODO: remove", "deprecated", "old approach", "spike"
- Packages in package.json with no import in source
- Routes/endpoints with no frontend caller
- UI screens unreachable from any navigation path
- Database columns/tables never queried by the backend
- Tests for deleted features

### 3. Grill One Area At A Time

For each candidate:

```
Area: <file or feature>

Evidence it's dead:
- <why you think it's unused>

Risk if wrong:
- <what breaks if we cut it and it turns out to matter>

Recommendation: CUT | KEEP | NEEDS CHECK

Reason: <one sentence>
```

Wait for confirmation before moving to the next area.

### 4. Cut On Confirmation

When the user says yes:
- Delete the files/code
- Remove unused imports and package.json entries
- Run build and tests to confirm nothing breaks
- Commit with message: `Cut: <short description>`

### 5. Keep A Running Tally

At the end of a session, summarise:

```
Cut The Crap: <scope>

Removed: <N files / N lines / N packages>
Kept:    <short list with reason>
Needs Check: <anything requiring human/device verification>
```

## Guardrails

- Do not cut based on filename alone — verify no callers.
- Do not cut shared utilities without checking all consumers.
- Do not cut tests just because the feature feels old — check if the test still describes real behaviour.
- If a feature is disabled but the design is still valid, suggest an issue rather than deletion.
- Prefer one focused session over a big-bang cleanup PR.
