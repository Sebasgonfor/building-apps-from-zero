# Stage 9 — Launch, Observability and Continuous Improvement

Goal: launch safely, confirm the app works in production, measure its real impact and keep improving it from evidence. Working in development, passing tests and looking good is not validation; real users, real data and unstable networks are. Deployment exists since slice 1 (walking skeleton); this stage is about going live for real users and operating the product.

## 1. Production readiness

| Area | Verify |
|------|--------|
| Infrastructure | Services, domains, HTTPS certificates |
| Configuration | Environment variables and secrets |
| Database | Migrations, indexes, backups |
| Security | Permissions, access controls, credentials |
| Performance | Expected capacity and resource limits |
| Observability | Logs, metrics, traces, alerts |
| Recovery | Rollback and data restore |
| Operation | Owners and incident procedure |

Also confirm: no development config active in production, no privileged test accounts, no exposed debug endpoints, no secrets in the code. Rule: never deploy a critical version without knowing how you will detect a failure and how you will recover.

## 2. Deployment strategy

Pick by risk and infrastructure: rolling (gradual instance replacement), blue-green (two environments, instant switch back), canary (small share of users first), feature flags (toggle features without redeploying). A small project may need only a conventional deploy with post-deploy checks and a prepared rollback. No complex infrastructure to look mature.

## 3. Progressive launch

1. **Internal release** — the team uses a production-equivalent version to catch configuration, integration and experience problems.
2. **Limited release** — a selected group uses it in real conditions; collect errors, metrics and feedback. Especially valuable for payments, sensitive data or complex business flows.
3. **General availability** — opened to the target audience once quality and operation criteria are met. Higher risk means stricter advancement criteria.

## 4. Observability

Four pillars: **logs** (events, errors, context to investigate), **metrics** (latency, error rate, volume, resources), **traces** (requests across components), **alerts** (conditions that require action). Every error carries enough technical context to diagnose it and never passwords, tokens, health data or other sensitive data. Availability and latency targets come from business needs; not every app needs the same service level.

## 5. Product analytics

Technical metrics say the app works; product metrics say users get value. An app with excellent uptime can still fail because users leave after three days.

| Category | Examples |
|----------|----------|
| Activation | Users who complete the first valuable action |
| Adoption | Users who use a feature |
| Retention | Users who return within a defined period |
| Conversion | Users who complete the expected goal |
| Efficiency | Time to complete a task |
| Satisfaction | Opinions and reported difficulties |
| Business | Revenue, costs, commercial goals |

Tie them to the 2-3 success metrics from discovery.

## 6. Event tracking plan

A consistent convention before logging anything: `object_action` in snake_case (`account_created`, `transaction_created`, `transaction_creation_failed`, `report_viewed`, `onboarding_completed`). Each event has a definition, owner, allowed properties and privacy rules. Send no unnecessary personal data to analytics platforms. Deliverable: `analytics-tracking-plan.md`.

## 7. Feedback loop

Sources: interviews, support, forms, usability sessions, error reports, behavior metrics. Never implement every suggestion automatically: collect → find recurring problems → weigh impact and evidence → prioritize experiments or improvements → implement and measure. Otherwise the roadmap becomes an endless list of individual requests.

## 8. Incident management

Owners, severity classification, communication channels, mitigation, recovery, follow-up. For a critical incident: detect (alert or report) → assess scope, severity and affected users → apply a safe mitigation → communicate status → restore service and verify data integrity → investigate causes and record preventive actions. Write a blameless postmortem for relevant incidents, focused on technical and organizational causes; depth matches impact.

## 9. Continuous improvement

Each iteration answers new evidence: fix a problem, improve a screen, simplify a flow, optimize a query, build a feature, or **remove a feature that adds no value**. Progress is not measured by code added. Going back to an earlier stage (PRD, UX, even discovery) when evidence demands it is part of the method, not a failure.

## 10. Maintenance

Update dependencies, patch vulnerabilities, review infrastructure costs, keep backups restorable (test the restore), renew certificates, control technical debt, check external integrations still work.

| Frequency | Activities |
|-----------|-----------|
| Continuous | Alerts, incidents, critical errors |
| Weekly | Product health, feedback, regressions |
| Monthly | Performance, costs, dependencies, technical debt |

Adjust frequency to risk and real usage.

## Tools (free tiers or open source; weigh cost and upkeep)

Sentry (errors), OpenTelemetry (instrumentation and traces), Grafana OSS (dashboards), PostHog (product analytics and experiments), Plausible (privacy-focused web analytics), GitHub Actions (deploy automation), Uptime Kuma (uptime monitoring). Some have limited free plans; others you host and operate yourself.

## Deliverables

Real product: `docs/operations/` with `production-readiness.md`, `deployment-strategy.md`, `rollback-plan.md`, `monitoring-and-alerting.md`, `analytics-tracking-plan.md`, `incident-response.md`, `feedback-management.md`, `maintenance-plan.md`, `launch-report.md`. The most important docs are the ones that let you deploy, operate, diagnose and recover.

Small project: a "Deploy and operation" section in the README (how to deploy, roll back, where errors show up) plus the tracking plan if analytics exist.

## Done when

- [ ] Production version meets launch criteria (release gate)
- [ ] Reproducible deploy procedure exists
- [ ] Applicable rollback or recovery strategy tested
- [ ] Migrations and backups controlled
- [ ] Relevant logs, metrics and alerts work
- [ ] Critical flows verified in production
- [ ] Analytics records the defined events
- [ ] Feedback channel for users exists
- [ ] Incident procedure exists
- [ ] Technical and product targets monitored
- [ ] Improvement prioritization process exists
- [ ] Maintenance plan defined
