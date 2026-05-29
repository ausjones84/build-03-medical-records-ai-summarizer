# Changelog — Medical Records AI Summarizer
## Build #3

All notable changes to this build are documented here.

---

## [v1.1.0] — 2026-05-29 — Demo Ready Release

### Added
- docs/demo-script.md — Step-by-step screen recording script for client demos (Scenes 1-6)
- docs/hipaa-considerations.md — HIPAA compliance checklist, BAA requirements, and deployment guidance
- demo/sample-summary-output.md — Pre-generated sample output for Johnson v. Martinez (backup demo asset)
- n8n/workflow-error-handler.json — Error handling workflow with 3-attempt retry logic, attorney email alerts, and GHL error logging
  - Enhancement: Borrowed retry pattern from build-01-ai-voice-intake-agent error handling design
  - Automatically retries failed PDF extractions up to 3 times before escalating
  - Sends formatted HTML error email to attorney when max retries reached
  - Logs error details to GHL contact notes for case tracking

### Enhanced
- README.md — Added demo instructions cross-reference and enhancements section
- CHANGELOG.md — This file (version tracking for demo readiness)

### Fixed
- Workflow connection: error webhook path added to complement pdf-intake and summary-delivery flows
- .env.example: Added SMTP variables and optional S3 storage variables for completeness

---

## [v1.0.0] — 2026-04-28 — Initial Release

### Added
- n8n/workflow-pdf-intake.json — PDF upload trigger, NCA Toolkit extraction, GPT-4o summarization, GHL delivery
- n8n/workflow-summary-delivery.json — Attorney email delivery, GHL task creation, contact field updates
- prompts/system-prompt.md — Legal medical records analyst system prompt for GPT-4o
- prompts/output-schema.md — Structured JSON schema for parsed summaries
- ghl/intake-form-setup.md — GHL form configuration with HIPAA consent
- ghl/dashboard-setup.md — Attorney dashboard, Smart List, pipeline stages
- docs/setup-guide.md — Full setup walkthrough with troubleshooting
- docs/pricing.md — Pricing breakdown and ROI analysis
- .env.example — Environment variables template

---

## Repos Referenced for Enhancements

### build-01-ai-voice-intake-agent (ausjones84)
- **Used for:** Error handling pattern and retry logic design
- **What it does:** 24/7 AI voice intake agent for law firms using Retell AI + GHL + n8n. Handles inbound calls, qualifies leads, scores them, and routes hot leads to attorneys via SMS. The error handling and retry logic from its n8n workflow was adapted for Build #3's error handler.
- **Enhancement applied:** The 3-attempt retry pattern with exponential wait time and attorney email escalation was modeled after the voice intake agent's call failure handling.

### build-04-client-status-update-automation (ausjones84)
- **Used for:** GHL pipeline stage naming conventions and SMS/email notification structure
- **What it does:** Automatically sends personalized case stage updates via SMS + email when a GHL pipeline stage changes. Fires within 60 seconds of a stage change and includes a 7-day no-movement check-in. Reduces inbound status calls by 40-60%.
- **Enhancement applied:** The pipeline stage names (Records Uploaded → Summary Ready → Attorney Reviewing → Summary Complete) align with Build #4's naming conventions so both builds work seamlessly in the same GHL account.

### no-code-architects-toolkit (stephengpope/no-code-architects-toolkit)
- **Used for:** PDF text extraction via REST API
- **What it does:** An open-source toolkit providing PDF-to-text, media conversion, and file processing endpoints. Deployed as a self-hosted API service. Build #3 calls its /api/v1/toolkit/pdf-to-text endpoint to extract raw text from uploaded medical records PDFs before sending to GPT-4o.

---

*Build #3 — Medical Records AI Summarizer | ausjones84*
