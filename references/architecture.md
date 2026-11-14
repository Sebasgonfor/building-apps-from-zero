# Stage 5 — Software Architecture and Technical Design

Goal: turn the PRD, UX and design system into a technical solution that works today, is easy to change tomorrow and can be operated with confidence. A good architecture is not a complex one: five services, three databases and queues are not better than one well-modularized app. Set real goals and risks first, then add only the complexity they need.

Two moments: a **preliminary** pass right after the PRD (drivers, stack, hosting, main risks) and a **detailed** pass per slice, written just before building it.

## Steps

1. **Architectural drivers** — read the PRD and list only requirements and constraints that change technical decisions: web, mobile or both; offline; expected users; sensitive data; real time; external integrations; availability and performance; budget, team and deploy constraints. Do not design for millions of users without users, but avoid choices that make growth needlessly hard.
2. **Stack selection** — compare alternatives per layer (frontend, backend, database, auth, storage, cache, hosting, observability) with a weighted matrix: functional fit, maintainability, total cost, team experience, scalability. Set the weights before scoring. Every dependency adds cost and operational complexity; include only what a driver needs. Deliverable: the evaluation and its justification.
3. **System architecture** — prefer a modular monolith first. Define module responsibilities and boundaries; separation of presentation, application, domain and persistence where it adds value; communication between components; allowed and forbidden dependencies; centralized error handling; async strategy. Diagram with C4 (context, containers, relevant components).
4. **Data model** — entities, relations, indexes, constraints, migrations, retention, backups. Resolve domain traps (money precision, currencies, history, time zones). Deliverable: model + entity dictionary.
5. **API contracts** — define before implementing: request, validation, success responses, errors, permissions, pagination, versioning, retries and **idempotency** for duplicate operations. Prefer OpenAPI versioned with the code, used to generate types and clients when helpful.
6. **Security and privacy by design** — authentication, authorization per resource, data protection (encryption, minimization), sessions (expiry, revocation, renewal), input validation, secrets management, audit of sensitive operations, dependency risk. Threat-model apps with relevant risk; use OWASP ASVS and Top 10 as checklists adapted to the app.
7. **Performance, reliability, scalability** — performance budgets, cache and pagination, background jobs, concurrency and resource limits, timeouts, retries, idempotency, backup and restore, availability and recovery targets when they apply.
8. **Observability and operations** — logs (relevant events and errors, no sensitive data), metrics (latency, errors, usage), traces, alerts that require action; dev, test and production environments; deploy and rollback strategy.
9. **ADRs** — mandatory for important decisions (below).
10. **Technical specs per complex feature** — written just before building it (below).

## Make the rules executable

With AI agents, architecture that lives only in documents erodes. Enforce the critical rules with types (strict TypeScript, schema validation such as Zod), tests, static analysis (lint rules for forbidden imports between modules), contract validation and CI that blocks merges.

## ADR template

`docs/architecture/adr/NNN-<decision>.md`

```markdown
# ADR-001: Use a modular monolith
Status: accepted · Date: YYYY-MM-DD
Context: early product, small team, need to ship features fast.
Decision: one backend application organized in modules with explicit boundaries.
Alternatives: traditional monolith; microservices.
Consequences: lower operational complexity and simple deploys; in exchange a shared deploy and discipline on module boundaries.
```

## Technical spec per feature

`docs/architecture/specs/<feature>.md` (or `docs/specs/<feature>.md`), for complex, critical or ambiguous features only:

1. Objective and related PRD requirements (IDs)
2. Scope and expected behavior
3. Affected components and files
4. Data model and contracts
5. Processing flow
6. Security and permissions
7. Errors and exceptional conditions
8. Tests needed
9. Risks, dependencies, open decisions

This gives an agent precise context without re-reading the whole architecture.

## Deliverables

Real product: `docs/architecture/` with `technical-requirements.md`, `technology-decisions.md`, `system-architecture.md`, `data-model.md`, `api-contracts.md` (or OpenAPI), `security.md`, `performance-reliability.md`, `observability.md`, `adr/`, `specs/`.

Small project: one `docs/architecture.md` (drivers, stack with reasons, module map, data model, API contract, security notes) plus ADRs for decisions someone could question. In a class project the data model and API contract may stay in the PRD.

## Done when

- [ ] Technical requirements and constraints identified
- [ ] Stack selected and justified
- [ ] Overall architecture documented
- [ ] Modules have clear responsibilities and boundaries
- [ ] Initial data model defined
- [ ] Main communication contracts established
- [ ] Security and privacy risks assessed
- [ ] Performance and reliability targets exist
- [ ] Monitoring and operation planned
- [ ] Important decisions have ADRs
- [ ] Technical risks and open questions documented
- [ ] Enough information to plan the implementation
