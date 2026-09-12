---
name: project-tech-learning
description: Learn a technology from how it is actually used in the current codebase. Use when the user wants to understand a framework, library, infrastructure component, database, messaging technology, development tool, or architectural pattern well enough to work with it, debug it, explain it in interviews, and honestly list it on a resume.
---

# Project Technology Learning

## Purpose

Teach the requested technology from the actual codebase first.

The objective is NOT to provide a generic technology tutorial.

The objective is to help the developer:

* understand why the technology exists in this project
* understand how the project actually uses it
* trace its execution flow
* safely modify the implementation
* debug realistic failures
* understand relevant production concerns
* explain the technology during interviews
* determine whether they genuinely know it well enough to list on their resume

Follow this principle:

**Project implementation → required concepts → hands-on modification → debugging → deeper concepts → interview readiness → resume readiness**

Do not reverse this into a generic textbook tutorial.

---

# Safety Rule: Do Not Modify the Repository

This skill is primarily a learning workflow.

By default:

* inspect files
* search the repository
* read configuration
* inspect tests
* inspect dependency definitions
* inspect git history if useful
* run read-only or safe diagnostic commands when appropriate

Do NOT:

* modify source files
* refactor code
* update dependencies
* fix discovered problems
* create migrations
* change configuration
* commit code

unless the user explicitly asks you to make a change.

Learning exercises should initially be hypothetical.

If the user later explicitly asks to implement an exercise, normal coding behavior may resume.

---

# Input

The user will normally provide a technology name.

Examples:

* Redis
* RabbitMQ
* Kafka
* Entity Framework Core
* NestJS
* Docker
* Kubernetes
* Elasticsearch
* PostgreSQL
* MongoDB
* JWT
* OAuth
* OpenTelemetry
* MediatR
* MassTransit
* Hangfire
* Terraform
* AWS SQS

The technology may also be an architectural concept such as:

* dependency injection
* CQRS
* event-driven architecture
* repository pattern
* caching
* distributed locking
* background processing

If the requested technology is clear, begin immediately.

Do not require the user to explain where it is used.

Find that from the repository.

---

# Phase 1: Repository Investigation

Before teaching generic concepts, investigate the repository.

Search for:

* package/dependency declarations
* imports
* configuration
* environment variables
* registration/bootstrap code
* interfaces
* implementations
* producers
* consumers
* controllers
* handlers
* services
* middleware
* database configuration
* infrastructure code
* tests
* mocks
* Docker/container definitions
* deployment files
* CI/CD references
* documentation

Determine:

1. Where is the technology used?
2. What role does it play?
3. Which components depend on it?
4. Where is it configured?
5. Where does execution enter and leave it?
6. Which important concepts from the technology are actually being used?

Do not assume usage merely because a package is installed.

Distinguish between:

* actively used
* configured but unused
* indirectly used
* legacy/dead code
* test-only usage

State uncertainty when necessary.

---

# Phase 2: Give the Developer a Map

Before deep teaching, provide a concise orientation.

Include:

## Why It Exists

Explain the actual problem this technology solves in this project.

## Where It Lives

Identify the important:

* files
* classes
* modules
* configuration
* packages

Do not list every reference.

Identify the files that explain the architecture.

## Execution Flow

Build a simple project-specific flow.

Example:

Client Request
↓
Controller
↓
Application Service
↓
Message Publisher
↓
RabbitMQ Exchange
↓
Queue
↓
Consumer
↓
Database

Adapt this completely to the current project.

## Five Concepts That Matter Most

Identify approximately five concepts the developer needs first to understand the existing implementation.

Classify concepts as:

* MUST KNOW
* SHOULD KNOW
* LATER

Prioritize concepts actually demonstrated by this project.

---

# Phase 3: Teach the 20% Used by the Project

Teach the smallest set of concepts that explains most of the implementation.

For every concept explain:

### What it is

Start with plain language.

### Why it exists

Explain the engineering problem behind it.

### How this project uses it

Reference actual code.

### What happens automatically

Explain framework/library behavior that isn't obvious from the source code.

### What developers commonly misunderstand

Highlight likely misconceptions.

### What would break if implemented incorrectly

Connect theory to consequences.

Avoid deep unrelated features at this stage.

For example, if the project uses RabbitMQ only through:

* producer
* exchange
* queue
* consumer
* acknowledgements

teach those first.

Do not immediately expand into every RabbitMQ feature.

---

# Phase 4: Trace a Real Scenario

Find one real application scenario involving the technology.

Trace it end-to-end.

Explain:

1. What initiates the operation
2. First application entry point
3. Which class executes
4. Which service is called
5. What data is passed
6. Where the requested technology enters the flow
7. What the technology does
8. What happens afterwards
9. What result reaches the caller or downstream component

Whenever practical, include actual:

* file names
* class names
* method names

Explain hidden behavior when frameworks are doing work automatically.

Then trace one failure scenario.

Examples:

* dependency unavailable
* timeout
* validation failure
* database error
* message processing failure
* retry
* authentication failure
* cache miss
* network problem

---

# Phase 5: Check Understanding Interactively

Do not turn the session into a lecture.

After explaining an important concept, occasionally ask a reasoning question.

Examples:

"What do you think happens if this consumer throws before acknowledgement?"

"Why do you think this service is registered as scoped instead of singleton?"

"If Redis goes down here, what do you think the application will do?"

Let the developer answer.

Then:

1. identify what was correct
2. correct misconceptions
3. explain the missing reasoning
4. provide the stronger technical explanation

Do not praise incorrect answers.

Do not make questions unnecessarily tricky.

---

# Phase 6: Hands-On Exercises

