# Stage 6 — Product Roadmap and Implementation Planning

Goal: turn the PRD, UX/UI and architecture into a plan that is incremental, verifiable and realistic, so the whole app gets built without losing control of architecture, scope, quality and detail.

## Three rules

1. **Every delivery produces something working and verifiable end to end**, never a folder of components or endpoints that do not yet complete a real task.
2. **No feature is declared complete without meeting its Definition of Done**, proven with evidence (tests that ran, behavior checked in the target environment). Error states, accessibility and tests are never "for the end". An agent saying "done" is not evidence.
3. **The roadmap is not an immutable promise.** Adjust it when new evidence appears, without losing control of scope.

## Steps

1. **MVP and release scope** — small in scope, complete and reliable enough to solve a real problem; never a half-built or badly designed app. Mark what comes later. Quality is mandatory from v1: security, no data loss, basic accessibility, acceptable performance, error handling.
2. **Outcome roadmap with milestones** — milestones describe results, not feature lists, and each has **exit criteria** (code written is not an exit criterion). Typical:
   1. Verifiable foundations — repo, environments, quality pipeline, architecture skeleton, first flow working and deployed
   2. Main flow complete — the user can do the task that justifies the product
   3. Functional MVP — every essential journey connected and testable end to end
   4. Launch readiness — security, performance, accessibility, observability, whole-product tests
   5. Initial launch — available to the intended users with monitoring and feedback
3. **Vertical slices** — each slice crosses UI, validation, API, business logic, database, security and tests. Shared infrastructure is allowed; large piles of isolated parts that solve no task are not.
4. **Decomposition** — Epic → Feature → Story → Task where it helps; a small project may need only features and tasks. Every item keeps its link to PRD requirement IDs and acceptance criteria.
5. **Ready-for-dev specs** — write a spec just before each complex feature (`specs/<feature>.md`, see `architecture.md` for the template), linked to its RF and UX flow IDs. It is ready when another developer or an agent can implement it without inventing business decisions.
6. **Dependencies and order** — order by: biggest risks → minimal foundations → main flow → complementary capabilities → launch. Not easiest first. Contracts, mocks or temporary adapters may unblock work if they are listed and their real integration is verified later.
7. **Risks and estimates** — each major risk gets a strategy (below). Estimate in ranges from real history, complexity, dependencies and uncertainty, never from an AI guess alone; revise when information changes.

| Risk | Strategy |
|------|----------|
| Uncertain external API | Early integration test |
| Complex data model | Technical prototype and validation |
| Design hard to implement | Technical spike of the component |
| Ambiguous requirements | Refine with acceptance criteria |
| Provider dependency | Check limits and alternatives |
| Uncertain deadlines | Range estimates and contingency |

## Definition of Ready (to start a feature)

- [ ] Goal and scope clear
- [ ] Verifiable acceptance criteria exist
- [ ] Important dependencies resolved or controlled
- [ ] Enough technical and design context (flows, states, tokens, contracts)
- [ ] Main risks identified

DoR exists to surface uncertainty, not to block experiments; a spike may start without it.

## Definition of Done (to call a feature finished)

The per-slice checklist in `SKILL.md` plus:
- [ ] Meets its acceptance criteria, with the evidence recorded (test output, checked behavior)
- [ ] Code reviewed and follows the architecture
- [ ] Relevant tests pass
- [ ] Design and interface states implemented
- [ ] Applicable security, accessibility and performance verified
- [ ] Needed documentation updated
- [ ] Usable and verifiable in the target environment

## Roles with Claude Code

- **Planner** — analyzes requirements, finds dependencies, proposes slices and risks.
- **Implementer** — builds one concrete feature following its spec.
- **Reviewer** — checks the change against PRD, architecture, design system and acceptance criteria, in a **different context from the implementer** (a fresh subagent or session) so it does not just confirm its own assumptions.

Never mark a task complete because the agent says so; require the evidence.

## Deliverables

Real product: `docs/planning/` with `product-roadmap.md`, `mvp-scope.md`, `backlog.md` (or ClickUp / GitHub Issues), `dependencies.md`, `risks.md`, `definition-of-ready.md`, `definition-of-done.md`, `specs/`.

Small project: phases, slices, DoD and risks inside the PRD plus the implementation plan from `superpowers:writing-plans`.

## Done when

- [ ] MVP scope defined
- [ ] Out-of-scope features identified
- [ ] Outcome roadmap exists
- [ ] Milestones have exit criteria
- [ ] Product split into vertical slices
- [ ] Features prioritized
- [ ] Critical dependencies identified
- [ ] Main risks have mitigation strategies
- [ ] Backlog with verifiable tasks exists
- [ ] First features have ready specs
- [ ] DoR and DoD defined
- [ ] Plan includes continuous testing and quality control
