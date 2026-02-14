# CurateTable — Lovable.dev Prompt

> Copy everything below and paste it into Lovable as a single prompt.

---

Build a complete AI-powered dinnerware configurator app called **CurateTable**. It helps restaurant owners describe their restaurant in a chat, then receives personalized dinnerware recommendations with a downloadable PDF catalog. This is a demo MVP — use simulated AI chat responses (no real AI API calls) with realistic scripted conversation logic, and a Supabase database for products. Use Unsplash product images for dinnerware as placeholders.

---

## DESIGN SYSTEM (follow exactly)

**Fonts:** Import "DM Serif Display" from Google Fonts for headings. Use Inter (already in Tailwind) for body text.

**Colors — extend Tailwind config:**
- Page background: `#F5F0EB` (warm sand — NEVER pure white for page backgrounds)
- Card/surface background: `#FAF8F5` (cream)
- Input/modal background: `#FFFFFF`
- Primary text: `#1C1917` (charcoal)
- Secondary text: `#44403C` (warm gray)
- Muted/label text: `#78716C` (stone)
- Primary accent (CTAs, links, active states): `#C2410C` (terracotta)
- Primary accent hover: `#EA580C`
- Primary accent light bg: `#FFF7ED`
- Secondary accent (success): `#4D7C0F` (sage)
- Warning: `#CA8A04` (amber)
- Error: `#DC2626`

**Personality:** Warm, premium, editorial — like a high-end tableware showroom website, NOT a cold SaaS dashboard. Generous whitespace. Photography-forward. Serif headings give it an editorial, premium feel.

**Icons:** Use Lucide React icons throughout.

---

## SUPABASE DATABASE

Create the following tables:

**manufacturers**
- id (uuid, PK), name (text), slug (text unique), logo_url (text), primary_color (text default '#C2410C'), secondary_color (text default '#1C1917'), contact_email (text), created_at (timestamptz default now())

**products**
- id (uuid, PK), manufacturer_id (uuid FK → manufacturers.id), name (text), sku (text unique), category (text — enum: 'dinner_plate', 'salad_plate', 'bowl', 'cup', 'saucer', 'serving_platter', 'glassware'), description (text), material (text), color (text), dimensions (text), weight (text), price (numeric), image_url (text), durability_rating (integer 1-5), style_tags (text array), active (boolean default true), created_at (timestamptz default now())

**restaurant_profiles**
- id (uuid, PK), session_id (text unique), restaurant_name (text), cuisine_type (text), location (text), seating_capacity (integer), budget (numeric), dining_style (text — 'fine_dining', 'casual', 'fast_casual', 'cafe'), style_preferences (text array), created_at (timestamptz default now())

**catalogs**
- id (uuid, PK), restaurant_profile_id (uuid FK → restaurant_profiles.id), manufacturer_id (uuid FK → manufacturers.id), recommendations (jsonb), total_cost (numeric), status (text default 'generated'), emailed_to (text), created_at (timestamptz default now())

Seed with 1 manufacturer (Arc Cardinal, slug: "arc-cardinal", logo_url: use a placeholder) and exactly 50 products across all categories with realistic dinnerware names, SKUs (format: "AC-XXXX"), materials (porcelain, stoneware, bone china, tempered glass, melamine), colors, prices ($3-$45 range), durability ratings, and style_tags (rustic, modern, classic, minimalist, colorful, organic, industrial). Use Unsplash dinnerware/plate/bowl/cup image URLs.

---

## PAGES AND ROUTES

### 1. Landing Page (`/`)

Full-screen hero with sand background:
- Navigation bar: "CurateTable" logo text in DM Serif Display on the left, "How It Works" and "Start Configuring" links on the right
- Hero section: Large DM Serif Display heading "The Smartest Way to Choose Your Restaurant's Dinnerware", subtitle in Inter "AI-powered recommendations tailored to your cuisine, location, and budget", large terracotta CTA button "Start Configuring" that navigates to `/chat`
- How It Works section: 3-step horizontal cards with icons — (1) Chat icon + "Tell Us About Your Restaurant" + "Describe your concept, cuisine, and budget in natural language", (2) Sparkles icon + "Get AI Recommendations" + "Our engine matches products to your exact needs", (3) FileText icon + "Download Your Catalog" + "Receive a personalized PDF catalog ready for ordering"
- Features section: 2x3 grid of feature cards with icons — Location Intelligence (MapPin), Menu Matching (UtensilsCrossed), Budget Optimization (DollarSign), Custom PDF Catalogs (FileText), Email Delivery (Mail), Smart Reordering (RefreshCw)
- Footer: "Built by AfterShock Labs" with copyright

### 2. Chat Page (`/chat`)

This is the CORE experience. Full-height layout (100vh) with:

**Header:** Slim bar with "CurateTable" logo left, "New Chat" button right (Plus icon)

