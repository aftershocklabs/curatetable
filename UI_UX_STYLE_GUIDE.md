# CurateTable - UI/UX Style Guide

> **Version:** 1.0
> **Last Updated:** February 14, 2026
> **Design Philosophy:** Clean, warm, professional — a digital showroom, not a spreadsheet.

---

## 1. Design Principles

### 1.1 Core Principles

| Principle | Description | Application |
|-----------|-------------|-------------|
| **Warm Professionalism** | Feel like a high-end showroom, not enterprise software | Generous whitespace, warm tones, photography-forward |
| **Conversational First** | The chat is the product — everything else supports it | Chat UI is dominant; product views emerge from conversation |
| **Show, Don't Tell** | Let products speak visually — minimize text walls | Large product images, minimal description text, visual budget breakdowns |
| **Progressive Disclosure** | Reveal complexity only when needed | Start simple (chat), build to detail (recommendations → catalog) |
| **Trust Through Clarity** | Build confidence in AI recommendations | Show reasoning, be transparent about scoring, explain "why" |

### 1.2 Design Personality

Think: **"If a boutique tableware showroom had a website that felt like talking to their best salesperson."**

- Not cold and corporate (no blue-gray enterprise dashboards)
- Not cutesy and playful (not a consumer app with bouncing animations)
- Warm, knowledgeable, confident — like a trusted advisor

---

## 2. Color System

### 2.1 Brand Colors

```
Primary Palette (Warm Neutrals + Accent)
─────────────────────────────────────────

Charcoal          #1C1917     — Primary text, headers
Warm Gray         #44403C     — Secondary text, body copy
Stone             #78716C     — Tertiary text, labels, muted elements
Sand              #F5F0EB     — Primary background (warm off-white)
Cream             #FAF8F5     — Card backgrounds, elevated surfaces
White             #FFFFFF     — Input fields, modals

Accent: Terracotta
  Default          #C2410C     — Primary CTAs, active states, links
  Light            #EA580C     — Hover states
  Lighter          #FFF7ED     — Accent backgrounds, notification bg
  Dark             #9A3412     — Pressed states

Secondary Accent: Sage
  Default          #4D7C0F     — Success states, positive indicators
  Light            #65A30D     — Hover
  Lighter          #F7FEE7     — Success backgrounds
  Dark             #3F6212     — Pressed
```

### 2.2 Semantic Colors

```
Success           #4D7C0F (Sage)         — Confirmations, positive actions
Warning           #CA8A04 (Amber)        — Caution states, budget warnings
Error             #DC2626 (Red)          — Errors, destructive actions
Info              #2563EB (Blue)         — Informational notes, tips
```

### 2.3 Color Usage Rules

