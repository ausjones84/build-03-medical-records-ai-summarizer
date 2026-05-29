# HIPAA Considerations — Medical Records AI Summarizer
## Build #3 | Compliance Notes

> DISCLAIMER: This document is for informational purposes only and does not constitute legal advice.
> Consult a qualified healthcare attorney or compliance officer before deploying in production.

---

## Overview

This build processes Protected Health Information (PHI) as defined under HIPAA. The following notes
outline key compliance considerations for law firms and their vendors using this system.

---

## Is This Build HIPAA Compliant?

The build itself is a workflow — compliance depends on HOW it is deployed and WHO the vendors are.

**Key compliance factors:**
- OpenAI: As of 2024, OpenAI offers a Business Associate Agreement (BAA) for qualifying enterprise customers. Without a signed BAA, sending PHI to OpenAI's API violates HIPAA.
- n8n: Self-hosted n8n keeps data within your own infrastructure. n8n Cloud may require a BAA.
- NCA Toolkit: Self-hosted versions keep data in your environment. Hosted versions require a BAA with the provider.
- GoHighLevel: GHL offers HIPAA-compliant hosting plans with BAAs for qualifying accounts.

---

## Before Going Live — Compliance Checklist

- [ ] Signed BAA with OpenAI (enterprise plan required)
- [ ] Signed BAA with n8n (if using cloud version)
- [ ] Signed BAA with NCA Toolkit provider (if using hosted version)
- [ ] Signed BAA with GoHighLevel (HIPAA plan required)
- [ ] Law firm has a signed BAA with your agency as a Business Associate
- [ ] HIPAA consent language reviewed by firm's attorney
- [ ] Data retention policy documented and communicated to client
- [ ] Access controls in place (who can view the GHL contact records)
- [ ] Breach notification procedure documented

---

## Data Flow and PHI Exposure Points

Understanding where PHI travels in this build:

1. CLIENT UPLOAD (GHL Form)
   - PHI enters via the GHL intake form
   - Stored in GHL — requires HIPAA-compliant GHL plan

2. WEBHOOK TO n8n
   - File URL and case metadata transmitted via webhook
   - n8n must be on HIPAA-compliant hosting or self-hosted

3. NCA TOOLKIT PDF EXTRACTION
   - Full PDF content (PHI) sent to NCA Toolkit
   - NCA Toolkit must be self-hosted OR have a signed BAA

4. OPENAI GPT-4o API CALL
   - Extracted text (PHI) sent to OpenAI API
   - REQUIRES signed BAA with OpenAI (Enterprise plan)
   - Alternative: Use Azure OpenAI Service (Microsoft provides BAA through Azure)

5. SUMMARY DELIVERY (Email + GHL)
   - Summary stored in GHL (requires HIPAA plan)
   - Email delivery — use encrypted email or confirm attorney email is HIPAA-compliant

---

## Recommended Compliant Configuration

**Option A — Fully Self-Hosted (Most Secure)**
- Self-host n8n on your own server or HIPAA-compliant VPS
- Self-host NCA Toolkit
- Use Azure OpenAI Service (BAA through Microsoft Azure)
- Use GHL HIPAA plan

**Option B — Cloud with BAAs**
- n8n Cloud with signed BAA
- Hosted NCA Toolkit with signed BAA
- OpenAI Enterprise with signed BAA
- GHL HIPAA plan with signed BAA

---

## HIPAA Consent Language (Intake Form)

The intake form includes the following consent checkbox. Review with the firm's attorney before deploying:

"I authorize [FIRM NAME] and its designated service providers to receive, process, and store
the uploaded medical records for the purpose of legal case evaluation. I understand that these
records contain protected health information (PHI) and that [FIRM NAME] will handle this
information in accordance with applicable federal and state privacy laws, including HIPAA.
My records will not be shared with any party other than the attorneys and staff of [FIRM NAME]
and its designated AI processing vendor."

---

## Data Retention

Recommend establishing a data retention policy:
- How long are raw PDFs stored in GHL?
- How long are summaries retained in contact notes?
- What is the deletion procedure when a case is closed?

Document this policy and communicate it to the law firm client.

---

## For Demo Purposes

When recording demos and testing:
- Use SYNTHETIC (fake) patient data only — never real patient records
- The sample data in demo/sample-summary-output.md uses fictional patient information
- Never upload real PHI to a non-HIPAA-compliant test environment

---

*Build #3 — Medical Records AI Summarizer*
*HIPAA Considerations v1.0 — Built by ausjones84*
*Not legal advice — consult a qualified compliance attorney*
