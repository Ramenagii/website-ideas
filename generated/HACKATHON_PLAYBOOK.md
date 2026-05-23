# Hackathon Playbook

This playbook turns the generated website ideas into projects that can win attention in a short demo. The goal is not to make every idea bigger. The goal is to make each one sharper, more visual, and easier for judges to understand.

## Selection Criteria

- Clear pain: the audience should recognize the problem immediately.
- Demo speed: the main flow should land in under 90 seconds.
- Technical spark: include one feature that feels alive, such as OCR, PDF export, local-first sync, AI review, or a GitHub import.
- Finishability: the MVP should be buildable in 24-48 hours.
- Shareability: the final result should have a public URL, seeded demo data, and a crisp README.

## Ranked Concepts

### 1. Receipts + Warranty Vault

**One-liner:** A searchable vault for receipts, warranties, and claim packets.

**Why it can win:** Everyone has lost a receipt or forgotten a warranty. The demo can show immediate transformation from messy purchase data into a useful packet.

**Weekend MVP:**
- Item vault with seeded purchases.
- Receipt upload state with mocked OCR extraction.
- Warranty timeline and expiration warnings.
- Claim packet preview and PDF export.

**Demo script:**
1. Open the vault and search for "laptop".
2. Show receipt, serial number, warranty deadline, and attachments.
3. Click "Build claim packet".
4. Export or preview the packet.

**Stretch:** Add email reminder scheduling and AI-generated claim notes.

### 2. Move-Out Checklist + Photo Inventory

**One-liner:** A deposit-protection packet builder for renters.

**Why it can win:** It has a concrete audience, strong visuals, and a satisfying final artifact.

**Weekend MVP:**
- Room checklist with condition status.
- Photo grid with timestamps and notes.
- Deposit-risk summary.
- Landlord-ready PDF packet.

**Demo script:**
1. Pick "Bedroom" and mark walls, floor, windows, and fixtures.
2. Add sample photos and notes.
3. Show missing evidence warnings.
4. Generate the final move-out packet.

**Stretch:** Before/after comparison and shareable landlord link.

### 3. Meal Planner + Auto Grocery List

**One-liner:** Plan the week and get one clean grocery list automatically.

**Why it can win:** It is easy to understand, fun to click through, and works well as a polished local-first app.

**Weekend MVP:**
- Weekly calendar.
- Recipe library with ingredients.
- Grocery list aggregation by aisle.
- Pantry toggle and local storage.

**Demo script:**
1. Drag meals onto the week.
2. Watch the grocery list merge duplicates.
3. Toggle pantry items off.
4. Export or copy the final list.

**Stretch:** AI meal suggestions based on dietary constraints.

### 4. Freelance Invoice + Client Portal

**One-liner:** Send a polished invoice and client portal from one simple flow.

**Why it can win:** It is business-useful, easy to monetize, and can look professional quickly.

**Weekend MVP:**
- Invoice builder.
- Public client portal route.
- Status timeline.
- PDF invoice and mock payment state.

**Demo script:**
1. Create invoice from seeded line items.
2. Open the client portal.
3. Show invoice, files, status, and payment CTA.
4. Mark paid and show receipt state.

**Stretch:** Stripe Checkout integration and email notifications.

### 5. Personal Goals Dashboard

**One-liner:** A dashboard that spots goal drift before it becomes failure.

**Why it can win:** It adds intelligence to a familiar habit tracker category.

**Weekend MVP:**
- Goal cards and habit streaks.
- At-risk scoring rules.
- Weekly review generator.
- Recovery action checklist.

**Demo script:**
1. Open a seeded dashboard.
2. Show which goal is at risk and why.
3. Generate a weekly review.
4. Accept recovery actions for next week.

**Stretch:** Calendar integration and AI coaching tone controls.

## GitHub-Ready Checklist

- Add screenshots or GIFs once the first UI exists.
- Keep `README.md` focused on what the project does, how to run it, and what the demo proves.
- Use GitHub issues for each idea's MVP tasks.
- Add labels such as `mvp`, `demo`, `design`, `stretch`, and `needs-data`.
- Open one issue per top-ranked concept so progress is visible.

## Suggested Next Build

Build `receipts-warranty-vault` first. It has the strongest mix of real-world utility, demo clarity, and technical flash. A polished prototype only needs seeded data, mocked OCR, a timeline, and an export preview to feel credible.
