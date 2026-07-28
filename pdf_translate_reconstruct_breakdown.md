# PDF Translate & Reconstruct (`pdf-translate-reconstruct`) Agent Guide

This document is an **Agent-to-Agent Operational Standard (SOP)** detailing how to extract text and images from English PDF reference manuals, preserve reading layout flow, perform translation into Traditional Chinese (`zh-TW`), and reconstruct the document into formatted Word (`.docx`) and PDF (`.pdf`) files.

---

## 1. Purpose & Capabilities

When translating complex PDF engineering manuals, brochures, or specification sheets, basic OCR or copy-paste loses image positions, table layouts, and reading sequence.

The `pdf-translate-reconstruct` skill automates:
1. **Extraction**: Extracting structured text blocks and images with PyMuPDF (`fitz`), tracking bounding boxes (`bbox`) and reading order.
2. **Translation Guidance**: Enabling page-by-page translation to Traditional Chinese while retaining technical and brand terms in English.
3. **Document Reconstruction**: Building formatted `.docx` files using `python-docx` with embedded images.
4. **Automated PDF Export**: Converting `.docx` to `.pdf` via Microsoft Word COM automation (`pywin32`).

---

## 2. Dependencies & Environment Setup

Execute commands via `uv` with required dependencies:

```bash
# 1. Extract text and images from PDF
uv run --with PyMuPDF C:\Users\jeffho\.gemini\config\skills\pdf-translate-reconstruct\scripts\pdf_translator.py extract --pdf input.pdf --output extracted_data.json --img-dir extracted_images

# 2. Build translated Word (.docx) document
uv run --with python-docx C:\Users\jeffho\.gemini\config\skills\pdf-translate-reconstruct\scripts\pdf_translator.py build --json translated_data.json --img-dir extracted_images --output output_ZH.docx

# 3. Convert Word to PDF via MS Word COM
uv run --with pywin32 C:\Users\jeffho\.gemini\config\skills\pdf-translate-reconstruct\scripts\pdf_translator.py convert --docx output_ZH.docx --output output_ZH.pdf
```

---

## 3. Workflow Protocol

1. **Extraction**: Run `extract` command to parse `input.pdf`. Output JSON maps page indices, text blocks, bounding boxes, and image references.
2. **Translation**: Read `extracted_data.json`, translate `"content"` values from English to Traditional Chinese (`zh-TW`), keep brand names/part numbers in English, and save as `translated_data.json` with `utf-8-sig` encoding.
3. **Reconstruction**: Run `build` command to create `output_ZH.docx`.
4. **PDF Generation**: Run `convert` command to render `output_ZH.pdf`.

---

## 4. Troubleshooting & Notes

- **Encoding**: Always load/save JSON with `utf-8-sig` in Python to prevent UTF-8 BOM parsing issues.
- **COM Automation**: The `convert` step requires Microsoft Word installed locally on Windows.
