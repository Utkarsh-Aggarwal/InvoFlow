# InvoFlow
# Invoice Data Entry Automation (Agentic AI Workflow)

An automated pipeline that eliminates manual invoice data entry — upload an invoice in any layout, and structured data flows straight into an Excel sheet.

![Demo](./demo.gif)
<!-- Replace with your actual demo file, e.g. demo.mp4 or demo.gif -->

## The Problem

Manual invoice entry is slow, repetitive, and error-prone. Most automation attempts fall apart because they rely on **fixed OCR zones or rigid templates** — the moment a vendor changes their invoice layout, the automation breaks.

## The Solution

This workflow uses **AI-driven extraction instead of static templates**, so it generalizes across different invoice formats without hardcoded field mapping.

**Pipeline:**

```
Invoice Upload → LlamaIndex Extraction → Field Validation → Excel Write-back
```

1. **Intake** — Invoice (PDF/image) is uploaded via a form/folder trigger in n8n.
2. **Extraction** — LlamaIndex parses the unstructured document and extracts structured fields (vendor, line items, amounts, dates) regardless of layout.
3. **Validation** — Extracted fields are checked/normalized before being written downstream.
4. **Write-back** — Structured data is automatically entered into an Excel sheet, ready for use — no manual retyping.

## Tech Stack

- **n8n** — workflow orchestration (trigger, control flow, integrations)
- **LlamaIndex** — AI-based document parsing and structured data extraction
- **Excel** — output destination for structured invoice data

## Why This Isn't "Just OCR"

Traditional invoice automation maps fixed pixel/text regions to fixed spreadsheet cells — it breaks the instant a vendor's invoice layout changes. This pipeline instead asks an AI extraction layer to *understand* the document and return structured fields, so it holds up across varying invoice structures, vendors, and layouts.

## What's in This Repo

- `workflow.json` — exported n8n workflow (import directly into your n8n instance)
- `demo.gif` / `demo.mp4` — short demo of the pipeline in action
- Screenshots of the workflow canvas (optional, add if included)

## Running It Yourself

1. Import `workflow.json` into your n8n instance.
2. Set up a LlamaIndex/LlamaParse API key in the relevant node's credentials.
3. Connect your Excel destination (Google Sheets/Excel node credentials).
4. Trigger the workflow by uploading an invoice through the configured intake node.

## Status

Built as a working demo/proof of concept. Currently tested across multiple invoice formats; not yet benchmarked on a large dataset.

## Future Improvements

- Add exception handling for missing/ambiguous fields (flag for manual review instead of silent failure)
- Support batch invoice uploads
- Add confidence scoring per extracted field
