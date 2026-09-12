# File Templates

All three files live in `docs/plan/`. Keep them terse — these files get read at the start of every session, so every unnecessary line costs tokens forever.

## SPEC.md

```markdown
# <Project Name> — Spec

## Positioning
One sentence: what it is, who it's for.

## Requirements
- R1: <must-have requirement>
- R2: ...

## Nice-to-have (post v1)
- N1: ...

## Out of scope
- Not X. Not Y. (verbatim from the user)

## Tech stack
- Backend:
- Frontend:
- Database:
- Infra/deploy:
- Testing:

## Constraints
- ...

## Decisions made on user's behalf
- <date>: chose X over Y because Z. (empty if none)
```

## PLAN.md

```markdown
# <Project Name> — Implementation Plan

Modules in dependency order. One module ≈ one session.

## M1: <name> [S|M|L]
- Goal: <one line>
- Covers: R1, R3
- Files: <paths to create/modify>
- Acceptance: <objective check — "dotnet build passes and GET /health returns 200">
- Depends on: —

## M2: <name> [S|M|L]
...

## Change log
- <date>: split M4 into M4a/M4b because ... (empty at creation)
```

Module sizing guidance:
- S: single concern, few files (a config setup, one endpoint)
- M: one vertical slice (endpoint + data layer + test) — the ideal default
- L: too big — split it before writing the plan

Typical first modules for greenfield projects: M1 = repo scaffold + build pipeline + hello-world runnable, M2 = data layer/schema, then vertical slices. Adjust to the project; don't force this shape.

## PROGRESS.md

```markdown
# <Project Name> — Progress

## Status
- [x] M1: scaffold — done 2026-07-07
- [ ] M2: data layer — in progress
- [ ] M3: ...

## Handoffs

### M1 (done 2026-07-07)
- Files: apps/api/Program.cs, Dockerfile, .github/workflows/ci.yml
- Decisions: used minimal API instead of controllers (less boilerplate, spec has 4 endpoints total)
- Verified: dotnet build clean, /health returns 200 locally
- Gotchas: CI workflow needs AWS creds secret before M6; flagged, not blocking

### M2 (in progress)
- Done: schema migration written and applied
- Not done: repository classes
- Resume at: apps/api/Data/ — start with UserRepository
```

Handoff rules:
- Written at module completion (or at mid-module stop), never reconstructed later
- Decisions and gotchas matter most — they're the things a fresh session can't infer from the code
- Keep each handoff under ~10 lines; link to code rather than pasting it
```
