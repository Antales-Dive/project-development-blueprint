# Medium/Large Project Development Blueprint

Use a directory of linked Markdown files when the project has multiple deployable components, durable data/API contracts, migrations, or a long task graph. Create an index first and keep IDs stable across files.

## Required files

### `00-index.md`

- Project goal, mode, status, revision, verdict
- Scope summary and document map
- Implementation order and cross-document dependencies
- Global assumptions, pending decisions, and risk summary
- Requirement confirmation status and high-impact decisions
- Master implementation brief and staged handoff map, when another coding model will implement

### `01-requirements.md`

- Problem and desired outcome
- Actors and scenarios
- Functional and non-functional requirements
- In/out scope
- Business constraints, assumptions, and acceptance criteria `AC-###`
- Guided requirement translation record and confirmation draft
- UI language/style, accessibility, and localization requirements when applicable

### `02-current-state.md` (existing-project or hybrid)

- Repository evidence and directory map
- Runtime entry points and execution paths
- Existing modules, data flows, dependencies, tests, and deployment
- Reusable capabilities and exact gaps

### `03-architecture.md`

- Target architecture and component responsibilities
- Dependency direction and ownership
- Data and control flow
- Mermaid diagrams only where useful
- Consumer ledger for every new component or abstraction
- Alternatives and decision rationale
- Responsibility-complete but appropriately simple architecture explanation
- Core module contracts: responsibility, non-responsibility, input, output, public interface, hidden internals, dependencies, extension points, run/test focus
- Change-impact notes for likely future features

### `04-contracts-and-data.md`

- API/event contracts and compatibility policy
- Auth and authorization boundaries
- Tables/collections, fields, constraints, indexes, relationships
- Migration, backfill, replay, rollback, and retention behavior
- Validation, errors, retries, idempotency, and concurrency
- AI runtime integrity, provider boundary, prompt ownership, output schema, parsing, and secret handling when applicable

### `05-implementation-plan.md`

- Ordered task IDs `TASK-###`
- Exact files/directories and ownership
- Prerequisites and dependency graph
- Concrete implementation instructions
- Completion criteria and verification per task
- Deferred or rejected scope
- Master implementation brief and staged coding prompts with exact files, forbidden actions, run checks, and failure stop conditions when applicable

### `06-verification-release.md`

- Test strategy and commands
- Contract, security, accessibility, performance, and operational checks
- Build/deploy/configuration
- Smoke checks, monitoring, alerts
- Rollback and failure containment
- Verification matrix mapping `AC-###` to evidence
- Stage completion evidence and final self-check results when staged handoff is used

## Split-document rules

- Put each fact or decision in one canonical file and link to it elsewhere.
- Keep requirement, component, contract, data, and task IDs stable.
- A task is not complete unless its files, dependencies, acceptance criteria, and verification evidence are named.
- The index must allow a coding model to navigate from each requirement to architecture, contracts/data, tasks, and verification without guessing.
