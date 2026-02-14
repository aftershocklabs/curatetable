# CurateTable - Product Requirements Document

> **Version:** 1.0
> **Last Updated:** February 14, 2026
> **Status:** Draft — Ready for Review
> **Authors:** Peepu (Domain Expert), Funky (Product/Engineering)

---

## 1. Executive Summary

CurateTable is an AI-powered dinnerware configurator that helps restaurant owners make informed purchasing decisions. The platform uses conversational AI to understand a restaurant's concept, location, menu, and budget, then generates personalized product recommendations delivered as branded PDF catalogs.

**Primary revenue model:** B2B SaaS — manufacturers pay, restaurants use for free.
**Design partner:** Arc Cardinal (anchor customer, free forever).
**Target MVP:** March 2026.

---

## 2. Goals & Success Criteria

### Business Goals

| Goal | Metric | Target (6 months post-launch) |
|------|--------|-------------------------------|
| Adoption | Catalogs generated | 500+ |
| Revenue influence | GMV influenced | $100k+ |
| Efficiency | Sales rep time saved per quote | 50%+ |
| Satisfaction | Customer satisfaction rating | 4.5+ stars |
| Growth | Manufacturers onboarded | 5+ |

### Product Goals

1. Reduce restaurant dinnerware purchasing from days to minutes
2. Enable manufacturers to reach small/independent restaurants directly
3. Automate the sales qualification and catalog generation workflow
4. Build a data moat around restaurant-dinnerware matching intelligence

---

## 3. User Personas

### Persona 1: Maria — Independent Restaurant Owner

- **Background:** Owns a 40-seat Mexican restaurant in Brooklyn
- **Pain:** Doesn't know which dinnerware fits her concept. Overwhelmed by catalogs. Bought the wrong plates twice.
- **Need:** "Just tell me what to buy for my restaurant and budget."
- **Tech comfort:** Uses Instagram, can browse a website, won't use enterprise software.

### Persona 2: Dave — Manufacturer Sales Rep

- **Background:** Sells dinnerware for Arc Cardinal, manages 80+ accounts
- **Pain:** Spends 2-3 hours per lead qualifying needs, building quotes manually. 60% of quotes never convert.
- **Need:** "Give me pre-qualified leads with their requirements already documented."
- **Tech comfort:** Uses SAP, email, CRM daily.

### Persona 3: Linda — Restaurant Chain Procurement Manager

- **Background:** Manages purchasing for 12 fast-casual locations
- **Pain:** Needs consistent tableware across locations. Current process involves spreadsheets and phone calls per location.
- **Need:** "Standardize our dinnerware and automate reorders."
- **Tech comfort:** Comfortable with SaaS tools, uses procurement platforms.

---

## 4. Feature Requirements — Phase 1 (MVP)

**Target:** 6 weeks | **Goal:** Working product with Arc Cardinal catalog

### 4.1 Conversational AI Interface

