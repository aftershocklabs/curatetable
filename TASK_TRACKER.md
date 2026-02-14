# CurateTable - Task Tracker

> **Last Updated:** February 14, 2026
> **Status Key:** `[ ]` Not Started | `[~]` In Progress | `[x]` Complete | `[!]` Blocked

---

## Phase 1: MVP (Weeks 1-6)

### Sprint 1 — Foundation (Week 1-2)

#### 1.1 Project Setup

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 1.1.1 | Initialize Next.js 14 project with App Router | Funky | [ ] | `pnpm create next-app` |
| 1.1.2 | Configure Tailwind CSS | Funky | [ ] | Included in Next.js setup |
| 1.1.3 | Install and configure shadcn/ui | Funky | [ ] | Add base components: Button, Input, Card, Dialog |
| 1.1.4 | Set up ESLint + Prettier configuration | Funky | [ ] | Enforce consistent code style |
| 1.1.5 | Set up testing framework (Vitest + React Testing Library) | Funky | [ ] | TDD-first approach |
| 1.1.6 | Set up Playwright for E2E tests | Funky | [ ] | Critical user paths |
| 1.1.7 | Configure CI/CD pipeline (GitHub Actions) | Funky | [ ] | Lint, test, build on every PR |
| 1.1.8 | Set up environment variable management | Funky | [ ] | `.env.example` with all required vars |
| 1.1.9 | Configure Vercel deployment | Funky | [ ] | Preview deploys on PRs |
| 1.1.10 | Set up Husky pre-commit hooks | Funky | [ ] | Run lint + tests before commit |

#### 1.2 Database Setup

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 1.2.1 | Provision PostgreSQL database (Neon) | Funky | [ ] | Free tier for dev |
| 1.2.2 | Set up Prisma ORM | Funky | [ ] | Schema-first approach |
| 1.2.3 | Design and create `manufacturers` table | Funky | [ ] | See PRD schema |
| 1.2.4 | Design and create `products` table | Funky | [ ] | Full product metadata |
| 1.2.5 | Design and create `restaurant_profiles` table | Funky | [ ] | Session-based |
| 1.2.6 | Design and create `catalogs` table | Funky | [ ] | JSONB for recommendations |
| 1.2.7 | Design and create `conversations` table | Funky | [ ] | JSONB for messages |
| 1.2.8 | Write database seed script | Funky | [ ] | Seed with Arc Cardinal data |
| 1.2.9 | Write migration scripts | Funky | [ ] | Prisma migrations |
| 1.2.10 | Write unit tests for database models | Funky | [ ] | TDD: write tests first |

#### 1.3 Product Data

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 1.3.1 | Define product data schema (TypeScript types) | Funky | [ ] | Match PRD spec |
| 1.3.2 | Collect Arc Cardinal product data (50 items min) | Peepu | [ ] | Need: name, SKU, price, images |
| 1.3.3 | Process and normalize product images | Funky | [ ] | Consistent sizing, optimization |
| 1.3.4 | Create product CSV import utility | Funky | [ ] | For bulk data loading |
| 1.3.5 | Seed database with Arc Cardinal products | Funky | [ ] | Depends on 1.3.2, 1.3.4 |
| 1.3.6 | Write validation tests for product data integrity | Funky | [ ] | TDD: validate required fields |

#### 1.4 Basic Chat UI

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 1.4.1 | Write tests for ChatMessage component | Funky | [ ] | TDD: test first |
| 1.4.2 | Build ChatMessage component (user + AI messages) | Funky | [ ] | Supports markdown rendering |
| 1.4.3 | Write tests for ChatInput component | Funky | [ ] | TDD: test first |
| 1.4.4 | Build ChatInput component (text input + send) | Funky | [ ] | Auto-resize textarea, send on Enter |
| 1.4.5 | Write tests for ChatContainer component | Funky | [ ] | TDD: test first |
| 1.4.6 | Build ChatContainer component (message list) | Funky | [ ] | Auto-scroll, loading states |
| 1.4.7 | Build chat page layout | Funky | [ ] | Full-height, responsive |
| 1.4.8 | Implement welcome/onboarding message | Funky | [ ] | Explain what CurateTable does, prompt first input |
| 1.4.9 | Add typing indicator animation | Funky | [ ] | Show while AI is responding |
| 1.4.10 | Write E2E test for basic chat flow | Funky | [ ] | Send message, receive response |

---

