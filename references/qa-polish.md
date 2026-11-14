# Stage 8 — Quality Assurance, UX Validation and Product Polish

Goal: prove the app is not only working but reliable, secure, fast, accessible, visually coherent and pleasant, by evaluating a **release candidate** as a QA engineer, product designer, accessibility specialist, security engineer and real user would. This stage does not replace the tests done during development; it validates the whole product. Polish is not added effects at the end: it is systematically removing the friction accumulated during development.

## Quality gates

Objective checks that must pass before moving on, so release never depends on anyone's opinion (Claude's included):

| Gate | Passes when |
|------|-------------|
| Feature gate | The feature meets its Definition of Done before integrating |
| Integration gate | Complete flows work and there are no important regressions |
| Release gate | The candidate meets the functional, security, performance, accessibility and quality criteria for launch |

## Ten areas

1. **Functional QA** — verify every requirement and acceptance criterion in normal and exceptional scenarios, and that features integrate. Typical cases: valid save stores once; invalid input gives an understandable error; double submit creates no duplicate; network loss during save never confirms an unknown result; edit and delete keep derived data right; access to another user's data is rejected; reload keeps data. Deliverable: functional test matrix with result and evidence per case.
2. **Exploratory testing** — sessions focused on one module, risk or failure category: repeated clicks, navigating away mid-operation, extremely long text, special characters and emoji, several tabs, interrupted requests, session expiring with a form open, empty, huge or inconsistent data. Ask "how could this fail and what would the user see?".
3. **Visual QA** — compare implementation screenshots with the approved design: spacing and alignment, type (font, weights, sizes, line height), semantic tokens, component variants and states, icons, responsive without overflow, real content and truncation, light and dark themes. Automate with Playwright screenshots at several viewports and visual regression between versions. Never claim visual verification without having inspected the rendered result.
4. **Interaction and motion QA** — use it for real: animations, feedback, hover, focus and pressed, loading indicators, modal open and close, scroll, keyboard, screen transitions, reduced motion respected. Every interaction should feel deliberate and predictable, not everything moving.
5. **Accessibility QA** — WCAG 2.2 AA where applicable. Automated (axe-core, Lighthouse) plus manual: keyboard-only use with logical focus order, contrast, text size and scaling, state differentiation, screen reader labels, roles, names and announcements, zoom, font sizes, touch targets, reduced motion.
6. **Performance QA** — measure with representative scenarios. Web references at the 75th percentile: LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1; plus critical-operation latency, JavaScript size, images, memory, large data sets, modest devices. Measure first, find the bottleneck, fix what users feel.
7. **Security and privacy QA** — confirm the controls designed in stage 5: authentication and sessions, authorization per resource and operation, input validation, common vulnerabilities, secrets, vulnerable dependencies, sensitive data exposure, safe errors and logs, retention and deletion. Higher-risk products need penetration tests and specialist review. An AI review is never a full security audit.
8. **Cross-device and compatibility** — the devices, browsers, resolutions and OS defined in planning: desktop (windows, keyboard, zoom, hover), tablet (orientation), mobile (touch, virtual keyboard, safe areas, scroll, modals, menus, long forms, rotation).
9. **UX validation with real users** — representative tasks ("register an expense of $25,000 and check your balance updated"), no hints on where to click; record success rate, time per task, errors, recovery, comments. A small group finds big problems but is not statistically representative. Validate behavior, not opinions about looks.
10. **Product polish pass** — the whole product reviewed as an extremely demanding user, removing friction and inconsistency, adding no features (checklist below).

## Product polish checklist

Visual
- [ ] No inconsistent spacing or alignment
- [ ] Type and icons coherent
- [ ] No overflow or cut-off text
- [ ] Light and dark states cared for

Interaction
- [ ] Every action gives feedback
- [ ] Errors explain how to recover
- [ ] No clicks or actions without response
- [ ] Loading states well resolved

Content
- [ ] Copy clear and consistent
- [ ] No placeholders or demo content left
- [ ] Dates, currency and numbers correctly formatted for the locale
- [ ] Empty states guide the user

Reliability
- [ ] Repeated actions create no duplicates
- [ ] Data is never lost unexpectedly
- [ ] Sessions and permissions work
- [ ] External failures handled

Whole experience
- [ ] Main journeys flow
- [ ] Target devices verified
- [ ] Serious accessibility issues fixed
- [ ] Performance meets targets

## Defects and launch criteria

| Severity | Example | Decision |
|----------|---------|----------|
| S0 Critical | Data loss or serious data exposure | Blocks launch |
| S1 High | Main flow unusable | Blocks launch |
| S2 Medium | Secondary feature affected, workaround exists | Evaluate risk |
| S3 Low | Small visual inconsistency | Can be scheduled |

Severity is not priority: a rare defect is critical if it compromises data or security. Keep an explicit policy for defects accepted temporarily, each with an owner and a mitigation.

## Tools (free or open source; pick per stack)

Playwright (E2E, screenshots, viewports), axe-core (accessibility), Lighthouse and Lighthouse CI (performance and regressions), Vitest (unit and integration), Storybook (component review), OWASP ZAP (automated security tests). They complement manual testing.

## Deliverables

Real product: `docs/quality/` with `test-strategy.md`, `functional-test-report.md`, `exploratory-testing.md`, `visual-qa.md`, `accessibility-report.md`, `performance-report.md`, `security-review.md`, `usability-findings.md`, `defect-register.md`, `release-readiness.md`.

Small project: one `docs/qa-report.md` with the functional matrix, polish checklist, accessibility and performance results, open defects with severity. Keep evidence, not long reports.

## Done when (release gate)

- [ ] Critical requirements verified
- [ ] Main E2E flows work
- [ ] No open S0 or S1 defects
- [ ] Designs and components consistent
- [ ] Interaction states complete
- [ ] Accessibility evaluated, blockers fixed
- [ ] Performance meets defined targets
- [ ] Security controls reviewed
- [ ] Target devices and browsers verified
- [ ] Appropriate usability testing done
- [ ] Pending defects classified, with owners
- [ ] Reproducible release candidate exists
