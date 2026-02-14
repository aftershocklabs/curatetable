# CLAUDE.md — CurateTable Development Guide

> This file provides context and instructions for AI-assisted development on the CurateTable project.

---

## Project Overview

CurateTable is an AI-powered dinnerware configurator for restaurants. It uses conversational AI to understand a restaurant's needs (cuisine, location, budget, style) and generates personalized product recommendations as branded PDF catalogs.

**Stack:** Next.js 14 (App Router), Tailwind CSS, shadcn/ui, PostgreSQL (Neon), Prisma ORM, Claude API, Google Maps API, react-pdf, Resend, Vercel.

---

## Repository Structure

```
curatetable/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── page.tsx            # Landing page
│   │   ├── chat/
│   │   │   └── page.tsx        # Chat interface
│   │   ├── catalog/
│   │   │   └── [id]/
│   │   │       └── page.tsx    # Catalog view/download
│   │   └── api/
│   │       ├── chat/
│   │       │   └── route.ts    # Chat endpoint
│   │       ├── products/
│   │       │   └── route.ts    # Products endpoint
│   │       ├── recommend/
│   │       │   └── route.ts    # Recommendation engine
│   │       ├── catalog/
│   │       │   └── route.ts    # PDF generation
│   │       ├── email/
│   │       │   └── route.ts    # Email delivery
│   │       └── location/
│   │           └── route.ts    # Location intelligence
│   ├── components/
│   │   ├── ui/                 # shadcn/ui base components
│   │   ├── chat/               # Chat-related components
│   │   ├── products/           # Product display components
│   │   ├── catalog/            # Catalog/PDF components
│   │   └── layout/             # Layout components
│   ├── lib/
│   │   ├── ai/                 # AI client, prompts, conversation logic
│   │   ├── db/                 # Prisma client, queries
│   │   ├── location/           # Google Maps integration
│   │   ├── pdf/                # PDF generation logic
│   │   ├── email/              # Email service
│   │   ├── recommend/          # Recommendation engine
│   │   └── utils/              # Shared utilities
│   ├── types/                  # TypeScript type definitions
│   └── styles/                 # Global styles
├── prisma/
│   ├── schema.prisma           # Database schema
│   ├── migrations/             # Migration files
│   └── seed.ts                 # Seed data
├── __tests__/
│   ├── unit/                   # Unit tests (mirror src/ structure)
│   ├── integration/            # Integration tests
│   └── e2e/                    # Playwright E2E tests
├── public/                     # Static assets
├── docs/                       # Documentation (PRD, vision, etc.)
└── scripts/                    # Utility scripts
```

---

## Development Philosophy: Test-Driven Development (TDD)

**This project follows strict TDD.** Every feature must follow the Red-Green-Refactor cycle.

### The TDD Workflow

```
1. RED    — Write a failing test that describes the desired behavior
2. GREEN  — Write the minimum code to make the test pass
3. REFACTOR — Clean up the code while keeping tests green
```

### TDD Rules

1. **Never write production code without a failing test first.** If you're about to create a component, service, or utility — write the test first.
2. **One test at a time.** Don't write a full test suite upfront. Write one test, make it pass, then write the next.
3. **Tests define the API.** The test is the first consumer of your code. If the test is awkward to write, the API needs redesign.
4. **Commit at green.** Every time tests go green after a refactor, that's a valid commit point.

### Test Categories

| Type | Framework | Location | Runs |
|------|-----------|----------|------|
| **Unit** | Vitest + React Testing Library | `__tests__/unit/` | On every save (watch mode) |
| **Integration** | Vitest | `__tests__/integration/` | Pre-commit hook |
| **E2E** | Playwright | `__tests__/e2e/` | CI pipeline + pre-deploy |

### What to Test

**Always test:**
- Component rendering and user interactions
- API endpoint request/response contracts
- Business logic (recommendation engine, budget calculator, quantity formulas)
- Data transformations (AI response → structured data, product data → PDF format)
- Error states and edge cases