### Sprint 2 — Core Features (Week 3-4)

#### 2.1 AI Conversation Engine

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 2.1.1 | Set up Claude API client | Funky | [ ] | With error handling, retries |
| 2.1.2 | Design system prompt for restaurant qualification | Funky | [ ] | Extract: cuisine, location, seats, budget, style |
| 2.1.3 | Write tests for conversation state machine | Funky | [ ] | TDD: test state transitions |
| 2.1.4 | Implement conversation state machine | Funky | [ ] | States: greeting → gathering → confirming → recommending |
| 2.1.5 | Write tests for structured data extraction | Funky | [ ] | TDD: test extraction accuracy |
| 2.1.6 | Implement structured data extraction from AI responses | Funky | [ ] | Parse AI output → RestaurantProfile |
| 2.1.7 | Build `/api/chat` endpoint | Funky | [ ] | POST: message in, AI response out |
| 2.1.8 | Implement conversation memory (session-based) | Funky | [ ] | Store messages in DB per session |
| 2.1.9 | Add guided prompts/quick replies | Funky | [ ] | Clickable suggestions for common inputs |
| 2.1.10 | Write integration tests for full chat flow | Funky | [ ] | End-to-end AI conversation test |

#### 2.2 Location Intelligence

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 2.2.1 | Set up Google Maps API client | Funky | [ ] | Places API + Geocoding |
| 2.2.2 | Write tests for location service | Funky | [ ] | TDD: mock Google API responses |
| 2.2.3 | Implement address autocomplete (`/api/location/autocomplete`) | Funky | [ ] | Google Places Autocomplete |
| 2.2.4 | Implement location analysis (`/api/location/analyze`) | Funky | [ ] | Demographics, nearby restaurants |
| 2.2.5 | Build location input component with autocomplete | Funky | [ ] | Integrated into chat flow |
| 2.2.6 | Cache location data to reduce API calls | Funky | [ ] | Redis or in-memory cache |
| 2.2.7 | Write tests for demographic scoring | Funky | [ ] | TDD: test scoring logic |
| 2.2.8 | Implement demographic scoring algorithm | Funky | [ ] | Income → price tier mapping |

#### 2.3 Recommendation Engine

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 2.3.1 | Write tests for scoring algorithm | Funky | [ ] | TDD: test with known inputs/outputs |
| 2.3.2 | Implement product scoring algorithm | Funky | [ ] | Style 30%, budget 25%, durability 25%, aesthetics 20% |
| 2.3.3 | Write tests for collection builder | Funky | [ ] | TDD: test collection coherence |
| 2.3.4 | Implement collection builder (ensures style coherence) | Funky | [ ] | Match color families, materials |
| 2.3.5 | Write tests for quantity calculator | Funky | [ ] | TDD: test multiplier logic |
| 2.3.6 | Implement quantity calculator | Funky | [ ] | Seats × multiplier × breakage |
| 2.3.7 | Write tests for budget allocator | Funky | [ ] | TDD: test allocation logic |
| 2.3.8 | Implement budget allocation across categories | Funky | [ ] | % split by category priority |
| 2.3.9 | Build `/api/recommend` endpoint | Funky | [ ] | Input: profile, Output: recommendations |
| 2.3.10 | Write tests for good/better/best tiers | Funky | [ ] | TDD: test tier generation |
| 2.3.11 | Implement alternative tier generation | Funky | [ ] | Show upgrade/downgrade options |
| 2.3.12 | Generate AI justification text per product | Funky | [ ] | "Recommended because..." |

#### 2.4 Product Selection UI

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 2.4.1 | Write tests for ProductCard component | Funky | [ ] | TDD: test rendering, interactions |
| 2.4.2 | Build ProductCard component | Funky | [ ] | Image, name, price, specs |
| 2.4.3 | Write tests for ProductGrid component | Funky | [ ] | TDD: test layout, filtering |
| 2.4.4 | Build ProductGrid component | Funky | [ ] | Responsive grid layout |
| 2.4.5 | Write tests for RecommendationView component | Funky | [ ] | TDD: test recommendation display |
| 2.4.6 | Build RecommendationView component | Funky | [ ] | Shows scored recommendations with justifications |
| 2.4.7 | Build budget breakdown visualization | Funky | [ ] | Bar chart or donut chart |
| 2.4.8 | Build quantity editor (adjust recommended quantities) | Funky | [ ] | +/- buttons, live total update |
| 2.4.9 | Build tier selector (good/better/best toggle) | Funky | [ ] | Tab or toggle UI |
| 2.4.10 | Write E2E test for recommendation → product view flow | Funky | [ ] | Full user journey |

