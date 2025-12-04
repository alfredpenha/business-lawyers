# Functional Requirements – Avvo Business Lawyer Directory (El Segundo, CA)

## User Stories (Canonical, grouped by epic)

### Epic: Directory Discovery & Navigation
- US-DN-1: As a visitor, I want to see the breadcrumb and page title for the practice area and city so that I know I am on the correct directory page.
- US-DN-2: As a visitor, I want to change the practice area and location via validated inputs so that I can refine the results and share the state through the URL.
- US-DN-3: As a visitor, I want to sort results (e.g., relevance, distance) so that I can prioritize the list based on my needs and keep the sort in the URL.
- US-DN-4: As a visitor, I want to page through results with the current page reflected in the URL so that I can browse all options without losing my filters and sort.

### Epic: Directory Results & Lead Capture
- US-DR-1: As a visitor, I want to scan lawyer cards (name, headshot, Avvo rating meter 0-10, stars, review count, years licensed, practice tags, city/state, distance) so that I can quickly assess fit.
- US-DR-2: As a visitor, I want to see badges like "Available for hire?" and "Phone consultation available" when applicable so that I know who is reachable and how.
- US-DR-3: As a visitor, I want to open a lawyer profile by clicking the card/name/photo so that I can view full details, and the click should be tracked.
- US-DR-4: As a visitor, I want to initiate contact from the card (click-to-call and/or Message modal with validation and feedback) so that I can reach the lawyer and know the request went through.
- US-DR-5: As a visitor, I want to see enhanced CTAs on promoted/Pro lawyer cards (Call for a free consultation, Chat/live chat, Message, and Visit website) so that I can choose my preferred contact channel.
- US-DR-6: As a visitor, I want to ask a question (Avvo Q&A) with the lawyer attribution carried over so that I can get public advice from that lawyer.
- US-DR-7: As a visitor, I want to read SEO/educational blocks and footer navigation so that I can learn about hiring and explore related cities/practice areas.
- US-DR-8: As a visitor, I want to interact with the cookie/consent notice so that my preference is recorded and respected.
- US-DR-9: As a visitor, I want to discover nearby cities, related practice areas, and additional resources (user help and attorney-facing help) so that I can continue exploring relevant options if this page does not meet my needs.
- US-DR-10: As a visitor, I want to understand how Avvo sources and moderates data/reviews and to see attorney insights lists (e.g., licensed longest, newest to area, most reviewed, best reviewed) so that I trust the information and can browse notable lawyers.
- US-DR-11: As a visitor, I want sponsored listings to be clearly labeled and positioned per business rules so that I can distinguish paid placements from organic results.
- US-DR-12: As a visitor, I want to complete a detailed message/intake form after clicking Message so that I can provide the attorney with structured information and receive confirmation of submission.

### Epic: Profile Page Experience
- US-PF-1: As a visitor, I want to see a profile header (name, photo, practice, location, rating meter, stars, review count, years licensed, "available for hire" status, discipline note if any) so that I can trust the lawyer's credentials.
- US-PF-2: As a visitor, I want to use primary CTAs ("Call now", "Message", "Ask a question") from the profile so that I can contact the lawyer directly with confirmation of success/failure.
- US-PF-3: As a visitor, I want to read the About section with a narrative summary so that I understand the lawyer's focus and background.
- US-PF-4: As a visitor, I want to view ratings details (Avvo rating dial, client rating, rating distribution, profile completeness) so that I know how the rating was derived.
- US-PF-5: As a visitor, I want to see a location block with map, address, and office details so that I can plan a visit or verify proximity.
- US-PF-6: As a visitor, I want to browse reviews with pagination, sort/filter (if offered), and dates so that I can gauge quality over time.
- US-PF-7: As a visitor, I want to see answers the lawyer has provided to questions so that I can assess expertise.
- US-PF-8: As a visitor, I want to read practice areas/services, fees/payment types, languages, and associations/awards so that I know if the lawyer matches my needs.
- US-PF-9: As a visitor, I want to see resume details (education, work history, licenses, publications) and endorsements from other attorneys so that I can verify credibility.
- US-PF-10: As a visitor, I want any disciplinary history to be clearly labeled so that I can make an informed decision.
- US-PF-11: As a visitor, I want to save/bookmark a lawyer, and if I am not signed in, I want to be prompted with a sign-in/sign-up flow (email or social login) so that I can complete the save action after authenticating.

