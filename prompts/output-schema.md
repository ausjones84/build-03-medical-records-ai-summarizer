# Output Schema — Medical Records AI Summarizer

Defines the structured output format returned by GPT-4o and parsed by n8n.

---

## JSON Output Schema

When using the JSON mode variant of the prompt, GPT-4o returns this structure:

```json
{
  "case_name": "string",
  "generated_at": "ISO 8601 timestamp",
  "patient": {
    "name": "string",
    "dob": "string",
    "incident_date": "string",
    "claim_type": "personal_injury | workers_comp | medical_malpractice | other",
    "primary_provider": {
      "name": "string",
      "specialty": "string"
    },
    "other_providers": [
      { "name": "string", "specialty": "string" }
    ]
  },
  "injuries": [
    {
      "diagnosis": "string",
      "body_part": "string",
      "severity": "mild | moderate | severe",
      "type": "acute | chronic | acute-on-chronic"
    }
  ],
  "pre_existing_conditions": ["string"],
  "treatment_timeline": [
    {
      "date": "string",
      "provider": "string",
      "visit_type": "string",
      "findings": "string",
      "treatments": ["string"],
      "pain_level": "number | null"
    }
  ],
  "medications": [
    {
      "name": "string",
      "dosage": "string",
      "purpose": "string",
      "prescriber": "string"
    }
  ],
  "diagnostic_tests": [
    {
      "test_type": "string",
      "date": "string",
      "results": "string"
    }
  ],
  "causation": {
    "link_strength": "strong | moderate | weak | insufficient",
    "key_findings": ["string"],
    "pre_existing_impact": "string",
    "supporting_quotes": [
      { "quote": "string", "provider": "string", "date": "string" }
    ]
  },
  "damages": {
    "medical_bills_to_date": "number | null",
    "future_medical_estimate_low": "number | null",
    "future_medical_estimate_high": "number | null",
    "lost_wages_documented": "boolean",
    "lost_wages_amount": "number | null",
    "permanent_impairment_rating": "string | null",
    "total_estimate_low": "number | null",
    "total_estimate_high": "number | null"
  },
  "key_quotes": [
    { "quote": "string", "provider": "string", "date": "string", "relevance": "string" }
  ],
  "flags": [
    {
      "type": "gap_in_treatment | causation_weakness | pre_existing | inconsistency | missing_records | other",
      "description": "string",
      "severity": "high | medium | low"
    }
  ],
  "recommendations": ["string"],
  "word_count": "number",
  "pages_processed": "number | null"
}
```

---

## Field Definitions

### patient.claim_type values
- personal_injury — Auto accidents, slip and fall, premises liability
- workers_comp — Workplace injuries, occupational disease
- medical_malpractice — Provider negligence, surgical errors
- other — Any other claim type

### causation.link_strength values
- strong — Physician explicitly states injuries caused by incident; no pre-existing conditions
- moderate — Medical records support causation but some documentation gaps exist
- weak — Limited documentation; pre-existing conditions complicate causation
- insufficient — Records do not establish causation; recommend IME

### flags.type values
- gap_in_treatment — Break of 30+ days in treatment (may indicate recovery or non-compliance)
- causation_weakness — No physician causation statement found
- pre_existing — Pre-existing conditions documented that may complicate damages
- inconsistency — Conflicting findings between providers or visits
- missing_records — Referenced providers/records not included in the upload
- other — Any other flag worth noting

---

## Text Output Format (Default)

When not using JSON mode, GPT-4o returns the formatted text output as defined in system-prompt.md.
The n8n workflow accepts both formats — text is stored as-is, JSON is parsed for GHL field mapping.

---

*Part of Build #3 — Medical Records AI Summarizer*
*Built by ausjones84*