---

### Sprint 3 — Output & Polish (Week 5-6)

#### 3.1 PDF Generation

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 3.1.1 | Set up react-pdf (@react-pdf/renderer) | Funky | [ ] | Server-side rendering |
| 3.1.2 | Write tests for PDF data transformer | Funky | [ ] | TDD: test data → PDF format |
| 3.1.3 | Design PDF template (cover page) | Funky | [ ] | Manufacturer branding + restaurant context |
| 3.1.4 | Design PDF template (product pages) | Funky | [ ] | Product image, specs, pricing |
| 3.1.5 | Design PDF template (summary page) | Funky | [ ] | Total cost, quantities, reorder date |
| 3.1.6 | Build `/api/catalog/generate` endpoint | Funky | [ ] | Input: recommendations, Output: PDF URL |
| 3.1.7 | Implement PDF preview in-app | Funky | [ ] | Render PDF in iframe or viewer |
| 3.1.8 | Implement PDF download | Funky | [ ] | Download button with filename |
| 3.1.9 | Write integration tests for PDF generation | Funky | [ ] | Verify PDF content and structure |

#### 3.2 Email Delivery

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 3.2.1 | Set up Resend email client | Funky | [ ] | API key config |
| 3.2.2 | Write tests for email service | Funky | [ ] | TDD: mock email sends |
| 3.2.3 | Design email HTML template | Funky | [ ] | Branded, responsive |
| 3.2.4 | Build `/api/email/send` endpoint | Funky | [ ] | Input: catalog ID + recipient |
| 3.2.5 | Build email input UI in app | Funky | [ ] | Email field + send button |
| 3.2.6 | Implement delivery confirmation | Funky | [ ] | Toast notification |
| 3.2.7 | Write E2E test for email flow | Funky | [ ] | Generate catalog → send email |

#### 3.3 Landing Page

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 3.3.1 | Design landing page layout | Funky | [ ] | Hero, how-it-works, CTA |
| 3.3.2 | Build hero section | Funky | [ ] | Headline + start CTA |
| 3.3.3 | Build how-it-works section | Funky | [ ] | 3-step visual flow |
| 3.3.4 | Build feature highlights section | Funky | [ ] | Key value propositions |
| 3.3.5 | Build CTA section | Funky | [ ] | "Configure Your Tableware" button |
| 3.3.6 | Implement responsive design | Funky | [ ] | Mobile, tablet, desktop |
| 3.3.7 | Write E2E test for landing → chat flow | Funky | [ ] | CTA click navigates to chat |

#### 3.4 Polish & QA

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 3.4.1 | Loading states for all async operations | Funky | [ ] | Skeletons, spinners |
| 3.4.2 | Error handling for API failures | Funky | [ ] | User-friendly error messages |
| 3.4.3 | Empty states for no results | Funky | [ ] | Helpful empty state messages |
| 3.4.4 | Mobile responsiveness audit | Funky | [ ] | Test on real devices |
| 3.4.5 | Accessibility audit (WCAG 2.1 AA) | Funky | [ ] | aXe, keyboard nav, screen reader |
| 3.4.6 | Performance audit (Lighthouse) | Funky | [ ] | Target: 90+ on all categories |
| 3.4.7 | Cross-browser testing | Funky | [ ] | Chrome, Firefox, Safari, Edge |
| 3.4.8 | Security review (input sanitization, API keys) | Funky | [ ] | OWASP checklist |
| 3.4.9 | User testing with 5 restaurant owners | Peepu | [ ] | Gather feedback, iterate |
| 3.4.10 | Bug fixes from user testing | Funky | [ ] | Address critical findings |
| 3.4.11 | Deploy to production | Funky | [ ] | Vercel production deployment |
| 3.4.12 | Set up monitoring (error tracking) | Funky | [ ] | Sentry or similar |

---

## Phase 2: Scale (Months 3-4)

