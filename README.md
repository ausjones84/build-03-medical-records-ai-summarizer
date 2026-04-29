# Build #3: Medical Records AI Summarizer

**Stack:** NCA Toolkit + GPT-4o + n8n
**Problem Solved:** Attorneys spend hours reading 200+ page medical records
**Pricing:** $2,000 Setup + $697/month

---

## Overview

This build deploys a fully automated medical records summarization pipeline. A client or paralegal uploads a PDF to a secure intake portal. NCA Toolkit extracts the raw text, sends it to GPT-4o, and returns a structured legal summary to the attorney dashboard in under 2 minutes.

**Key metric:** A 200-page medical record that takes a paralegal 3-4 hours to review is summarized in under 2 minutes with consistent, structured output every time.

---

## Architecture

Client/Paralegal
  -> Secure Upload Portal (GHL Form)
  -> n8n Webhook Trigger
  -> NCA Toolkit PDF Text Extraction
  -> GPT-4o Structured Summary Generation
  -> Structured Output: Injuries, Timeline, Causation, Damages
  -> Attorney Dashboard (GHL Note + Email)

---

## Tech Stack

| Component | Tool | Purpose |
|---|---|---|
| PDF Extraction | NCA Toolkit | Extracts raw text from PDF medical records |
| Workflow | n8n | Orchestrates upload, extraction, AI call, delivery |
| AI Summarization | OpenAI GPT-4o | Generates structured legal summary |
| Intake Portal | GoHighLevel (GHL) | Secure file upload form for clients/paralegals |
| Delivery | GHL + Email | Delivers summary to attorney dashboard |

---

## File Structure

build-03-medical-records-ai-summarizer/
  README.md
  n8n/
    workflow-pdf-intake.json          # Upload trigger + NCA extraction workflow
    workflow-summary-delivery.json    # GPT-4o summary + attorney delivery
  prompts/
    system-prompt.md                  # GPT-4o system prompt for medical summarization
    output-schema.md                  # Structured output format definition
  ghl/
    intake-form-setup.md              # GHL intake form configuration
    dashboard-setup.md                # Attorney dashboard/delivery setup
  docs/
    setup-guide.md                    # Full setup walkthrough
    pricing.md                        # Pricing and deliverables
  .env.example

---

## How It Works

### Step 1: PDF Upload
Client or paralegal uploads the medical records PDF via GHL intake form.
Form submits and triggers n8n webhook with file URL and case details.

### Step 2: Text Extraction (NCA Toolkit)
n8n sends the PDF to NCA Toolkit PDF-to-text endpoint.
NCA Toolkit returns raw extracted text.
n8n chunks the text if it exceeds GPT-4o token limits.

### Step 3: GPT-4o Summarization
n8n sends extracted text to GPT-4o with the legal system prompt.
GPT-4o returns a structured summary with:
- Patient and Case Overview
- Injury Summary (diagnoses, severity, body parts)
- Treatment Timeline (chronological visits, procedures, medications)
- Causation Analysis (incident-injury links)
- Damages Estimate (medical bills, future care, lost wages)
- Key Quotes (verbatim excerpts supporting liability)

### Step 4: Delivery
n8n formats the summary and delivers to attorney via:
- GHL contact note (logged to the case contact)
- Email to attorney with formatted summary
- GHL task created for attorney review

### Step 5: Case Logging
GHL contact record updated with summary status and full text.

---

## Sample Output

=== MEDICAL RECORDS SUMMARY ===
Case: Johnson v. Martinez | Generated: 2026-04-28

PATIENT OVERVIEW
Name: Sarah Johnson | DOB: 1985-03-12
Incident Date: 2025-11-04 | Claim Type: Personal Injury (MVA)
Primary Provider: Dr. Michael Chen, MD

INJURY SUMMARY
1. Cervical disc herniation at C4-C5 (confirmed MRI 2025-11-18)
2. Lumbar strain with radiculopathy — L4-L5
3. Post-traumatic headaches (onset 3 days post-incident)

TREATMENT TIMELINE
2025-11-04: ER visit, pain 8/10, discharged with Naproxen
2025-11-08: Orthopedic consult, referred for MRI
2025-11-18: MRI confirmed C4-C5 herniation
2025-11-25: Physical therapy started (2x/week x 8 weeks)
2026-01-10: Epidural steroid injection, partial relief
2026-02-20: Surgical evaluation recommended

CAUSATION ANALYSIS
Strong causal link: MRI findings consistent with acute traumatic disc
herniation. No pre-existing conditions documented. Treating physician
states injuries "directly caused by the MVA of 11/04/2025."

DAMAGES ESTIMATE
Medical Bills to Date: $47,832
Projected Future Treatment: $85,000-$120,000
Lost Wages: 6 weeks ($12,400 estimated)
Total Estimated Damages: $145,232-$180,232
=== END SUMMARY ===

---

## Environment Variables

OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
OPENAI_MODEL=gpt-4o
NCA_TOOLKIT_URL=https://your-nca-toolkit.com
NCA_TOOLKIT_API_KEY=your_nca_api_key
GHL_API_KEY=your_ghl_api_key
GHL_LOCATION_ID=your_location_id
GHL_ATTORNEY_EMAIL=attorney@yourfirm.com
N8N_PDF_INTAKE_WEBHOOK=https://your-n8n.com/webhook/pdf-intake

---

## Pricing

| Item | Cost |
|---|---|
| Setup Fee | $2,000 (one-time) |
| Monthly Retainer | $697/month |

Setup includes NCA Toolkit integration, n8n workflow build, GPT-4o prompt
engineering, GHL intake + delivery setup, 5 test records, and documentation.

Monthly retainer includes quality monitoring, prompt refinements, and
up to 2 hours/month of changes.

---

## ROI

Paralegal at $35/hr x 3 hrs/record = $105/record
At 10 records/month = $1,050/month in labor
This build automates it for $697/month — saving $353+/month with faster,
more consistent output.

---

## Repos Referenced

- no-code-architects-toolkit: PDF text extraction
- n8n: Workflow automation

---

MIT — Built by ausjones84