**Message area:** Centered container (max-width 768px), scrollable, messages stack vertically:
- AI messages: Left-aligned, cream background `#FAF8F5`, border 1px `#78716C33`, rounded-2xl (top-left-sm), max-width 85%, subtle shadow-sm. Show small plate icon + "CurateTable" label above message.
- User messages: Right-aligned, terracotta `#C2410C` background, white text, rounded-2xl (top-right-sm), max-width 75%
- Messages animate in with fade + slide up (300ms ease-out)

**Quick reply chips:** When the AI asks a question, show clickable pill buttons below the message — terracotta border, transparent bg, terracotta text. On click, they fill in and send as a user message.

**Input bar:** Sticky bottom, frosted glass backdrop (`backdrop-blur-md` + `bg-white/80`), centered max-width 768px. Rounded-full input with placeholder "Tell us about your restaurant...", auto-growing textarea (max 4 lines). Terracotta circular send button (ArrowUp icon) on the right, disabled when empty.

**SIMULATED CHAT FLOW — implement this as a state machine with these steps:**

Step 1 (initial): AI sends welcome message: "Welcome to CurateTable! I'm your personal dinnerware consultant. Tell me about your restaurant — your cuisine, location, number of seats, and budget — and I'll recommend the perfect tableware for you. Or just start with your restaurant name and we'll go from there!"

Step 2 (after first user message): Parse the user's text to extract any of: restaurant name, cuisine type, location, seat count, budget. For anything not mentioned, AI asks a follow-up. Example: if user says "Italian bistro in Manhattan", AI responds: "An Italian bistro in Manhattan — love it! That suggests warm, classic tableware with durability for a bustling neighborhood. How many seats do you have?" with quick reply chips: ["Under 30", "30-50", "50-80", "80+"]

Step 3 (after seats): AI asks about budget. "Got it! And what's your approximate dinnerware budget?" with chips: ["Under $1,000", "$1,000-$2,500", "$2,500-$5,000", "$5,000+"]

Step 4 (after budget): AI asks about style preference. "Last question — what vibe are you going for?" with chips: ["Classic & Elegant", "Modern & Minimalist", "Rustic & Earthy", "Bold & Colorful"]

Step 5 (after style): AI shows a confirmation card — a styled card component embedded in the chat showing the extracted restaurant profile:
```
Restaurant Profile:
📍 [Name] — [Location]
🍽️ [Cuisine Type] · [Dining Style]
💺 [Seat Count] seats
💰 Budget: $[amount]
🎨 Style: [preference]
```
With a "Generate Recommendations" terracotta button and "Edit Details" text link below. Store this profile to Supabase `restaurant_profiles` table.

Step 6 (after clicking Generate): Show typing indicator (3 pulsing terracotta dots), wait 2 seconds, then navigate to `/recommendations/[session_id]`

At every step, if the user provides multiple pieces of info at once, skip the already-answered questions and jump ahead.

### 3. Recommendations Page (`/recommendations/:sessionId`)

This page shows the AI-curated product recommendations. Fetch the restaurant profile from Supabase and run the recommendation logic client-side.

**Header:** "CurateTable" logo, "Back to Chat" button (ArrowLeft), "Download PDF" button (Download icon, terracotta)

**Restaurant context banner:** Sand background card at top showing: Restaurant name (DM Serif Display), location with MapPin icon, cuisine + dining style, seat count, budget. All in one horizontal line on desktop, stacked on mobile.

**Budget breakdown section:**
- Left: Donut chart (use Recharts) showing budget allocation by category. Center of donut shows total budget in DM Serif Display. Colors: terracotta, sage, amber, blue `#2563EB`, purple `#7C3AED`, pink `#DB2777`
- Right: Horizontal bar breakdown — category name, colored bar, percentage, dollar amount
- Categories and default allocation: Dinner Plates 30%, Bowls 20%, Salad Plates 15%, Cups & Mugs 15%, Serving Platters 10%, Glassware 10%

**Tier selector:** Three-tab toggle: "Good" / "Better" (selected by default) / "Best" — each shows a different total cost. Good = 70% of budget, Better = 100%, Best = 140%. Active tab has white bg + shadow, inactive is transparent. Switching tiers re-filters products by price range.

**Product sections:** One section per category (Dinner Plates, Bowls, Salad Plates, Cups & Mugs, Serving Platters, Glassware). Each section has:
- Category heading in DM Serif Display
- Responsive grid of ProductCards (1 col mobile, 2 tablet, 3-4 desktop)

**ProductCard component:**
- White background, rounded-xl, border stone/15, hover: shadow-md + translateY -2px (200ms ease-out)
- Top: Product image on sand bg, 1:1 aspect ratio, object-cover
- Match score badge (positioned top-right of image): pill shape showing "★ 92 match". Colors by score — 90-100: terracotta bg/white text, 70-89: sage light bg/sage text, 40-69: amber light bg/amber text
- Product name (font-semibold), SKU in monospace caption
- AI justification text in italic, small, warm-gray (e.g. "Durable porcelain, perfect for high-turnover casual Italian dining")
- Price per unit (large, charcoal), quantity with +/- stepper buttons, live-updating subtotal
- "Add to Catalog" toggle button (outline → filled terracotta when selected)