### Sprint 4 — SAP & Multi-Manufacturer

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 4.1 | Design SAP integration architecture | Peepu | [ ] | OData vs RFC/BAPI |
| 4.2 | Set up SAP development sandbox | Peepu | [ ] | Test environment |
| 4.3 | Implement SAP OData client | Funky | [ ] | With Peepu's guidance |
| 4.4 | Build material master lookup | Funky | [ ] | Validate SKUs |
| 4.5 | Build quotation creation (VA21) | Funky | [ ] | Push recommendations to SAP |
| 4.6 | Write tests for SAP integration | Funky | [ ] | Mock SAP responses |
| 4.7 | Design manufacturer onboarding flow | Funky | [ ] | Registration, branding, catalog upload |
| 4.8 | Build manufacturer registration page | Funky | [ ] | Email, company, tier selection |
| 4.9 | Build catalog bulk import (CSV/XML) | Funky | [ ] | Validate, transform, insert |
| 4.10 | Build manufacturer branding settings | Funky | [ ] | Logo, colors, PDF template customization |
| 4.11 | Build manufacturer dashboard | Funky | [ ] | Basic analytics: catalogs generated, products viewed |
| 4.12 | Implement authentication (NextAuth.js) | Funky | [ ] | For manufacturers only |

### Sprint 5 — Reorder & Analytics

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 5.1 | Design reorder prediction algorithm | Funky | [ ] | Based on seat count, breakage rate, usage |
| 5.2 | Build reorder schedule calculator | Funky | [ ] | "Reorder in X weeks" |
| 5.3 | Implement email reminder system (cron jobs) | Funky | [ ] | Scheduled via Vercel Cron |
| 5.4 | Build one-click reorder flow | Funky | [ ] | Re-generate previous catalog with updates |
| 5.5 | Build analytics data pipeline | Funky | [ ] | Track events: catalog_generated, email_sent, etc. |
| 5.6 | Build analytics dashboard UI | Funky | [ ] | Charts: catalogs over time, top products, geography |
| 5.7 | Implement conversion tracking | Funky | [ ] | Catalog → quote → order pipeline |
| 5.8 | Write tests for analytics calculations | Funky | [ ] | TDD: accurate metrics |

---

## Phase 3: Marketplace (Months 5-8)

### Sprint 6 — E-Commerce Foundation

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 6.1 | Set up Stripe integration | Funky | [ ] | Payment processing |
| 6.2 | Build shopping cart | Funky | [ ] | Add from recommendations |
| 6.3 | Build checkout flow | Funky | [ ] | Address, payment, confirmation |
| 6.4 | Build order management | Funky | [ ] | Order history, status tracking |
| 6.5 | Implement wholesale pricing tiers | Funky | [ ] | Volume-based discounts |
| 6.6 | Build restaurant accounts | Funky | [ ] | Save orders, preferences |
| 6.7 | Write E2E tests for purchase flow | Funky | [ ] | Full checkout journey |

### Sprint 7 — Inventory & AR

| # | Task | Owner | Status | Notes |
|---|------|-------|--------|-------|
| 7.1 | Design inventory tracking schema | Funky | [ ] | Per-restaurant, per-product |
| 7.2 | Build inventory dashboard | Funky | [ ] | Current stock, reorder thresholds |
| 7.3 | Implement auto-reorder triggers | Funky | [ ] | Threshold-based notifications |
| 7.4 | Research AR frameworks (AR.js / model-viewer) | Funky | [ ] | Technical feasibility |
| 7.5 | Build AR preview prototype | Funky | [ ] | Camera → table → overlay product |
| 7.6 | Source/create 3D product models | Peepu | [ ] | Top 10 products |
| 7.7 | Multi-location management | Funky | [ ] | Restaurant chain support |

---

## Ongoing / Cross-Cutting

| # | Task | Owner | Status | Recurrence |
|---|------|-------|--------|------------|
| O.1 | Update documentation | Funky | [ ] | Weekly |
| O.2 | Dependency updates | Funky | [ ] | Bi-weekly |
| O.3 | Performance monitoring | Funky | [ ] | Weekly |
| O.4 | Security audit | Funky | [ ] | Monthly |
| O.5 | User feedback collection | Peepu | [ ] | Ongoing |
| O.6 | Competitive analysis | Peepu | [ ] | Monthly |

---

## Summary

| Phase | Tasks | Completed | Progress |
|-------|-------|-----------|----------|
| Phase 1 (MVP) | 76 | 0 | 0% |
| Phase 2 (Scale) | 20 | 0 | 0% |
| Phase 3 (Marketplace) | 14 | 0 | 0% |
| Ongoing | 6 | 0 | 0% |
| **Total** | **116** | **0** | **0%** |
