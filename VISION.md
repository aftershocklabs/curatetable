# CurateTable - Vision Document

> **AI-Powered Dinnerware Configurator for Restaurants**

---

## 🎯 Vision

Empower restaurant owners to make smarter dinnerware purchasing decisions through AI-driven recommendations that consider their unique context — menu, location, budget, and business model.

## 🚀 Mission

Eliminate the guesswork from restaurant supply purchasing by creating an intelligent platform that acts as a virtual sales consultant, understanding each customer's needs and delivering personalized product catalogs.

---

## 📋 Problem Statement

### The Current State
- **Restaurant owners** (especially mom & pop shops) lack expertise in dinnerware selection
- **Sales reps** spend hours manually analyzing customer needs and creating quotes
- **Distributors** add markup without adding value for small orders
- **Manufacturers** struggle to reach small restaurants directly
- **Ordering process** is fragmented: catalogs, phone calls, emails, manual quotes

### Pain Points
1. Restaurant owners don't know which products fit their concept
2. No easy way to match menu style → appropriate dinnerware
3. Budget optimization is guesswork (cheap vs durable tradeoffs)
4. Reorder patterns are manual and inefficient
5. Branding (custom logos on materials) is an afterthought

---

## 💡 Solution Overview

**CurateTable** is a conversational AI platform that:

```
┌─────────────────────────────────────────────────────────────┐
│                     RESTAURANT OWNER                         │
│  "I run a Mexican cantina in Brooklyn, 50 seats, $2k budget" │
└─────────────────────────────────────┬───────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────┐
│                    🤖 CURATETABLE AI                        │
│                                                             │
│  📍 Analyzes Google Maps location                          │
│     → Demographics, foot traffic, neighborhood type        │
│                                                             │
│  🍽️ Understands menu & concept                             │
│     → Mexican = rustic, colorful, durable plates           │
│                                                             │
│  💰 Optimizes for budget                                   │
│     → $2k = mid-tier, prioritize durability                │
│                                                             │
│  📊 Predicts business patterns                             │
│     → 50 seats, casual = higher turnover, more breakage    │
│                                                             │
│  🔄 Recommends purchasing strategy                         │
│     → "Buy mid-range, resupply every 3 months"             │
└─────────────────────────────────────┬───────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   📄 GENERATED OUTPUT                        │
│                                                             │
│  ✅ Personalized product recommendations                   │
│  ✅ Custom-branded PDF catalog (restaurant's logo)         │
│  ✅ Pricing breakdown & total cost                         │
│  ✅ Reorder schedule recommendation                        │
│  ✅ One-click: Email to sales rep OR Create SAP quotation  │
└─────────────────────────────────────────────────────────────┘
```

---

## 👥 Target Users

### Primary Users

| User | Need | How CurateTable Helps |
|------|------|----------------------|
| **Mom & Pop Restaurant Owners** | Easy ordering without middlemen | Conversational AI, skip distributors |
| **Small Restaurant Chains** | Standardized ordering across locations | Consistent recommendations, bulk pricing |
| **Sales Representatives** | Faster quote generation | AI pre-qualifies leads, generates catalogs |

### Secondary Users
- **Procurement Teams** (larger chains)
- **Restaurant Consultants** (setting up new venues)
- **Interior Designers** (coordinating tableware with decor)

---

## ✨ Key Features

### MVP (Phase 1)
- [ ] **Conversational Interface** — Natural language input for restaurant details
- [ ] **Location Intelligence** — Google Maps API integration for demographics
- [ ] **Menu Analysis** — Upload menu or describe cuisine type
- [ ] **Budget Optimization** — Smart recommendations within constraints
- [ ] **Product Database** — Structured catalog with images, pricing, specs
- [ ] **PDF Generation** — Custom-branded catalog with selected products
- [ ] **Email Delivery** — Send generated catalog to sales rep or customer

### Phase 2
- [ ] **SAP Integration** — Push quotations directly to SAP ECC/S4HANA
- [ ] **Reorder Automation** — Scheduled resupply recommendations
- [ ] **Analytics Dashboard** — Insights for manufacturers
- [ ] **Multi-Manufacturer** — Support multiple dinnerware brands