## Acceptance Criteria (traceable checklist)

### US-DN-1
- [ ] Breadcrumb and H1 show practice area + city derived from URL/state; SEO title/description present and rendered server-side.
- [ ] Page load displays correct location context without user input.

### US-DN-2
- [ ] Practice area/location inputs validate non-empty and allowed values; invalid entries show inline error and block submit.
- [ ] On submit, results refresh and URL gains query params for practice + location; reloading preserves state.

### US-DN-3
- [ ] Sort control shows relevance and distance (plus any configured sorts); default is relevance.
- [ ] Selecting a sort refreshes results within one user action and updates the URL; reload preserves sort.
- [ ] Analytics event fires on sort change with sort id, location/practice context, and page number.

### US-DN-4
- [ ] Pagination control shows current page; next/previous changes results and URL page param.
- [ ] Filters and sort persist when paging forward/back; reload on a paged URL shows the same list.
- [ ] Analytics event fires on page change with page number, filters, sort, and location/practice context.

### US-DR-1
- [ ] Each card renders name, photo (with fallback), rating meter 0-10, stars, review count, years licensed, practice tags, city/state, distance; missing data uses explicit placeholders.
- [ ] Data matches backend payload for the same lawyer id.

### US-DR-2
- [ ] “Available for hire?” and “Phone consultation available” badges display only when the backend flags are true; absent otherwise.

### US-DR-3
- [ ] Clicking card/name/photo opens the profile (same/new tab per design); event logs lawyer id and list position.

### US-DR-4
- [ ] Click-to-call uses `tel:` with formatted number; click event logged.
- [ ] Message CTA opens modal, enforces required fields, blocks duplicate submit while pending, and shows success/failure.
- [ ] Analytics events for call click and message open/submit (success/failure) include lawyer id and list position.

### US-DR-5
- [ ] Pro cards show "Call for a free consultation" (tel link, tracked), "Chat" opens live chat widget/session, "Message" follows same validation, and "Visit website" opens external site in a new tab with tracking.
- [ ] Pro CTAs render only when backend flags are set; if chat service is unavailable, chat CTA hides or shows an error state.
- [ ] Chat opens a live session in a new window/modal to the configured provider (e.g., ngage), shows provider branding and disclaimer, loads within 2-3s, and is not blocked by default pop-up settings (or gracefully instructs user if blocked).
- [ ] Chat allows the user to send messages (up to provider limit, e.g., 1500 chars), displays operator join status, and can collect contact info (phone/email) inline.
- [ ] If chat disconnects or operator unavailable within SLA, user sees a clear fallback (e.g., leave a message or use call/message CTAs).
- [ ] Analytics events for Pro CTAs (call, chat open/close, chat fail, website click, message) include lawyer id and sponsored flag.

### US-DR-6
- [ ] Ask-a-question link deep-links to Q&A with lawyer attribution; click is tracked; link resolves.

### US-DR-7
- [ ] SEO/educational blocks and footer links render and are clickable; links are crawlable (no blocked robots meta on these blocks).
- [ ] Analytics events for key content link clicks (e.g., education blocks) include section id and destination.

### US-DR-8
- [ ] Cookie/consent banner appears once per user/session until actioned; accept/dismiss choice stored (cookie/local storage) and respected on reload.
- [ ] Consent choice is logged for audit (no PII), and future analytics respect consent status.