- **Sand (#F5F0EB)** is the default page background — never pure white for full pages
- **Terracotta** is reserved for primary CTAs and interactive elements — don't overuse
- **Charcoal on Sand** is the primary text-on-background pairing (contrast ratio: 12.5:1)
- Product images should always sit on **White or Cream** backgrounds for consistency
- Dark mode: Not in MVP scope. Design with light mode only for now.

---

## 3. Typography

### 3.1 Font Stack

```
Headings:    "DM Serif Display", Georgia, serif
Body:        "Inter", system-ui, -apple-system, sans-serif
Monospace:   "JetBrains Mono", "Fira Code", monospace  (code, SKUs)
```

**DM Serif Display** — Warm, editorial serif for headings. Communicates quality and craft without being stuffy.
**Inter** — Clean, highly readable sans-serif for body text. Excellent at small sizes. Variable font for performance.

### 3.2 Type Scale

```
Display     — 48px / 1.1 line-height / DM Serif Display   (Landing hero only)
H1          — 36px / 1.2 line-height / DM Serif Display   (Page titles)
H2          — 28px / 1.3 line-height / DM Serif Display   (Section titles)
H3          — 22px / 1.4 line-height / Inter 600           (Subsections)
H4          — 18px / 1.4 line-height / Inter 600           (Card titles)
Body Large  — 18px / 1.6 line-height / Inter 400           (Lead paragraphs)
Body        — 16px / 1.6 line-height / Inter 400           (Default body text)
Body Small  — 14px / 1.5 line-height / Inter 400           (Secondary text, captions)
Caption     — 12px / 1.4 line-height / Inter 500           (Labels, metadata)
```

### 3.3 Tailwind Config

```javascript
// tailwind.config.ts
fontFamily: {
  serif: ['"DM Serif Display"', 'Georgia', 'serif'],
  sans: ['Inter', 'system-ui', '-apple-system', 'sans-serif'],
  mono: ['"JetBrains Mono"', '"Fira Code"', 'monospace'],
}
```

---

## 4. Spacing & Layout

### 4.1 Spacing Scale

Use Tailwind's default 4px-based spacing scale:

```
4px   (1)   — Tight gaps within compact elements
8px   (2)   — Within components (icon-to-text gap)
12px  (3)   — Between related elements
16px  (4)   — Default spacing between elements
24px  (6)   — Between component groups
32px  (8)   — Between sections
48px  (12)  — Major section separation
64px  (16)  — Page-level vertical rhythm
```

### 4.2 Layout Grid

```
Max content width:    1280px (max-w-7xl)
Chat interface:       768px max (max-w-3xl) — centered
Product grid:         1280px with 4-column grid (desktop)
Side padding:         16px mobile, 24px tablet, 32px+ desktop
```

### 4.3 Breakpoints

Use Tailwind defaults:

```
sm:    640px    — Large phones, landscape
md:    768px    — Tablets
lg:    1024px   — Small laptops
xl:    1280px   — Desktops
2xl:   1536px   — Large screens
```

### 4.4 Page Layout Patterns

**Chat Page (primary experience):**
```
┌─────────────────────────────────────────┐
│  Logo                        [New Chat] │  ← Minimal header
├─────────────────────────────────────────┤
│                                         │
│         Chat Messages Area              │  ← Scrollable, centered
│         (max-w-3xl, mx-auto)            │
│                                         │
│  ┌───────────────────────────────────┐  │
│  │  AI: Welcome to CurateTable...    │  │
│  └───────────────────────────────────┘  │
│                                         │
│  ┌───────────────────────────────────┐  │
│  │  You: Mexican cantina, Brooklyn...│  │
│  └───────────────────────────────────┘  │
│                                         │
├─────────────────────────────────────────┤
│  [ Type your message...        ] [Send] │  ← Sticky bottom input
└─────────────────────────────────────────┘
```

**Recommendation View (emerges from chat):**
```
┌─────────────────────────────────────────┐
│  Logo    [Back to Chat]    [Download]   │
├─────────────────────────────────────────┤
│                                         │
│  "Your Curated Collection"              │
│  Mexican Cantina · Brooklyn · $2,000    │
│                                         │
│  ┌─────────┐  Budget Breakdown          │
│  │ [Donut] │  Plates: $600              │
│  │ [Chart] │  Bowls: $400               │
│  └─────────┘  Cups: $300...             │
│                                         │
│  ── Dinner Plates ──────────────────    │
│  ┌─────┐ ┌─────┐ ┌─────┐              │
│  │ img │ │ img │ │ img │              │
│  │name │ │name │ │name │              │
│  │$12  │ │$15  │ │$18  │              │
│  └─────┘ └─────┘ └─────┘              │
│                                         │
│  ── Bowls ──────────────────────────    │
│  ...                                    │
│                                         │
│  [Generate PDF Catalog] [Email to Rep]  │
└─────────────────────────────────────────┘
```

---

## 5. Component Design

### 5.1 Chat Components

#### Chat Message — AI

```
┌──────────────────────────────────────────────┐
│  🍽️  CurateTable                              │
│                                              │
│  Great choice! A Mexican cantina in Brooklyn │
│  — that's a vibrant neighborhood. Let me     │
│  ask a few questions to find the perfect     │
│  dinnerware for you.                         │
│                                              │
│  What's your approximate seating capacity?   │
│                                              │
│  [25-40 seats]  [40-60 seats]  [60+ seats]  │  ← Quick reply chips
└──────────────────────────────────────────────┘

Style:
  - Background: cream (#FAF8F5)
  - Border: 1px solid stone/20 (#78716C33)
  - Border-radius: 16px (top-left: 4px for AI, top-right: 4px for user)
  - Padding: 16px
  - Max width: 85% of container
  - AI messages: left-aligned
  - Shadow: sm (subtle depth)
```

#### Chat Message — User

```
                ┌──────────────────────────────┐
                │  Mexican cantina in Brooklyn, │
                │  about 50 seats, $2k budget  │
                └──────────────────────────────┘

Style:
  - Background: terracotta (#C2410C)
  - Text: white (#FFFFFF)
  - Border-radius: 16px (top-right: 4px)
  - Padding: 12px 16px
  - Max width: 75% of container
  - User messages: right-aligned
```

#### Quick Reply Chips

```
  [25-40 seats]  [40-60 seats]  [60+ seats]

Style:
  - Background: transparent
  - Border: 1.5px solid terracotta (#C2410C)
  - Text: terracotta (#C2410C)
  - Border-radius: 999px (pill)
  - Padding: 8px 16px
  - Hover: background terracotta/10, scale 1.02
  - Active: background terracotta, text white
  - Font: 14px Inter 500
```

#### Chat Input

```
┌──────────────────────────────────────────────┐
│  Tell us about your restaurant...        ⬆️  │
└──────────────────────────────────────────────┘

Style:
  - Background: white (#FFFFFF)
  - Border: 1.5px solid stone/30 (#78716C4D)
  - Border-radius: 24px
  - Padding: 12px 16px, right padding for send button
  - Focus: border terracotta (#C2410C), shadow ring terracotta/20
  - Send button: terracotta circle icon, disabled when empty
  - Textarea auto-grows up to 4 lines
  - Position: sticky bottom with frosted glass backdrop
```

### 5.2 Product Components

#### Product Card

```
┌───────────────────────────┐
│                           │
│      [Product Image]      │  ← 1:1 aspect ratio, object-cover
│       white background    │
│                           │
├───────────────────────────┤
│  Product Name             │  ← H4, Charcoal, 1 line truncate
│  SKU: AC-2847             │  ← Caption, Stone, monospace
│                           │
│  ★ 92 match               │  ← Match score, terracotta
│  "Durable, rustic style"  │  ← AI justification, Body Small
│                           │
│  $12.50 /unit             │  ← H3, Charcoal
│  Qty: [-] 125 [+]        │  ← Quantity adjuster
│  Subtotal: $1,562.50      │  ← Body Small, Stone
└───────────────────────────┘

Style:
  - Background: white (#FFFFFF)
  - Border: 1px solid stone/15 (#78716C26)
  - Border-radius: 12px
  - Shadow: sm (hover: md with slight translateY -2px)
  - Transition: all 200ms ease
  - Image container: bg-sand, rounded-t-12
```

#### Match Score Badge

```
  ★ 92 match

Style:
  - 90-100: terracotta background, white text ("Excellent match")
  - 70-89:  sage/light background, sage text ("Great match")
  - 40-69:  amber/light background, amber text ("Good match")
  - Font: 12px Inter 600
  - Border-radius: 999px (pill)
  - Padding: 4px 10px
```

### 5.3 Budget Visualization

#### Donut Chart

```
  ┌──────────┐
  │  ╭────╮  │   Dinner Plates  ████████  30%  $600
  │ ╭╯    ╰╮ │   Bowls          ██████    20%  $400
  │ │$2,000│ │   Salad Plates   █████     15%  $300
  │ ╰╮    ╭╯ │   Cups & Mugs   █████     15%  $300
  │  ╰────╯  │   Platters       ███       10%  $200
  └──────────┘   Specialty      ███       10%  $200

Colors:
  - Dinner Plates: terracotta (#C2410C)
  - Bowls: sage (#4D7C0F)
  - Salad Plates: amber (#CA8A04)
  - Cups: blue (#2563EB)
  - Platters: purple (#7C3AED)
  - Specialty: pink (#DB2777)

Center: Total budget in DM Serif Display
Legend: Horizontal bar chart with labels
```

### 5.4 Tier Selector

```
  ┌─────────────┬─────────────┬─────────────┐
  │    Good      │  ● Better   │    Best      │
  │   $1,450     │   $2,000    │   $2,780     │
  └─────────────┴─────────────┴─────────────┘

Style:
  - Container: bg-sand, rounded-12, border stone/20
  - Active tab: bg-white, shadow-sm, font-semibold
  - Inactive tab: transparent, text-stone
  - Transition: background 200ms, shadow 200ms
  - Price shown below label in Body Small
```

---

## 6. Motion & Animation

### 6.1 Principles

- **Purposeful, not decorative.** Every animation communicates state change.
- **Fast.** Default duration: 200ms. Nothing exceeds 400ms.
- **Easing:** `ease-out` for entrances, `ease-in` for exits, `ease-in-out` for transitions.

### 6.2 Animation Inventory

| Element | Animation | Duration | Easing |
|---------|-----------|----------|--------|
| Chat message (appear) | Fade in + slide up 8px | 300ms | ease-out |
| Typing indicator | 3 dots pulse | 1.2s loop | ease-in-out |
| Quick reply chips | Staggered fade in | 150ms + 50ms stagger | ease-out |
| Product card (hover) | Translate Y -2px + shadow increase | 200ms | ease-out |
| Page transition | Fade in | 200ms | ease-out |
| Button (press) | Scale 0.97 | 100ms | ease-in |
| Toast notification | Slide in from top right | 300ms | ease-out |
| Budget chart | Segments animate in sequentially | 600ms total | ease-out |
| Score badge | Count up from 0 | 400ms | ease-out |
| Modal | Backdrop fade + content scale from 0.95 | 200ms | ease-out |

### 6.3 Loading States

**Chat AI response:**
```
  ┌──────────────────────────────┐
  │  🍽️  CurateTable              │
  │                              │
  │  ●  ●  ●                     │  ← Pulsing dots, terracotta
  └──────────────────────────────┘
```

**Product loading:**
```
  ┌───────────────────────┐
  │  ░░░░░░░░░░░░░░░░░░  │  ← Skeleton shimmer (sand → cream pulse)
  │  ░░░░░░░░░░░░░░░░░░  │
  ├───────────────────────┤
  │  ░░░░░░░░░░░░         │
  │  ░░░░░░               │
  │  ░░░░░░░░░░           │
  └───────────────────────┘
```

Skeleton color: Animate between `#F5F0EB` (sand) and `#FAF8F5` (cream), 1.5s duration.

---

## 7. Iconography

### 7.1 Icon Library

Use **Lucide React** (the icon set used by shadcn/ui).

### 7.2 Common Icons

| Usage | Icon | Size |
|-------|------|------|
| Send message | `Send` (or `ArrowUp` in circle) | 20px |
| Back/return | `ArrowLeft` | 20px |
| Download PDF | `Download` | 20px |
| Email | `Mail` | 20px |
| Location | `MapPin` | 16px |
| Budget | `DollarSign` | 16px |
| Seats | `Users` | 16px |
| Cuisine | `UtensilsCrossed` | 16px |
| Close | `X` | 20px |
| Menu | `Menu` | 24px |
| Check/success | `Check` | 16px |
| Warning | `AlertTriangle` | 16px |
| Info | `Info` | 16px |
| New chat | `Plus` | 20px |

### 7.3 Icon Style Rules

- Stroke width: 1.5px (Lucide default)
- Color: inherit from parent text color
- Always pair icons with text labels (accessibility)
- Minimum touch target: 44x44px for interactive icons

---

## 8. Imagery

### 8.1 Product Photography

- **Background:** Pure white or very light gray (#FAFAFA)
- **Style:** Top-down (plan view) for plates; 45-degree angle for cups/bowls
- **Aspect ratio:** 1:1 (square) in cards, 4:3 in detail views
- **Quality:** WebP format, max 400KB per image, srcset for responsive
- **Placeholder:** Sand-colored placeholder with faded utensil icon while loading

### 8.2 Hero/Marketing Imagery

- **Style:** Warm, editorial — styled tabletop shots with food and dinnerware
- **Treatment:** Slight warm color grade, natural lighting feel
- **Overlay:** Semi-transparent sand overlay for text readability

---

## 9. Responsive Behavior

### 9.1 Mobile (< 768px)

- Chat is full-screen, edge-to-edge
- Product cards: single column, full width
- Bottom input bar with safe area inset for iOS
- No side navigation — use bottom sheet for secondary actions
- Quick reply chips: horizontal scroll if they overflow

### 9.2 Tablet (768px - 1024px)

- Chat centered at max-w-2xl
- Product cards: 2-column grid
- PDF preview in modal instead of inline

### 9.3 Desktop (> 1024px)

- Chat centered at max-w-3xl
- Product cards: 3-4 column grid
- Recommendation view: side panel possible for chat history
- PDF preview: inline with scroll

---

## 10. Accessibility

### 10.1 Requirements

| Requirement | Standard | Implementation |
|-------------|----------|----------------|
| Color contrast | WCAG 2.1 AA (4.5:1 body, 3:1 large text) | Verified for all color pairings |
| Focus indicators | Visible focus rings on all interactive elements | 2px terracotta outline, 2px offset |
| Keyboard navigation | Full functionality via keyboard | Tab order, Enter/Space for actions, Escape for dismiss |
| Screen reader | All content accessible to screen readers | Semantic HTML, ARIA labels, live regions for chat |
| Reduced motion | Respect `prefers-reduced-motion` | Disable animations, use instant transitions |
| Touch targets | 44x44px minimum for touch devices | Applied to all buttons, links, interactive elements |

### 10.2 Chat-Specific Accessibility

- New messages announced via `aria-live="polite"` region
- AI typing indicator: `aria-label="CurateTable is typing"`
- Quick reply chips: `role="listbox"` with `role="option"` for each
- Chat input: clear `aria-label="Message input"`, associated with send button
- Message history: `role="log"` on container

### 10.3 Focus Management

```
Tab order: Logo → New Chat → Message History → Chat Input → Send Button
After sending: Focus returns to chat input
After AI responds: Screen reader announces new message
Modal open: Focus trapped in modal, Escape closes
```

---

## 11. Dark Mode (Future)

Not in MVP scope. When implemented:

- Swap Sand → `#1C1917` (Charcoal) for backgrounds
- Swap Charcoal → `#F5F0EB` (Sand) for text
- Terracotta accent remains the same
- Product images retain white background (floating card style)
- Use `prefers-color-scheme` media query + manual toggle

---

## 12. PDF Catalog Styling

The PDF is a distinct deliverable with its own styling:

### Cover Page
```
┌─────────────────────────────────┐
│                                 │
│     [Manufacturer Logo]         │
│                                 │
│     ─────────────────           │
│                                 │
│     Curated For:                │
│     Maria's Mexican Cantina     │  ← DM Serif Display, large
│     Brooklyn, NY                │
│                                 │
│     February 14, 2026           │
│                                 │
│     Prepared by CurateTable     │  ← Small footer attribution
└─────────────────────────────────┘
```

### Product Page
```
┌─────────────────────────────────┐
│  [Product Image]     Product    │
│  (large, left)       Name      │
│                      SKU: XXX  │
│                                │
│                      Material: │
│                      Color:    │
│                      Size:     │
│                                │
│                      $12.50/ea │
│                      Qty: 125  │
│                      = $1,562  │
│                                │
│  "Recommended because this     │
│   plate's rustic finish and    │
│   durability match..."         │
│                                │
│  ─────────────────────────     │
│  Arc Cardinal · CurateTable    │
└─────────────────────────────────┘
```

### Summary Page
```
┌─────────────────────────────────┐
│  Order Summary                  │
│                                 │
│  Dinner Plates    125  $1,562   │
│  Bowls             75    $825   │
│  Salad Plates      75    $450   │
│  ...                            │
│  ─────────────────────────      │
│  Total            350  $3,987   │
│                                 │
│  Recommended reorder: May 2026  │
│                                 │
│  Contact: sales@arccardinal.com │
│  ─────────────────────────      │
│  Generated by CurateTable       │
└─────────────────────────────────┘
```

**PDF fonts:** Use Inter (embedded) for body, DM Serif Display for headings.
**PDF colors:** Manufacturer's brand colors for accents, Charcoal for text.

---

## 13. Design Token Summary (Tailwind)

```javascript
// tailwind.config.ts — custom theme extension
{
  colors: {
    brand: {
      charcoal: '#1C1917',
      'warm-gray': '#44403C',
      stone: '#78716C',
      sand: '#F5F0EB',
      cream: '#FAF8F5',
    },
    terracotta: {
      DEFAULT: '#C2410C',
      light: '#EA580C',
      lighter: '#FFF7ED',
      dark: '#9A3412',
    },
    sage: {
      DEFAULT: '#4D7C0F',
      light: '#65A30D',
      lighter: '#F7FEE7',
      dark: '#3F6212',
    },
  },
  fontFamily: {
    serif: ['"DM Serif Display"', 'Georgia', 'serif'],
    sans: ['Inter', 'system-ui', '-apple-system', 'sans-serif'],
    mono: ['"JetBrains Mono"', '"Fira Code"', 'monospace'],
  },
  borderRadius: {
    DEFAULT: '8px',
    lg: '12px',
    xl: '16px',
    full: '999px',
  },
}
```

---

## 14. Component Library Reference (shadcn/ui)

The following shadcn/ui components should be installed for MVP:

| Component | Usage |
|-----------|-------|
| `Button` | CTAs, actions, send message |
| `Input` | Form fields, email input |
| `Textarea` | Chat input (auto-resize) |
| `Card` | Product cards, summary cards |
| `Dialog` | Confirmations, email input modal |
| `Tabs` | Good/Better/Best tier selector |
| `Badge` | Match score, status indicators |
| `Toast` | Success/error notifications |
| `Skeleton` | Loading states |
| `Tooltip` | Icon explanations, score details |
| `ScrollArea` | Chat message container |
| `Separator` | Section dividers |
| `Avatar` | AI avatar in chat |

All shadcn/ui components should be customized to match the color palette defined above. Override the default shadcn theme in `globals.css`.
