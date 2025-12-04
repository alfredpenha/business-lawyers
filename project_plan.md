# Project Plan - Avvo Business Lawyer Directory (El Segundo, CA)

## Phases (1-2 weeks each, incremental releases with demos)
- Phase 0 - Discovery (1 week): Confirm taxonomy, sponsorship rules, lead/CRM integration, analytics spec, SEO requirements, accessibility bar, legal/privacy; define KPIs (CTR, lead rate, call clicks, bounce). Demo: requirements/KPI review; no code release.
- Phase 1 - Foundations (1-2 weeks): Data model + ingestion; search schema; SSR shell with SEO metadata and cookie/consent; feature flag scaffolding; CI pipeline. Demo: SSR shell with basic routing; Release: none or dark-launch infra only.
- Phase 2 - APIs & Services (1-2 weeks): Search endpoints (filters, sort, pagination, facets) for US-DN-2/3/4 and US-DR-1/2; geo distance; sponsored blending; lead submission endpoints for US-DR-4/12; event logging; error handling/fallbacks. Demo: API contracts + Postman run; Release: backend endpoints behind flags.
- Phase 3 - Web UI: Directory (1-2 weeks): Directory page for US-DN-1/2/3/4 and US-DR-1/2/3/4/5/6/7/8/9/10/11/12; contact CTA modal + detailed message/intake flow; ask-a-question; save/bookmark entry points; SEO/education blocks; transparency/insights; nearby cities/practice areas/resources; accessibility pass. Demo: staging walkthrough; Release: staged/canary with feature flags.
- Phase 4 - Profile Experience (1-2 weeks): Profile page for US-PF-1..11 including save/bookmark auth redirect, Pro CTAs, ratings, map, reviews/answers, resume, discipline banner. Demo: staging walkthrough; Release: flagged/canary.
- Phase 5 - Quality & Compliance (1-2 weeks): Unit/contract/E2E tests mapped to US IDs; performance budgets (LCP/CLS/TTI); security review (CSRF/XSS/input validation); accessibility audit; analytics validation. Demo: test/QA report; Release: incremental fixes to staging/prod behind flags.
- Phase 6 - UAT (1-2 weeks): Client/stakeholder UAT on staging with US ID checklist; sign-off on acceptance criteria, analytics events, and accessibility; triage/fix UAT defects. Demo: UAT review; Release: fixes via flags/canary.
- Phase 7 - Launch & Iterate (ongoing): Progressive rollout (no big bang), canary/feature flags; monitor KPIs; tune search relevance and sponsorship weights; enhancements (saved filters, richer facets, nearby cities suggestions).

## Team & Roles (suggested staffing)
- Product: 1 PM (requirements/KPIs/backlog), 1 UX/Content strategist (information architecture, copy for trust/SEO blocks).
- Design/UX: 1 Product Designer (directory + profile UI, forms, chat/CTA states), 1 UX Researcher (lightweight validation/UAT support).
- Frontend: 2 FE Engineers (SSR/SSG, directory/profile pages, forms, accessibility), 1 shared FE QA automation.
- Backend: 2 BE Engineers (search/indexing, lead/chat integrations, sponsored logic, auth/save), 1 Data/Infra Engineer (ETL/indexing, observability, CI/CD).
- QA: 1 QA Lead (test plan, UAT coordination) + 1 QA Engineer (automation/E2E mapped to US IDs).
- Analytics/Observability: 1 Analytics Engineer (event schema, dashboards, alerting) shared with team.

## Deliverables
- PRD with canonical user stories grouped by epics; acceptance criteria per story; API contracts; UI/interaction mocks (directory + profile + save/auth redirect); tracking plan; test plan; ops/runbook; launch checklist.
- US-to-test mapping matrix (US IDs ↔ acceptance criteria ↔ test cases), used as a checklist for dev/QA/client signoff.
- Event/analytics schema covering directory interactions (sort/filter/pagination/card clicks/CTA clicks/save) and profile interactions (CTA clicks, save/bookmark, reviews pagination, map click); auth funnel events (save-triggered login, success/failure, return-to); message/intake form events (open, validation errors, submit success/fail, retry).
- Observability plan: logging/metrics/traces coverage for search, lead submission (message/intake), chat, sponsored inventory, and save/bookmark flows; dashboards and alerts defined; runbook for alert response.
- Release plan with per-phase demos and incremental launches (canary/flags), avoiding big bang release.

## Risks & Mitigations
- Search relevance/latency: cache + tuned scoring; monitor p95 latency.
- Lead spam/abuse: captcha + rate limits + heuristic/blacklist + anomaly alerts.
- SEO regressions: enforce SSR, canonical/structured data, crawlable internal links; monitor crawl/index metrics.
- Accessibility gaps: early axe/Pa11y in CI; manual audits.
- Analytics integrity: event schema versioning; QA dashboards; UTM propagation tests.
