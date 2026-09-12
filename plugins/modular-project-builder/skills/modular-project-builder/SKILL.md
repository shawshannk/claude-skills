---
name: modular-project-builder
description: Plan, build, and maintain projects with persistent specs, modular plans, progress notes, and a backlog. Use when starting a substantial build, resuming implementation, or analyzing and tracking ideas, bugs, enhancements, and new features in a project tracked in docs/plan/. Keep small tracked tasks lightweight; plan files alone do not require this workflow for unrelated tasks.
---

# Modular Project Builder

Turn a project idea into three persistent files (SPEC, PLAN, PROGRESS), then implement the plan module by module across multiple sessions. The files on disk are the memory. Each session should be able to start fresh, read those three files plus the current module's code, and continue with zero archaeology of old conversations.

## Why this exists

Long build conversations exhaust context. The fix is not "be brief" but externalize state: requirements and decisions live in files, not chat history. A new session that reads `docs/plan/` knows everything it needs. Treat updating those files as part of the work, not an afterthought — a module is not done until PROGRESS.md says what happened.

## Phase 0: Detect state (always do this first)

Inspect the existing project instructions, working-tree changes, and any files in `docs/plan/` before choosing a starting point.

- **Existing tracked project with a new topic, idea, issue, or change request** → use Work intake below, even if all original modules are done. Recover any missing plan state first.
- **Plan and progress exist, with no new request** → resume at Phase 3. If all work is done, report that state; do not invent another module.
- **Only some plan files exist** → read and preserve them, reconstruct the missing state from the code and available context, and ask only about unresolved decisions that block progress.
- **No plan files exist** → start at Phase 1, using the existing code and documentation as context if this is an established project.

For an explicit re-plan or restart, revise within the requested scope and retain useful decisions and completed-work history. Do not discard existing work without authorization.

After identifying the target project, assign or reuse a work-item ID before substantive project work, including investigation, planning, implementation, tests, configuration, and documentation. Initial inspection and the act of creating/updating tracking records belong to that intake and do not need recursive work items. For a new project, create a minimal planning item when establishing `docs/plan/`, then refine it with the plan. Related supporting edits share an item; unrelated user changes are not claimed as this skill's work.

## Phase 1: Understand the project

Goal: enough clarity to write SPEC.md. Not a full BRD — just what's needed to decide modules and make the first architectural calls.

Read the user's brief, relevant documentation, and existing code first. Reuse established requirements, stack, and conventions. Do not import preferences from unrelated projects.

Identify purpose and users, core flows, scope, stack, and constraints. Use `references/requirements-guide.md` when requirements need further clarification; it is a checklist of considerations, not a required question sequence.

Ask only when a missing answer materially affects scope, architecture, or the next implementation step. Keep related questions brief. Make reasonable reversible choices for routine details and record consequential assumptions and decisions in SPEC.md. Do not present assumptions as user requirements. Defer questions that only affect later modules.

## Phase 2: Write the plan files

Create `docs/plan/` with three files. Templates are in `references/templates.md` — read that file before writing them.

