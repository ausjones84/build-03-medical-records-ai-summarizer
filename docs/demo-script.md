# Demo Script — Medical Records AI Summarizer
## Build #3 | Screen Recording Guide
Use this script when recording your demo for clients and users.
Estimated demo time: 8-12 minutes

---

## Pre-Demo Checklist

- [ ] n8n is open — both workflows visible and Active
- [ ] GHL is open — contacts list visible, intake form URL ready
- [ ] A test PDF is ready (use demo/sample-medical-record.txt)
- [ ] Attorney email inbox is open in another tab
- [ ] Screen is clean — close unnecessary tabs
- [ ] Resolution: 1920x1080 recommended

---

## Demo Flow

### SCENE 1 — The Problem (0:00-1:30)
**What to show:** GHL contact record with no summary, blank notes tab

**Script:**
"Right now, when a client uploads medical records, a paralegal has to manually read through 200+ pages — that takes 3 to 4 hours per file. We built this system to do it in under 2 minutes."

---

### SCENE 2 — The Intake Portal (1:30-3:00)
**What to show:** GHL intake form in browser

**Script:**
"The client or paralegal goes to the intake form — a simple, secure upload page. They fill in the case name, claim type, upload the PDF, and check the HIPAA consent box."

**Actions:**
1. Open the GHL form URL
2. Fill in: First Name = Sarah, Last Name = Johnson, Email = demo@test.com
3. Case Name = Johnson v. Martinez
4. Claim Type = Personal Injury
5. Upload the test PDF
6. Check HIPAA consent and click Submit

---

### SCENE 3 — The Workflow Fires (3:00-5:00)
**What to show:** n8n execution log in real time

**Script:**
"As soon as that form is submitted, our n8n workflow fires. Watch the execution log — NCA Toolkit extracts the PDF text, it goes to GPT-4o, and the structured summary is built."

**Actions:**
1. Switch to n8n tab
2. Open the PDF Intake workflow — click Executions
3. Walk through each node: Webhook → Extract Data → NCA Toolkit → Chunk Text → GPT-4o → Combine → GHL Log

---

### SCENE 4 — The Summary Delivered (5:00-7:30)
**What to show:** GHL contact notes + attorney email

**Script:**
"In under 2 minutes, the attorney gets this — a structured, formatted medical summary ready for case review."

**Actions:**
1. Switch to GHL — open the Sarah Johnson contact record
2. Click the Notes tab — show the Medical Records Summary note
3. Scroll through: Patient Overview → Injury Summary → Treatment Timeline → Causation → Damages
4. Switch to email inbox — show the HTML-formatted email
5. Show the GHL review task created for the attorney

---

### SCENE 5 — The Value Statement (7:30-8:30)
**Script:**
"A paralegal charges $35 an hour. A 200-page file takes 3 to 4 hours. That is over $100 per record.
This system does it in 2 minutes, for pennies in API costs, with consistent structured output every time.
At just 10 records a month, it pays for itself within the first month."

---

### SCENE 6 — The Setup (8:30-10:00) — Optional for technical audiences
**Actions:**
1. Show GitHub repo structure
2. Open n8n/workflow-pdf-intake.json — highlight NCA Toolkit and GPT-4o nodes
3. Open prompts/system-prompt.md — show the output structure
4. Open .env.example — show the required variables

---

## Backup Demo (If Live Run Fails)

If the live pipeline does not complete during recording:
1. Open demo/sample-summary-output.md — pre-generated output for Johnson v. Martinez
2. Paste it into GHL manually as a contact note
3. Continue from Scene 4

---

*Build #3 — Medical Records AI Summarizer | Demo Script v1.0 — Built by ausjones84*