**Priority:** P0 (Must Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F1.1 | Chat interface | Single-page conversational UI where users describe their restaurant | User can type natural language and receive structured responses |
| F1.2 | Multi-turn conversation | AI asks clarifying questions to gather all required inputs | System collects: cuisine type, location, seat count, budget, style preferences |
| F1.3 | Structured data extraction | AI converts free-text into structured restaurant profile | Extracted data shown to user for confirmation before recommendations |
| F1.4 | Conversation memory | Context maintained throughout the session | User can reference earlier statements ("change the budget I mentioned") |
| F1.5 | Guided flow fallback | If user is stuck, offer guided form-like prompts | System detects low-confidence input and offers structured choices |

**AI Behavior Specification:**

```
Input: "Mexican cantina in Brooklyn, 50 seats, $2k budget"

AI extracts:
  - cuisine_type: "Mexican"
  - restaurant_style: "Cantina" (maps to: rustic, colorful, durable)
  - location: "Brooklyn, NY"
  - seating_capacity: 50
  - budget: $2,000
  - durability_priority: "high" (inferred from casual dining + seat count)

AI asks follow-up:
  - "Do you have a preference for plate shape — round, square, or organic?"
  - "Will you need serving platters for family-style dishes?"
```

### 4.2 Location Intelligence

**Priority:** P0 (Must Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F2.1 | Address lookup | Google Places Autocomplete for restaurant address | User can type partial address and select from suggestions |
| F2.2 | Demographic analysis | Fetch neighborhood demographics from location | System determines: income level, dining density, neighborhood type |
| F2.3 | Competitor context | Identify nearby restaurant density and types | Used internally for recommendation weighting, not shown to user |
| F2.4 | Location-based pricing | Adjust recommendations based on area price sensitivity | Higher-end area = premium recommendations; budget area = value picks |

### 4.3 Menu & Cuisine Analysis

**Priority:** P0 (Must Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F3.1 | Cuisine type selection | Select or describe cuisine type | Supports 20+ cuisine categories with AI flexibility for custom types |
| F3.2 | Menu upload (optional) | Upload menu as image or PDF for analysis | AI extracts dish types and serving requirements |
| F3.3 | Serving style detection | Determine plating needs from cuisine/menu | Maps cuisine to: plate sizes, bowl types, serving vessels needed |
| F3.4 | Course mapping | Identify courses served (apps, mains, desserts) | Generates dinnerware requirements per course |

### 4.4 Budget Optimization Engine

**Priority:** P0 (Must Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F4.1 | Budget input | Accept total budget in USD | Supports range ("$1,500-$2,000") or fixed amount |
| F4.2 | Quantity calculation | Auto-calculate units needed from seat count | Formula: seats x multiplier (e.g., 2.5x for casual, 3x for fine dining) |
| F4.3 | Cost optimization | Maximize value within budget constraints | Prioritize: durability for high-turnover, aesthetics for fine dining |
| F4.4 | Budget breakdown | Show cost per category (plates, bowls, cups, etc.) | Visual breakdown with percentage allocation |
| F4.5 | Alternative tiers | Offer good/better/best options | User can see what upgrading or downgrading looks like |

### 4.5 Product Database & Catalog

**Priority:** P0 (Must Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F5.1 | Product schema | Structured product data with full metadata | Fields: name, SKU, category, dimensions, weight, material, color, price, image_url, durability_rating, style_tags |
| F5.2 | Arc Cardinal seed data | Import initial product catalog | Minimum 50 products across categories for MVP |
| F5.3 | Product images | High-quality product photography | At least one image per product, consistent aspect ratio |
| F5.4 | Category taxonomy | Organized product categories | Categories: dinner plates, salad plates, bowls, cups, saucers, serving platters, glassware |
| F5.5 | Product filtering | Backend filtering by attributes | Filter by: price range, material, style, color family, durability |
| F5.6 | Manufacturer scoping | Products scoped to manufacturer | Each manufacturer sees only their products; restaurants see curated cross-manufacturer results (Phase 2) |

### 4.6 Recommendation Engine

**Priority:** P0 (Must Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F6.1 | AI-powered matching | Match restaurant profile to products | Recommendations consider: cuisine, style, budget, durability, location |
| F6.2 | Scoring algorithm | Weighted scoring for product ranking | Weights configurable per manufacturer; default: style 30%, budget 25%, durability 25%, aesthetics 20% |
| F6.3 | Collection building | Group recommended products into a cohesive set | Ensure color/style consistency across recommended items |
| F6.4 | Quantity recommendations | Suggest quantities per product | Based on seat count, turnover rate, breakage estimates |
| F6.5 | Justification text | AI explains why each product was recommended | "Recommended because: durable for high-turnover casual dining, matches rustic Mexican aesthetic" |

### 4.7 PDF Catalog Generation

**Priority:** P0 (Must Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F7.1 | Branded PDF | Generate PDF with manufacturer branding | Includes: logo, brand colors, contact info |
| F7.2 | Product pages | Each recommended product on a page/section | Shows: image, name, SKU, price, specs, recommendation reason |
| F7.3 | Summary page | Overview of full recommendation | Total cost, quantity breakdown, estimated reorder date |
| F7.4 | Restaurant context | Include restaurant details in PDF | Restaurant name, location, cuisine type, budget — personalized header |
| F7.5 | Download & preview | Preview PDF in-app before downloading | Render preview in browser; download as PDF |

### 4.8 Email Delivery

**Priority:** P1 (Should Have)

| ID | Requirement | Details | Acceptance Criteria |
|----|-------------|---------|---------------------|
| F8.1 | Email to self | User emails catalog to themselves | Simple email input, sends PDF attachment |
| F8.2 | Email to sales rep | Send catalog to manufacturer's sales team | Pre-configured sales rep email per manufacturer |
| F8.3 | Email template | Branded email with summary | HTML email with catalog summary + PDF attachment |
| F8.4 | Delivery confirmation | Confirm email was sent successfully | Toast notification with success/failure state |

---

## 5. Feature Requirements — Phase 2 (Scale)

**Target:** Month 3-4 | **Goal:** SAP integration, multi-manufacturer, analytics

### 5.1 SAP Integration

| ID | Requirement | Details | Priority |
|----|-------------|---------|----------|
| F9.1 | SAP quotation creation | Push recommendation as SAP Sales Quotation (VA21) | P0 |
| F9.2 | Material master lookup | Validate product SKUs against SAP material master | P0 |
| F9.3 | Pricing from SAP | Pull real-time pricing from SAP pricing conditions | P1 |
| F9.4 | Customer master | Create/link restaurant as SAP customer | P1 |
| F9.5 | Order status tracking | View quotation → order conversion status | P2 |

**Technical approach:** SAP OData services (preferred) or RFC/BAPI via middleware.

### 5.2 Reorder Automation

| ID | Requirement | Details | Priority |
|----|-------------|---------|----------|
| F10.1 | Reorder schedule | Calculate recommended reorder dates | P0 |
| F10.2 | Email reminders | Automated reorder reminder emails | P1 |
| F10.3 | One-click reorder | Re-generate previous order with updated quantities | P1 |
| F10.4 | Breakage tracking | User inputs breakage to refine reorder predictions | P2 |

### 5.3 Multi-Manufacturer Support

| ID | Requirement | Details | Priority |
|----|-------------|---------|----------|
| F11.1 | Manufacturer onboarding | Self-serve manufacturer registration | P0 |
| F11.2 | Catalog import | Bulk product import (CSV/XML) | P0 |
| F11.3 | Brand customization | Per-manufacturer branding (logo, colors, PDF template) | P0 |
| F11.4 | Manufacturer dashboard | View catalog performance, leads, conversions | P1 |

### 5.4 Analytics Dashboard

| ID | Requirement | Details | Priority |
|----|-------------|---------|----------|
| F12.1 | Catalog analytics | Track: catalogs generated, products viewed, emails sent | P0 |
| F12.2 | Conversion tracking | Track: catalog → quote → order pipeline | P1 |
| F12.3 | Product insights | Most recommended products, trending styles | P1 |
| F12.4 | Geographic heatmap | Where catalogs are being generated | P2 |

---

## 6. Feature Requirements — Phase 3 (Marketplace)

**Target:** Month 5-8 | **Goal:** Direct ordering, inventory, AR

### 6.1 E-Commerce

| ID | Requirement | Details | Priority |
|----|-------------|---------|----------|
| F13.1 | Shopping cart | Add recommended products to cart | P0 |
| F13.2 | Checkout flow | Stripe payment processing | P0 |
| F13.3 | Order management | View order history, track shipments | P1 |
| F13.4 | Wholesale pricing | Volume-based discount tiers | P1 |

### 6.2 Inventory & Reorder

| ID | Requirement | Details | Priority |
|----|-------------|---------|----------|
| F14.1 | Inventory tracking | Restaurant tracks current dinnerware stock | P0 |
| F14.2 | Auto-reorder triggers | System suggests reorders at threshold | P1 |
| F14.3 | Multi-location management | Manage inventory across restaurant locations | P2 |

### 6.3 AR Preview

| ID | Requirement | Details | Priority |
|----|-------------|---------|----------|
| F15.1 | Mobile AR viewer | Point camera at table, see product overlay | P0 |
| F15.2 | Product 3D models | 3D models for top products | P1 |
| F15.3 | Share AR preview | Screenshot/video sharing from AR view | P2 |

---

## 7. Non-Functional Requirements

### 7.1 Performance

| Requirement | Target |
|-------------|--------|
| Chat response time | < 3 seconds (AI response) |
| Page load time | < 2 seconds (initial load) |
| PDF generation | < 10 seconds |
| Concurrent users | 100+ simultaneous sessions |

### 7.2 Security

| Requirement | Details |
|-------------|---------|
| Authentication | Email/password + OAuth (Google) for manufacturers; anonymous or optional for restaurants |
| API security | Rate limiting, API key management for AI/Maps APIs |
| Data privacy | No PII stored beyond email; GDPR-compliant data handling |
| Input sanitization | All user inputs sanitized; AI prompt injection prevention |

### 7.3 Accessibility

| Requirement | Details |
|-------------|---------|
| WCAG compliance | WCAG 2.1 AA minimum |
| Keyboard navigation | Full keyboard accessibility for chat and product browsing |
| Screen reader support | Semantic HTML, ARIA labels on interactive elements |
| Color contrast | 4.5:1 minimum contrast ratio |

### 7.4 Reliability

| Requirement | Target |
|-------------|--------|
| Uptime | 99.5% |
| Error rate | < 1% of requests |
| Data backup | Daily automated backups |
| Disaster recovery | < 4 hour RTO |

---

## 8. Technical Architecture

### 8.1 System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                      CLIENT (Browser)                    │
│  Next.js 14 App Router + Tailwind CSS + shadcn/ui       │
└───────────────────────┬─────────────────────────────────┘
                        │ HTTPS
                        ▼
┌─────────────────────────────────────────────────────────┐
│                    NEXT.JS API ROUTES                     │
│                  (Vercel Serverless)                      │
│                                                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │  Chat    │  │ Products │  │  PDF     │              │
│  │  API     │  │  API     │  │  API     │              │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘              │
│       │              │              │                    │
└───────┼──────────────┼──────────────┼────────────────────┘
        │              │              │
   ┌────▼─────┐  ┌────▼─────┐  ┌────▼─────┐
   │ Claude / │  │PostgreSQL│  │  react-  │
   │ OpenAI   │  │ (Neon/   │  │   pdf    │
   │  API     │  │ Supabase)│  │          │
   └──────────┘  └──────────┘  └──────────┘
        │
   ┌────▼──────────┐
   │ Google Maps   │
   │ API           │
   └───────────────┘
```

### 8.2 Database Schema (Core)

```sql
-- Manufacturers
manufacturers (
  id, name, slug, logo_url, brand_colors,
  contact_email, sap_config, tier, created_at
)

-- Products
products (
  id, manufacturer_id, name, sku, category,
  subcategory, description, material, color,
  dimensions, weight, price, image_urls,
  durability_rating, style_tags, active, created_at
)

-- Restaurant Profiles (session-based)
restaurant_profiles (
  id, session_id, name, cuisine_type, location_address,
  location_lat, location_lng, seating_capacity, budget,
  style_preferences, demographics_data, created_at
)

-- Generated Catalogs
catalogs (
  id, restaurant_profile_id, manufacturer_id,
  recommendations (JSONB), pdf_url, total_cost,
  status, emailed_to, created_at
)

-- Conversations
conversations (
  id, restaurant_profile_id, messages (JSONB),
  extracted_data (JSONB), status, created_at
)
```

### 8.3 API Endpoints (MVP)

```
POST   /api/chat              — Send message, get AI response
GET    /api/chat/:sessionId   — Get conversation history

GET    /api/products          — List products (filtered)
GET    /api/products/:id      — Get product details

POST   /api/recommend         — Generate recommendations
GET    /api/recommend/:id     — Get recommendation details

POST   /api/catalog/generate  — Generate PDF catalog
GET    /api/catalog/:id       — Get catalog details
GET    /api/catalog/:id/pdf   — Download PDF

POST   /api/email/send        — Send catalog via email

GET    /api/location/analyze  — Analyze location demographics
GET    /api/location/autocomplete — Address autocomplete
```

---

## 9. Data Requirements

### 9.1 Product Data (Arc Cardinal)

**Minimum viable catalog:**

| Category | Min Products | Required Fields |
|----------|-------------|-----------------|
| Dinner Plates | 10 | name, SKU, price, image, dimensions, material, color, style_tags |
| Salad/Appetizer Plates | 8 | same as above |
| Bowls | 8 | same + capacity (oz) |
| Cups & Mugs | 6 | same + capacity (oz) |
| Serving Platters | 5 | same + serving_style |
| Glassware | 8 | same + capacity (oz), glass_type |
| Specialty | 5 | same + use_case description |
| **Total** | **50** | |

### 9.2 Product Data Ingestion

**MVP approach:** Manual data entry + CSV import.
**Phase 2:** API-based catalog sync, XML feed processing.

---

## 10. Decisions & Open Items

### Resolved Decisions

| Decision | Resolution | Rationale |
|----------|-----------|-----------|
| AI provider | Claude API (primary), OpenAI (fallback) | Better structured output, vision capabilities for menu upload |
| Database | PostgreSQL via Neon | Serverless-friendly, generous free tier, good DX |
| PDF library | react-pdf (@react-pdf/renderer) | React-native approach, server-side rendering, good styling control |
| Hosting | Vercel | Native Next.js support, edge functions, easy deploys |
| Email | Resend | Modern API, good DX, generous free tier |

### Open Items

| # | Item | Options | Decision Needed By |
|---|------|---------|-------------------|
| 1 | Product data source | Manual entry vs PDF catalog scraping vs XML feed | Week 1 |
| 2 | Pricing strategy | Real prices vs placeholder pricing for MVP | Week 1 |
| 3 | Authentication | Anonymous-first vs account-required | Week 1 |
| 4 | Initial branding | Arc Cardinal branded vs white-label CurateTable | Week 1 |
| 5 | Menu upload format | Image-only vs PDF vs both | Week 2 |

---

## 11. Risks & Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| AI recommendation quality is poor | High | Medium | Extensive prompt engineering; human review of first 50 catalogs; feedback loop |
| Arc Cardinal product data is incomplete | High | Medium | Start with manual data entry; don't depend on automated feed for MVP |
| Google Maps API costs spike | Medium | Low | Cache location data aggressively; limit API calls per session |
| Low adoption by restaurant owners | High | Medium | Validate with 10 restaurant owners before building; keep UX dead simple |
| SAP integration complexity (Phase 2) | Medium | High | Isolate SAP as a separate module; use middleware pattern; Peepu's SAP expertise |

---

## 12. Out of Scope (MVP)

The following are explicitly **not** included in the MVP:

- User accounts / authentication (session-based only)
- Payment processing
- Multi-manufacturer support (Arc Cardinal only)
- SAP integration
- Inventory tracking
- AR preview
- Mobile native app
- Multi-language support
- Real-time collaboration

---

## Appendix A: Glossary

| Term | Definition |
|------|-----------|
| **Catalog** | A personalized PDF document containing dinnerware recommendations for a specific restaurant |
| **GMV** | Gross Merchandise Value — total value of products recommended/ordered through the platform |
| **SKU** | Stock Keeping Unit — unique product identifier |
| **SAP ECC/S4HANA** | Enterprise Resource Planning systems used by manufacturers for orders and inventory |
| **VA21** | SAP transaction code for creating a Sales Quotation |
| **OData** | Open Data Protocol — REST-like API standard used by SAP |