- **SPEC.md** — what and why. Requirements (numbered R1, R2...), stack, constraints, out-of-scope. Update when intended behavior or scope changes.
- **PLAN.md** — how. Modules (numbered M1, M2...) in dependency order. Each module has: goal, files it will touch/create, acceptance criteria (how we know it's done — build passes, specific test, manual check), and estimated size (S/M/L). Modules should be sized so one module fits comfortably in one session: roughly "one coherent vertical slice or one infrastructure concern". If a module feels L, split it.
- **Backlog section in PLAN.md** — deferred ideas, topics, bugs, and changes, with stable B1, B2... IDs, type, intent, refinement state, and open questions. Backlog entries are outside the active implementation queue.
- **PROGRESS.md** — state. Module checklist with status (pending / in-progress / blocked / done), the next action, plus a per-module handoff log written at completion or interruption.

Map each must-have requirement to a module and an observable acceptance check. Include a final integrated check of the core user flow so individually completed modules also work together.

Present the module breakdown. If the user requested implementation, proceed within that scope; do not add a separate approval gate. If they asked only for planning or explicitly required review before coding, stop at that boundary. Resolve material scope ambiguities before implementing the affected work.

## Work intake: Analyze, clarify, and record

Use this flow for every new project topic, idea, bug, enhancement, feature, module, or backlog request. Read `references/work-intake.md` for the type definitions, Q&A workflow, bug triage, and backlog lifecycle. Apply the same analysis and clarification principles during initial project planning.

- **Analyze first:** examine relevant evidence, existing items, feasibility, scope, dependencies, and conflicts. Triage bugs before prescribing a fix. Scale the effort to the request; a quick backlog capture does not require a full investigation.
- **Clarify collaboratively:** for vague requests, propose a concrete interpretation and ask focused questions that affect the outcome. Use answers to develop scope and acceptance checks, keeping assumptions visible. A sufficiently clear request can proceed without a forced Q&A round or repeated approval.
- **Record and route:** every task has an ID and type. Modules/submodules organize active work; backlog is a holding section, not a work type. Finalize the item after needed clarification, or preserve a draft with unresolved questions. “Not now” stays in the backlog. Follow Phase 4 only for authorized execution; investigation or discussion does not authorize the resulting implementation.
- **Keep records consistent:** PLAN.md owns scope and acceptance, PROGRESS.md owns active status and handoffs, and SPEC.md changes only when intended behavior, scope, or constraints change. Preserve IDs, completed history, and the reason for revised requirements.

## Phase 3: Resume session

1. Read SPEC.md, PLAN.md, PROGRESS.md and inspect the working tree. Check the current module's recorded state against its code and relevant checks; preserve unrelated user changes. Read the listed files and handoff references first, expanding to dependencies when needed. Reconcile stale notes before relying on them.
2. Give the user a 3-5 line status summary: modules done, what's next, any open issues flagged in the last handoff.
3. Continue the current incomplete module or the next module whose dependencies are satisfied, following the user's requested scope. Include follow-up work items; do not automatically start proposed or deferred work. For a blocked module, record the blocker and continue independent authorized work when possible.

## Phase 4: Implement a module

1. Follow the session scope already given. A request for a specific module ends there; a request to complete the build can span multiple modules. Do not ask the user to restate authorization each session or module.
2. Implement the module. Follow the acceptance criteria in PLAN.md as the definition of done.
3. **Verify**: perform the checks named in the acceptance criteria. For implementation, run the relevant build/tests or manual checks; for investigation or planning, verify the agreed findings or deliverable and record unresolved uncertainty. Investigation can be complete without the investigated bug being fixed. Use a regression test for a bug when practical and proportionate, and check affected integrations as needed.
4. **Write the handoff** in PROGRESS.md before declaring the module complete:
   - Status → done, with date
   - Files created/modified
   - Key decisions made and why (especially deviations from PLAN.md)
   - Gotchas or open issues the next session must know
   - Verification commands and outcomes, including failed or unrun checks
   - For interrupted or blocked work: completed pieces, remaining work, blocker, and the exact next action
   - Anything that changed in PLAN.md as a result (update PLAN.md too if module scope shifted)
5. Report to the user: what was built, what was verified, what's next. Continue while authorized work remains and dependencies permit it; otherwise stop with a clear handoff.

If context is getting long mid-module, finish the smallest coherent piece, write an honest in-progress handoff ("M4 half done: X works, Y not started, resume at file Z"), and tell the user this is a good point to start a fresh session.

## Rules that hold across all phases

- Respect planning-only requests and explicit review gates. Never mark a module done without its acceptance checks passing; an unavailable check remains an open verification item.
- Implement one module at a time, within the user's requested scope.
- Explain consequential tradeoffs and propose alternatives when they improve the outcome; preserve the user's explicit choices.
- PLAN.md is living: if reality diverges (a module splits, a dependency appears), update it and note the change in PROGRESS.md. Stale plans are worse than no plans.
- Before declaring requested work complete, check that all project tasks and edits made by this skill are accounted for by work-item IDs and outcomes, including analysis-only work. Use backlog notes for intake/refinement and PROGRESS.md handoffs for active work.
- Keep `docs/plan/` suitable for version control; record configuration names and setup needs, never secret values. Follow the repository's commit workflow and the user's instructions.
