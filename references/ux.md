# Stage 3 — UX Design (experience and behavior)

Goal: turn the PRD into an experience that is intuitive, efficient, accessible and coherent. Decide how it works before final colors, shadows or decorative motion.

## Steps

1. **Information architecture** — hierarchy of sections, grouping, main navigation, relations between screens. A one-screen app documents its zones instead.
2. **User flows** — step by step for each important task, with branches: happy path plus lost connection, duplicates, cancel, insufficient permissions, recovery after failure. No branch ends in a dead end. Draw branching flows as a diagram, not a list.
3. **Wireframes** — layout without final identity. Low fidelity for distribution and navigation, high fidelity for component structure. Answer: what appears first, which action stands out, how many steps, what happens on a small screen (375 px). Cover the critical screens on mobile and desktop.
4. **States and behaviors** — the state matrix (see SKILL.md) per screen: loading, empty/first use, error, success, offline, restricted, edge data.
5. **Interaction specifications** — see the checklist below.
6. **Interactive prototype** — Claude Design, Figma, or code for the critical journeys and the most complex interactions only.
7. **Usability check** — representative people try it. Ask: can they finish tasks without instructions, do they understand each action, do they notice errors, can they go back or cancel, how long does it take, what confuses them. Log issues with severity and changes; retest the important fixes.

## Interaction specification checklist

Decide each one explicitly; these details are what make an app feel polished.

- [ ] Browser/system **Back** closes overlays and steps back inside the app instead of leaving it
- [ ] **Focus**: moves into a dialog when it opens, is trapped while open, returns to the element that opened it when it closes
- [ ] **Keyboard**: logical Tab order, visible focus, Enter/Esc/arrow behavior in inputs, lists and menus
- [ ] **URL state**: searches, filters and open items live in the URL so reload and share keep them
- [ ] **Real-time validation**: when it fires, where the message shows, how it clears
- [ ] **Data preservation**: nothing typed is lost on error, retry, navigation or reload
- [ ] **Feedback**: every action answers within 100 ms (pressed state, optimistic update or progress)
- [ ] **Repeat requests**: debounce input, cancel stale requests, keep current results dimmed instead of flashing empty
- [ ] **Confirmations and undo**: destructive actions confirm or offer undo
- [ ] **Buttons**: disabled vs loading states, double-submit prevented
- [ ] **Deep links**: opening a link straight into a nested state works and looks intentional

## Deliverables

Real product: `docs/ux/information-architecture.md`, `docs/ux/user-flows.md`, `docs/ux/interaction-specifications.md`, `docs/ux/wireframes/`, `docs/ux/prototype/`.

Small project: an "Experience" section in the PRD with flow diagram, wireframes (text sketches are fine), state matrix and interaction rules table.

## Done when

- [ ] Information architecture defined
- [ ] Main flows documented with alternative and error branches
- [ ] Wireframes for critical screens, mobile and desktop
- [ ] Interface states specified (state matrix)
- [ ] Navigation and interactions consistent (checklist above)
- [ ] Accessibility and target devices considered
- [ ] Navigable prototype of the main journeys (may be code under time pressure)
- [ ] Usability check done with at least one person
- [ ] Critical UX issues fixed or documented
