# Antigravity Agent Global Skills & Workflow Guide

Welcome! This repository is a comprehensive guide detailing all **64 global skills** available in this Antigravity Agent environment. It is designed to serve as a design contract, a tool guide, and a workflow manual for other AI Agents.

By reading this repository, other Agents can understand the available tools, parse their schemas, and follow the exact workflows we established to construct and query this knowledge base.

## Repository Contents

*   **[README.md](README.md)**: This main entry point and workflow orchestrator.
*   **[global_skills_directory.md](global_skills_directory.md)**: A complete, categorized list of all 61 global skills with descriptions and file paths.
*   **[yaml_image_deck_breakdown.md](yaml_image_deck_breakdown.md)**: A case study of the `yaml-image-deck` skill, illustrating skill layout, schema, prompting, and validation rules.
*   **[notebooklm_workflows.md](notebooklm_workflows.md)**: Step-by-step instructions for executing NotebookLM-style tasks (visual slides, AI podcasts, interactive study guides, and video transcripts).

---

## Agent Workflow: How to Reconstruct the Knowledge Base

If you are a new Agent entering this workspace, follow this exact workflow to build and operate the knowledge base:

### Step 1: Initialize and Audit the Environment
1.  Read `global_skills_directory.md` to register all 64 available skills and their system paths.
2.  Use these paths to inspect any specific skill's `SKILL.md` when tasked with a corresponding domain (e.g., biological databases, presentation builders, quality audits).

### Step 2: Understand the Skill Architecture
1.  Study the `yaml_image_deck_breakdown.md` file. It serves as the standard template for how skills are structured in this workspace (consisting of configuration axes, prompting pipelines, and scripts).
2.  For any target skill, inspect its folder structure (such as `references/` for schema definitions, `scripts/` for validations, and `assets/` for templates).

### Step 3: Run Document and Quality Audits
*   If auditing QA sheets or Product Quality Plans (PQP), invoke `data-audit-msa`, `drawing-spec-pqp-comparison`, or `pqp-msa-chinese-audit` using their specified parameters.
*   Validate all configurations using local Python scripts (`validate_spec.py`) before final packaging.

### Step 4: Execute NotebookLM-Style Conversions
*   When the user requests a translation of raw materials into dynamic presentations, double-speaker audio files, interactive practice books, or structured notes, follow the precise steps outlined in `notebooklm_workflows.md`.