### US-DR-9
- [ ] "Nearby cities" chips/links render for the current metro/region; each link navigates to the respective city directory and is crawlable.
- [ ] "Related practice areas" chips/links render; each navigates to the related practice directory for the same location and is crawlable.
- [ ] Additional resources (user help: FAQs, messaging privacy, reviews, Avvo rating; attorney help: grow practice, edit claimed profile, increase rating) render as links; each link resolves and is tracked.
- [ ] Links open within the site context (no unexpected external opens) unless explicitly external; if external, open in new tab with clear indication.

### US-DR-10
- [ ] Transparency/trust block renders explanatory text on data sources, verification, review policies, and moderation; includes a working support contact link.
- [ ] Attorney insights lists render tabs/pills for “Licensed the longest,” “Newest to the area,” “Most Reviewed,” “Best Reviewed” with counts; default tab selected per design.
- [ ] Each list shows lawyers with name linked to profile and relevant metric (e.g., years licensed, review count, rating); data matches backend for the location/practice.
- [ ] “Sort lawyers by…” link/button navigates to the appropriate sorted directory view (e.g., by most years licensed) and preserves location/practice context.

- [ ] Analytics events for tab switches and support link clicks include list type and location/practice context.

### US-DR-11
- [ ] Sponsored listings render in a dedicated area with explicit "Sponsored" or equivalent label; label is visible and readable.
- [ ] Sponsored cards include the same core card data as organic plus Pro CTAs if applicable; links to profiles work and are tracked distinctly as sponsored.
- [ ] Sponsored placement order follows backend ranking rules; when no sponsored inventory is available, the section hides gracefully.
- [ ] Analytics capture sponsored impressions/clicks separately from organic; disclosures comply with policy.

### US-DR-12
- [ ] Message flow opens a dedicated intake form prefilled with the lawyer’s name/profile summary; form includes required dropdowns for incident context (e.g., injury at work, time since incident, actions taken, primary injury type) and location input.
- [ ] Freeform description textarea supports up to 2000 characters with live counter; required; cannot submit empty.
- [ ] Optional phone callback preference checkbox; when checked, phone field and time-of-day radio buttons become required and enforce format/selection.
- [ ] CAPTCHA present and required; submit disabled until CAPTCHA passes and required fields are valid; inline errors shown for missing/invalid inputs.
- [ ] Submission posts lead to backend; on success, user sees confirmation; on failure, user sees an error without losing entered data and can retry; links to Terms of Use, Community Guidelines, and Privacy Policy are present near submit.

### US-PF-1
- [ ] Profile header shows name, photo, practice, location, rating meter/stars, review count, years licensed, availability, and discipline note (if any); matches directory card values.

### US-PF-2
- [ ] Call uses `tel:` link; Message validates required fields and shows success/failure; Ask deep-links to Q&A with attribution; all clicks tracked.

### US-PF-3
- [ ] About section renders narrative text with preserved line breaks; long text truncates/expands per design.

### US-PF-4
- [ ] Ratings block shows dial (0-10), client rating, distribution histogram, and profile completeness; values match backend and card summary.

### US-PF-5
- [ ] Location block shows address, phone, office hours (if provided), and map pin; map link opens external map provider; address is copyable.

### US-PF-6
- [ ] Reviews list paginates or lazy-loads; each review shows reviewer name/initials, date, rating, and text; sort/filter works if present; abuse/report link appears if required.

### US-PF-7
- [ ] Answers section lists Q&A responses with timestamps and links to the original questions; paginates if over page size.

### US-PF-8
- [ ] Practice/services, fees/payment, languages, associations/awards render as structured lists; “View more” expands long lists.

### US-PF-9
- [ ] Resume shows education, work history, licenses, publications; endorsements show peer name/role/text; moderation filters inappropriate content.

### US-PF-10
- [ ] Discipline banner displays when provided, cannot be dismissed, and links to details when available.

### US-PF-11
- [ ] Save/bookmark CTA toggles saved state for authenticated users and reflects state (icon/label).
- [ ] Unauthenticated users are redirected to sign-in (email-first plus social options: Facebook, Twitter/X, LinkedIn, Google); return-to path/state preserved; on return, saved state is applied and confirmed.