**RECOMMENDATION ENGINE (client-side logic):**
Query products from Supabase. Score each product using:
- `style_match` (0-100): Compare product style_tags against restaurant style preference — exact match = 90-100, partial = 50-70, none = 20-40 (randomize within ranges for variety)
- `budget_fit` (0-100): How well the per-unit price fits the per-category budget allocation — under budget = 80-100, at budget = 60-80, over = 20-50
- `durability_match` (0-100): Compare durability_rating against dining style needs — fast_casual needs 4-5, fine_dining accepts 2-3, casual = 3-4
- `aesthetic_score` (0-100): Randomized 60-95 to simulate AI aesthetic judgment
- Final score: `(style × 0.30) + (budget × 0.25) + (durability × 0.25) + (aesthetic × 0.20)`. Exclude products below 40. Show top 3-5 per category, sorted by score descending.

Pre-select the top 2 products per category. Auto-calculate quantities: `seating_capacity × multiplier × 1.15` (15% breakage buffer). Multipliers: fine_dining = 3.0, casual = 2.5, fast_casual = 2.0, cafe = 1.5. Round to nearest 5.

**Floating bottom bar:** Shows: "[X] items selected" • "Total: $[amount]" • "Generate PDF Catalog" terracotta button • "Email to Sales Rep" outline button. Slides up on scroll, subtle shadow.

**Save catalog to Supabase** `catalogs` table when user clicks Generate PDF.

### 4. Catalog Preview / PDF Page (`/catalog/:catalogId`)

Fetch catalog data from Supabase. Show a visual PDF preview and download option.

**Use `@react-pdf/renderer`** to generate a real downloadable PDF. Also show an HTML preview on-screen styled to look like the PDF.

**PDF Layout:**

Page 1 — Cover:
- Manufacturer logo (placeholder) centered top
- Horizontal rule
- "Curated For:" label in small caps
- Restaurant name in large DM Serif Display
- Location, cuisine, date
- "Prepared by CurateTable" small footer

Page 2 — Summary:
- "Your Dinnerware Collection" heading
- Table: Category, Product, Qty, Unit Price, Subtotal — one row per selected product
- Total row at bottom, bold
- "Estimated Reorder Date: [3 months from now]"
- Budget donut chart (static image version)

Pages 3+ — Product detail pages (one per selected product):
- Left: Large product image
- Right: Product name (DM Serif Display), SKU, material, color, dimensions
- Price per unit, quantity, subtotal
- AI recommendation reason in italic
- Match score
- Horizontal rule + "Arc Cardinal · CurateTable" footer

**On-screen controls:**
- "Download PDF" button (generates and downloads the PDF file)
- "Email Catalog" button — opens a modal dialog: email input field, "Send" button. On send, show a success toast "Catalog sent to [email]!" (simulate — no real email). Save the email to the catalog's `emailed_to` field in Supabase.
- "Back to Recommendations" link
- "Start New Configuration" link → `/chat`

### 5. Not Found Page

Warm, friendly 404 with "Looks like this plate is empty" heading, illustration placeholder, and "Go Home" button.

---

## GLOBAL UI PATTERNS

**Loading states:** Use shimmer skeleton components (animate between sand and cream colors, 1.5s loop) for all async data loading. Chat typing indicator: 3 dots pulsing in terracotta.

**Toasts:** Use sonner or shadcn toast. Appear top-right, slide in 300ms. Success = sage accent, Error = red accent.

**Responsive:** Mobile-first. Chat is edge-to-edge on mobile. Product grid collapses to single column. Bottom bar is full-width on mobile. All touch targets minimum 44x44px.

**Transitions:** Page transitions use fade-in (200ms). Chat messages use fade + slide-up (300ms). Product cards use hover translateY + shadow (200ms). Buttons scale to 0.97 on press (100ms).

**Empty states:** If no products match, show: plate icon + "No matches found" + "Try adjusting your preferences" link.

**Error states:** Friendly messages like "Something went wrong. Let's try that again." with a retry button.

---

## IMPORTANT IMPLEMENTATION NOTES

1. The chat must feel real — implement the state machine carefully with smooth transitions, typing delays (800-1500ms before AI responds), and natural language in the responses
2. Pre-seed the Supabase database with 50 realistic Arc Cardinal dinnerware products using the seed SQL. Include varied styles, materials, and price points
3. The recommendation scoring must be deterministic given the same inputs — use the profile data to seed calculations, not Math.random()
4. The PDF must actually download as a real .pdf file using @react-pdf/renderer
5. The entire app should feel like a polished product demo — no placeholder text, no "lorem ipsum", no broken layouts
6. All product images should use real Unsplash dinnerware photos (use specific search terms: "white dinner plate", "ceramic bowl", "coffee cup porcelain", "serving platter", "wine glass")
7. Make the sand (#F5F0EB) background the dominant visual — this is what makes it feel warm and premium, not generic
