# Pivot Profiles — MVP Product Requirements Document

## 1. Problem

* Current **Consultant Profiles** are Word resumes in SharePoint → stale, hard to update, emailed without control.
* Sales chases Pivots for updates → awkward and brittle.
* Once sent, no visibility: who opened, what they looked at, or whether it was forwarded.
* No ability to revoke, watermark, or track engagement.
* Inconsistent branding across formats.

## 2. Objectives

* One **source of truth** for profiles (Markdown + YAML, versioned in Git).
* **Sales Composer**: create an Engagement, select consultants, toggle sections, generate share links, view counters.
* **Client Viewer**: sleek, branded, light/dark theme; scoped profile rendering; expiry banner; mock download buttons.
* **Tracking**: simple counters for opens, section views, and downloads.
* **Local-first**: fully containerised stack with Next.js + Postgres, runnable via `docker compose up`.

Later we can extend to Supabase/Auth, real PDF/DOCX exports, watermarking, and nudging.

## 3. Users & Roles

* **Pivot (Consultant)**: Maintains their profile in Git as Markdown+YAML.
* **Sales Staff**: Uses Sales Composer to create and share profiles for a lead.
* **Customer (Recipient)**: Views profiles via secure share link, can (mock) download PDF/DOCX.

## 4. MVP Scope

### In scope

* Parse sample consultant YAML profiles into JSON at runtime (from `profiles/`).
* Sales Composer web app:

  * Engagement name + expiry input
  * Consultant selector (from parsed profiles)
  * Section toggles (bio, skills, projects, employment, education)
  * Generate/copy share link
  * Revoke share link
  * Counters: opens, section views, downloads
* Client Viewer web app:

  * Render scoped consultant profiles
  * Expiry banner
  * Download PDF/DOCX buttons (mock: `alert("Download…")`)
  * Branded light/dark theme, sleek/professional look
* Tracking:

  * Log open (after “meaningful view” threshold), section views (IntersectionObserver), download clicks
  * Increment counters in Sales Composer

### Out of scope

* Real email sending
* Per-recipient tokens
* Watermarking/fingerprinting
* Real PDF/DOCX generation
* Nudging for stale profiles
* Auth (fake role toggle, e.g. `?as=sales` vs default viewer)

## 5. Flows

1. **Sales creates share**: inputs name/expiry → selects consultants → toggles sections → generates link.
2. **Customer opens link**: sees scoped profile(s) → expiry banner → can scroll (logs section views) → clicks “Download” (mock).
3. **Sales dashboard updates**: counters show views and downloads in near-real time.
4. **Revocation**: Sales clicks “Revoke” → link shows “This link has expired/revoked”.

## 6. Data Model (simplified for MVP)

* **Profile**: parsed from YAML (`name, role, summary, skills[], industries[], employment[], education[], projects[]`).
* **Share**: `{ id, engagement_name, expiry_at, consultants[], sections[], revoked_at }`.
* **Event**: `{ ts, share_id, type (open|section_view|download), meta }`.

All persisted in Postgres (via docker-compose service).

## 7. Tech Stack

* **Frontend**: React/Next.js (App Router)
* **Backend**: Next.js API routes
* **Database**: Postgres (dockerised, local)
* **Dev**: Docker Compose for `web` + `db`, seeded with 5 sample YAML profiles

## 8. Non-Functional Requirements

* Local-first: must run with `docker compose up` without cloud dependencies.
* Theming: light/dark mode toggle with brand tokens (ink, muted, bg, card, border, accent, badge).
* Professional & sleek design (SixPivot branding cues).
* Extensible: clear seams for swapping Postgres → Supabase, fake auth → Supabase Auth, mock downloads → real exports.

## 9. Demo Script

1. Open Sales Composer → create engagement, select 2 profiles, toggle sections, generate link.
2. Open link in new tab → customer view appears, scroll & click download.
3. Switch back → counters increment.
4. Revoke link → refresh viewer tab → “This link has expired/revoked.”

## 10. Risks

* AI agents need tight contracts to avoid scope creep.
* Time-boxed demo: keep exports & auth mocked to avoid build bottlenecks.
* Ensure light/dark theming + brand tokens are consistent and not hardcoded.