## Mobile/Responsive Criteria (applies across user stories)
- [ ] Layout adapts to mobile viewport (e.g., single-column cards, readable text without zoom, no horizontal scroll).
- [ ] Tap targets meet minimum size (~44px) with adequate spacing; CTAs remain visible and tappable.
- [ ] Sticky or easily reachable CTAs on profile/message pages (if designed); fixed elements do not obscure content.
- [ ] Forms (message/intake) fit within viewport, inputs accessible with on-screen keyboard; validation/errors visible without forcing horizontal scroll.
- [ ] Navigation, filters/sorts, and pagination are usable on mobile (e.g., dropdowns/selects sized for touch); cookie/consent banner does not block primary actions.
- [ ] Images and maps scale responsively; cards and sections wrap/stack gracefully; footers remain navigable on mobile.

## Business Logic & Behaviors
- Ranking: default relevance; distance sort uses geo from selected location (El Segundo centroid unless overridden). Sponsored/featured (if present) are labeled and ranked per ad rules without hiding disclosures.
- Pagination: consistent page size; URL carries page number; maintaining filters/sort between pages.
- Contact CTAs: click-to-call logs event; message modal posts lead to backend; ask-a-question deep-link carries attribution; phone numbers formatted for tel links.
- Message intake form: prefilled with lawyer data; enforces required context dropdowns, location, description length, optional phone callback preference and time-of-day; CAPTCHA required; preserves data on submit failures.
- Ratings: Avvo 0-10 meter and star equivalent; review count shown; years licensed derived from bar admission year.
- Badges: availability and phone consultation derived from profile attributes; only shown when applicable.
- Empty/error states: if no results or search failure, show helpful guidance/nearby options and keep SEO content visible.
- SEO content blocks and footer links are crawlable; directory links use canonical URLs.
- Profile tabs (About/Reviews/Resume/Contact) load content without losing contact CTAs; tab state deep-linkable if available.
- Profile rating details include rating dial, client rating, distribution histogram, and profile completeness; data stays consistent with card summary.
- Profile reviews support pagination, date display, and ordering; review spam/abuse moderated.
- Map block uses geo coordinates for the office; address is copyable and click-to-map opens in an external map provider.
- Endorsements display peer name/role and are moderated; discipline notices appear prominently when present.
- Pro/promoted logic: backend flags enable enhanced CTAs (free consultation call, chat, website link); disclosures/labels shown if required; CTAs degrade gracefully if the service is unavailable.
- Save/bookmark: requires authentication; if not authenticated, redirect to sign-in with email-first and social OAuth options; on success, redirect back and persist saved state. Show saved/unsaved UI states and allow undo if supported.
- Chat behavior: external/live chat opens in new window/modal; includes provider branding/disclaimer; supports operator join/typing status; collects optional contact info; fallback messaging if no operator responds within SLA; pop-up blockers handled gracefully.
- Sponsored listings: clearly labeled; placement order per ads ranking rules; separable tracking for impressions/clicks; hide section when no sponsored inventory; disclosures compliant with ads policy.
- Observability: key flows (search, lead submission, chat, save/bookmark) emit logs/metrics/traces; alerts on elevated error rates or latency regressions; dashboards for traffic, conversion, and CTA-level performance.

