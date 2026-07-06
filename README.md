# InvoFlow — Agentic Invoice Data Entry Automation

An automated pipeline that eliminates manual invoice data entry — drop an invoice into Google Drive, and structured data flows straight into Google Sheets.

## The Problem

Manual invoice entry is slow, repetitive, and error-prone. Most automation attempts fall apart because they rely on **fixed OCR zones or rigid templates** — the moment a vendor changes their invoice layout, the automation breaks.

## The Solution

InvoFlow uses **AI-driven extraction instead of static templates**, so it generalizes across different invoice formats without hardcoded field mapping.

**Pipeline:**

```
Google Drive Upload → LlamaIndex + Groq Extraction → Field Validation → Google Sheets Write-back
```

1. **Intake** — Invoice (PDF/image) is uploaded to a watched Google Drive folder, which triggers the n8n workflow.
2. **Extraction** — LlamaIndex parses the unstructured document and uses a Groq-hosted LLM to extract structured fields (vendor, line items, amounts, dates) regardless of layout.
3. **Validation** — Extracted fields are checked/normalized before being written downstream.
4. **Write-back** — Structured data is automatically entered into a Google Sheet, ready for use — no manual retyping.

## Tech Stack

- **n8n** — workflow orchestration (trigger, control flow, integrations)
- **Google Drive** — invoice intake / trigger source
- **LlamaIndex** — document parsing and extraction pipeline
- **Groq** — LLM inference backend powering the extraction step
- **Google Sheets** — output destination for structured invoice data

## Why This Isn't "Just OCR"

Traditional invoice automation maps fixed pixel/text regions to fixed spreadsheet cells — it breaks the instant a vendor's invoice layout changes. InvoFlow instead asks an LLM-driven extraction layer to *understand* the document and return structured fields, so it holds up across varying invoice structures, vendors, and layouts.

## What's in This Repo

- `workflow.json` — exported n8n workflow (import directly into your n8n instance)
- `demo.gif` / `demo.mp4` — short demo of the pipeline in action
- Screenshots of the workflow canvas (optional, add if included)

## Running It Yourself

1. Import `workflow.json` into your n8n instance.
2. Connect a Google Drive account and set the watched folder as the trigger.
3. Add your Groq API key in the LLM node's credentials.
4. Connect your Google Sheets destination and target sheet.
5. Drop an invoice into the watched Drive folder to trigger the workflow.

## Status

Built as a working demo/proof of concept. Currently tested across multiple invoice formats; not yet benchmarked on a large dataset.

## Future Improvements

- Add exception handling for missing/ambiguous fields (flag for manual review instead of silent failure)
- Support batch invoice uploads
- Add confidence scoring per extracted field
