---
name: pdf-translate-reconstruct
description: >-
  Extracts text and images from a PDF manual, assists in translating the text to Traditional Chinese, and reconstructs the document back to formatted Word (.docx) and PDF (.pdf) files.
---

# PDF Translate & Reconstruct

## Overview
This skill extracts text blocks and images from an English PDF reference manual, sorts the elements to follow the original reading flow, enables page-by-page translation to Traditional Chinese (retaining brand/technical terms in English), and reconstructs the output into a formatted `.docx` file and converts it to `.pdf` via Microsoft Word.

## Dependencies
- `PyMuPDF` (for PDF text/image extraction)
- `python-docx` (for Word document reconstruction)
- `pywin32` (for Microsoft Word COM automation and PDF export)

## Quick Start
To translate a PDF named `input.pdf` in the current working directory:

1. **Extract text and images**:
   ```bash
   uv run --with PyMuPDF C:\Users\jeffho\.gemini\config\skills\pdf-translate-reconstruct\scripts\pdf_translator.py extract --pdf input.pdf --output extracted_data.json --img-dir extracted_images
   ```

2. **Translate the extracted JSON**:
   Read `extracted_data.json` and translate the `"content"` fields from English to Traditional Chinese, keeping brand names and formatting, then save it as `translated_data.json`.

3. **Rebuild the document**:
   ```bash
   uv run --with python-docx C:\Users\jeffho\.gemini\config\skills\pdf-translate-reconstruct\scripts\pdf_translator.py build --json translated_data.json --img-dir extracted_images --output output_ZH.docx
   ```

4. **Convert Word to PDF**:
   ```bash
   uv run --with pywin32 C:\Users\jeffho\.gemini\config\skills\pdf-translate-reconstruct\scripts\pdf_translator.py convert --docx output_ZH.docx --output output_ZH.pdf
   ```

## Utility Scripts

### `pdf_translator.py` Commands

- **`extract`**:
  `python pdf_translator.py extract --pdf <input.pdf> --output <output.json> --img-dir <dir>`
  - `--pdf`: Path to the input PDF file.
  - `--output`: Output JSON filepath.
  - `--img-dir`: Bounding box and extracted image outputs are written here.

- **`build`**:
  `python pdf_translator.py build --json <translated.json> --img-dir <dir> --output <output.docx>`
  - `--json`: Translated JSON file path.
  - `--img-dir`: Directory containing extracted images.
  - `--output`: Output Word `.docx` document.

- **`convert`**:
  `python pdf_translator.py convert --docx <input.docx> --output <output.pdf>`
  - `--docx`: Input Word `.docx` file.
  - `--output`: Output PDF file.

## Common Mistakes
- **UTF-8 BOM in JSON**: When saving translated JSONs, make sure to read using `utf-8-sig` encoding in python to prevent parsing errors due to BOM.
- **Word COM Automation**: The conversion subcommand (`convert`) requires Microsoft Word to be installed on the local system. It will fail on headless Linux boxes or environments without MS Word.
