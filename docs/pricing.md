# Pricing & Deliverables — Medical Records AI Summarizer

## Pricing

| Item | Cost |
|---|---|
| Setup Fee | $2,000 (one-time) |
| Monthly Retainer | $697/month |

---

## Setup Fee — $2,000 (One-Time)

### What's Included

**NCA Toolkit Integration**
- NCA Toolkit deployment or connection setup
- PDF-to-text pipeline configuration and testing
- Handling for standard medical record formats (typed, scanned-OCR)

**n8n Workflow Build**
- workflow-pdf-intake.json: Upload trigger, NCA extraction, GPT-4o summarization
- workflow-summary-delivery.json: Attorney email delivery, GHL task creation, contact field updates
- Error handling and retry logic
- Chunking for large documents (200+ pages)

**OpenAI GPT-4o Integration**
- Legal medical summary prompt engineering
- Output schema configuration
- Token optimization for large documents
- Structured output validation

**GHL Configuration**
- Intake form build (Medical Records Upload form)
- All custom fields created and mapped
- Attorney email delivery setup
- Smart List and pipeline stage configuration
- Review task automation

**Testing**
- 5 complete end-to-end test records processed
- Large document test (100+ page equivalent)
- Error scenario testing (invalid files, missing fields)
- Output quality review with sample legal summaries

**Documentation & Handoff**
- This repository with all files
- Video walkthrough of the system (30 minutes)
- Written handoff document
- 1-hour onboarding call

---

## Monthly Retainer — $697/Month

### What's Included

**Monitoring (Weekly)**
- Review n8n execution logs for errors
- Spot-check 2-3 summary outputs for quality
- Alert client if error rate exceeds 5%

**Prompt Maintenance**
- Update system prompt as GPT-4o models update
- Refine extraction quality based on client feedback
- Add new case type templates as needed

**Usage Reporting (Monthly)**
- Total PDFs processed
- Average processing time
- Error rate
- Summary quality notes
- Recommendations for improvement

**Ongoing Support**
- Up to 2 hours/month of changes included
- Bug fixes included at no extra cost
- Additional hours billed at $150/hour

---

## Additional Services (A La Carte)

| Service | Cost |
|---|---|
| Additional case type template | $250 |
| Custom output format (Word doc, Google Doc) | $350 |
| Batch processing (upload multiple PDFs at once) | $500 |
| GHL snapshot for multi-location deployment | $300 |
| Attorney-facing web portal (custom branded) | $1,500 |
| HIPAA Business Associate Agreement (BAA) setup | $500 |
| Integration with case management software | Quote |

---

## Estimated Monthly Platform Costs (Client Pays Separately)

| Platform | Estimated Cost |
|---|---|
| OpenAI API (GPT-4o) | $30-$150/month (depends on volume) |
| NCA Toolkit | $0-$50/month (self-hosted = free) |
| n8n (Cloud) | $20-$50/month |
| GoHighLevel | $97-$297/month (existing subscription) |
| Total Platform Cost | ~$150-$550/month |

**Note:** At 50 records/month using GPT-4o, OpenAI costs are approximately $50-$80/month.
At 200 records/month, estimate $150-$200/month in API costs.

---

## ROI Analysis

**Without this build:**
- Paralegal time: 3 hours/record at $35/hour = $105/record
- 10 records/month = $1,050/month in labor
- 50 records/month = $5,250/month in labor

**With this build:**
- Processing cost: $697 retainer + ~$100 OpenAI = $797/month
- At 10 records/month: saves $253/month + frees 30 paralegal hours
- At 50 records/month: saves $4,453/month + frees 150 paralegal hours
- Payback on setup fee: less than 2 months at 10 records/month

**Additional value:**
- Summaries produced in 2 minutes vs. 3 hours
- Consistent structured output every time
- No human fatigue or missed details
- Paralegals freed for higher-value work

---

*Build #3 — Medical Records AI Summarizer*
*Built by ausjones84*
