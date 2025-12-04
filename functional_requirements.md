# Functional Requirements – Avvo Business Lawyer Directory (El Segundo, CA)

## User Stories (Canonical, grouped by epic)

### Epic: Directory Discovery & Navigation
- As a visitor, I want to see the breadcrumb and page title for the practice area and city so that I know I am on the correct directory page.
- As a visitor, I want to change the practice area and location via validated inputs so that I can refine the results and share the state through the URL.
- As a visitor, I want to sort results (e.g., relevance, distance) so that I can prioritize the list based on my needs and keep the sort in the URL.
- As a visitor, I want to page through results with the current page reflected in the URL so that I can browse all options without losing my filters and sort.

### Epic: Directory Results & Lead Capture
- As a visitor, I want to scan lawyer cards (name, headshot, Avvo rating meter 0-10, stars, review count, years licensed, practice tags, city/state, distance) so that I can quickly assess fit.
- As a visitor, I want to see badges like "Available for hire?" and "Phone consultation available" when applicable so that I know who is reachable and how.
- As a visitor, I want to open a lawyer profile by clicking the card/name/photo so that I can view full details, and the click should be tracked.
- As a visitor, I want to initiate contact from the card (click-to-call and/or Message modal with validation and feedback) so that I can reach the lawyer and know the request went through.
- As a visitor, I want to see enhanced CTAs on promoted/Pro lawyer cards (Call for a free consultation, Chat/live chat, Message, and Visit website) so that I can choose my preferred contact channel.
- As a visitor, I want to ask a question (Avvo Q&A) with the lawyer attribution carried over so that I can get public advice from that lawyer.
- As a visitor, I want to read SEO/educational blocks and footer navigation so that I can learn about hiring and explore related cities/practice areas.
- As a visitor, I want to interact with the cookie/consent notice so that my preference is recorded and respected.

### Epic: Profile Page Experience
- As a visitor, I want to see a profile header (name, photo, practice, location, rating meter, stars, review count, years licensed, "available for hire" status, discipline note if any) so that I can trust the lawyer's credentials.
- As a visitor, I want to use primary CTAs ("Call now", "Message", "Ask a question") from the profile so that I can contact the lawyer directly with confirmation of success/failure.
- As a visitor, I want to read the About section with a narrative summary so that I understand the lawyer's focus and background.
- As a visitor, I want to view ratings details (Avvo rating dial, client rating, rating distribution, profile completeness) so that I know how the rating was derived.
- As a visitor, I want to see a location block with map, address, and office details so that I can plan a visit or verify proximity.
- As a visitor, I want to browse reviews with pagination, sort/filter (if offered), and dates so that I can gauge quality over time.
- As a visitor, I want to see answers the lawyer has provided to questions so that I can assess expertise.
- As a visitor, I want to read practice areas/services, fees/payment types, languages, and associations/awards so that I know if the lawyer matches my needs.
- As a visitor, I want to see resume details (education, work history, licenses, publications) and endorsements from other attorneys so that I can verify credibility.
- As a visitor, I want any disciplinary history to be clearly labeled so that I can make an informed decision.
- As a visitor, I want to save/bookmark a lawyer, and if I am not signed in, I want to be prompted with a sign-in/sign-up flow (email or social login) so that I can complete the save action after authenticating.

## Acceptance Criteria (per user story)

### Epic: Directory Discovery & Navigation
- Breadcrumb/page title visible on load; match practice area + city from URL; SEO tags present.
- Practice area/location inputs validate (non-empty, known geo/practice); submitting updates list and URL query params.
- Sort dropdown exposes relevance/distance (and any additional sorts); selection updates list within 1 refresh; persists in URL.
- Pagination shows current page; clicking next/previous updates list and URL; filters/sort preserved across pages.

### Epic: Directory Results & Lead Capture
- Cards display name, photo, rating meter (0-10), stars, review count, years licensed, practice tags, city/state, distance; all fields populated from backend; missing data uses graceful fallbacks.
- Availability/phone consultation badges show only when true; hidden when not applicable.
- Clicking card/name/photo opens profile in same/new tab per design; navigation tracked with event payload (lawyer id, position).
- Click-to-call uses tel link on mobile/desktop; triggers tracking event; Message CTA opens modal, enforces required fields, shows success/failure; no duplicate submissions when pending.
- Pro/promoted cards show “Call for a free consultation” (tel link, tracked), “Chat” opens live chat widget/session, “Message” uses same validation rules, and “Visit website” opens lawyer’s external site in new tab with tracking; CTAs available only when provisioned by backend flags.
- Ask-a-question link pre-fills attribution for the lawyer; tracked click; deep link resolves.
- SEO/education/footer blocks render on page; links are crawlable and functional.
- Cookie/consent banner appears once per user/session until actioned; accept/dismiss stored and respected on reload.

### Epic: Profile Page Experience
- Header shows name, photo, practice, location, rating meter/stars, review count, years licensed, availability, and discipline note if applicable; matches directory card data.
- Primary CTAs (Call, Message, Ask) visible above the fold; Call uses tel link; Message validates required fields, shows success/failure; Ask deep-links to Q&A with attribution.
- About section renders narrative text; preserves basic formatting; truncates/expands per design if long.
- Ratings block shows dial (0-10), client rating, distribution histogram, and profile completeness; values match backend; no mismatches with card.
- Location block displays address, phone, office hours (if provided) and map pin; map link opens external map provider; address copyable.
- Reviews list paginates (or lazy-loads); shows reviewer name/initials, date, rating, text; sort/filter if offered; abuse-report link if required.
- Answers section lists Q&A responses with links back to questions; timestamps visible; pagination if more than page size.
- Practice/services, fees/payment, languages, associations/awards present as structured lists; “View more” expands long lists.
- Resume shows education, work history, licenses, publications; endorsements show peer name/role/text; moderation filters inappropriate content.
- Discipline banner displays when provided; cannot be hidden; links to details (if available).
- Save/bookmark CTA triggers save on authenticated users; unauthenticated users are redirected to sign-in with email-first plus social options (Facebook, Twitter/X, LinkedIn, Google); return-to path/state preserved; saved state reflected on return (e.g., icon toggled, confirmation).

## Business Logic & Behaviors
- Ranking: default relevance; distance sort uses geo from selected location (El Segundo centroid unless overridden). Sponsored/featured (if present) are labeled and ranked per ad rules without hiding disclosures.
- Pagination: consistent page size; URL carries page number; maintaining filters/sort between pages.
- Contact CTAs: click-to-call logs event; message modal posts lead to backend; ask-a-question deep-link carries attribution; phone numbers formatted for tel links.
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

## Non-Visible / Backend Requirements
- Data model: lawyer profile with name, license status/year, practice areas, location (city/state + geo point), phone, contactability, ratings, review count, consultation flags, sponsorship level, availability.
- Search/index: geo search with facets, sort options, pagination; fast responses; graceful fallback if search is degraded.
- Lead handling: contact form posts to CRM/notification service; rate limits, captcha/abuse checks; email/SMS/webhook alerts to lawyers; audit logs for submissions.
- Tracking/analytics: pageviews; sort/filter changes; card impressions; CTA clicks (call/message/ask); pagination events; UTM propagation; A/B flags.
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
