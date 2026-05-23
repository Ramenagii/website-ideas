# Local Business Landing Page — Practical Draft

This is a reusable landing-page spec you can adapt to *any* local business (plumber, cafe, tutoring, salon, pet grooming, etc.). Keep it simple, fast, and conversion-focused.

## Goal
Turn “search / map / social” traffic into:
- Calls/texts
- Quote requests
- Booked appointments

## Audience
- People within your service area who need the service **now**
- People comparing 2–3 options and looking for trust signals

## MVP Pages
- `/` Single landing page (one page is enough)
- `/privacy` (optional, if you run forms/analytics)

Optional later:
- `/services` SEO service pages (1 per service)
- `/areas` service-area pages (1 per neighborhood/city)
- `/gallery` before/after
- `/reviews` embedded highlights
- `/contact` (if you don’t want a long single page)

## Information Architecture (section order)
1. **Sticky header**
   - Logo + primary CTA button: “Call now” / “Get a quote”
   - Secondary: “Services”, “Reviews”, “Service area”
2. **Hero**
   - Clear offer + location: “{Service} in {City} — same-day availability”
   - One sentence promise: “On time. Transparent pricing. 5-star local reviews.”
   - CTAs: primary “Call/Text”, secondary “Get a quote” (form)
3. **Trust strip**
   - 3–5 items: years in business, rating, license/insured, warranty, response time
4. **Services**
   - 3–6 cards with 1-line descriptions + “From $X” if you can
5. **How it works**
   - 3 steps: Contact → On-site/remote assessment → Job done + follow-up
6. **Service area**
   - Map screenshot or list of neighborhoods + “Outside this list? Ask.”
7. **Proof**
   - Reviews highlights (3–6)
   - Before/after gallery (6–12 photos) if relevant
8. **About**
   - 1–2 short paragraphs + real photo + values (no stock imagery if possible)
9. **FAQ**
   - Pricing, timing, coverage, guarantees, cancellations
10. **Final CTA**
   - Repeat phone number + short form
11. **Footer**
   - NAP (name, address, phone), hours, links, social

## Copy Starter (fill the blanks)

### Hero (examples)
- “{Business Name}: {Service} in {City}”
- “Same-day {Service} — {City} & nearby”
- “Reliable {Service} for {City} homeowners”

**Subhead:**
“Fast response, clear pricing, and work that lasts. Serving {Neighborhoods/City}.”

**Primary CTA button:**
- “Call/Text {Phone}”

**Secondary CTA button:**
- “Get a free quote”

### Services cards (template)
**{Service name}**
One sentence benefit + who it’s for.

### FAQ (starter questions)
- “How much does {service} cost?”
- “Do you offer same-day appointments?”
- “What areas do you serve?”
- “Are you licensed/insured?”
- “Do you guarantee the work?”

## Forms (minimal, high-conversion)
Keep it 3–5 fields max:
- Name
- Phone (required)
- Zip / neighborhood (optional)
- What do you need? (short text)
- Preferred time (optional)

On submit:
- Show a confirmation message with next-step expectation (“We’ll reply within 15 minutes during business hours.”)
- Send an email + (optional) SMS to the owner

## Design Direction (clean local-service aesthetic)
- High contrast, large headings, oversized CTAs
- Use real photos: team, storefront, truck, worksite, before/after
- Keep animations minimal; prioritize load speed on mobile

Simple tokens baseline:
```css
:root{
  --bg:#0b1220;
  --panel:#0f1a2e;
  --text:#eef2ff;
  --muted:#b6c0d6;
  --brand:#22c55e;
  --brand2:#38bdf8;
  --border:rgba(238,242,255,.12);
  --radius:16px;
  --max:1100px;
}
```

## SEO / Local Search Checklist
- Use the city in:
  - Title: “{Service} in {City} | {Business Name}”
  - H1: “{Service} in {City}”
  - Meta description: include phone + key differentiator
- Put NAP + hours in footer (and in schema)
- Add `LocalBusiness` schema + `Service` schema
- Add a Google Business Profile link and review link
- Add one page per high-intent service keyword later (don’t do it on day 1)

## Conversion Checklist
- Phone number is visible above the fold on mobile
- CTA buttons use `tel:` and `sms:` on mobile
- Reviews are real names/initials + city when possible
- Show “what happens next” after form submit

## Implementation Notes (practical)
- MVP can be pure HTML/CSS or a simple static site (Astro/Next static)
- Host on Vercel/Netlify/Cloudflare Pages
- Use image optimization (WebP/AVIF) and lazy-load below the fold
- Add basic analytics (privacy-friendly) after launch

## Follow-up Tasks (to make it real)
- Pick a specific business type + fill in all placeholders
- Add 6 real photos (no stock if possible)
- Add 3 real review quotes (even if short)
- Decide 1 primary CTA (call vs quote form) and optimize for it
- Add a pricing anchor (“Starting at…”) if your market supports it