## Non-Visible / Backend Requirements
- Data model: lawyer profile with name, license status/year, practice areas, location (city/state + geo point), phone, contactability, ratings, review count, consultation flags, sponsorship level, availability.
- Search/index: geo search with facets, sort options, pagination; fast responses; graceful fallback if search is degraded.
- Lead handling: contact form posts to CRM/notification service; rate limits, captcha/abuse checks; email/SMS/webhook alerts to lawyers; audit logs for submissions.
- Tracking/analytics: pageviews; sort/filter changes; card impressions; CTA clicks (call/message/ask); pagination events; UTM propagation; A/B flags.
- Observability/monitoring: structured logs for errors and key flows (search, lead submission, chat), metrics for latency/error rates/throughput, traces for API calls; dashboards and alerts on search errors, lead failures, chat failures, sponsored inventory outages.
- SEO: SSR/SSG for directory; canonical tags; structured data (LocalBusiness/Attorney list); OpenGraph/Twitter metadata.
- Accessibility/compliance: semantic headings; aria labels on buttons/forms; keyboard focus states; color contrast; CSRF protection on forms; TLS everywhere; cookie consent handling.
- Performance: image lazy-load; CDN for assets; caching for search queries; hydration for interactivity; monitor LCP/CLS/TTI.
- Operations: feature flags for UI and ranking tweaks; logging/metrics/alerts on search errors and lead failures; rate limiting for APIs.
- Profile data services: detailed profile API exposing about text, ratings breakdown, reviews feed with pagination, endorsements, Q&A answers, resume/education/licensing, fees/languages/payment methods, associations/awards, and discipline status.
- Structured data on profile: Person/Attorney schema with sameAs/aggregateRating if allowed, and canonical URLs.
- Review and endorsement moderation pipelines; spam/abuse detection for Q&A answers and reviews.
- Map integration uses geo coordinates; external map links templated; privacy-respecting embedding where applicable.
- Consistency checks to ensure directory card summary matches profile header data (rating, reviews, years licensed, availability).
- Save service/API: persists saved lawyers to user account; idempotent toggle; requires auth token; returns saved state for hydration. Sign-in supports email-first and social OAuth providers; return-to parameter preserved after login/signup. Security: CSRF protection, OAuth state/PKCE where applicable.
- Pro/promoted services: flags per lawyer indicating Pro status and enabled CTAs (consult call number, live chat endpoint/config, website URL); chat service integration with availability status and failover; external website links validated/whitelisted; tracking on all Pro CTAs; labeling/disclosure where required.
- Chat integration: provider configuration (URL, website id, branding), SLA/timeout handling, transcript storage (if allowed), privacy/disclaimer text management, pop-up handling instructions; fallback to message/lead capture when chat unavailable; analytics for chat open/close, operator connect, message sent, fail/timeout.
- Ads/sponsored service: supplies sponsored inventory with labels, placement rules, and tracking ids; ensures compliance with disclosure policies; returns empty when no inventory; separates analytics for sponsored vs organic.
- Message intake: lead payload includes structured fields (context dropdowns, location, description up to 2000 chars, optional phone + time preference), lawyer id, and source; CAPTCHA verification; idempotent submission handling and retry without data loss.

## Definition of Done
- All acceptance criteria checkboxes for included user stories are satisfied and demonstrated.
- Automated tests updated/added (unit for logic, integration/contract for APIs, UI/E2E for critical flows: search/sort/pagination, contact, save/bookmark, Pro CTAs).
- Accessibility checks pass (keyboard, aria labels, contrast) on directory and profile views.
- Analytics/tracking events verified in lower envs for all CTAs (call, message, ask, chat, save, website).
- Performance meets agreed thresholds (e.g., LCP/CLS within budget on directory and profile for p75).
- No known Sev1/Sev2 defects open for the implemented scope; documentation updated (API contracts, runbooks if applicable).

## Assumptions
- Standard Avvo directory layout and taxonomy are used; no on-page account creation needed.
- Ratings/reviews are precomputed and supplied by backend; no inline review submission.
- Sponsored placements, if any, are injected by a ranking service with clear labels.
- Geo defaults to El Segundo city centroid unless user overrides location.
- Ask-a-question routes to existing Avvo Q&A flow with attribution.
- Cookie consent stored client-side (cookie/local storage) and respected.
- Profile content (about, resume, answers) is read-only here; edits happen elsewhere by the lawyer.
- Discipline data is provided by a trusted source and flagged for display when present.
- Save/bookmark uses existing Avvo account system; social logins are federated via OAuth and do not auto-post to networks.
- Logged-in state is assumed available (account menu, notifications, saved items, asked questions, reviews, sign out); authentication UX itself is out of scope except for redirects from save/bookmark flows.


