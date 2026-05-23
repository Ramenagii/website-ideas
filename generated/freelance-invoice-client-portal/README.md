# Freelance invoices + lightweight client portal (MVP draft)

Goal: help a solo freelancer create invoices quickly, send a single clean link to a client, and track “sent / viewed / paid” without a full accounting suite.

## Target users
- Freelancers: designers, developers, writers, consultants
- Small agencies (1–5 people) who just need “good enough” invoicing + a client-facing page

## Non-goals (keep it small)
- Full bookkeeping/tax accounting
- Inventory, payroll, time tracking (can be added later)
- Multi-currency/VAT edge cases in MVP

## Core flows
1) Freelancer creates an invoice (draft → sent)
2) App generates a shareable invoice link (public-but-unguessable) and an email template
3) Client views invoice, downloads PDF, pays (or marks paid manually)
4) Freelancer sees status: sent/viewed/paid/overdue + reminders

## Page map
- `/` Marketing / “Sign in”
- `/app` Dashboard
  - KPIs: outstanding amount, overdue count, paid this month
  - Lists: Draft, Sent, Overdue, Paid
- `/app/clients`
  - Client list + create/edit
- `/app/invoices`
  - Invoice list + filters (status, client)
- `/app/invoices/new`
  - Invoice editor
- `/app/invoices/:id`
  - Invoice details + activity log + send/remind + mark paid/unpaid
- `/i/:token`
  - Client portal invoice view (no login)
  - Download PDF
  - Pay button (Stripe Checkout) OR “How to pay” instructions
- `/app/settings`
  - Profile + business info (name/address/logo)
  - Payment settings
  - Invoice defaults (due days, footer note)

## Minimal data model

**User**
- `id`
- `email`
- `name`
- `businessName`
- `businessAddress` (string for MVP)
- `logoUrl?`
- `defaultCurrency` (e.g., `USD`)

**Client**
- `id`
- `userId`
- `name`
- `email?`
- `company?`
- `billingAddress?`

**Invoice**
- `id`
- `userId`
- `clientId`
- `number` (e.g., `2026-004`)
- `status` (`draft|sent|viewed|paid|void|overdue`)
- `issueDate`
- `dueDate`
- `notes?`
- `subtotal`
- `tax` (number; optional MVP)
- `total`
- `publicToken` (random, unique)
- `sentAt?`
- `lastViewedAt?`
- `paidAt?`
- `paymentMethod` (`stripe|manual`)
- `stripeCheckoutSessionId?`

**InvoiceLineItem**
- `id`
- `invoiceId`
- `description`
- `quantity`
- `unitPrice`
- `amount` (stored for snapshot safety)

**InvoiceEvent** (activity log)
- `id`
- `invoiceId`
- `type` (`created|sent|viewed|reminder_sent|marked_paid|marked_unpaid|voided`)
- `createdAt`
- `meta` (JSON)

## Status logic (simple, deterministic)
- `overdue` when `status in (sent, viewed)` and `today > dueDate` and `paidAt is null`
- `viewed` on first client page view (`/i/:token`)
- `paid` when Stripe webhook confirms payment OR user manually marks paid

## Integrations (pick one for MVP)

### Option A: Stripe Checkout (recommended)
- Freelancer configures Stripe (connect their account)
- Client clicks “Pay now” → hosted Stripe Checkout
- Webhook updates invoice `paidAt` + `status=paid`

**Pros:** real payments, clean UX, less fraud handling  
**Cons:** needs webhook + env + Stripe setup

### Option B: Manual payments
- Invoice view shows payment instructions (bank transfer / PayPal link / etc.)
- Freelancer clicks “Mark paid”

**Pros:** simplest operationally  
**Cons:** no automatic confirmation

## Email templates (copy-ready)
**Send invoice**
- Subject: `Invoice {{invoice.number}} from {{businessName}} (due {{invoice.dueDate}})`
- Body: short note + link `{{publicUrl}}`

**Reminder**
- Subject: `Reminder: Invoice {{invoice.number}} is due {{invoice.dueDate}}`
- Body: one sentence + link

## MVP build checklist
- Auth: email magic link or password (single-user is fine)
- CRUD: clients, invoices, line items
- Public invoice page with token auth + “viewed” tracking
- PDF rendering (server-side) with consistent template
- Status + filters + export (CSV of invoices)
- Stripe (optional) + webhook handler + local test mode

## Tech stack suggestions (practical)
- Next.js (App Router) + Postgres (Neon/Supabase) + Prisma
- Auth: Clerk / NextAuth / simple magic links
- PDF: `@react-pdf/renderer` or server HTML → PDF (Playwright) later
- Email: Resend (or just “copy email” in MVP)

## Next improvements (after MVP)
- Recurring invoices
- Saved items/templates
- Multiple team members
- Client history page (`/c/:token`) with past invoices
- Late fee rules + automated reminders
- Branding themes + custom domain for portal

