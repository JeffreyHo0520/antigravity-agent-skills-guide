# Process FMEA Generator (`process-fmea-generator`) Agent Guide

This document is an **Agent-to-Agent Operational Standard (SOP)** detailing how to parse manufacturing Standard Operating Procedure (SOP) Word documents (`.docx`) and Product Quality Plan (PQP/Control Plan) Excel workbooks (`.xlsm`), map assembly/inspection/packaging steps against AIAG/VDA failure mode taxonomies, and automatically populate or update Process FMEA (PFMEA) sheets with dynamic Risk Priority Number (RPN) formulas.

---

## 1. Executive Summary & Purpose

Manufacturing and QA engineers frequently update Control Plans and SOPs. Manually transcribing process steps into Process FMEA sheets introduces human error, broken merged-cell formatting, and corrupted Excel VBA macros.

The `process-fmea-generator` skill automates:
1. **Extraction**: Structured parsing of SOP Word documents and PQP Control Plan Excel sheets.
2. **Semantic Matching**: Aligning process steps with potential failure modes, causes, effects, current controls, and SEV/OCC/DET risk ratings.
3. **Cell Injection**: Writing formatted text into merged cell ranges starting at Row 18 in the `Process FMEA` worksheet.
4. **Formula Injection**: Dynamic RPN formula insertion (`S*Z*AG` and post-action `BA*BB*BC`) while preserving VBA macro code (`keep_vba=True`).

---

## 2. Prerequisites & Environment Setup

To run the FMEA engine, the agent must execute Python via `uv` with necessary dependencies:

```bash
uv run --with python-docx --with openpyxl python fmea_engine.py parse-cp --excel "PQP.xlsm" --sheet "Control Plan (Foster)"
```

### Critical Rules for Excel Operations:
* **VBA Preservation**: ALWAYS use `openpyxl.load_workbook(xl_path, keep_vba=True)` when saving `.xlsm` files to prevent destroying macro macros.
* **Merged Cell Targeting**: OpenPyXL requires writing values and applying styles directly to the **top-left cell** of a merged range. Writing to secondary cells inside a merged range will fail silently or corrupt layout.
* **Dynamic Row Height**: Compute row height based on newline characters (`\n`): `ws.row_dimensions[row].height = max(45, max_lines * 22)`.

---

## 3. Failure Mode & Risk Rating Taxonomy (AIAG / VDA Rules)

When analyzing process steps, agents MUST apply the following standard severity (SEV), occurrence (OCC), and detection (DET) rating rules:

| Process Category | Potential Failure Mode Examples | SEV | OCC | DET | Baseline Controls |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **Assembly / Line** | Surface scratch, pinched/reversed cables, missing clips, improper clip seating | 7 - 9 | 3 | 2 | Visual inspection, assembly jig alignment |
| **Screw Tightening** | Wrong sequence, stripped thread, torque out of spec (over/under tightened) | 5 - 6 | 3 | 2 | Calibrated electric screwdriver with auto-shutoff & torque sensor |
| **Grease / Press-fit** | Insufficient/excess grease contaminating optical parts, high resistance torque (> 5 cN-m) | 5 - 7 | 3 | 2 | Automated dispenser, torque meter check |
| **Functional / Electrical** | Standby current > 200 µA, incorrect LED sequence, door hand detection failure | 9 | 3 | 1 | 100% automated ICT / functional test fixture |
| **Packaging & Labeling** | Missing accessories, misprinted/mismatched QR or Logo labels, skewed pallet stacking | 5 - 8 | 2 - 3 | 2 | Barcode scanner verification, visual check sheet |

---

## 4. Excel Cell Mapping & Formula Reference

Data rows are populated sequentially starting from **Row 18** in the `Process FMEA` worksheet:

| Column Range | Merged Cell Target | Target Field | Data Type & Alignment | Formula / Value Example |
| :--- | :--- | :--- | :--- | :--- |
| **A - F** | `Col A (1)` | Process Step / Input | Text, Left-aligned, Wrap | `[10] Lock Top Cover Screws` |
| **G - L** | `Col G (7)` | Potential Failure Mode | Text, Left-aligned, Wrap | `Screw stripped or torque under spec` |
| **M - R** | `Col M (13)` | Potential Failure Effect | Text, Left-aligned, Wrap | `Cover loose, water ingress risk` |
| **S** | `Col S (19)` | Severity (SEV) | Integer, Center-aligned | `6` |
| **T - Y** | `Col T (20)` | Potential Causes | Text, Left-aligned, Wrap | `Bit worn out, operator angle tilted` |
| **Z** | `Col Z (26)` | Occurrence (OCC) | Integer, Center-aligned | `3` |
| **AA - AF** | `Col AA (27)` | Current Controls | Text, Left-aligned, Wrap | `Auto-shutoff screwdriver + 100% torque check` |
| **AG** | `Col AG (33)` | Detection (DET) | Integer, Center-aligned | `2` |
| **AH** | `Col AH (34)` | Initial RPN Formula | Formula, Center-aligned | `=IF(ISBLANK(S{row})," ",S{row}*Z{row}*AG{row})` |
| **BD** | `Col BD (56)` | Post-Action RPN Formula | Formula, Center-aligned | `=IF(ISBLANK(BA{row})," ",BA{row}*BB{row}*BC{row})` |

---

## 5. Python FMEA Engine Reference Implementation

Below is the production-ready script snippet (`fmea_engine.py`) used to inject parsed FMEA data into Excel:

```python
import openpyxl
from openpyxl.styles import Font, Alignment

def populate_fmea(xl_path, fmea_sheet_name, fmea_data, start_row=18):
    """Populate FMEA rows into Excel while preserving VBA and formatting."""
    wb = openpyxl.load_workbook(xl_path, keep_vba=True)
    if fmea_sheet_name not in wb.sheetnames:
        raise ValueError(f"Sheet '{fmea_sheet_name}' not found in {xl_path}")
    ws = wb[fmea_sheet_name]
    
    font_text = Font(name='Arial', size=9, bold=False)
    font_num = Font(name='Arial', size=8, bold=False)
    font_formula = Font(name='Arial', size=5, bold=False)
    
    align_left = Alignment(horizontal='left', vertical='center', wrap_text=True)
    align_center = Alignment(horizontal='center', vertical='center', wrap_text=True)
    
    for i, item in enumerate(fmea_data):
        row = start_row + i
        
        # Write merged cell targets
        mappings = [
            (1, item["process_step"], font_text, align_left),
            (7, item["failure_mode"], font_text, align_left),
            (13, item["failure_effect"], font_text, align_left),
            (19, item["sev"], font_num, align_center),
            (20, item["causes"], font_text, align_left),
            (26, item["occ"], font_num, align_center),
            (27, item["controls"], font_text, align_left),
            (33, item["det"], font_num, align_center),
            (34, f'=IF(ISBLANK(S{row})," ",S{row}*Z{row}*AG{row})', font_formula, align_center),
            (56, f'=IF(ISBLANK(BA{row})," ",BA{row}*BB{row}*BC{row})', font_formula, align_center)
        ]
        
        for col, val, font, align in mappings:
            cell = ws.cell(row=row, column=col)
            cell.value = val
            cell.font = font
            cell.alignment = align

        # Calculate dynamic row height
        lines = max(
            item["process_step"].count('\n') + 1,
            item["failure_mode"].count('\n') + 1,
            item["failure_effect"].count('\n') + 1,
            item["causes"].count('\n') + 1,
            item["controls"].count('\n') + 1
        )
        ws.row_dimensions[row].height = max(45, lines * 22)
        
    wb.save(xl_path)
    wb.close()
    print(f"Successfully populated {len(fmea_data)} FMEA rows into '{fmea_sheet_name}'.")
```

---

## 6. Agent Action Protocol (How Other Agents Construct Knowledge)

When another AI Agent enters this repository to execute PFMEA generation:

1. **Step 1 - Discover Protocol**: Read this document (`process_fmea_generator_breakdown.md`) to understand the schema and cell mapping.
2. **Step 2 - Parse Inputs**: Use `python-docx` to extract text blocks from `.docx` SOP files and `openpyxl` to extract Control Plan process tables.
3. **Step 3 - Synthesize FMEA Matrix**: Construct a list of dictionaries matching the AIAG/VDA failure taxonomy rules.
4. **Step 4 - Execute Script**: Call `fmea_engine.py` with `--excel` and `--sheet` flags to update the workbook.
5. **Step 5 - Validate**: Inspect the resulting `.xlsm` file to ensure RPN formulas evaluate correctly and VBA macros remain intact.
