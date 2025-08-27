We’re exploring a project called **Pivot Profiles** at SixPivot. Please give me a structured overview of the system and help refine the concept. Don’t go into code or build specifics yet — just map out the landscape and clarify the major moving parts.

### Context

* **Today’s state**:

  * Our “Consultant Profiles” are just resumes in Word format, stored in SharePoint.
  * Sales must nudge consultants to update them.
  * Once emailed to customers, we lose all control — we don’t know if they looked, what they focused on, or if the files were forwarded.
  * Formatting is inconsistent, branding gets lost, and there’s no revocation or visibility.

### The idea

Pivot Profiles is a new system to:

* Keep one **source of truth**: Markdown + YAML files in Git for each consultant profile.
* Render these into multiple branded formats (Web, PDF, Word).
* Give **Sales** an app to create “Engagements”: select consultants, choose which sections of their profile to expose, add attachments, and send secure links to customers.
* Provide a **Client Viewer** app where recipients can open these links in a branded, secure, no-index web view, with options to download allowed formats.
* Add **tracking and revocation**: see when a profile was opened, how long they viewed, which sections they looked at, downloads, and instantly revoke access if needed.
* Build **nudging** so consultants get reminders when their profiles are stale.
* Longer term, use structured profile data + skills matrix + engagement history to build an **Experience Graph** and eventually **match the right Pivot to the right gig**.

### Major components we’ve identified

1. **Profiles pipeline**

   * Markdown + YAML as source of truth.
   * CI pipeline validates, snapshots JSON, pre-renders base Web/PDF/Word outputs.

2. **Sales Composer**

   * Internal app for creating engagements and shares.
   * Configure defaults (expiry, watermark, formats) and per-consultant overrides (sections, project filters).
   * Attach supporting documents (SoW, case studies).

3. **Client Viewer**

   * Public, branded web view for recipients.
   * Recipient-bound links (JWT tokens) with expiry/revocation.
   * Web view with allowed downloads, security headers (`noindex`, anti-framing, CSP).

4. **Exports & Watermarking**

   * PDFs/Word generated once from Markdown → base artefacts.
   * On download, apply watermark + fingerprint (recipient, share, timestamp).

5. **Analytics & Signals**

   * First-party event collection (`/collect`) for opens, meaningful views, section attention, scroll depth, downloads, attachment opens.
   * Aggregate metrics: opens, attention minutes, top sections, conversion to downloads.
   * Live counters for Sales dashboard.

6. **Nudging & Freshness**

   * Signals to remind consultants when their profile hasn’t been updated (60/90/120 day thresholds).
   * Slack DM/email reminders, prefilled “Update PR” links.

7. **Future extensions**

   * Integrate with existing skills matrix.
   * Build an Experience Graph (projects × skills × durations × outcomes).
   * Fit Score for upcoming gigs.
   * Multi-template branding for different customers or verticals.

### What I’d like from you

* Help me refine this overview: Are we missing any major pieces?
* Highlight potential challenges we should prepare for (but don’t dive into implementation yet).
* Suggest how we might frame the **value story** for different stakeholders (consultants, sales, customers, leadership).
