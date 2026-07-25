# NotebookLM-Style Conversion Workflows

This document outlines the step-by-step instructions for other Agents to convert raw materials (PDFs, text files, notes) into NotebookLM-style outputs using the environment's global skills.

---

## 1. Visual Slide Deck (NotebookLM Presentations)
Translate dense documents into a highly visual, structured slide deck.

### Instructions
1.  Study the input text to extract:
    *   Target Audience and Core Takeaway.
    *   Slide Count (typically 5 to 10 slides).
2.  Use the `yaml-image-deck` spec format. Initialize a `spec.yaml` using [spec-template.yaml](file:///C:/Users/User/.gemini/config/skills/yaml-image-deck/assets/spec-template.yaml).
3.  Assign each slide an informational relationship and select a corresponding `layout.id` (e.g. `cover_hero` for covers, `comparison_split` for contrast).
4.  Run validation:
    ```powershell
    python .\scripts\validate_spec.py --spec .\spec.yaml
    ```
5.  Generate a **Golden Sample** content slide first and lock its style by writing its path to `design_system.style_reference`.
6.  Generate the rest of the slides sequentially (or in parallel via subagents if requested).
7.  Verify output aspect ratios (must be 16:9):
    ```powershell
    python .\scripts\verify_images.py --spec .\spec.yaml --images-dir .\slides\images
    ```
8.  Package the slides:
    *   **Baked mode**: Render final slide images.
    *   **Plate mode**: Output text-free plates and write editable text boxes in PPTX.

---

## 2. AI Audio Podcast (NotebookLM Audio Overview)
Generate double-speaker audio files summarizing a document.

### Instructions
1.  Read the target document and extract the core thesis and sub-arguments.
2.  Generate a **natural-sounding double-speaker dialogue script** (e.g., Host A and Host B) in Traditional Chinese (`zh-TW`).
    *   Ensure conversational tones, pauses, and rhetorical questions.
3.  Use the [voxcpm2-voice-cloner](file:///C:/Users/User/.gemini/config/skills/voxcpm2-voice-cloner/SKILL.md) skill to manage dialogue records.
4.  Invoke [use-ho-cloned_voice](file:///C:/Users/User/.gemini/config/skills/use-ho-cloned_voice/SKILL.md) to synthesize the speech using the cloned voice model for Ho (何思齊).
5.  Save the final synthesized audio clips locally and report the paths to the user.

---

## 3. Interactive Study Book (NotebookLM Study Guides)
Turn textbooks, exam papers, or notes into an interactive web interface.

### Instructions
1.  Identify the input PDF containing questions, solutions, and diagrams.
2.  Use [interactive-practice-book-generator](file:///C:/Users/User/.gemini/config/plugins/science/skills/interactive-practice-book-generator/SKILL.md).
3.  The generator will parse the PDF and:
    *   Extract and crop diagrams and tables.
    *   Render math formulas in LaTeX.
    *   Hide answers behind a click-to-reveal button.
    *   Store flagged errors in local storage (`localStorage`).
4.  Verify the generated responsive HTML review book using the browser dev tools.

---

## 4. Video & Audio Subtitle Extractor
Convert online video lectures or audio into readable structured notes.

### Instructions
1.  Take the YouTube URL list from the user.
2.  Run the [video-audio-downloader](file:///C:/Users/User/.gemini/config/skills/video-audio-downloader/SKILL.md) tool.
    *   Download subtitle files (prioritizing `zh-TW`).
3.  Process the raw timeline transcript:
    *   Analyze silence pauses and sentences.
    *   Auto-reorganize them into clean, structured paragraph headers.
4.  Output the polished summary notes in Markdown format.
