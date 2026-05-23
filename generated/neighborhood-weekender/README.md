# Neighborhood Weekender (Hyperlocal Planner)

Build a small website/app that helps someone answer: “What should I do this weekend near me?” without doom-scrolling. It produces a tight plan (2–4 activities + 1–2 food stops) based on distance, budget, and vibes, and can export a shareable itinerary link.

## Target user
- People who want to get out of the house but don’t want to research
- Couples/friends planning last-minute
- New residents exploring their neighborhood

## Core value
One screen that turns messy inputs (location + preferences) into a confident weekend plan.

## MVP (hackathon-friendly)
### Inputs
- Home base (typed neighborhood or lat/long)
- Time window (Sat/Sun, morning/afternoon/evening)
- Radius (e.g. 1km / 3km / 5km)
- Budget (free / $ / $$ / $$$)
- Vibes (chips): chill, outdoors, arts, coffee, nightlife, family-friendly, nerdy

### Output
- “Plan card” with 3–5 stops in order:
  - Stop name, short why, ETA/travel time
  - “Swap” button to cycle alternatives
- One-tap share link (public read-only)
- “Export” (simple): copy text / calendar (.ics) download

## Demo data strategy (no external APIs required)
Seed a local JSON dataset to keep the demo reliable:
- `venues.json`: parks, cafes, galleries, markets
- `events.json`: weekend events with time windows

Bonus: add a “Use live data” toggle later (Google Places, Yelp, Eventbrite, Meetup, Ticketmaster, etc.), but keep MVP deterministic with seeds.

## Killer demo flow (3 minutes)
1. Enter “Tiong Bahru” (or your local neighborhood), pick “Sat afternoon”, radius 3km, budget $$
2. Select vibes: coffee + arts + outdoors
3. App generates:
   - Coffee stop → gallery → park → dinner
4. Hit “Swap” on one stop, see it re-plan the route coherently
5. Export to calendar and open share link on a second device/tab

## Wow moment
“Constraint-aware re-plan”: swapping a stop automatically re-orders and adjusts the rest (including time windows) so it still fits the selected afternoon.

## Simple scoring / planning logic
- Filter candidates by:
  - distance radius
  - open hours / event time window overlap
  - budget tag
- Score with weighted preferences:
  - vibe match count
  - rating/popularity (from seed)
  - diversity bonus (avoid 3 cafes in a row)
- Route:
  - greedy nearest-neighbor with a “don’t backtrack” penalty (good enough for hackathon)

## Pages
- `/` Home: inputs + “Generate plan”
- `/plan/:id` Plan view: itinerary + swaps + export
- `/seed` (dev only): preview/edit seed data

## Tech suggestions (pick one)
- Next.js + Tailwind + local JSON seeds (fastest)
- SvelteKit (great for small apps)
- Remix + SQLite (if you want persistence)

## Data model (minimal)
```ts
type Venue = {
  id: string;
  name: string;
  category: "coffee" | "food" | "park" | "museum" | "shop" | "bar" | "viewpoint";
  vibes: string[];
  price: "free" | "$" | "$$" | "$$$";
  lat: number;
  lng: number;
  open: { day: number; start: string; end: string }[];
  popularity: number; // seed: 0..100
};

type Event = {
  id: string;
  name: string;
  vibes: string[];
  price: "free" | "$" | "$$" | "$$$";
  lat: number;
  lng: number;
  startISO: string;
  endISO: string;
  popularity: number;
};

type Plan = {
  id: string;
  createdAtISO: string;
  baseLabel: string;
  window: "sat-morning" | "sat-afternoon" | "sat-evening" | "sun-morning" | "sun-afternoon" | "sun-evening";
  radiusKm: number;
  budget: "free" | "$" | "$$" | "$$$";
  vibes: string[];
  stops: { kind: "venue" | "event"; refId: string; note: string }[];
};
```

## Next build steps (concrete)
1. Create seeds for one neighborhood (15 venues, 10 events)
2. Implement filter + scoring + plan builder
3. Implement “Swap stop” that re-plans subsequent stops
4. Add shareable plan links (KV store or SQLite)
5. Add export: copy text + `.ics`

