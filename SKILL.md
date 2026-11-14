---
name: building-apps-from-zero
description: Use when starting a new app, product or major feature from scratch (app desde cero, proyecto nuevo, nueva aplicación, arrancar un proyecto), when writing or reviewing a PRD, product discovery, UX flows or a design system, when asked how to plan, scope or phase a new product, or when the user wants an app that is genuinely useful and polished (pulida, atención al detalle, bien hecha).
---

# Building Apps From Zero

## Overview

Polish is not a phase at the end. It is a bar every slice clears before the next one starts. Decide *what* (problem, Phase 1, flows and states) before *how*, build in vertical slices, and have something deployed on day 1.

Two rules cross all nine stages:
- **Evidence for every important claim, a reason for every design decision.** AI may research, propose, implement and review; it never asserts what it did not check.
- **Not a rigid waterfall.** When evidence from a later stage contradicts an earlier one (architecture limits the PRD, usability breaks a screen, production reveals a wrong assumption), go back and update that stage's source of truth. The goal is better decisions, not nine documents.

Conversation stays in `superpowers:brainstorming` (one question at a time); plans go through `superpowers:writing-plans`. This skill defines which stages and artifacts must exist. Write every doc in the user's language. Before working a stage, read its reference file.

## Stages and required outputs

| # | Stage | Required output | Reference |
|---|-------|-----------------|-----------|
| 1 | Product discovery | Problem, users and their current workaround, **alternatives** (including a general AI) and why ours wins, value proposition, **riskiest assumption + how and when it is checked**, **2-3 success metrics** | `references/discovery.md` |
| 2 | PRD | Objectives, roles, **functional requirements with ID + MoSCoW + acceptance criteria**, **measurable non-functional requirements**, business rules, exceptional cases, **Phases 1/2/3** (Phase 1 = MVP), out of scope, risks, traceability | `references/prd.md` |
| 3 | UX design | Information architecture, **flow diagram with error branches**, wireframes (mobile + desktop), **state matrix** (below), **interaction rules** (back button, focus, keyboard, URL state), prototype of critical journeys, usability check with one person | `references/ux.md` |
| 4 | UI and design system | **Visual research first**: real references with links, **three distinct directions, the user picks one**, a scored pilot screen. Then semantic tokens, type scale, components with states, **motion rules** (purpose, durations, easing, reduced motion), responsive and accessibility rules | `references/ui-design-system.md`, `references/inspiration-mcp.md`, `ui-polish`, `impeccable` |
| 5 | Architecture | **Architectural drivers** first; stack chosen with a weighted matrix; modular monolith unless a driver says otherwise; data model, API contracts (validation, errors, idempotency), security, performance, observability; **ADR per important decision**; technical spec per complex feature just before building it; critical rules enforced by types, tests, lint and CI | `references/architecture.md` |
| 6 | Roadmap and plan | MVP with quality mandatory from v1; outcome milestones with **exit criteria**; vertical slices ordered **risks → foundations → main flow → complements → launch**; ready-for-dev specs; dependencies, risks with strategies; **Definition of Ready and Done**. **Slice 1 = walking skeleton deployed** (repo, CI, tests, one endpoint + one screen live) | `references/planning.md`, `superpowers:writing-plans` |
| 7 | Build | Reproducible repo and engineering standards in the project's CLAUDE.md; per feature: **read existing code → reviewed plan → small increments with tests → review by a separate agent → integrate on DoD**; design-system components reused; CI from the first delivery; labeled mocks only | `references/implementation.md` |
| 8 | QA and polish | On a **release candidate**: functional matrix with evidence, exploratory sessions, visual QA from real screenshots, interaction and motion QA, accessibility (automated + manual), performance (measured), security review, target devices, usability with real users, whole-product polish checklist; defects classified S0-S3 | `references/qa-polish.md` |
| 9 | Launch and improve | Production readiness (no debug config, secrets or test accounts), deploy strategy sized to risk, **tested rollback**, internal → limited → general release, logs/metrics/traces/alerts without sensitive data, product analytics tied to the success metrics, event tracking plan, feedback loop, incident procedure with blameless postmortems, maintenance routines; metrics decide Phase 2 | `references/launch-operations.md` |

**Size the docs to the project.** A doc exists only if it changes a decision.
- Class project, weekend, prototype: one `docs/prd.md` holds stages 1-3 and the API/data contract, plus `docs/design-system.md` and the plan.
- Real product: `docs/01-product-discovery.md`, `02-prd.md`, `ux/` (information-architecture, user-flows, interaction-specifications, wireframes, prototype), `design/` (visual direction, tokens, components, motion), `architecture/` (drivers, stack decisions, system, data model, API contracts, security, observability, `adr/`, `specs/<feature>.md`), `07-roadmap.md`, `08-quality.md`, `09-release.md`.

