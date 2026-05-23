# Move-out checklist + photo inventory for renters

A practical website/app to help renters plan a move-out, avoid deposit disputes, and keep an organized photo inventory of the unit condition.

## 1) The one-sentence pitch

Create a room-by-room move-out checklist, schedule tasks, and store timestamped photos/notes so you can document the unit’s condition and be ready for the final walkthrough.

## 2) Target audience

- Renters moving out (especially first-timers)
- Roommates splitting responsibilities
- Tenants in places where deposits commonly get disputed

## 3) Primary user goals

- Know exactly what to do each week before move-out day
- Avoid forgetting “small” items that trigger deposit deductions
- Capture consistent photo evidence (before + after cleaning, repairs, etc.)
- Export/share a clean “move-out packet” (PDF/ZIP link) if needed

## 4) Key pages / screens

1. **Home / Dashboard**
   - Countdown to move-out date
   - Today’s tasks + overdue tasks
   - “Capture photos” quick action
2. **Checklist builder**
   - Template chooser (studio / 1BR / 2BR / house)
   - Room sections (kitchen, bathroom, bedrooms, living, balcony, storage)
   - Task details (difficulty, supplies, est. minutes)
3. **Room detail**
   - Task list + “done” toggles
   - Photo log timeline (before/after, issues found)
   - Notes (e.g., “stain near sink”, “chip on tile”)
4. **Photo capture + labeling**
   - Prompts for consistent shots (wide shot, close-up of fixtures, floors, walls)
   - Tags: room, category (wall, floor, appliance), issue/severity
5. **Calendar / Schedule**
   - Suggested timeline (4 weeks out, 2 weeks out, final 48 hours)
   - Assign tasks to roommates (optional)
6. **Export / Share**
   - PDF “Move-out packet”: checklist completion + notes + photo thumbnails
   - Optional ZIP export of originals
   - Share link with expiry (account version) or local download (offline version)
7. **Settings**
   - Privacy controls
   - Data retention / delete all

## 5) MVP scope (2–5 days)

- Create a move-out “project” with move-out date and unit type
- Generate a checklist from templates, editable by user
- Mark tasks done + show progress bar
- Add photos to a room with timestamp + short note
- Export a simple PDF summary (no ZIP) containing:
  - Move-out date, address nickname (not full address by default)
  - Checklist completion
  - Photo thumbnails + notes per room

## 6) Nice-to-haves (later)

- Offline-first storage (IndexedDB) + local encryption
- Multi-device sync via accounts
- Roommate collaboration (invite link, task assignment)
- “Inspection mode” list of shots to capture during final walkthrough
- Reminders (email/push) for key deadlines
- Region-specific guidance (basic, non-legal): cleaning expectations, common deposit deductions

## 7) Data model (conceptual)

- `Project`
  - `id`, `name`, `moveOutDate`, `unitType`, `createdAt`
- `Room`
  - `id`, `projectId`, `name`, `sortOrder`
- `Task`
  - `id`, `roomId`, `title`, `notes`, `estimateMinutes`, `status`, `completedAt`
- `Photo`
  - `id`, `roomId`, `capturedAt`, `fileRef`, `caption`, `tags[]`

## 8) Suggested checklist templates (starter)

**Kitchen**
- Clean oven/stovetop (incl. drip pans, hood filter)
- Wipe inside/outside of fridge (defrost if needed)
- Clean sink + descale faucet aerator
- Wipe cabinets/drawers + remove liners

**Bathroom**
- Scrub grout + descale showerhead
- Clean toilet base + tank exterior
- Wipe mirror + vents/fan cover
- Check for mold spots + document if present

**General**
- Patch nail holes (if permitted) + touch-up paint (if permitted)
- Vacuum edges/baseboards + mop floors
- Clean windowsills/tracks + blinds
- Replace burnt bulbs (match type)

## 9) Tech stack options

### Option A: Offline-first single-user (fastest)

- Next.js (App Router) + React
- Local persistence via IndexedDB (Dexie) or `localStorage` for MVP
- PDF export via a server route (if using server) or client-side PDF library

Pros: no auth, privacy-friendly, easiest deploy.

### Option B: Account-based sync (more complete)

- Next.js + Auth (Clerk/Auth.js)
- Postgres (Neon/Supabase) + Prisma
- Blob storage for photos (S3/R2/Supabase Storage)
- Background job for PDF generation

Pros: multi-device, share links; Cons: more complexity + costs.

## 10) Seed content for landing page

**Headline:** Move out with confidence.  
**Subhead:** A simple checklist and photo log to help you get your deposit back.

**Value bullets**
- Know what to do each week before move-out
- Capture consistent, timestamped photos by room
- Export a neat move-out packet in one click

**FAQ (non-legal, careful wording)**
- *Is this legal advice?* No—this is an organizing tool. Check your lease and local rules.
- *Do you store my photos?* In offline mode, photos stay on your device unless you export/share them.

## 11) Next decisions

- Offline-first vs accounts/sync (pick one to avoid a split MVP)
- What export format matters most for users (PDF only vs PDF+ZIP)
- The level of “guidance” content (keep generic to avoid legal claims)

