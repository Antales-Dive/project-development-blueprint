# Guided Design and Execution

This reference combines guided architecture clarification with the evidence and delivery discipline of the project blueprint. It is especially useful for AI-powered applications, ambiguous greenfield requests, and plans intended for another coding model.

## 1. Guided requirement translation

Use plain-language questions and translate the answers into engineering decisions internally. Ask one primary question per turn, and ask only questions that can change the accepted scope or design. A useful sequence is:

1. project outcome and why it matters;
2. target users, roles, and primary workflow;
3. input types and output shape;
4. v1 capabilities and explicit exclusions;
5. later features that are likely enough to influence a boundary;
6. data objects, persistence, retention, and sensitive data;
7. deployment, availability, compatibility, and operating constraints;
8. UI language, style, accessibility, and localization needs;
9. technology constraints, coding tool, and team skill level;
10. for AI features, provider, model configuration, prompt ownership, output schema, and failure behavior.

Use A/B/C/D/E choices only when the choices are real and mutually meaningful. Do not ask architecture jargon such as "which service boundary do you want?" when the user can answer more naturally with a workflow or operating preference. Record answers once and mark unanswered items as `UNKNOWN` or as a labeled assumption.

When enough information has been collected, produce a requirement confirmation draft containing:

- understood outcome;
- actors and primary scenarios;
- in-scope and out-of-scope behavior;
- v1 versus later features;
- evidence, assumptions, unknowns, and decisions required;
- initial complexity assessment and the reason for any scope reduction.

Do not finalize architecture decisions that depend on unresolved high-impact items without either obtaining confirmation or clearly stating the consequence of the assumption.

## 2. Responsibility-complete, appropriately simple architecture

The architecture must cover every responsibility required by the accepted behavior, while its complexity must be justified by scale, risk, compliance, availability, team, or explicit requirements. A modular monolith is a valid default for a small or medium application, but it is not a rule that overrides evidence.

For a typical AI text or file workflow, consider these responsibility areas when applicable:

- page and application shell;
- user input and file constraints;
- validation and sensitive-data warnings;
- business-flow orchestration;
- prompt/template ownership;
- server-side provider client;
- output schema and result parsing;
- file extraction;
- result display and export/copy;
- configuration and secret handling;
- error presentation;
- persistence/history;
- language and style boundaries;
- observability and run checks.

Do not add an area merely because it appears on this list. Every addition must be recorded in the consumer ledger with an owner, committed consumer, reachable path, semantic effect, and absence test.

Explicitly reject complexity that has no evidence, such as microservices, message queues, distributed jobs, complex DDD, CQRS/event sourcing, plugin marketplaces, multi-tenant identity, payment infrastructure, generic wrapper layers, or unused dependencies. If an enterprise requirement does justify one, document the trigger, boundary, failure model, operational owner, and rollback plan.

## 3. Core module contract

Every core module gets a contract in the architecture or contracts document:

### Module: `<name>`

- **Responsibility**: what it owns.
- **Non-responsibility**: what it must not own.
- **Input**: exact structures, validation status, and source.
- **Output**: exact structures, side effects, and error shape.
- **Public interface**: methods, routes, events, or UI contracts exposed to consumers.
- **Hidden internals**: implementation details that must not leak.
- **Dependencies**: allowed modules and external systems.
- **Extension points**: only likely future capabilities with a named consumer.
- **Run/test focus**: unit, integration, contract, accessibility, operational, or manual checks.

Common anti-patterns to rule out:

- UI components calling an external model provider directly;
- UI components concatenating full prompts;
- file parsers calling the model directly;
- result components owning export logic;
- one module owning input, prompt construction, provider calls, parsing, rendering, and export;
- public interfaces exposing secrets, provider-specific internals, or unstable raw payloads.

## 4. AI runtime integrity

For an AI feature, the blueprint must show:

`UI or API -> validation -> orchestration -> prompt builder -> provider adapter -> structured result parser -> result presenter/export`

The provider key and deployable model configuration belong on the server side or in the approved runtime boundary. The design must define provider errors, timeouts, rate limits, malformed output, missing configuration, retry/idempotency behavior, and sensitive-data handling.

Allowed non-result states include empty, loading, validation failure, provider failure, parsing failure, and missing configuration. Hardcoded analysis, fake API responses, random output, sample JSON presented as live output, and "connect the model later" as the default runtime path are prohibited. Examples must be labeled as examples.

## 5. Change-impact notes

For each likely future feature, document:

- modules that will change;
- modules that should remain unchanged;
- interfaces or schemas that extend;
- persistence or configuration additions;
- migration/backfill and compatibility implications;
- why the current v1 boundary supports the feature.

Typical examples include login, history, export formats, model switching, batch processing, localization, additional file parsers, analytics, and administrative controls. Reserve interfaces only when the feature is plausible and the reservation has a consumer or clear compatibility value.

## 6. Staged LLM execution handoff

When a coding model will implement the plan, produce:

### Master brief

- project outcome and non-negotiable constraints;
- accepted architecture and source-of-truth documents;
- implementation order and dependency graph;
- global forbidden actions;
- required verification and release constraints.

### Stage prompt

- stage ID and goal;
- prerequisites and source documents;
- exact files/directories allowed to change;
- concrete implementation behavior;
- interfaces and invariants that must remain stable;
- forbidden scope expansion;
- acceptance criteria and tests;
- commands for build, lint, type-check, unit/integration/e2e, or smoke checks;
- self-check and completion report format;
- stop condition: if a required check fails, preserve the failure evidence and stop before starting the next stage.

The stage prompt must not duplicate or silently override the blueprint. If a conflict is found, the coding model reports it and the blueprint is revised as the source of truth.

## 7. Final self-check

Before delivery, verify:

- the user's outcome is traceable to requirements, architecture, tasks, and acceptance evidence;
- high-impact unknowns are confirmed or explicitly labeled with consequences;
- every core module has a contract and a real consumer;
- responsibility coverage is complete for the accepted slice;
- complexity is justified and excluded scope is explicit;
- AI features use a real provider path and protect secrets;
- UI language, style, accessibility, and state behavior are specified when applicable;
- future features have change-impact notes without speculative abstractions;
- every implementation stage has exact files, checks, and a failure stop condition;
- the final verdict and remaining uncertainty are visible.
