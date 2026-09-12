# File Templates

All three files live in `docs/plan/`. Keep them terse — these files get read at the start of every session, so every unnecessary line costs tokens forever.

Adapt the sections to the project. Omit irrelevant stack fields and empty optional sections.

## SPEC.md

```markdown
# <Project Name> — Spec

## Positioning
One sentence: what it is, who it's for.

## Requirements
- R1: <must-have requirement>
- R2: ...

## Future ideas
- See PLAN.md Backlog: B1, ... (optional links; details live there)

## Out of scope
- <agreed exclusions>

## Tech stack
- Backend:
- Frontend:
- Database:
- Infra/deploy:
- Testing:

## Constraints
- ...

## Decisions and assumptions
- <date>: chose X over Y because Z. Source: <user / codebase / agent default>.

## Open questions
- <unresolved decision> — affects M<N>; resolve before <dependent work>.
```

## PLAN.md

```markdown
# <Project Name> — Implementation Plan

Modules in dependency order. Each module fits within a session; a session can cover multiple modules when requested.

## M1: <name> [S|M|L]
- Type: feature | enhancement | bug | maintenance | documentation | investigation
- Source/intent: <user request or linked B-ID; implement, investigate, or plan>
- Goal: <one line>
- Covers: R1, R3
- Files: <paths to create/modify>
- Acceptance: <objective check — "dotnet build passes and GET /health returns 200">
- Depends on: —

## M2: <name> [S|M|L]
...

## Integrated verification
- <check the core user flow across completed modules; include command or manual steps and expected result>

## Backlog

### B1: <idea or task>
- Type: <work type; investigation if the topic is not yet defined>
- State: draft | deferred | ready | promoted | dropped
- Source/intent: <date, user request or AI proposal>; <capture for later, refine only, etc.>
- Problem/outcome: <what is missing and the desired result>
- Related: <module, requirement, or other backlog IDs, if known>
- Scope/acceptance: <known boundaries and success checks; omit if not yet developed>
- Open questions/next step: <what needs clarification or what would trigger reconsideration>
- Notes: <analysis, decisions, assumptions; for promotion, date and M-ID links>

## Change log
- <date>: split M4 into M4a/M4b because ... (empty at creation)
```

Module sizing guidance:
- S: single concern, few files (a config setup, one endpoint)
- M: one vertical slice (endpoint + data layer + test) — the ideal default
- L: too big — split it before writing the plan

Typical first modules for greenfield projects: M1 = repo scaffold + build pipeline + hello-world runnable, M2 = data layer/schema, then vertical slices. Adjust to the project; don't force this shape.

### Follow-up work item in PLAN.md

Append a new module or submodule without renumbering existing items. Use this compact form for a small change; use the full module form and split the work when larger. A child item does not overwrite its parent's completed history.

```markdown
## M3.1: Fix duplicate submissions [S]
- Type: bug
- Source: <date and user report or issue reference>; requested scope: implement fix
- Related: M3; covers R2 (one record per submission)
- Behavior: repeated clicks create duplicates; expected: one record
- Scope/files: <affected flow and paths>; includes supporting tests and documentation
- Acceptance: <reproduction steps no longer produce duplicates; relevant regression check passes>
- Depends on: M3
```

For enhancements/features, describe current and desired behavior and link to added or revised requirements. Put proposed or deferred work in Backlog. For an active investigation, specify the question and expected evidence/deliverable as acceptance; completion does not imply a fix was implemented. Read `work-intake.md` for types, triage, and promotion rules.

For bug entries, add a compact triage note with expected/actual behavior, reproduction steps, environment, evidence/reproduction status, impact/severity, and the next diagnostic or verification step. Mark unknowns rather than inventing details. Backlog-only reports can defer reproduction.

## PROGRESS.md

```markdown
# <Project Name> — Progress

## Status
- [x] M1: scaffold — done 2026-07-07
- [ ] M2: data layer — in progress
- [ ] M3: ...
- [ ] M3.1: fix duplicate submissions — pending (bug; follow-up to M3)

## Next action
- <module, file or command, and concrete next step>

## Blockers
- <module>: <what is blocked, what resolves it, and any independent work that can continue>

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
- Verification: <command and outcome, or checks still pending>
```

Handoff rules:
- Written at module completion (or at mid-module stop), never reconstructed later
- Decisions and gotchas matter most — they're the things a fresh session can't infer from the code
- Keep each handoff under ~10 lines; link to code rather than pasting it
- Use the same module/submodule ID in PLAN.md, status, and handoffs, including follow-up bugs and enhancements