**Under time pressure, compress, never skip:** the Phase 1 cut, the state matrix, the interaction rules, the approved design and the Definition of Done. Screens are designed and approved in a design tool before any frontend code; prototyping straight in code only when the user explicitly chooses it.

## Quality gates

Nothing advances on opinion. **Feature gate**: the slice meets its Definition of Done before integrating. **Integration gate**: complete flows work with no important regressions. **Release gate**: the candidate passes stage 8 with no open S0/S1 defects.

## State matrix (stage 3)

One row per screen or zone. Every cell says what the user sees and can do.

| Screen | Loading | Empty / first use | Error | Success | Edge (long text, 0 / 500 items, offline, no permission) |
|--------|---------|-------------------|-------|---------|------|

## Definition of Done (copy into every slice of the plan)

- [ ] Happy path works and has tests
- [ ] Loading, empty and error states built, with copy that says what happened and what to do
- [ ] Survives odd data: very long text, zero items, hundreds of items, special characters
- [ ] Every state change animates; nothing pops in or out
- [ ] Hover, focus and pressed feedback on everything interactive
- [ ] Interaction rules hold: back button, focus return, keyboard, URL state
- [ ] Works at 375 px and on desktop
- [ ] Keyboard usable, contrast passes, respects reduced motion
- [ ] Uses design tokens only; no invented colors or spacing
- [ ] Copy is plain language and consistent in tone
- [ ] Builder used it end to end and fixed what felt wrong; `ui-polish` audit run on this slice's screens now, not after the build

## Red flags

| Thought | Reality |
|---------|---------|
| "We'll do a polish pass at the end" | The end is when time runs out. Polish is in the Definition of Done of each slice; stage 8 is a whole-product check on top of that, never a substitute. |
| "It looks good, let's launch" | Launch only through the release gate: evidence per area, no open S0/S1. |
| "Deploy and we'll see what happens" | Never ship a critical version without knowing how a failure is detected and how you recover. Rollback is tested, not assumed. |
| "Users asked for it, add it" | Feedback is evidence to weigh, not a backlog. Find recurring problems, measure impact, then decide; removing a feature is also progress. |
| "Uptime is 99.9%, the product works" | Technical health is not value. Watch activation and retention against the discovery metrics. |
| "Claude reviewed the security" | An AI review is not a security audit. Higher-risk products need specialist review or penetration tests. |
| "Empty and error states later" | Later never comes. They are in the state matrix before the screen is built. |
| "Build the whole backend, then the frontend" | Layers hide integration bugs until the end. Build vertical slices. |
| "We have the PRD, skip flows and prototype" | The PRD says what; flows say what the user sees. Prototype changes requirements cheaply. |
| "Deploy when it's ready" | Deploy is slice 1. Infra problems are cheap on day 1 and expensive on the last. |
| "Phases go at the end of planning" | Cut Phase 1 in the PRD, or you design and spec work that never ships. |
| "Success = it works" | Define 2-3 metrics in discovery; they decide Phase 2. |
| "Nothing else does this" | Something always does: a spreadsheet, WhatsApp, a general AI. Name it and say why ours wins, or rethink. |
| "Everyone needs this" | That is the riskiest assumption. Write it down and check it with a real person before building. |
| "Claude says it's done" | An agent's word is not evidence. Done = DoD met, with test output or checked behavior recorded. Otherwise report it as unverified. |
| "Phase 1 frontend, Phase 2 backend, Phase 3 integration" | Value and integration bugs appear last. Plan vertical slices, each usable end to end. |
| "Easy features first to build momentum" | Order by risk: biggest risks, minimal foundations, main flow, then the rest. |
| "I'll write a new modal for this feature" | Search the shared component library first. Five modals doing the same thing is AI drift. |
| "Generate the whole module, I'll review after" | Review the plan and its technical decisions before code; implement in small verified increments. |
| "The code is clean" | Not a review. Name concrete findings and run the checks. |
| "Mock it for now" | Allowed only if labeled and replaced or validated before the feature counts as integrated. |
| "Here is the PRD, build the app" | Global context, small verified tasks: one slice, its spec, a reviewed plan, tests, review, merge on Done. |
| "The full template has 18 sections, fill them all" | Size to the project. An empty or repeated section is noise. |
| "Make it modern and premium" | That prompt produces the average AI look. Research real references, deal three directions, let the user pick. |
| "The direction is picked, I'll build the pilot in code" | A direction is not a design. Design the pilot in Claude Design, get it approved, then write frontend code. |
| "Generate each screen with AI" | Screens generated one by one drift. The AI follows the design system, never invents one per screen. |
| "Let's use microservices, queues and Redis to be ready to scale" | Complexity needs a driver. Start with a modular monolith and add pieces when a real goal or risk demands them, recorded in an ADR. |
| "The architecture is documented, the agent will follow it" | Documents erode. Enforce critical rules with types, tests, lint and CI. |
| "I know what Linear looks like" | Memory is not a look. Open the reference in a browser and screenshot it, or do not make visual claims about it. |
