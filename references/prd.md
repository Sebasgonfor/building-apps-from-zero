# Stage 2 — Product Requirements Document (PRD)

Goal: turn discovery into requirements that are clear, prioritized and verifiable, so design, development and QA read them the same way. No code and no visual design yet. Do not pick implementation tech here (Firebase vs JWT is a technical-design decision).

## What the PRD defines

1. **Vision and objectives** — purpose and measurable results ("log a daily expense in under 15 s").
2. **Users, roles and permissions** — only the roles the product really needs.
3. **Functional requirements** — grouped by module; each with ID, description, priority, rules, acceptance criteria.
4. **Non-functional requirements** — performance, security, privacy, availability, accessibility, compatibility, scalability, reliability, observability; measurable whenever possible, never invented arbitrary targets.
5. **Business rules and special scenarios** — validations, permissions, exceptions, duplicates, lost connection, partial failures.
6. **Prioritization and scope** — MoSCoW, MVP = Phase 1, explicit out-of-scope list.
7. **Acceptance criteria and traceability** — each requirement links to the problem, objective or use case that justifies it.

## Requirement format

```markdown
### RF-001 · Sign in            Must · Module: Auth · Use case: UC-1
Story: As a registered user, I want to access my account with my credentials to use my data.
Rules:
- Validate credentials; never reveal whether an account exists.
- Throttle automated attempts; manage the session securely.
Acceptance criteria:
- Given valid credentials, when the user signs in, then they reach their account.
- Given invalid credentials, the user sees a safe, understandable message.
- On a connection error, the user can retry without retyping what they entered.
- When the session expires, the app asks to sign in again where needed.
```

Small projects may use one table instead: `ID | Requirement | Priority | Phase | Use case | Acceptance criterion`.

## Non-functional requirements

`ID | Category | Requirement | How it is verified`. Examples: 95% of critical operations under the agreed latency; WCAG 2.2 AA; server-side authorization on protected operations; no duplicate critical operations; supported browsers/devices for the audience; critical failures logged without sensitive data; collect only needed data with a retention rule.

## MoSCoW

| Priority | Meaning |
|----------|---------|
| Must | Without it, the first version does not solve the core problem |
| Should | High value, but there is an acceptable workaround |
| Could | Improves the experience, can wait |
| Won't | Not in this delivery, may come later |

Prioritize by user value, business impact, risk, effort and dependencies, not by what looks most fun.

## Document structure

Real product (`docs/02-prd.md`): executive summary · context and problem · vision · objectives and metrics · users and roles · scope · modules and features · functional requirements · non-functional requirements · business rules · user stories · acceptance criteria · exceptional cases · prioritization and MVP · dependencies and constraints · risks and open questions · traceability · approval criteria. Large sections may become their own docs; the PRD stays a readable source of truth.

Small project: problem and goal · users and use cases · alternatives and assumptions · scope · phases · functional requirements table · non-functional table · business rules · data model and API contract · experience (flows, state matrix, interaction rules) · delivery checklist · open questions.

## Done when

- [ ] Objectives clear and measurable
- [ ] Users and roles identified
- [ ] Features organized by module
- [ ] Functional requirements have IDs and priorities
- [ ] Non-functional requirements defined and verifiable
- [ ] Business rules documented
- [ ] Important exceptional scenarios covered
- [ ] Acceptance criteria verifiable
- [ ] MVP (Phase 1) and out-of-scope defined
- [ ] Dependencies, risks and open questions recorded
