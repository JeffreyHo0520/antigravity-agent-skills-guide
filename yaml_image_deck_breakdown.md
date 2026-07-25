# Case Study: `yaml-image-deck` Skill Breakdown

This document serves as an architectural template for other Agents to study how a specific skill is structured and operated in this workspace.

---

## 1. Skill Folder Structure

The `yaml-image-deck` folder contains:
*   `SKILL.md`: Main execution instructions and constraints.
*   `assets/`: Templates (e.g., `spec-template.yaml`).
*   `references/`: Detailed sub-schemas, layout parameters, prompt templates, and batch parameters.
*   `scripts/`: Python scripts to validate YAML schema and verify output image dimensions.

---

## 2. Configuration Axes

The skill defines four main configuration parameters in the YAML:
*   `output_mode`:
    *   `baked`: Chinese/English text is generated directly *inside* the image. Best for rapid prototyping.
    *   `plate`: Creates clean, text-free background images with empty safe-zones. PPTX overlays are used to add editable text boxes on top of the images.
*   `planning_mode`: `quick` or `yaml_spec` (defaults to `yaml_spec`).
*   `generation_strategy`: `sequential` or `subagents`.
*   `style_lock`: `none` or `golden_sample` (defaults to `golden_sample`).

---

## 3. Style-Locking Mechanism (Golden Sample)

To prevent visual drift when generating multi-page presentations:
1.  Generate **Page 2** (or any typical content page) first.
2.  Inspect its look and feel. Once approved, save its path as `design_system.style_reference`.
3.  Inject this sample path into the prompt compilation pipeline for all other pages to lock in the background tint, texture, lighting, and general illustrations.

---

## 4. Typography Policy

When generating slides:
*   For **Baked slides**, the system injects a strict prompt constraint demanding **bold rounded Traditional Chinese type** (`粗圓、飽滿、低稜角繁體字`) and explicitly forbidding angular calligraphic, stenciled, or condensed technical fonts.
*   For **Plate slides**, the packaging system reads installed fonts from the local system in priority order:
    1.  `jf open 粉圓 2.1`
    2.  `GenSenRounded TW` (源泉圓體)
    3.  `源柔ゴシック` / `GenJyuuGothic` (源柔黑體)

---

## 5. Automated Quality Scripts

Agents must execute the following scripts locally during the compilation workflow:

### A. Spec Validation
```powershell
python .\scripts\validate_spec.py --spec .\spec.yaml
```
*Checks if the YAML schema parameters are complete, page numbers are sequential, layout IDs are supported, and typography is specified.*

### B. Image Ratio Verification
```powershell
python .\scripts\verify_images.py --spec .\spec.yaml --images-dir .\slides\images
```
*Ensures all output images specified in the slides list exist locally and possess a strict 16:9 aspect ratio.*
