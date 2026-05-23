# Personal Goals Dashboard (Website Draft)

## One-liner
A private dashboard to set goals, break them into habits/projects, and review progress with weekly check-ins.

## Target user
People who want a simple, self-hostable alternative to sprawling “life OS” tools: students, early-career professionals, makers.

## Core promise
Turn “I want to do X” into an actionable plan with:
- clear outcomes (goals)
- consistent actions (habits)
- visible progress (check-ins + charts)

## MVP scope (ship in 1–2 weekends)
### 1) Goals
- Create/edit/archive goals
- Fields: title, category, start date, target date, success metric (free text), status
- Optional: link goals to habits and projects

### 2) Habits
- Simple daily/weekly habits (e.g., “Run 3x/week”)
- Habit schedule: days-of-week or N times per week
- Check off completions; show streaks and “this week vs target”

### 3) Weekly check-in (the “sticky” feature)
- A guided form every week:
  - What went well?
  - What didn’t?
  - What will I change next week?
  - Choose top 3 priorities for next week
- Auto-summarize prior week stats on the check-in page

### 4) Dashboard
- “This week” overview:
  - habit progress bars
  - goals at risk (near target date, low activity)
  - quick-add completion
- A simple trend chart: last 8 weeks habit completion %

## Key pages
- `/` Dashboard
- `/goals` Goal list + filters
- `/goals/:id` Goal detail (linked habits/projects + notes)
- `/habits` Habit list
- `/check-in` Weekly check-in (current week + history)
- `/settings` (theme, export, data reset)

## Data model (minimal)
- Goal: `id`, `title`, `category`, `startAt`, `targetAt`, `metric`, `status`, `notes`
- Habit: `id`, `title`, `targetPerWeek`, `schedule`, `goalIds[]`, `createdAt`
- Completion: `id`, `habitId`, `completedAt` (date)
- CheckIn: `id`, `weekStart`, `wentWell`, `didnt`, `change`, `priorities[]`, `createdAt`

## Differentiators (avoid feature creep)
- Weekly check-in is first-class (history view + lightweight stats)
- “At risk” highlighting (simple heuristics; no complicated AI)
- Export/backup from day 1 (JSON + CSV)

## Nice-to-haves (post-MVP)
- “Projects” linked to goals (milestones + due dates)
- Tags + smart filters
- Calendar view for habit completions
- Reminders (email/push) + “missed check-in” nudge
- Read-only public “year review” share page (opt-in)

## Tech stack suggestion (practical)
- Next.js (App Router) + Tailwind
- SQLite (local dev) + Prisma
- Auth: optional single-user password or “magic link” (keep simple)
- Charts: lightweight (e.g., Recharts) or just sparklines

## Launch checklist
- Seed demo data
- One-click deploy instructions (optional)
- Basic privacy statement (“data stays with you”)
- Export button + confirmation dialogs for delete/reset