**Don't test:**
- Third-party library internals (shadcn/ui, Prisma, react-pdf)
- CSS styling details (test behavior, not appearance)
- Implementation details (test outcomes, not how they're achieved)

### Test Naming Convention

```typescript
describe('RecommendationEngine', () => {
  it('scores products higher when style matches cuisine type', () => { ... })
  it('excludes products above the budget threshold', () => { ... })
  it('returns empty array when no products match criteria', () => { ... })
})
```

Format: `it('[action] when [condition]')` — describes behavior, not implementation.

### Mocking Strategy

- **AI API calls:** Always mock. Use fixture responses that mirror real Claude output structure.
- **Database:** Use Prisma's test utilities or an in-memory SQLite for unit tests. Real Neon DB for integration tests.
- **Google Maps API:** Always mock. Store fixture responses in `__tests__/fixtures/`.
- **Email (Resend):** Always mock. Verify the send function was called with correct params.
- **PDF generation:** Mock for unit tests. Generate real PDFs in integration tests.

---

## Commands

```bash
# Development
pnpm dev                    # Start dev server (localhost:3000)
pnpm build                  # Production build
pnpm start                  # Start production server
pnpm lint                   # Run ESLint
pnpm format                 # Run Prettier

# Testing
pnpm test                   # Run all unit tests
pnpm test:watch             # Run tests in watch mode (use during TDD)
pnpm test:coverage          # Run tests with coverage report
pnpm test:integration       # Run integration tests
pnpm test:e2e               # Run Playwright E2E tests
pnpm test:e2e:ui            # Run Playwright with UI mode

# Database
pnpm db:push                # Push schema changes (dev)
pnpm db:migrate             # Run migrations (production)
pnpm db:seed                # Seed database
pnpm db:studio              # Open Prisma Studio

# Utilities
pnpm type-check             # TypeScript type checking
pnpm clean                  # Remove build artifacts
```

---

## Coding Standards

### TypeScript

- **Strict mode enabled.** No `any` types except in test mocks.
- Use `interface` for object shapes, `type` for unions/intersections.
- Export types from `src/types/` — co-locate component-specific types with the component.
- Use Zod for runtime validation at API boundaries.

### Components

- Functional components only. No class components.
- Use `'use client'` directive only when the component needs client-side interactivity.
- Keep components small — if a component exceeds ~100 lines, split it.
- Props interface named `{ComponentName}Props`.
- No default exports for components (use named exports).

```typescript
// Good
export function ChatMessage({ message, isAI }: ChatMessageProps) { ... }

// Bad
export default function ChatMessage(props: any) { ... }
```

### API Routes

- Use Zod schemas to validate request bodies.
- Return consistent response shapes: `{ data: T }` for success, `{ error: string }` for failures.
- Always return appropriate HTTP status codes.
- Handle errors with try/catch — never let unhandled errors reach the client.

```typescript
// API response pattern
export async function POST(req: Request) {
  try {
    const body = await req.json()
    const validated = schema.parse(body)
    const result = await doSomething(validated)
    return Response.json({ data: result })
  } catch (error) {
    if (error instanceof z.ZodError) {
      return Response.json({ error: 'Invalid input', details: error.errors }, { status: 400 })
    }
    return Response.json({ error: 'Internal server error' }, { status: 500 })
  }
}
```

### File Naming

- Components: `PascalCase.tsx` (e.g., `ChatMessage.tsx`)
- Utilities/services: `camelCase.ts` (e.g., `recommendationEngine.ts`)
- Test files: `*.test.ts` or `*.test.tsx` (e.g., `ChatMessage.test.tsx`)
- Types: `camelCase.ts` in `src/types/` (e.g., `product.ts`)

### Git Workflow

- Branch naming: `feature/short-description`, `fix/short-description`
- Commit messages: imperative mood, 50 char subject line
  - `Add chat message component with markdown support`
  - `Fix budget calculator overflow for large seat counts`
  - `Test recommendation engine scoring algorithm`
- Commit at every green test cycle in TDD
- PR required for merging to main — CI must pass

---

## Environment Variables

```env
# Database
DATABASE_URL=               # Neon PostgreSQL connection string

# AI
ANTHROPIC_API_KEY=          # Claude API key
OPENAI_API_KEY=             # OpenAI API key (fallback)

# Google Maps
GOOGLE_MAPS_API_KEY=        # Google Maps Platform API key

# Email
RESEND_API_KEY=             # Resend API key

# App
NEXT_PUBLIC_APP_URL=        # Application URL (e.g., https://curatetable.com)
```

---

## AI Integration Notes

### Claude API Usage

- **Model:** `claude-sonnet-4-5-20250929` for conversation, `claude-haiku-4-5-20251001` for extraction tasks
- **System prompt:** Located in `src/lib/ai/prompts.ts` — all prompts centralized here
- **Structured output:** Use Claude's tool use feature to get structured JSON from conversations
- **Token management:** Track token usage per session. Budget ~4,000 tokens per conversation turn.
- **Streaming:** Use streaming responses for chat UI to show real-time typing

### Prompt Engineering Guidelines

- System prompts define the AI's role as a dinnerware consultant
- Use few-shot examples in prompts for consistent data extraction
- Separate extraction prompts from conversation prompts
- Version control all prompts — treat them as code, not config

---

## Key Business Logic

### Quantity Calculation

```
units_needed = seating_capacity × multiplier × (1 + breakage_buffer)

Multipliers by dining style:
  - Fine dining: 3.0x (multiple courses, formal place settings)
  - Casual dining: 2.5x (standard turnover)
  - Fast casual: 2.0x (high turnover, simpler settings)
  - Cafe/bistro: 1.5x (minimal settings)

Breakage buffer:
  - High durability products: 10%
  - Standard products: 15%
  - Delicate products: 25%
```

### Recommendation Scoring

```
product_score = (style_match × 0.30)
             + (budget_fit × 0.25)
             + (durability_match × 0.25)
             + (aesthetic_score × 0.20)

Each factor is scored 0-100.
Products below score 40 are excluded.
Top 3-5 products per category are recommended.
```

### Budget Allocation

```
Default allocation by category:
  - Dinner plates: 30%
  - Bowls: 20%
  - Salad/appetizer plates: 15%
  - Cups/mugs: 15%
  - Serving platters: 10%
  - Specialty items: 10%

Adjusted by cuisine type (e.g., Asian cuisine → higher bowl allocation).
```

---

## Common Pitfalls

1. **Don't call AI APIs in tests** — always mock. Tests must be fast and deterministic.
2. **Don't hardcode API keys** — always use environment variables.
3. **Don't skip the test** — if you're tempted to write code without a test, stop and write the test first.
4. **Don't over-fetch** — use Prisma's `select` and `include` to query only needed fields.
5. **Don't trust user input** — validate with Zod at every API boundary.
6. **Don't block the UI** — use streaming for AI responses, optimistic updates for interactions.
7. **Don't commit `.env`** — it's in `.gitignore`. Use `.env.example` for documentation.

---

## Reference Documents

- [PRD](./PRD.md) — Full product requirements
- [Vision](./VISION.md) — Product vision and strategy
- [Task Tracker](./TASK_TRACKER.md) — Development task tracking
- [Bug Tracker](./BUG_TRACKER.md) — Bug reporting and tracking
- [UI/UX Style Guide](./UI_UX_STYLE_GUIDE.md) — Design system and style guide
