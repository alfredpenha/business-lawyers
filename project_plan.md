# Project Plan – Avvo Business Lawyer Directory (El Segundo, CA)

## Architecture
- SSR/SSG web app (e.g., Next.js/Remix) consuming search + lead APIs; CDN for assets; feature flags for rollouts; observability (logs/metrics/traces).
- Search index (Elasticsearch/Algolia) with geo fields, facets, and sponsored blending; relational store for lawyer source-of-truth; ingestion/ETL to index.

## Phases
- Phase 0 - Discovery (1-2 wks): Confirm taxonomy, sponsorship rules, lead/CRM integration, analytics spec, SEO requirements, accessibility bar, legal/privacy; define KPIs (CTR, lead rate, call clicks, bounce).
- Phase 1 - Foundations (1-2 sprints): Data model + ingestion; search schema; SSR shell with SEO metadata and cookie/consent; feature flag scaffolding; CI pipeline.
- Phase 2 - APIs & Services (2-3 sprints): Search endpoints (filters, sort, pagination, facets), geo distance, sponsored blending; lead submission endpoint with captcha/rate limits; event logging; error handling/fallbacks.
- Phase 3 - Web UI (2-3 sprints): Directory page (Discovery & Navigation epic) with filters/sorts/pagination + cards (Results & Lead Capture epic); contact CTA modal; ask-a-question link; save/bookmark entry points; SEO/education blocks; accessibility pass.
- Phase 4 - Profile Experience (1-2 sprints): Profile page (Profile Page Experience epic) with header/CTAs, about, ratings breakdown, map/location, reviews/answers, practice/services, fees/languages, resume/endorsements, discipline banner, and save/bookmark behavior (auth redirect + post-login state restore).
- Phase 5 - Quality & Compliance (1-2 sprints): Unit/contract/E2E tests; performance budgets (LCP/CLS/TTI); security review (CSRF/XSS/input validation); accessibility audit; analytics validation.
- Phase 5 - Launch & Iterate (ongoing): Canary/flagged rollout; monitor KPIs; tune search relevance and sponsorship weights; add enhancements (saved filters, richer facets, nearby cities suggestions).

## Team & Roles
- PM (requirements/KPIs), Tech Lead (architecture), FE dev(s) (SSR/UI), BE dev(s) (search/lead), Data/Infra (indexing/ops), QA (automation/E2E), Designer (UX/accessibility).

## Deliverables
- PRD with canonical user stories grouped by epics; acceptance criteria per story; API contracts; UI/interaction mocks (directory + profile + save/auth redirect); tracking plan; test plan; ops/runbook; launch checklist.
- Event/analytics schema covering directory interactions (sort/filter/pagination/card clicks/CTA clicks/save) and profile interactions (CTA clicks, save/bookmark, reviews pagination, map click); auth funnel events (save-triggered login, success/failure, return-to).

## Risks & Mitigations
- Search relevance/latency: cache + tuned scoring; monitor p95 latency.
- Lead spam/abuse: captcha + rate limits + heuristic/blacklist + anomaly alerts.
- SEO regressions: enforce SSR, canonical/structured data, crawlable internal links; monitor crawl/index metrics.
- Accessibility gaps: early axe/Pa11y in CI; manual audits.
- Analytics integrity: event schema versioning; QA dashboards; UTM propagation tests.
