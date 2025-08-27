We’re exploring a project called **Pivot Profiles** at SixPivot. Please help me design the user experience — flows, interfaces, and surfaces. Don’t go into code implementation; I just want the UX vision and UI concepts.

### Context

* **Today’s state:**

  * Consultant Profiles are Word resumes stored in SharePoint.
  * Sales has to chase consultants to update them.
  * Profiles are emailed to customers, and once sent, we lose all control.
  * Formatting is inconsistent, and there’s no insight into who viewed or downloaded.

### The new idea

Pivot Profiles is a new system with three main roles and apps:

1. **Pivots (consultants):**

   * Maintain their own profile as a Markdown + YAML file in Git.
   * Nudged when their profile is stale (60/90/120 days).
   * Profiles render automatically into Web, PDF, and Word formats.

2. **Sales Staff:**

   * Use a **Sales Composer app** to:

     * Create an Engagement (lead/opportunity).
     * Select consultants to include.
     * Choose which sections of each profile to expose (bio, skills, projects, employment, education).
     * Add supporting attachments (e.g. Statement of Work, case studies).
     * Configure options like expiry, watermarking, allowed formats.
     * Send secure, recipient-specific links.
   * See a **Sales dashboard** with live counters (opens, downloads, time spent, sections viewed).
   * Revoke access if needed.

3. **Customers (recipients):**

   * Receive a secure branded link to a **Client Viewer app**.
   * Clean, professional, SixPivot-branded profile viewer.
   * Allowed downloads (PDF/Word) with watermarking/fingerprints.
   * “This link expires in X days” banner.
   * No clutter, just the scoped consultant profiles + optional attachments.

### Key UX flows to design

* **Pivot profile lifecycle:** Consultant updates → auto-rendered formats.
* **Sales workflow:** Create engagement → add recipients → select consultants → toggle sections → add attachments → preview → send.
* **Customer experience:** Open branded viewer → browse profiles → optional downloads → clear expiry/revocation messaging.
* **Analytics backflow:** Sales can see which profiles were opened, for how long, which sections were most viewed, and what was downloaded.

### UX goals

* **Consistency:** Brand-correct across web, PDF, and Word.
* **Simplicity:** Minimal friction for Pivots (update once), Sales (few clicks to send), and Customers (clean viewer).
* **Transparency:** Customers know the share is confidential; Pivots know when they’re stale.
* **Scalability:** Leave room for future features like skills matching and template variants.

### What I’d like from you

* Map the **key flows** for each role (Pivot, Sales, Customer).
* Propose **UI layouts and navigation** for:

  * Sales Composer (internal)
  * Client Viewer (external)
  * Sales dashboard (activity/analytics)
* Suggest a **visual language** aligned with SixPivot’s professional brand.
* Highlight UX challenges we should watch out for (e.g. balancing detail vs. simplicity).