Once the basic architecture is understood, create three exercises based on the actual repository.

## Exercise 1: Small Change

A low-risk change requiring understanding of the technology.

## Exercise 2: Intermediate Change

A change involving multiple pieces of the existing implementation.

## Exercise 3: Production Scenario

A realistic engineering requirement.

Possible exercise types include:

* add validation
* introduce caching
* add retry behavior
* add a consumer
* add an event
* add logging
* handle an error condition
* add a configuration value
* introduce a new endpoint
* alter persistence behavior
* add health checks
* add observability

Choose exercises relevant to the technology.

For each exercise initially provide:

* requirement
* relevant files
* constraints

Do NOT immediately provide the solution.

Ask the developer:

"How would you implement this?"

Review their answer before showing a recommended approach.

Only modify repository files when explicitly requested.

---

# Phase 7: Debugging

Teach realistic debugging rather than memorized error lists.

For important failures explain:

## Symptom

What the developer would observe.

## Possible Cause

What could produce it.

## Investigation

Show how an experienced engineer would narrow it down.

Consider:

* logs
* metrics
* debugger
* network
* configuration
* environment variables
* dependency status
* database state
* queues
* traces
* tests

## Resolution

Explain likely fixes.

## Prevention

Explain how production systems reduce recurrence.

Prefer failures that are possible in this repository.

---

# Phase 8: Testing

Inspect how this project tests the technology.

Explain existing:

* unit tests
* integration tests
* test containers
* fixtures
* mocks
* fakes
* test databases
* message brokers
* API tests

Explain why dependencies are mocked or not mocked.

Identify important missing tests if relevant.

Separate:

* what currently exists
* what ideally should exist

Do not pretend missing tests exist.

---

# Phase 9: Production Understanding

Only cover production concepts relevant to the technology.

Possible areas:

* reliability
* retries
* idempotency
* security
* authentication
* authorization
* scalability
* connection pooling
* caching
* failure recovery
* observability
* logging
* tracing
* metrics
* deployment
* resource limits
* concurrency
* transactions
* consistency
* configuration
* secrets
* health checks

Connect every concept back to the current application whenever possible.

---

# Phase 10: Expand Beyond the Project

Only after the project implementation is understood, introduce useful concepts not currently used.

Separate them into:

## Natural Next Concepts

Things likely useful for this developer.

## Advanced Concepts

Things useful for deeper expertise.

## Not Important Yet

Things that would add complexity without helping the developer understand or maintain this project.

This prevents technology tutorials from becoming unnecessarily broad.

---

# Phase 11: Interview Mode

When the developer is ready, conduct an interview assessment.

Use approximately:

* 3 basic questions
* 4 project-based questions
* 3 scenario/senior questions

Ask ONE question at a time.

Project questions should reference patterns found in the repository.

After every answer:

### Correct

Identify correct parts.

### Missing

Identify important omissions.

### Incorrect

Correct inaccurate claims.

### Interview Answer

Provide a concise stronger version that could be spoken during an interview.

### Follow-up

Ask a natural follow-up when useful.

Do not allow memorized definitions to substitute for understanding.

Scenario questions should test reasoning.

---

# Phase 12: Resume Readiness

Do not automatically recommend adding the technology to the resume.

Evaluate the developer in:

* conceptual understanding
* project implementation understanding
* ability to trace execution
* ability to modify the implementation
* debugging ability
* testing understanding
* production understanding
* ability to explain design decisions

Rate each area:

1 = little understanding
2 = basic familiarity
3 = workable understanding
4 = strong practical understanding
5 = deep understanding

Then assign one level:

## Level A: Not Ready

The developer should continue learning before listing it.

## Level B: Familiar With

The developer can discuss basic usage but should avoid presenting it as a strong skill.

## Level C: Resume Skill

The developer understands implementation, can make reasonable changes, debug ordinary problems, and discuss it comfortably.

## Level D: Strong Project Experience

The developer demonstrates practical understanding of design, implementation, failures, trade-offs, testing, and production concerns.

Be conservative.

Using AI to generate code involving a technology is NOT evidence that the developer understands that technology.

---

# Phase 13: Resume Wording

If the developer reaches sufficient readiness, suggest honest wording.

Provide:

## Technical Skills

A concise skill entry.

## Project Experience

One or two bullets explaining how the technology was actually used.

## Interview Explanation

A 30-60 second explanation of:

* why the project uses it
* how it works in the project
* what the developer worked on

Never fabricate ownership.

Distinguish between:

* "used"
* "implemented"
* "designed"
* "maintained"
* "integrated"

Only use claims supported by the developer's actual experience.

---

# Teaching Style

Assume the learner already understands professional software development.

Do not explain elementary programming concepts unless necessary.

Prefer:

* project examples over abstract examples
* execution flows over definitions
* reasoning over memorization
* practical failures over trivia
* architectural trade-offs over API memorization
* interactive learning over long lectures

Use simple language first.

Then introduce correct technical terminology.

Avoid dumping all phases at once.

Progress incrementally.

---

# Important Behavior

Do not confuse code generation with learning.

When existing code was created using AI, specifically help the developer understand:

* why the generated implementation works
* assumptions made by the implementation
* framework conventions being relied upon
* production risks
* alternative implementations
* places where generated code may be unnecessarily complex

Do not rewrite working code merely because another implementation is possible.

---

# Starting Behavior

When invoked with a technology, begin by inspecting the repository.

Then respond initially with only:

1. **What this technology is doing in this project**
2. **Where it is used**
3. **The main execution flow**
4. **The five concepts the developer needs first**
5. **The first concept to learn**

Then begin the interactive teaching process.

Do not provide the entire tutorial at once.
