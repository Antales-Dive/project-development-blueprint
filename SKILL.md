---
name: project-development-blueprint
description: Analyze business requirements and an existing codebase (or design from requirements alone), then produce an implementation-ready project development blueprint with guided requirement clarification, architecture, technology choices, file-level tasks, module contracts, change impact, staged coding prompts, testing, deployment, and acceptance criteria. Use when another developer or coding model must be able to build the project from the document without inventing key decisions. Do not use for a code-only explanation, a small mechanical edit, or implementation of an already-approved plan.
---

# Project Development Blueprint

Turn requirements into an implementation-ready development blueprint. The deliverable is a design and execution reference for another coding model, not source code. Default language follows the user's language; preserve exact code identifiers, paths, commands, and API names.

## Design operating model

Use three connected layers and keep the handoff between them explicit:

1. **Requirement translation**: convert the user's language, repository evidence, and constraints into structured goals, actors, scenarios, inputs, outputs, scope, data, risks, deployment context, UI language/style, assumptions, and unknowns.
2. **Architecture design**: convert the confirmed requirements into responsibility-complete components with high cohesion, low coupling, explicit contracts, data flow, ownership, failure boundaries, security/configuration boundaries, and justified extension points.
3. **LLM execution handoff**: convert the accepted architecture into ordered coding tasks or staged prompts with exact files, prerequisites, forbidden actions, acceptance criteria, run checks, and a stop condition when checks fail.

Do not skip from a vague idea directly to implementation tasks. For an AI-powered feature, also specify the real provider path, prompt ownership, output schema, parsing, provider error mapping, and secret boundary. Empty, loading, error, and missing-configuration states are valid; fabricated analysis results are not.

For a new or materially ambiguous project, use a guided clarification loop. Ask one high-impact question at a time, preferably with a small set of meaningful choices explained in plain language. Skip questions already answered by the user or repository, do not repeat a question, and do not turn the process into a long questionnaire. When the remaining choices materially affect scope, architecture, safety, cost, compatibility, or acceptance, present a compact requirement confirmation draft before finalizing the blueprint.

Read [guided-design-and-execution.md](references/guided-design-and-execution.md) when the request is ambiguous, AI-powered, intended for another coding model, or large enough to require staged delivery.

## Operating boundary

- Generate and save documentation only. Do not modify business code, create migrations, deploy, commit, or change external systems unless the user separately requests implementation.
- Inspect the repository and its documentation conventions when a repository is available. If no convention exists, use `docs/implementation/`.
- Never invent business rules, compliance obligations, SLAs, pricing, retention, or priority from code. Mark them as assumptions or pending decisions.
- Separate every important claim into `VERIFIED`, `INFERENCE`, or `UNKNOWN`.
- Ask only questions whose answers materially change scope, architecture, safety, cost, compatibility, or acceptance. Continue with clearly labeled assumptions when safe.
- Treat enterprise-grade as evidence-driven completeness, not automatic distributed-system complexity. Cover operational, security, data, compatibility, and recovery responsibilities that the accepted scope requires; add microservices, queues, complex identity, workflow engines, or other infrastructure only when a committed consumer, scale/risk constraint, or explicit requirement justifies it.

## Select the analysis mode

1. **Existing-project mode**: a repository or codebase is present. Read the project guide, directory tree, package manifests, entry points, configuration, schemas/migrations, API definitions, tests, and relevant recent changes. Describe current behavior before proposing changes.
2. **Greenfield mode**: no useful codebase is present. Derive a minimum sufficient architecture from the requirements and constraints. Explain technology choices and assumptions.
3. **Hybrid mode**: a partial repository exists but the requested capability is new. Treat existing code as verified context and design only the missing slice.

Record the selected mode in the document. Do not assume that a familiar framework is already in use.

## Required analysis gates

### 1. Establish the outcome

State the user-visible or system-observable problem, desired outcome, affected actors, core scenarios, in-scope behavior, out-of-scope behavior, and success metrics. Check whether existing behavior, configuration, or operating procedure already satisfies the outcome.

### 2. Map current and target architecture

For existing projects, include relevant directory structure, runtime entry points, module boundaries, dependency direction, data flow, persistence, external integrations, and test/deploy commands. For all projects, define target components and their responsibilities, interfaces, ownership, lifecycle, and failure boundaries. Generate Mermaid diagrams only when cross-module relationships or data flow would otherwise be difficult to understand.

### 3. Maintain a consumer ledger

For every proposed module, service, table, field, event, API, configuration item, or abstraction, name:

- producer or lifecycle owner;
- committed consumer in the accepted slice;
- behavior or decision changed by consumption;
- reachable production-to-consumption path;
- absence test: what accepted behavior fails if it is removed.

