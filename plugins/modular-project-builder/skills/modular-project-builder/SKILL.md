---
name: modular-project-builder
description: Interview-driven project builder that turns an idea into a persistent spec, a modular implementation plan, and then implements modules one session at a time so context/tokens never run out. Use this skill whenever the user wants to start building a new project, app, service, or sizable feature ("let's build X", "new project", "I have an idea for"), whenever they ask to resume or continue implementation of a planned project ("continue where we left off", "next module", "resume the build"), or whenever a docs/plan/ directory with SPEC.md, PLAN.md, or PROGRESS.md exists in the repo. Also use it when the user complains about running out of context mid-build and wants a structured way to split work across sessions.
---

# Modular Project Builder

Turn a project idea into three persistent files (SPEC, PLAN, PROGRESS), then implement the plan module by module across multiple sessions. The files on disk are the memory. Each session should be able to start fresh, read those three files plus the current module's code, and continue with zero archaeology of old conversations.

## Why this exists

Long build conversations exhaust context. The fix is not "be brief" but externalize state: requirements and decisions live in files, not chat history. A new session that reads `docs/plan/` knows everything it needs. Treat updating those files as part of the work, not an afterthought — a module is not done until PROGRESS.md says what happened.

## Phase 0: Detect state (always do this first)

Check whether `docs/plan/PROGRESS.md` exists in the repo.

- **Exists** → this is a RESUME session. Go to Phase 3.
- **Doesn't exist** → this is a NEW PROJECT session. Go to Phase 1.

If the user explicitly asks to re-plan or restart, confirm before overwriting any existing plan files.

## Phase 1: Requirements and stack interview

Goal: enough clarity to write SPEC.md. Not a full BRD — just what's needed to decide modules and make the first architectural calls.

**Two entry modes:**

**A. Project docs exist (README, design doc, uploaded spec).** Read them first. Extract everything you can: purpose, functional requirements, tech stack, constraints. Then present the extraction as a prefilled summary and ask for confirmation, e.g. "From your README I'm assuming: .NET 8 API, Next.js frontend, Postgres, deployed to AWS. Requirements R1..R5 as listed below. Confirm, correct, or add." Only ask about genuine gaps.

**B. No docs.** Interview from a blank slate. Do NOT assume a stack from prior conversations or user history — each project starts blank. Ask in small focused batches (2-3 related questions max per turn, never a wall of questions). Read `references/interview-guide.md` for the full question checklist. Cover, in order:

1. What the project does and who it's for (one-sentence positioning)
2. Functional requirements (core flows, must-have vs nice-to-have)
3. Explicit out-of-scope list (prevents scope creep in later sessions)
4. Tech stack (language, framework, DB, infra, testing) — ask, don't assume
5. Constraints (deadlines, existing code to integrate with, budget/free-tier requirements)

Stop interviewing when you can write every SPEC.md section without guessing. If the user says "just decide", make the call, but record it in SPEC.md under "Decisions made on user's behalf" so it's visible and reversible.

## Phase 2: Write the plan files and get approval

Create `docs/plan/` with three files. Templates are in `references/templates.md` — read that file before writing them.

- **SPEC.md** — what and why. Requirements (numbered R1, R2...), stack, constraints, out-of-scope. Changes rarely.
- **PLAN.md** — how. Modules (numbered M1, M2...) in dependency order. Each module has: goal, files it will touch/create, acceptance criteria (how we know it's done — build passes, specific test, manual check), and estimated size (S/M/L). Modules should be sized so one module fits comfortably in one session: roughly "one coherent vertical slice or one infrastructure concern". If a module feels L, split it.
- **PROGRESS.md** — state. Module checklist with status (pending / in-progress / done), plus a per-module handoff log written at completion time.

Present the module breakdown to the user and **get explicit approval before writing any code**. The user may reorder, merge, or split modules. Do not start M1 in the same breath as presenting the plan.

## Phase 3: Resume session

1. Read SPEC.md, PLAN.md, PROGRESS.md. Do not re-read the whole codebase — read only the files listed in the current/next module plus anything the handoff notes flag.
2. Give the user a 3-5 line status summary: modules done, what's next, any open issues flagged in the last handoff.
3. Confirm the next module (or let them pick a different one) before starting.

## Phase 4: Implement a module

1. **Ask session scope first, every session**: "How many modules this session — just M4, or keep going until you say stop?" Never assume. The user decides per session.
2. Implement the module. Follow the acceptance criteria in PLAN.md as the definition of done.
3. **Verify**: run the build, run the module's tests, or perform the manual check named in the acceptance criteria. A module that doesn't compile is not done.
4. **Write the handoff** in PROGRESS.md before declaring the module complete:
   - Status → done, with date
   - Files created/modified
   - Key decisions made and why (especially deviations from PLAN.md)
   - Gotchas or open issues the next session must know
   - Anything that changed in PLAN.md as a result (update PLAN.md too if module scope shifted)
5. Report to the user: what was built, what was verified, what's next. Then either continue (if they asked for multiple modules) or stop cleanly.

If context is getting long mid-module, finish the smallest coherent piece, write an honest in-progress handoff ("M4 half done: X works, Y not started, resume at file Z"), and tell the user this is a good point to start a fresh session.

## Rules that hold across all phases

- Never write code before the plan is approved. Never mark a module done without verification.
- One module at a time. Do not "quickly also do M5" unless the user asked for it this session.
- Keep answers honest: if a user requirement is a bad idea (wrong tool, unnecessary complexity), say so directly during the interview, propose the alternative, and let them decide.
- PLAN.md is living: if reality diverges (a module splits, a dependency appears), update it and note the change in PROGRESS.md. Stale plans are worse than no plans.
- Commit `docs/plan/` to git so the plan survives machine changes. Suggest committing after each module completes.
