# Portfolio Site (Developer/Creator) — Practical Draft

## Goal
Build a fast, credible portfolio that helps a visitor answer, in under 30 seconds:
1) what you do, 2) what you’ve shipped, 3) why you’re trustworthy, 4) how to contact you.

## Audience
- Hiring managers / recruiters
- Potential clients
- Other builders (collaboration)

## Core Pages (MVP)
- `/` Home (single-page layout is OK)
- `/projects` Project index + detail sections (can be anchors on `/` initially)
- `/about` About / bio (can be section on `/`)
- `/contact` Contact (or modal/section)

Optional later:
- `/blog` Writing (3–5 posts max to start)
- `/now` “What I’m working on”
- `/uses` Tools/setup (creator-friendly)

## IA / Sections (Home)
1. **Hero**
   - One-liner role + niche (“Full‑stack engineer shipping payments & dashboards”)
   - 2 CTAs: “View projects” + “Email me”
   - Social icons: GitHub, LinkedIn, X/Bluesky, email
2. **Proof strip**
   - 3–5 quick credibility chips: years, domains, notable metrics, locations/timezone
3. **Featured projects (3)**
   - Card: name, problem, what you did, result, stack, links (live + code)
4. **Capabilities**
   - 6–8 bullets grouped by theme: product, frontend, backend, infra, UX
5. **About**
   - 2 short paragraphs + headshot
   - “Principles” list (quality, shipping, empathy, etc.)
6. **Testimonials (optional)**
   - 1–3 quotes with name/company (or “Former manager” if needed)
7. **Contact**
   - Email, calendly link, location/timezone, availability
8. **Footer**
   - Copyright, sitemap, RSS if blog exists

## Copy Starter (Editable)

### Hero
**Headline (pick one):**
- “I build reliable web products that ship.”
- “Full‑stack developer focused on fast, accessible UX.”
- “Creator‑engineer turning ideas into shipped software.”

**Subhead:**
- “I design and build high‑performance web apps end‑to‑end—frontend, backend, and deployment. Currently open to {role/type} work.”

**CTAs:**
- Primary: “See projects”
- Secondary: “Contact me”

### Project card template
- **Title:** {Project name}
- **Problem:** 1 sentence
- **Solution:** 1–2 sentences (your role + what you built)
- **Impact:** 1 metric (latency, conversion, revenue, time saved)
- **Stack:** {list}
- **Links:** Live / Repo / Case study

### About (short)
“I’m a {role} based in {location/timezone}. I like building simple, durable products—especially where performance, design, and developer experience meet.”

## Design Direction (Simple + Premium)

### Tokens (CSS variables)
Use these as a baseline theme; tweak freely.

```css
:root{
  --bg: #0B0F14;
  --panel: #0F1620;
  --text: #E6EEF8;
  --muted: #A8B3C1;
  --brand: #6EE7FF;
  --brand2:#A78BFA;
  --border: rgba(230,238,248,.12);
  --shadow: 0 10px 30px rgba(0,0,0,.35);
  --radius: 16px;
  --max: 1100px;
}
```

### Typography
- Headings: Geist/Inter/System UI
- Body: Inter/System UI
- Code: ui-monospace

### Layout rules
- Max width `--max`, 24px gutters, generous vertical spacing
- Cards with subtle border + hover lift
- Focus states obvious (2px outline)

## SEO + Social
- Title format: `{Name} — {Role} | {Niche}`
- Meta description: 140–160 chars, concrete outcomes
- Add Open Graph image concept: name + role + 1–2 keywords
- Add structured data: `Person` + `WebSite` (optional)

## Accessibility Checklist
- Keyboard reachable nav and cards
- Visible focus ring
- Color contrast for text on panels
- `prefers-reduced-motion` respected
- Images with alt text; headshot alt is descriptive

## Implementation Notes (Tech-Agnostic)
MVP can be:
- Single HTML page + CSS + minimal JS, or
- Static site generator (Astro / Next static export), or
- Any framework you already ship with.

Suggested structure:
- `data/projects.json` (title, description, tags, links, highlights)
- `content/case-studies/*.md` (optional long-form writeups)

## Follow-up Tasks (to make it “real”)
- Collect 3 projects with one measurable impact each
- Write 1 case study (before/after + tradeoffs)
- Add 1 testimonial (or a “Work history” section)
- Add contact form (spam-protected) or mailto + calendar link
- Add basic analytics (privacy-friendly) and error monitoring

