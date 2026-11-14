# Stage 7 — Implementation and Engineering Workflow

Goal: turn specs, architecture and plan into software that is functional, secure, maintainable and verifiable, keeping quality the whole way. Professional code is code you can understand, check, change and deploy without fear; with AI agents the process must prevent mass generation, duplicated logic, improvised architecture and features that look finished but fail in real use.

## Five principles

1. **Spec before code** when a feature is complex enough to need one.
2. **Small verifiable changes**, never whole modules generated at once.
3. **Reuse before reinventing**, especially components and architectural patterns.
4. **Test before declaring done**, with real evidence from the checks.
5. **Keep the product working** throughout: integrate complete increments, never pile up disconnected work.

Tests, accessibility, performance and security live inside implementation, not only in stage 8.

## 1. Reproducible repository (slice 1)

Git, project and package manager, pinned runtime and dependency versions, `.env.example` without secrets, strict typing, linter and formatter, test framework, dev/test/prod environments, initial CI. Structure follows the chosen architecture, not a generic template. Rule: someone else can clone and run it from the README with no hidden machine setup.

## 2. Engineering standards (write them into the project's CLAUDE.md)

| Area | Define |
|------|--------|
| Code | Naming and style |
| Organization | Module boundaries and responsibilities |
| Typing | Types, interfaces, validation (for example Zod at boundaries) |
| Errors | One consistent handling and representation |
| Data | Access, transactions, validation |
| Components | Reuse and separation of concerns |
| Dependencies | Criteria to add a library |
| Tests | Strategy and minimum criteria |
| Git | Commits, branches, pull requests |
| Docs | When to update specs and ADRs |

Do not impose complex patterns for looking professional; anyone should see quickly where a feature goes and how to change it safely.

## 3. Controlled cycle per feature

1. Select the feature spec: scope and acceptance criteria (Definition of Ready met).
2. **Read the existing code** first: architecture, conventions, dependencies, reusable pieces. No new abstraction before that.
3. Plan the changes: files, contracts, risks, tests. Review the plan before code; never let an agent implement a whole module without reviewing the technical decisions it introduces.
4. Implement incrementally, code and tests together.
5. Verify and review: tests, security, UX, quality.
6. Integrate only when the Definition of Done is met.

## 4. Vertical slice order inside a feature

Data model → business rules and validation → API contract and endpoint → UI with design-system components → connect to real services → loading, error and success states → tests and edge cases. Done means usable end to end. Mocks are allowed during development only if labeled and replaced or validated before the feature counts as integrated; no pending parts hidden behind a finished-looking UI.

## 5. Tests while building

- **Unit**: business rules, calculations, transformations.
- **Integration**: modules, APIs, database and services together.
- **End-to-end**: critical user journeys.

The mix depends on the project; prioritize critical behavior and highest-risk scenarios over a coverage percentage. For complex rules, write the tests that describe them first (TDD when the project uses it).

## 6. Design system in code

Shared component library (`components/ui/`) and centralized tokens (`styles/tokens.css` or Tailwind theme); features compose them (`features/<name>/components|hooks|services|types`). Five modals that do the same thing with different animations is the typical AI drift: search for the existing component before writing one. Reuse genuinely shared patterns; no premature generic abstractions just to save lines.

## 7. Version control and review

Short branches per feature, or small verifiable commits straight to the integration branch for solo personal work; pull requests when they add value. Changes stay traceable and easy to revert.

Review checklist for every relevant change:
- [ ] Meets the spec and PRD
- [ ] Adds no unrequested features
- [ ] Respects the architecture
- [ ] Duplicates no existing logic or component
- [ ] Handles errors and exceptional conditions
- [ ] Exposes no credentials or sensitive data
- [ ] Has appropriate tests
- [ ] Does not degrade UX/UI

"The code is clean" is not a review: findings must be concrete and the available checks must actually run.

## 8. CI/CD from the first delivery

Push or PR → lint and format → typecheck → unit and integration tests → build → preview or staging deploy → critical-flow checks. Security, accessibility and E2E run in the same pipeline or separate stages depending on cost. Production gets extra controls when risk requires it.

## 9. Working with Claude Code: three modes

- **Plan** — analyze the spec, inspect the repo, propose the implementation; no code changes until the plan is defined.
- **Implement** — scoped changes, existing patterns reused, relevant tests run.
- **Review** — a reviewer agent compares the diff, tests and real behavior against the spec, without relying on the implementer's explanations, and asks for evidence that checks ran.

Policies: no edits outside the scope without justification; no new dependency unless needed and justified.

## 10. Continuous quality

Watch during construction: duplicated logic and components, unneeded dependencies, excess coupling, inefficient queries, silenced errors, unsafe types, forgotten temporary code, flaky tests, docs diverging from code. Refactor what affects the current feature or is a real risk, not the whole project constantly. Professional code is predictable, understandable and reliable, not the one with the most patterns.

## Deliverables

Working code, tests (`tests/unit`, `tests/integration`, `tests/e2e` or colocated), CI pipeline, `.env.example`, README, updated docs and ADRs, test evidence, and an environment where implemented flows can be checked.

## Done when

- [ ] Repository and environments configured
- [ ] Code conventions documented
- [ ] Structure follows the architecture
- [ ] Features built as vertical slices
- [ ] Interfaces reuse the design system
- [ ] Business rules have appropriate tests
- [ ] Integrations and critical flows verified
- [ ] CI pipeline works
- [ ] Code reviewed before integration
- [ ] Features meet acceptance criteria
- [ ] Relevant errors and edge cases handled
- [ ] Technical docs updated