Remove or defer additions that have no real consumer. Treat public or external contracts as compatibility boundaries even when no repository caller is visible.

### 4. Define module contracts and future change impact

For every core module, include:

- responsibility and non-responsibility;
- input and output structures;
- public methods, components, routes, or events;
- hidden implementation details;
- allowed dependencies and ownership;
- extension points with a real likely consumer;
- focused tests and run checks.

For each important reserved feature, state which modules change, which must not change, which interfaces or data structures extend, and why the accepted design supports the change. Do not reserve speculative abstractions merely because they are technically possible.

### 5. Choose the smallest sufficient solution

Evaluate, in order: no change; documentation/configuration/process; reuse existing capability; local behavior fix; extension of an existing abstraction; new abstraction; new subsystem or migration. Recommend one option, explain trade-offs, and explicitly reject speculative scope. Prefer independently reversible slices.

### 6. Specify consequences and verification

Cover only applicable dimensions, but do not silently omit them: callers, API/data/event/UI contracts, authorization and privacy, persistence and migrations, retries/idempotency/concurrency, compatibility and performance, operations/observability, deployment, and rollback. Distinguish restored application state from external side effects that cannot be undone.

Every acceptance criterion must contain a scenario, trigger, observable expected result, meaningful prohibited side effect, verification method, safety/environment constraint when relevant, and priority. Replace vague terms such as "correctly", "securely", or "fast" with evidence or label them as human judgment.

## Choose the output shape

Use the smallest shape that remains implementation-ready:

- **Small project**: use [small-project-template.md](references/small-project-template.md) and produce one complete Markdown document when the work has few components, no cross-service contract, and a short independently testable task list.
- **Medium or large project**: use [large-project-template.md](references/large-project-template.md) and split the deliverable when there are multiple deployable components, persistence/API contracts, migrations, several actors, or enough tasks that one file would be hard to navigate.

Do not split documents merely for appearance. In a split deliverable, create an index and link every document and task dependency.

## Implementation-ready detail

The blueprint must let a separate coding model start without making architectural decisions. Include, where applicable:

- product goal and final-state behavior;
- functional and non-functional requirements;
- actors, permissions, business rules, assumptions, and pending decisions;
- current architecture and target architecture;
- selected frameworks, libraries, versions or compatibility ranges, and selection rationale;
- module/file/directory ownership and exact change locations;
- API routes, methods, auth, request/response fields, errors, pagination, idempotency, and compatibility policy;
- tables/collections, fields, types, constraints, indexes, relationships, migration/backfill/rollback;
- configuration and environment variables using placeholders only;
- state transitions, validation, error handling, retries, concurrency, logging, metrics, traces, and alerts;
- UI language, UI style, empty/loading/error states, accessibility implications, and i18n boundaries when a user interface exists;
- for AI features: prompt ownership, model/provider adapter boundary, structured output schema, parsing failures, provider fallback policy, and explicit prohibition of fake runtime results;
- a responsibility-complete but appropriately simple architecture explanation, including excluded complexity and the evidence required before adding it;
- ordered implementation tasks with prerequisites, concrete files, completion criteria, and tests;
- local commands, CI checks, deployment steps, smoke checks, rollback, and operational handoff;
- acceptance criteria and a verification matrix mapped to tasks.

## Coding-model handoff

When the blueprint will be handed to an AI coding tool, include both a master implementation brief and staged execution prompts when useful. Each stage must name its goal, prerequisites, exact changed files, implementation constraints, acceptance criteria, run-check commands, self-checks, and completion report. The coding model must stop and report when a required check fails instead of silently proceeding. Keep the blueprint authoritative; prompts are an execution view, not a second source of truth.

## Quality gate before delivery

Before returning the document:

1. Reconcile requirements, architecture, API, data model, and task list; fix contradictions.
2. Ensure every required behavior has an implementation location and verification method.
3. Ensure every proposed addition has a named consumer and an absence test.
4. Scan for unmarked assumptions, `TBD`, `TODO`, vague claims, invented business rules, secrets, and production data.
5. For AI features, verify there is a real runtime provider path and no mock-result path presented as production behavior.
6. Verify every stage has a run check and an explicit failure stop condition when staged prompts are included.
7. State the final verdict: `IMPLEMENTABLE`, `REDUCE_SCOPE`, `REVISE_DESIGN`, `NEEDS_EVIDENCE`, or `NO_CHANGE_NEEDED`.
8. List remaining uncertainty and the exact decision or evidence needed. Do not hide blockers inside prose.

The final response should link the generated document(s), summarize the verdict and blockers, and state that no project code was changed.
