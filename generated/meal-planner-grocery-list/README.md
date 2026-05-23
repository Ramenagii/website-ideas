# Meal Planner + Grocery List (Local‑first)

## One‑liner
A fast weekly meal planner that automatically builds a grocery list, with optional pantry tracking and recipe clipping — designed to work offline and without accounts.

## Goal
Help a household answer “what are we eating this week?” and “what do we need to buy?” with minimal friction, fewer forgotten ingredients, and less food waste.

## Target audience
- Busy individuals/couples/families who repeat meals and want a simple routine.
- People who prefer privacy/offline tools over account-based apps.
- Anyone doing “one big weekly grocery trip”.

## MVP scope (ship this first)
### Core flows
1) Plan meals for a week
- Choose days (Mon–Sun) and slots (Breakfast/Lunch/Dinner).
- Add meals from a small recipe list or as free-text (“Tacos”, “Leftovers”).

2) Generate a grocery list
- Each recipe has ingredients with quantities + units.
- Grocery list aggregates ingredients across the week.
- Supports marking items as “already have” or “in pantry”.

3) Grocery list execution
- Check items off in-store.
- Optional: group by store section (Produce, Dairy, Pantry, Frozen, Other).

### Explicit non-goals for MVP
- Nutrition tracking, calories/macros.
- Complex inventory management (expiry scanning, barcode).
- Multi-user sync and shared real-time lists.

## Key pages
- Home / This week
- Weekly planner (grid)
- Recipes (browse + create/edit)
- Grocery list (generated + check-off)
- Pantry (optional, simple quantities)
- Settings (start day of week, meal slots, units)

## Data model (minimal)
### Recipe
- id
- title
- servings (number)
- ingredients[]:
  - name (string; normalized for matching)
  - quantity (number; optional)
  - unit (string; optional; e.g., g, ml, tbsp, “can”)
  - section (enum; optional)
- notes (string; optional)
- sourceUrl (string; optional)

### Plan entry
- date (YYYY-MM-DD)
- slot (breakfast|lunch|dinner|snack)
- recipeId (optional) OR freeTextTitle
- servingsMultiplier (number; default 1)

### Pantry item (optional)
- id
- name (normalized)
- quantity (number; optional)
- unit (string; optional)
- section (enum; optional)

## UX details that make it “practical”
- “Repeat last week” button (copies plan entries forward by 7 days).
- “Leftovers night” quick action that doesn’t add groceries.
- Ingredient name normalization (simple): lowercase + trim + strip plural “s” heuristic.
- “Staples” list: items you always buy weekly unless pantry says otherwise (milk, eggs).
- Pantry is optional; users can still “mark as have” per grocery item.

## Tech stack suggestions
### Option A (fastest): Next.js + local-first storage
- Next.js App Router
- IndexedDB via `idb` or Dexie
- Export/import JSON file (for backup)
- Optional: PWA install + offline caching

### Option B: Static SPA (very simple)
- Vite + React
- LocalStorage for MVP (upgrade to IndexedDB later)

## Implementation checklist (MVP)
1) Recipe editor
- Add/edit recipe, ingredient rows, units dropdown + free-text.

2) Weekly planner
- Grid UI, add meal modal, quick actions (repeat last week).

3) Grocery list generator
- Aggregate by normalized ingredient name + unit.
- Handle missing quantities gracefully (“to taste”, blank quantity).

4) Grocery list UI
- Section grouping, check-off persistence, “mark as have”.

5) Backup
- Export all data to JSON.
- Import JSON with validation and conflict strategy (replace).

## Seed content (to avoid empty app)
Include ~12 starter recipes with realistic ingredients:
- Spaghetti + salad
- Chicken stir-fry + rice
- Taco night
- Lentil soup
- Sheet pan veggies + sausage
- Omelets + toast

## Follow-ups (nice-to-have)
- Shared list via “sync code” (later: accounts)
- Price estimates + budget per week
- Print-friendly grocery list PDF
- Recipe clipping via browser extension

## Next concrete decision(s)
- Pantry: default OFF or ON?
- Units: allow mixed units or enforce a single per ingredient?
- Start day of week: Monday or locale-based?

