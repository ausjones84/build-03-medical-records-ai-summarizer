# GHL Intake Form Setup — Medical Records AI Summarizer

Setup guide for the GoHighLevel intake form where clients and paralegals upload medical records PDFs.

---

## Overview

The intake form is the entry point for the summarization pipeline. When a PDF is submitted:
1. GHL stores the uploaded file and contact information
2. GHL fires a webhook to n8n with the file URL and contact details
3. n8n triggers the full summarization workflow

---

## Step 1: Create the Intake Form in GHL

1. Go to **Sites > Forms > Builder**
2. Click **+ New Form**
3. Name it: "Medical Records Upload"
4. Set the form style to Inline or Popup depending on your site

---

## Step 2: Add Form Fields

Add the following fields in order:

| Field | Type | Required | Notes |
|---|---|---|---|
| First Name | Text | Yes | Auto-maps to contact |
| Last Name | Text | Yes | Auto-maps to contact |
| Email | Email | Yes | Auto-maps to contact |
| Phone | Phone | Yes | Auto-maps to contact |
| Case Name / Reference | Text | Yes | Custom field |
| Claim Type | Dropdown | Yes | Options: Personal Injury, Workers Comp, Medical Malpractice, Other |
| Medical Records PDF | File Upload | Yes | Allow: PDF only, Max: 50MB |
| Additional Notes | Textarea | No | Optional notes for the attorney |
| HIPAA Consent | Checkbox | Yes | Required before submission |

### HIPAA Consent Field Text
"I authorize [FIRM NAME] and its AI processing systems to review and summarize the uploaded medical records for legal case evaluation purposes. These records will be handled in accordance with applicable privacy laws."

---

## Step 3: Configure File Upload Settings

1. Click the File Upload field
2. Set accepted file types: .pdf
3. Set max file size: 50MB
4. Enable "Store in Media Library"
5. The file URL will be available as a merge field: {{custom.medical_records_file}}

---

## Step 4: Set Up the Form Webhook

1. In the form settings, go to **Integrations > Webhooks**
2. Click **+ Add Webhook**
3. Set the URL to your n8n webhook: {{N8N_PDF_INTAKE_WEBHOOK}}
4. Set trigger: On Form Submit
5. Select fields to include in payload:
   - contact_id
   - first_name
   - last_name
   - email
   - phone
   - custom.case_name
   - custom.claim_type
   - custom.medical_records_file (this is the PDF URL)
   - custom.additional_notes

---

## Step 5: Create the Custom Fields in GHL

Go to **Settings > Custom Fields > Contacts** and create:

| Field Label | Key | Type |
|---|---|---|
| Case Name | case_name | Text |
| Claim Type | claim_type | Dropdown |
| Medical Records File | medical_records_file | File |
| Summary Status | summary_status | Dropdown |
| Summary Generated At | summary_generated_at | Date/Time |
| Summary Text | summary_text | Textarea |
| Summary Word Count | summary_word_count | Number |

### Dropdown Values for claim_type
- personal_injury
- workers_comp
- medical_malpractice
- other

### Dropdown Values for summary_status
- pending_upload
- processing
- completed
- error

---

## Step 6: Embed the Form

1. Copy the form embed code from GHL
2. Embed on your client portal page or send as a direct link
3. Set the page to require login if using a client portal

---

## Step 7: Test the Form

1. Fill out the form with a test PDF (use a small, non-sensitive test document)
2. Submit and verify:
   - Contact is created/updated in GHL
   - n8n webhook fires within 5 seconds
   - File URL is accessible from the webhook payload
   - n8n workflow completes and summary appears in contact notes

---

*Part of Build #3 — Medical Records AI Summarizer*
*Built by ausjones84*
