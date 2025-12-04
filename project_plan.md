# Project Plan - Avvo Business Lawyer Directory (El Segundo, CA)

## Overview
- Objective: deliver an Avvo-style business lawyer directory and profile experience for El Segundo, CA with lead capture (call/message/chat), Pro CTAs, sponsored listings, transparency/insights content, and strong SEO/accessibility.
- Approach: incremental, flag-driven releases per phased plan; user stories/acceptance criteria drive scope; observability and analytics built in for all critical flows.
- Outcomes: searchable directory with filters/sort/pagination, rich profiles, intake/contact flows, sponsored placements with disclosure, and validated tracking/quality gates before launch.
- Timeline (worst case): ~15 weeks through UAT based on phased durations; staged releases can ship earlier for directory (after Phase 3) and profile (after Phase 4) under flags/canary.

## Phases (incremental releases with demos; worst-case durations)
- Phase 0 - Discovery (approx 1 week): Confirm taxonomy, sponsorship rules, lead/CRM integration, analytics spec, SEO requirements, accessibility bar, legal/privacy; define KPIs (CTR, lead rate, call clicks, bounce). Demo: requirements/KPI review; no code release.
- Phase 1 - Foundations (approx 2 weeks): Data model + ingestion; search schema; SSR shell with SEO metadata and cookie/consent; feature flag scaffolding; CI pipeline. Demo: SSR shell with basic routing; Release: none or dark-launch infra only.
- Phase 2 - APIs & Services (approx 3 weeks): Search endpoints (filters, sort, pagination, facets) for US-DN-2/3/4 and US-DR-1/2; geo distance; sponsored blending; lead submission endpoints for US-DR-4/12; event logging; error handling/fallbacks. Demo: API contracts + Postman run; Release: backend endpoints behind flags.
- Phase 3 - Web UI: Directory (approx 3 weeks): Directory page for US-DN-1/2/3/4 and US-DR-1/2/3/4/5/6/7/8/9/10/11/12; contact CTA modal + detailed message/intake flow; ask-a-question; save/bookmark entry points; SEO/education blocks; transparency/insights; nearby cities/practice areas/resources; accessibility pass. Demo: staging walkthrough; Release: staged/canary with feature flags.
- Phase 4 - Profile Experience (approx 2 weeks): Profile page for US-PF-1..11 including save/bookmark auth redirect, Pro CTAs, ratings, map, reviews/answers, resume, discipline banner. Demo: staging walkthrough; Release: flagged/canary.
- Phase 5 - Quality & Compliance (approx 2 weeks): Unit/contract/E2E tests mapped to US IDs; performance budgets (LCP/CLS/TTI); security review (CSRF/XSS/input validation); accessibility audit; mobile/responsive verification; analytics validation. Demo: test/QA report; Release: incremental fixes to staging/prod behind flags.
- Phase 6 - UAT (approx 2 weeks): Client/stakeholder UAT on staging with US ID checklist; sign-off on acceptance criteria, analytics events, and accessibility; triage/fix UAT defects. Demo: UAT review; Release: fixes via flags/canary.
- Phase 7 - Launch & Iterate (ongoing): Progressive rollout (no big bang), canary/feature flags; monitor KPIs; tune search relevance and sponsorship weights; enhancements (saved filters, richer facets, nearby cities suggestions).

## Team & Roles (suggested staffing)
- Product: 1 PM (requirements/KPIs/backlog), 1 UX/Content strategist (information architecture, copy for trust/SEO blocks).
- Design/UX: 1 Product Designer (directory + profile UI, forms, chat/CTA states), 1 UX Researcher (lightweight validation/UAT support).
- Frontend: 2 FE Engineers (SSR/SSG, directory/profile pages, forms, accessibility), 1 shared FE QA automation.
- Backend: 2 BE Engineers (search/indexing, lead/chat integrations, sponsored logic, auth/save), 1 Data/Infra Engineer (ETL/indexing, observability, CI/CD).
- QA: 1 QA Lead (test plan, UAT coordination) + 1 QA Engineer (automation/E2E mapped to US IDs).
- Analytics/Observability: 1 Analytics Engineer (event schema, dashboards, alerting) shared with team.

### Minimal team (roles combined where feasible)
- PM/UX writer (combined): owns requirements, KPIs, backlog, and UX copy (trust/SEO/consent text).
- Product Designer: owns directory/profile UI, forms, chat/CTA states, and accessibility in design.
- FE Engineer (2): builds SSR/SSG UI, forms, Pro CTAs, accessibility; one also covers basic FE automation.
- BE Engineer (1–2): owns search endpoints, lead/chat integrations, sponsored logic, auth/save; pairs with FE on contracts.
- QA (1): plans/executes tests, drives UAT checklist; leverages FE for automation support.
- Analytics/Observability (part-time): defines events, dashboards, alerts; can be covered by BE/FE with support from PM if dedicated role unavailable.

## Implementation Plan & Delivery (worst-case)
- Sequenced per phases above with demos at each phase end; feature flags/canary releases to avoid big bang.
- Worst-case cumulative delivery to production feature-complete (through UAT sign-off): ~15 weeks (1+2+3+3+2+2+2), excluding ongoing Launch & Iterate. Critical scope can ship earlier via staged releases after Phases 3–4.
- UAT is run on staging with the US-to-test checklist; only Sev1/Sev2 blockers delay release; non-blockers triaged for post-launch fixes.

## Deliverables
- PRD with canonical user stories grouped by epics; acceptance criteria per story; API contracts; UI/interaction mocks (directory + profile + save/auth redirect); tracking plan; test plan; ops/runbook; launch checklist.
- US-to-test mapping matrix (US IDs ↔ acceptance criteria ↔ test cases), used as a checklist for dev/QA/client signoff.
- Event/analytics schema covering directory interactions (sort/filter/pagination/card clicks/CTA clicks/save) and profile interactions (CTA clicks, save/bookmark, reviews pagination, map click); auth funnel events (save-triggered login, success/failure, return-to); message/intake form events (open, validation errors, submit success/fail, retry).
- Observability plan: logging/metrics/traces coverage for search, lead submission (message/intake), chat, sponsored inventory, and save/bookmark flows; dashboards and alerts defined; runbook for alert response.
- Release plan with per-phase demos and incremental launches (canary/flags), avoiding big bang release.
- Mobile test plan: responsive breakpoints, tap-target sizes, form usability on mobile keyboards, sticky CTA behavior, and mobile performance budgets.

## Risks & Mitigations
- Search relevance/latency: cache + tuned scoring; monitor p95 latency.
- Lead spam/abuse: captcha + rate limits + heuristic/blacklist + anomaly alerts.
- SEO regressions: enforce SSR, canonical/structured data, crawlable internal links; monitor crawl/index metrics.
- Accessibility gaps: early axe/Pa11y in CI; manual audits.
- Analytics integrity: event schema versioning; QA dashboards; UTM propagation tests.
