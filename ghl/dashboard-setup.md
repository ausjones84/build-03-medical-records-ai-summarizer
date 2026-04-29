# GHL Attorney Dashboard Setup — Medical Records AI Summarizer

This document explains how to configure the attorney-facing side of the system in GoHighLevel: where summaries appear, how to create review tasks, and how to set up email delivery.

---

## How Summaries Are Delivered to the Attorney

When a medical records summary is generated, the n8n delivery workflow does the following in GHL:

1. Adds a Contact Note with the full summary text
2. Creates a Task assigned to the attorney for review
3. Sends an email to the attorney with the summary formatted as HTML
4. Updates custom contact fields (summary_status, summary_generated_at)

---

## Setting Up the Attorney Email

### Option A: Send via GHL Email System
1. Go to Settings > Email Services
2. Configure your SMTP or use GHL's built-in email
3. Add the attorney's email to GHL_ATTORNEY_EMAIL in your .env file
4. The n8n workflow will use this address for all summary deliveries

### Option B: Send via External SMTP (Recommended)
1. In n8n, configure the "Send Email to Attorney" node with your SMTP credentials
2. Use an authenticated business email (e.g., cases@yourfirm.com)
3. This ensures better deliverability and professional formatting

---

## Setting Up the Review Dashboard (GHL Smart List)

Create a Smart List so attorneys can see all pending summaries at a glance:

1. Go to **Contacts > Smart Lists > + New Smart List**
2. Name it: "Medical Records — Pending Review"
3. Add filters:
   - Custom Field: summary_status = completed
   - Tag: does not include "summary-reviewed"
   - Date: Created in last 30 days
4. Save and pin to the top of the contacts view

---

## Setting Up Pipeline for Medical Records Cases

Create or use an existing pipeline for medical record cases:

**Recommended Pipeline Stages:**
1. Records Uploaded — PDF received, processing started
2. Summary Ready — AI summary generated, awaiting attorney review
3. Attorney Reviewing — Attorney opened and is reviewing the summary
4. Summary Complete — Attorney has reviewed and actioned the case
5. Follow-Up Needed — Attorney flagged for additional records or IME

### GHL Automation: Move to "Summary Ready" Stage
Trigger: Webhook from n8n (fires when summary is complete)
Action: Move contact to "Summary Ready" stage
Action: Add tag: summary-ready
Action: Create task: Review Medical Summary — [Case Name]

---

## Contact Note Format

The n8n workflow logs summaries to the contact record in this format:

[MEDICAL RECORDS SUMMARY — {timestamp}]
Case: {case_name}
Client: {client_name}

{full summary text}

---

To view contact notes:
1. Open the contact record
2. Click the "Notes" tab
3. Look for the note starting with [MEDICAL RECORDS SUMMARY]

---

## Setting Up a Summary Review Task Template

In GHL, create a Task Template for attorney review:

1. Go to Settings > Task Templates
2. Create new template: "Medical Records Review"
3. Template fields:
   - Title: Review Medical Summary: {{contact.custom.case_name}}
   - Due Date: 24 hours from creation
   - Assigned To: Lead Attorney
   - Priority: High
   - Body: AI-generated medical records summary is ready. Review the contact notes and update the pipeline stage when complete.

---

## Optional: Attorney Dashboard Snapshot (GHL Snapshot)

If multiple sub-accounts will use this build, create a GHL Snapshot including:
- Medical Records intake form
- Pipeline with all stages
- Smart Lists
- Task templates
- Custom fields

Export the snapshot via Agency > Snapshots > Create Snapshot.

---

*Part of Build #3 — Medical Records AI Summarizer*
*Built by ausjones84*
