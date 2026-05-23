# Receipts & Warranty Vault (web app) — Practical Draft

Store purchase receipts and warranty details, get reminders before coverage expires, and export a “proof packet” when you need to file a claim, return something, or submit reimbursements.

## Goal

Make it painless to answer:
- “Where is the receipt for this?”
- “Is this still under warranty?”
- “What do I need to send to support/insurance/HR?”

## Target Audience

- People who buy electronics/appliances/furniture and lose receipts
- Renters/homeowners who need proof for claims
- Freelancers/employees who submit reimbursements

## Core Differentiator

One item = receipt(s) + warranty timeline + quick “export packet” for claims.

## MVP Scope (v1)

### Must-have
- Add an item with: merchant, purchase date, price, category, notes
- Attach files: photo/PDF receipts, manuals, screenshots (serial number, order confirmation)
- Warranty fields: coverage length, expiration date (auto-calculated), provider contact/URL
- Search + filter (category, merchant, expiring soon, missing receipt)
- Reminders list (in-app): “expiring in 30/14/7 days”
- Export packet:
  - Single-item ZIP download containing attachments + a generated summary PDF/HTML
  - Or “claim view” page with everything in one place

### Nice-to-have (still v1 if easy)
- Barcode/QR scanning for serial numbers (camera input)
- OCR extraction from receipts (optional; can be manual-only in MVP)

### Explicitly not in MVP
- Multi-party sharing, team plans
- Automatic email reminders (do in v2)
- Integrations (Gmail, Amazon, Apple receipts)

## Key Pages / IA

1. Landing (`/`)
2. Auth (optional) (`/login`, `/signup`)
3. Dashboard (`/app`)
   - Expiring soon
   - Recently added
   - “Missing data” prompts (no receipt, no warranty, no serial)
4. Items list (`/app/items`)
5. Item detail (`/app/items/:id`)
   - Summary, warranty status, attachments
   - “Export packet” action
6. Add/edit item (`/app/items/new`, `/app/items/:id/edit`)
7. Reminders (`/app/reminders`)
8. Settings (`/app/settings`)
   - Export all data, import, delete account/data

## Data Model (minimal)

### `User`
- `id`
- `email`
- `createdAt`

### `Item`
- `id`
- `userId`
- `title` (e.g., “LG 27\" Monitor”)
- `merchant`
- `purchaseDate`
- `price` (number + currency)
- `category` (enum or string)
- `serialNumber` (optional)
- `orderNumber` (optional)
- `notes` (optional)
- `createdAt`, `updatedAt`

### `Warranty`
- `id`
- `itemId`
- `type` (manufacturer / extended / store)
- `providerName`
- `startDate` (defaults to purchase date)
- `durationMonths` (optional if `endDate` is set)
- `endDate`
- `policyNumber` (optional)
- `supportUrl` (optional)
- `supportPhone` (optional)

### `Attachment`
- `id`
- `itemId`
- `kind` (receipt / manual / photo / screenshot / other)
- `filename`
- `mimeType`
- `sizeBytes`
- `storageKey` (blob/object store key)
- `uploadedAt`

### `ReminderRule` (derived-first; persist later)
- For MVP, compute reminders from `Warranty.endDate`:
  - 30/14/7/1 days before expiration

## Reminder Logic (MVP)

- “Expiring soon” if `endDate` is within the next 30 days.
- “Overdue” if `endDate` is in the past.
- For the Reminders page, generate rows:
  - `itemId`, `daysUntilEnd`, `label`, `dueDate`

## Export Packet (MVP)

Two paths (pick one for first build):

### Option A — HTML “Claim View” (fastest)
- Server renders a single printable page with:
  - Item summary
  - Warranty details
  - Attachment gallery/list with download links
- Add “Download all attachments (ZIP)” as a separate action later

### Option B — ZIP + Manifest (more useful)
- Create `manifest.json` for the item
- Include `summary.html` (or `summary.pdf`) plus all attachments
- ZIP filename like `receipt-vault_<item-title>_<purchase-date>.zip`

## Tech Stack (practical)

### Easiest modern build
- Next.js (App Router) + TypeScript
- Auth: NextAuth/Auth.js (or Clerk)
- DB: Postgres (Neon/Supabase) with Prisma
- File storage: S3-compatible (Cloudflare R2 / AWS S3) via presigned uploads
- PDF/print: HTML-to-PDF optional; start with printable HTML

### “Offline-first” variant (alternative)
- Single-user, no login
- IndexedDB for metadata + File System Access API for attachments (where supported)
- Export/import as a ZIP
This variant avoids server costs but is more browser-compat dependent.

## API Sketch (if server-backed)

- `POST /api/items` create item
- `GET /api/items?query=&filter=` list
- `GET /api/items/:id` detail
- `PATCH /api/items/:id` update
- `POST /api/items/:id/attachments` create upload intent (presigned URL)
- `POST /api/items/:id/export` returns export artifact (HTML/PDF/ZIP)

## Seed Content / Example Items

1. “Dyson V8 Vacuum”
   - Purchase: 2025-11-02
   - Warranty: 24 months, ends 2027-11-02
   - Attachments: receipt PDF, serial photo
2. “IKEA MALM bed frame”
   - Purchase: 2024-06-18
   - Warranty: store policy 365 days

## UX Notes

- Make “Add item” extremely fast: title + purchase date + add receipt photo
- Highlight missing critical info on item detail:
  - No receipt attached
  - Warranty end date unknown
  - Serial number missing
- On mobile: camera-first receipt capture with auto-crop (optional later)

## Metrics / Success Criteria

- Time to add an item: under 60 seconds (mobile)
- “Find receipt” success: under 15 seconds via search
- Export packet: one click + shareable/printable output

## Next Steps

1. Decide MVP mode:
   - Server-backed accounts + blob storage, or
   - Offline-first local vault
2. Choose export approach (Claim View vs ZIP)
3. Draft UI wireframes for:
   - Items list, item detail, add flow, reminders

