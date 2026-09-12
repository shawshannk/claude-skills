# Work Intake and Backlog

Read when a user introduces a project topic, idea, issue, change, or deferred request. Use this workflow during initial planning too. Keep detail proportional to the task.

## Work model

Every project task has an ID, a type, requested scope, and a recorded outcome or next action. Structure and type are separate:

- **Module (`M8`)**: a coherent unit of active planned work.
- **Submodule (`M3.1`)**: a bounded child or follow-up linked to a module. It uses the same type and acceptance fields as a module.
- **Backlog item (`B4`)**: a candidate or deferred task in PLAN.md's Backlog section. It can have any work type; being recorded or fully specified does not authorize execution.

| Type | Use for |
| --- | --- |
| feature | A new user or system capability. |
| enhancement | An improvement or extension to an existing capability. |
| bug | Behavior that differs from the intended behavior; label unverified reports as suspected. |
| maintenance | Refactoring, dependency updates, tooling, or operational upkeep. |
| documentation | A standalone documentation or guidance deliverable. |
| investigation | Research, diagnosis, design/planning, or a topic whose outcome needs exploration. |

Infer the type and placement and explain the choice briefly; do not ask the user to choose administrative labels. Tests and documentation supporting a feature or fix belong to its item. Use investigation for an unformed topic until its purpose is clearer; record a type revision if later evidence changes the classification. Split separately actionable outcomes into linked items, rather than creating an item for each file or question.

## Analyze and refine with the user

1. **Capture intent and reuse context.** Determine whether the user wants execution now, investigation, discussion, or capture for later. Search existing modules and backlog for overlapping work; enrich the matching item instead of silently duplicating it. Preserve the new report's source and any changed intent. Assign a draft ID before substantive work; refine that record after Q&A.
2. **Scrutinize the request.** Read relevant code and requirements. Identify the underlying problem, affected users/flows, present versus desired behavior, feasibility, dependencies, and material tradeoffs. Explain unsupported assumptions or conflicts and offer a useful alternative when appropriate. Distinguish evidence from hypotheses.
3. **Ask focused questions when needed.** For vague ideas, propose a concrete interpretation or a few meaningful options, then ask about the decisions that change scope or success. Prefer short related batches, reuse answers already given, and avoid a fixed questionnaire. AI should develop the details with the user rather than require the user to write the specification. A request to capture a rough idea can be recorded immediately with open questions for later.
4. **Synthesize the item.** Turn the answers into the problem, desired outcome, included/excluded scope, affected requirements/modules, dependencies, and observable acceptance checks. Mark agent proposals and unresolved assumptions explicitly. Share the resulting interpretation so the user can correct it. Keep unanswered consequential questions as blockers to dependent execution; do not treat silence as agreement.
5. **Route by intent.** Clear execution requests proceed within their scope. Ask for a decision only if expected behavior is unclear, requirements conflict ambiguously, or a consequential choice exceeds authorization. A clear request revising an earlier requirement needs no extra approval. Discussion, analysis, and backlog capture end with recorded findings or a refined item, not automatic implementation. If intent itself is unclear, clarify it while continuing useful analysis.

## Bug triage

For a bug, capture expected versus actual behavior, reproduction steps, relevant environment/version, impact, and available evidence. Inspect the affected code and attempt reproduction within the requested scope. Record one of: reproduced, supported by evidence but not reproduced, or needs information. Do not claim a root cause until evidence supports it.

Assess severity from impact (for example, data loss versus a minor display issue); distinguish it from scheduling priority, which follows user direction. Identify affected modules and whether this is a regression or duplicate when evidence permits. Ask for missing reproduction details when they affect diagnosis. Propose the next diagnostic step or a bounded fix with acceptance checks. If expected behavior is a new preference rather than an established requirement, explain why enhancement may fit better.

A “record this bug for later” request gets lightweight triage from supplied evidence, with unperformed reproduction and open questions recorded. It does not authorize an extended investigation or a fix. Investigation findings can recommend linked implementation work; keep that work deferred unless authorized.

## Backlog lifecycle

Keep one Backlog section in PLAN.md; do not create a fourth required planning file. Each entry has a stable B-number, title, type, source/date, intent, summary, related items, and next refinement step. Add scope, acceptance, dependencies, and priority only when known or useful. Mark AI suggestions as proposals separately from user requests.

Use a refinement state:

- **draft**: captured, with material questions still open.
- **deferred**: understood enough to retain, intentionally not scheduled.
- **ready**: sufficiently specified for future execution; still not authorized to start.
- **promoted**: linked to active module/submodule IDs.
- **dropped**: retained with the reason it was dismissed or superseded.

“This should exist, but not now” goes here. Do not change active SPEC requirements or the active module queue merely because an idea is recorded. If SPEC has a future-ideas section, link to B-IDs instead of duplicating the backlog. Record lightweight analysis and refinement outcomes on the B-item itself; substantial explicitly requested research becomes a linked active investigation module while the feature remains deferred.

Promotion requires a user instruction that includes the item or an already agreed selection policy. Finishing active modules, a high severity, or a `ready` label alone does not promote it. On promotion, recheck the item against current code and requirements, resolve blocking questions, create or reuse the appropriate M-ID(s), and add active status in PROGRESS.md. Move the detailed execution scope to those modules and retain a B-ID summary with promotion date and links, so there is one current execution record and a preserved origin. Update SPEC only for an authorized change to intended behavior or scope.

Never renumber IDs or overwrite completed module history. A later fix or enhancement to a completed module gets a new related item. A general “continue” resumes authorized active work and leaves explicitly deferred backlog alone.
