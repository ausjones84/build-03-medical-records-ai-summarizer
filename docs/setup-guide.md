# Setup Guide — Medical Records AI Summarizer

Complete step-by-step setup for Build #3.

**Time to complete:** 2-3 hours
**Prerequisites:** GHL account, n8n instance, OpenAI API key, NCA Toolkit access

---

## Step 1: NCA Toolkit Setup

### Option A: Use Hosted NCA Toolkit
1. Get access to a hosted NCA Toolkit instance
2. Get the base URL (e.g., https://your-nca-toolkit.com)
3. Get your API key from the NCA Toolkit dashboard
4. Test the PDF endpoint: POST /api/v1/toolkit/pdf-to-text

### Option B: Self-Host NCA Toolkit
1. Fork https://github.com/stephengpope/no-code-architects-toolkit
2. Deploy to Railway, Render, or your own server
3. Set environment variables per the NCA Toolkit README
4. Note your deployment URL and generate an API key

### Test NCA Toolkit
curl -X POST https://your-nca-toolkit.com/api/v1/toolkit/pdf-to-text \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{"file_url": "https://example.com/test.pdf"}'

Expected response: {"text": "extracted text content..."}

---

## Step 2: n8n Setup

### 2a. Import Workflows
1. Open your n8n instance
2. Go to Workflows > Import from File
3. Import n8n/workflow-pdf-intake.json
4. Import n8n/workflow-summary-delivery.json
5. Both workflows should appear in your workflow list

### 2b. Configure Credentials
In n8n Settings > Credentials, create:

**NCA Toolkit API (HTTP Header Auth)**
- Header Name: Authorization
- Header Value: Bearer YOUR_NCA_API_KEY

**OpenAI API**
- API Key: your OpenAI API key

**GHL API (HTTP Header Auth)**
- Header Name: Authorization
- Header Value: Bearer YOUR_GHL_API_KEY

**Email (SMTP)**
- Configure with your business email SMTP settings

### 2c. Set Environment Variables in n8n
In n8n Settings > Environment Variables, add:
- NCA_TOOLKIT_URL: your NCA Toolkit base URL
- OPENAI_MODEL: gpt-4o
- GHL_API_KEY: your GHL API key
- GHL_ATTORNEY_EMAIL: attorney's email address
- SUMMARIZER_SYSTEM_PROMPT: paste the full prompt from prompts/system-prompt.md

### 2d. Activate Workflows
1. Open workflow-pdf-intake — toggle Active to ON
2. Copy the webhook URL from the Webhook trigger node
3. Open workflow-summary-delivery — toggle Active to ON
4. Note both webhook URLs

---

## Step 3: GHL Setup

### 3a. Create Custom Fields
Follow ghl/intake-form-setup.md Step 5 to create all custom fields.

### 3b. Create Intake Form
Follow ghl/intake-form-setup.md Steps 1-6 to build and configure the form.

### 3c. Connect Webhook
In the form settings, set the webhook URL to your n8n PDF intake webhook URL.

### 3d. Set Up Attorney Dashboard
Follow ghl/dashboard-setup.md to configure email delivery, Smart List, and pipeline.

---

## Step 4: OpenAI Configuration

1. Ensure your OpenAI API key has access to GPT-4o
2. Copy the system prompt from prompts/system-prompt.md
3. Paste it into the SUMMARIZER_SYSTEM_PROMPT environment variable in n8n
4. For very long records (500+ pages), consider using chunking with a summary-of-summaries approach

---

## Step 5: Testing

### Test 1: Full Pipeline with a Sample PDF
1. Find a non-sensitive 5-10 page test document
2. Go to your GHL intake form URL
3. Fill in: First Name, Last Name, Email, Case Name
4. Upload the test PDF
5. Submit the form
6. Within 2 minutes, verify:
   - n8n workflow executed successfully
   - Summary appears in GHL contact notes
   - Attorney received an email with the summary
   - Review task was created in GHL

### Test 2: Large PDF Handling (100+ pages)
1. Find a large test PDF (can be any text-heavy document)
2. Submit through the intake form
3. Verify that chunking works and all chunks are summarized
4. Verify the final summary is coherent and complete

### Test 3: Error Handling
1. Submit a non-PDF file and verify it fails gracefully
2. Submit with missing required fields and verify GHL form validation catches it
3. Test with an invalid PDF URL and verify the error is logged in n8n

---

## Step 6: Go Live Checklist

- [ ] NCA Toolkit responding to PDF-to-text requests
- [ ] n8n PDF intake workflow active and webhook URL copied to GHL
- [ ] n8n summary delivery workflow active
- [ ] GHL intake form live and accessible
- [ ] GHL form webhook pointing to correct n8n URL
- [ ] All custom GHL fields created
- [ ] Attorney email configured and verified
- [ ] Test PDF processed end-to-end successfully
- [ ] Summary appeared in GHL contact notes
- [ ] Attorney received the email summary
- [ ] Review task created in GHL

---

## Troubleshooting

**PDF not extracting:**
- Verify NCA Toolkit API key and URL
- Check that the PDF URL is publicly accessible (not behind login)
- Check n8n execution logs for HTTP errors

**GPT-4o not responding:**
- Verify OpenAI API key is valid and has credits
- Check that SUMMARIZER_SYSTEM_PROMPT is set in n8n env vars
- For timeout errors: increase timeout on the HTTP Request node to 180s

**Summary not appearing in GHL:**
- Verify GHL API key has write permissions for contacts
- Check that contact_id in the webhook payload is a valid GHL contact ID
- Review n8n execution log for the GHL API call

**Email not received:**
- Check spam folder
- Verify SMTP credentials in n8n
- Test email node independently with a simple test message

---

*Build #3 — Medical Records AI Summarizer*
*Stack: NCA Toolkit + GPT-4o + n8n + GHL*
*Pricing: $2,000 Setup + $697/month*
*Built by ausjones84*
