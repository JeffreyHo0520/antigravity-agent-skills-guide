# Drawing Specification & PQP Comparison (`drawing-spec-pqp-comparison`) Agent Guide

This document is an **Agent-to-Agent Operational Standard (SOP)** detailing how to audit a Product Quality Plan (PQP) Excel workbook against mechanical engineering drawing PDFs (Top-Level Assembly and sub-assemblies).

---

## 1. Executive Summary & Purpose

In product quality assurance and engineering supplier management (e.g. ASSA ABLOY / HHI), verifying that a supplier's Product Quality Plan (PQP) matches engineering drawing specifications is critical.

The `drawing-spec-pqp-comparison` skill automates end-to-end extraction and 12 core compliance audits:

1. **Metadata Alignment**: Verifies Part Number, Description, Drawing Number, and Revision match across all visible sheets.
2. **Multi-Drawing Part Number Audit**: Scans across all provided PDF drawings (or subassemblies) to detect conflicting or inconsistent Part/Drawing Numbers.
3. **Control Plan Torques**: Checks assembly torques in Control Plan steps against drawing flag notes.
4. **MSA & Process Capability**: Audits Gage R&R and Capability sheets for empty data or `#DIV/0!` formula errors.
5. **100% Dimensional Drift Alerts**: Flags measurements exceeding tolerance or marked for investigation.
6. **Sample # Sequence Completeness Audit**: Audits 100% Dimensional Inspection worksheets to verify `Sample#` entries are non-empty, start from 1, and follow a contiguous integer sequence (`1, 2, 3... N`) across all balloon items.
7. **Auto OCR Fallback**: Renders PDF pages at 300 DPI and runs OCR via `pymupdf` and `rapidocr-onnxruntime` if CAD exports contain vector geometry instead of text elements.
8. **Enhanced Fraction & Unit Checking**: Converts fractions (e.g., `8-5/8` -> `8.625`) and respects explicit `INCH`/`MM` unit callouts.
9. **Robust Angle Auditing**: Matches angular dimensions (e.g., `45.0°`) and tolerances (e.g., `ANGLES: +/- 1`).
10. **Limit & Reference Dimensions**: Auto-bypasses standard tolerance checks for `MIN`, `MAX`, and `REF` dimensions.
11. **Fuzzy FFF Sheet Matching**: Resolves sheet title variants (e.g., `' FFF (overall)'`).
12. **Embedded FFF Workbook Detection**: Inspects embedded child Excel workbooks (`xl/embeddings/Microsoft_Excel_Worksheet*.xlsx`) for Form, Fit, Function photo evidence, signatures, and test statuses.

---

## 2. Quick Start Command

Execute the end-to-end compliance check using `uv run`:

```bash
uv run C:/Users/User/.gemini/config/plugins/science/skills/drawing-spec-pqp-comparison/scripts/compare_dwg_pqp.py all \
  --pqp "/path/to/pqp_workbook.xlsm" \
  --dwgs "/path/to/dwg1.pdf,/path/to/dwg2.pdf" \
  --output "/path/to/audit_report.md"
```

---

## 3. CLI Subcommands

### 1. `extract`
Extracts specification metadata, torques, and dimensions from drawing PDFs into JSON format:
```bash
uv run compare_dwg_pqp.py extract --dwgs "/path/to/drawing.pdf" --output "/path/to/spec.json"
```

### 2. `audit`
Audits PQP workbook compliance against pre-extracted specification JSON:
```bash
uv run compare_dwg_pqp.py audit --pqp "/path/to/pqp.xlsm" --output "/path/to/audit_report.md"
```

### 3. `all`
Performs end-to-end PDF extraction and PQP audit, generating a complete Markdown report.

---

## 4. Key Audit Rules Reference

| Audit Section | Condition Checked | Action / Outcome |
| :--- | :--- | :--- |
| **Section 1: Metadata & Part Numbers** | Sheet headers vs Drawing info; Multi-drawing PDF part number conflicts | Flags mismatches in `Part Number`, `Description`, `Drawing Number`, or `Revision` |
| **Section 2: Control Plan Torques** | Assembly torque step text vs Flag notes (e.g., `1.4 ± 0.1 N-m`) | Flags missing or mismatching torque values |
| **Section 3: MSA & Capability** | Unfilled cell values or `#DIV/0!` errors in `Variable R&R` / `Process Capability` | Reports exact cell coordinates and missing data errors |
| **Section 4: 100% Dimensional & Sample#** | `Sample#` continuity (`1..N`), blank `Sample#`, and Disposition != `Acceptable` | Reports missing/gap sample numbers and non-acceptable measurement rows |
| **Section 5: Drawing Cross-Check** | Excel Balloon Nominals/Tolerances vs PDF Drawing Callouts | Compares inch/mm callouts, flag notes, angles, and limit dimensions |
| **Section 6: 3F (FFF) Photo Verification** | Embedded workbooks and physical photo OCR for Model, FCC ID, IC, HVIN | Verifies embedded sub-reports and photo OCR signatures |
