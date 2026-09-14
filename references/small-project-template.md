# Small Project Development Blueprint

Use one file for a small, bounded project. Replace every bracketed placeholder before delivery; do not leave `TBD` or `TODO` in the result.

## 1. Overview

- Project:
- Mode: Existing-project | Greenfield | Hybrid
- Status and revision:
- Repository revision and generation date:
- Teaching mode: enabled | disabled
- Goal:
- Final product behavior:
- Verdict: IMPLEMENTABLE | REDUCE_SCOPE | REVISE_DESIGN | NEEDS_EVIDENCE | NO_CHANGE_NEEDED

## 2. Scope and context

### In scope

### Out of scope

### Actors and primary scenarios

### Evidence

| Claim | Status | Source or reason |
| --- | --- | --- |

### Assumptions and pending decisions

### Requirement confirmation

- Confirmed outcome:
- Confirmed primary workflow:
- High-impact decisions confirmed:
- Remaining unknowns and consequences:

## 3. Requirements and acceptance criteria

### Functional requirements

### Non-functional requirements

### Acceptance criteria

For each criterion include Scenario, Action, Expected, Must not, Verification, Safety/environment, and Priority.

## 4. Architecture

### Current architecture (existing-project or hybrid)

### Target architecture

### Components and responsibilities

### Data flow

Include Mermaid only when it materially improves understanding.

### Consumer ledger

| Addition | Owner/producer | Committed consumer | Semantic effect | Reachable path | Absence test |
| --- | --- | --- | --- | --- | --- |

### Core module contracts

For each core module, include Responsibility, Non-responsibility, Input, Output, Public interface, Hidden internals, Dependencies, Extension points, and Run/test focus.

### Teaching notes (when teaching mode is enabled)

For each major requirement and design decision, explain business decomposition, design choice, rationale, code location, and verification method in 2–6 sentences.

### Change-impact notes

For each likely future feature, state modules that change, modules that remain stable, interfaces/data that extend, and why the current design supports it.

## 5. Technical design

### Technology and framework choices

| Area | Choice and version | Why | Alternatives rejected |
| --- | --- | --- | --- |

### Files and directories

| Path | Change | Responsibility |
| --- | --- | --- |

### API and contracts

### Data model and migrations

### Validation, errors, retries, and idempotency

### Auth, privacy, and permissions

### Configuration and environment

### Observability

### AI runtime integrity (when applicable)

- Provider and model path:
- Prompt ownership:
- Output schema and parsing:
- Provider/configuration/error behavior:
- Secret boundary:
- Explicitly prohibited fake-result behavior:

## 6. Ordered implementation plan

For every task include ID, objective, prerequisites, exact files, implementation details, completion criteria, tests, and risks.

| ID | Objective | Prerequisites | Files | Completion and verification |
| --- | --- | --- | --- | --- |

### Staged coding handoff (when another coding model will implement)

For each stage include goal, prerequisites, exact files, implementation constraints, forbidden actions, acceptance criteria, run checks, self-check, completion report, and failure stop condition.

## 7. Test, release, and rollback

- Test commands and fixtures:
- Unit/integration/end-to-end coverage:
- Manual and accessibility checks:
- Build and deployment steps:
- Smoke checks:
- Rollback and migration reversal:
- Operational handoff:

## 8. Verification matrix and remaining uncertainty

| Requirement/criterion | Evidence | Status |
| --- | --- | --- |