### Phase 3
- [ ] **E-Commerce** — Direct ordering & payment
- [ ] **Inventory Tracking** — Know when to reorder
- [ ] **AR Preview** — See products on your tables (mobile)

---

## 🛠️ Tech Stack

### Frontend
- **Next.js 14** — React framework with App Router
- **Tailwind CSS** — Styling
- **shadcn/ui** — Component library
- **Vercel** — Hosting & deployment

### Backend
- **Next.js API Routes** — Serverless functions
- **PostgreSQL** — Product database (Supabase or Neon)
- **OpenAI / Claude API** — Conversational AI
- **Google Maps API** — Location intelligence

### Integrations
- **PDF Generation** — react-pdf or Puppeteer
- **Email** — Resend or SendGrid
- **SAP** — RFC/BAPI or OData (Phase 2)

---

## 📊 MVP Scope (4-6 weeks)

### Week 1-2: Foundation
- [ ] Project setup (Next.js, Tailwind, shadcn)
- [ ] Database schema design
- [ ] Product data seeding (sample catalog)
- [ ] Basic chat interface

### Week 3-4: Core Features
- [ ] AI conversation flow (menu, location, budget)
- [ ] Google Maps integration
- [ ] Recommendation engine logic
- [ ] Product selection UI

### Week 5-6: Output & Polish
- [ ] PDF generation with branding
- [ ] Email delivery
- [ ] Testing with real users
- [ ] Deploy to production

---

## 💰 Revenue Model

### For Manufacturers (Primary)
| Tier | Price | Features |
|------|-------|----------|
| **Starter** | Free | Limited products, CurateTable branding |
| **Pro** | $499/mo | Full catalog, custom branding, analytics |
| **Enterprise** | $2,000+/mo | SAP integration, API access, SLA |

### For Restaurants (Future)
- Free to use (manufacturers pay)
- Premium features: saved orders, reorder reminders

---

## 🎁 Go-to-Market Strategy

### Phase 1: Pilot
- **Arc Cardinal** = First customer (free forever)
- Build, iterate, and perfect with real feedback
- Case study for sales

### Phase 2: Expand
- Target 5-10 similar manufacturers
- "Trusted by Arc Cardinal" social proof
- Industry trade shows & LinkedIn

### Phase 3: Scale
- Self-serve onboarding
- Marketplace of manufacturers
- Restaurants choose their supplier

---

## 🏆 Success Metrics

| Metric | Target (6 months) |
|--------|-------------------|
| Catalogs generated | 500+ |
| Orders influenced | $100k+ GMV |
| Sales rep time saved | 50%+ per quote |
| Customer satisfaction | 4.5+ stars |
| Manufacturers onboarded | 5+ |

---

## 🤝 Team

| Role | Responsibility |
|------|----------------|
| **Peepu** | Founder, Domain Expert, SAP Integration |
| **Funky (AI)** | Product Development, Engineering |
| **Arc Cardinal** | Design Partner, Feedback |

---

## 📅 Timeline

```
Feb 2026      Mar 2026      Apr 2026      May 2026
    │             │             │             │
    ▼             ▼             ▼             ▼
┌────────┐   ┌────────┐   ┌────────┐   ┌────────┐
│  MVP   │───│ Pilot  │───│  SAP   │───│ Scale  │
│ Build  │   │ w/Arc  │   │ Integ  │   │ Sales  │
└────────┘   └────────┘   └────────┘   └────────┘
```

---

## 📝 Open Questions

1. **Product Data** — PDF catalog vs XML feed from Arc Cardinal?
2. **Pricing** — Use dummy prices initially or real pricing?
3. **Auth** — Do users need accounts or anonymous usage?
4. **Branding** — Arc Cardinal branded or white-label?

---

## 🔗 Links

- **Repository:** https://github.com/aftershocklabs/curatetable
- **Domain:** curatetable.com (to be registered)
- **Design Partner:** [Arc Cardinal](https://arccardinal.com/)

---

*Created: February 14, 2026*
*Author: Funky 💋*
*Status: Vision Complete — Ready to Build!*
