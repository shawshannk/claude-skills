# Requirements Guide

Considerations for Phase 1. Use the brief, documentation, and code to answer these where possible. Ask only about gaps that affect important decisions or the next step; omit irrelevant topics and record assumptions explicitly.

## 1. Purpose and users

- What does this project do, in one sentence?
- Who uses it? (an individual, a team, public users, another system)
- What is the intended use: experiment, internal tool, or production service? Match testing and operational requirements to that use.

## 2. Functional requirements

- What are the 3-5 core flows? Walk through the main one step by step.
- For each flow: what's the input, what's the output, what can go wrong?
- Which requirements are needed for the first release, and which can wait? Preserve priorities already provided by the user.
- Any existing system this replaces or integrates with?

## 3. Out of scope

- What is this explicitly NOT? (not multi-tenant, no auth in v1, no mobile, etc.)
- Record the agreed exclusions in SPEC.md; distinguish them from proposed deferrals.

## 4. Tech stack

Use the existing stack and conventions when available. For a new project, clarify consequential preferences and choose reasonable defaults for routine details:

- Language and framework for backend? For frontend (if any)?
- Database? (relational vs document vs none — and why, if they have a reason)
- Where does it run? (local only, Docker, cloud provider, serverless)
- Testing expectations? (unit tests per module, integration tests, none for a spike)
- Package/build tooling preferences?
- Any library the user specifically wants to use or avoid?

Record consequential choices and their rationale in SPEC.md under "Decisions and assumptions". Distinguish user choices, codebase facts, and agent-selected defaults.

## 5. Constraints

- Deadline or time budget?
- Cost constraints? (free tier only, existing cloud account)
- Existing code or repo to build inside?
- Anything the user already tried that didn't work?
- Where relevant: access control, sensitive data, performance, accessibility, or compatibility requirements that affect architecture or acceptance checks?
- External services or credentials needed, and whether a local substitute can unblock development? Record setup requirements without secret values.

## When to stop

Start planning when scope and the first architectural choices are clear enough. Record unresolved items with the module they affect; only block work that depends on an answer. Details that only affect one later module can wait until that module.
