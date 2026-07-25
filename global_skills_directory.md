# Global Agent Skills Directory

This directory registers all **64 global skills** available in this Antigravity Agent environment. They are organized by functional domain to help other Agents identify the appropriate tool for a task.

---

## 1. 簡報製作與設計 (Presentation & Slide Design)

These skills compile structured inputs or documents into premium visual presentation slide decks.

*   **[soil-teaching-deck](file:///C:/Users/User/.gemini/config/plugins/soil-presentation-skills/skills/soil-teaching-deck/SKILL.md)**: Based on Prof. Li Chun-yi's SOIL Teaching Deck Workflow (6 engines), analyzes cognitive load, outlines presentation structure, and edits/refines pedagogical slide decks.
*   **[soil-html-deck](file:///C:/Users/User/.gemini/config/plugins/soil-presentation-skills/skills/soil-html-deck/SKILL.md)**: Generates highly responsive, interactive HTML presentations featuring charts (Chart.js), videos, and animations.
*   **[soil-image-deck](file:///C:/Users/User/.gemini/config/plugins/soil-presentation-skills/skills/soil-image-deck/SKILL.md)**: Uses image generation tools (e.g., `gpt-image-2`) to create single-image slides, packaging them into full-bleed image PowerPoint decks.
*   **[yaml-image-deck](file:///C:/Users/User/.gemini/config/skills/yaml-image-deck/SKILL.md)**: Compiles structured YAML content into consistent, visual-first slide decks with style locking.
*   **[yaml-assa-abloy-pptx-generator](file:///C:/Users/User/.gemini/config/plugins/soil-presentation-skills/skills/yaml-assa-abloy-pptx-generator/SKILL.md)**: Uses the ASSA ABLOY brand template and YAML style rules to generate corporate presentation decks.
*   **[engineering-pptx-builder](file:///C:/Users/User/.gemini/config/skills/engineering-pptx-builder/SKILL.md)**: Automatically builds English/Traditional Chinese bilingual engineering/QA-themed slides.
*   **[digital-business-card-builder](file:///C:/Users/User/.gemini/config/skills/digital-business-card-builder/SKILL.md)**: Creates self-contained single-page responsive HTML business cards with embedded assets.
*   **[interactive-practice-book-generator](file:///C:/Users/User/.gemini/config/plugins/science/skills/interactive-practice-book-generator/SKILL.md)**: Translates exam PDFs into interactive study books with hidden answers and LaTeX formula support.

---

## 2. 品質管理與工程稽核 (Quality & Engineering Audit)

These tools automate spreadsheet operations, mechanical drawing parsing, and discrepancy reports.

*   **[data-audit-msa](file:///C:/Users/User/.gemini/config/plugins/science/skills/data-audit-msa/SKILL.md)**: Validates metadata integrity and audits Gage R&R metrics in Measurement System Analysis (MSA) and Product Quality Plan (PQP) sheets.
*   **[pqp-msa-chinese-audit](file:///C:/Users/User/.gemini/config/skills/pqp-msa-chinese-audit/SKILL.md)**: Scans files and auto-generates Traditional Chinese audit markdown reports for MSA/PQP files.
*   **[drawing-spec-pqp-comparison](file:///C:/Users/User/.gemini/config/plugins/science/skills/drawing-spec-pqp-comparison/SKILL.md)**: Audits PQP sheets against mechanical drawing PDFs (TLA/Subassemblies), checking dimensions, torques, and capabilities.
*   **[pcb-pqp-spec-comparison](file:///C:/Users/User/.gemini/config/plugins/science/skills/pcb_pqp_spec_comparison/SKILL.md)**: Compares PCB specs, PQP sheets, and QA inspection reports for compliance (dimensions, solder mask thickness, revisions).
*   **[engineering-doc-diff-ppt](file:///C:/Users/User/.gemini/config/skills/engineering-doc-diff-ppt/SKILL.md)**: Performs side-by-side discrepancy comparisons between spec PDFs and supplier drawings, exporting a PowerPoint diff report.
*   **[excel-grr-generator](file:///C:/Users/User/.gemini/config/skills/excel-grr-generator/SKILL.md)**: Scans dimensional sheets, identifies critical-to-quality (CTQ) dimensions, and populates ANOVA Gage R&R sheets.
*   **[fai-report-generator](file:///C:/Users/User/.gemini/config/skills/fai-report-generator/SKILL.md)**: Parses drawings, extracts specifications, and populates First Article Inspection (FAI) reports with simulated normal distribution values.
*   **[pqp-drawing-balloon-updater](file:///C:/Users/User/.gemini/config/skills/pqp-drawing-balloon-updater/SKILL.md)**: Overlays movable and editable balloon shape indicators at inspected locations in Excel PQP sheets.
*   **[excel-work-hour-migrator](file:///C:/Users/User/.gemini/config/skills/excel-work-hour-migrator/SKILL.md)**: Shifts monthly work hour statistic sheets to the next month, resetting daily cells and adjusting sum formulas.
*   **[excel-workhour-sync](file:///C:/Users/User/.gemini/config/skills/excel-workhour-sync/SKILL.md)**: Synchronizes work hours across monthly files, clearing retired entries and repairing broken formulas.
*   **[excel-defect-tracker-updater](file:///C:/Users/User/.gemini/config/skills/excel-defect-tracker-updater/SKILL.md)**: Clears and populates QA defect tracking Excel sheets. Automatically analyzes defect photos, determines correct orientation, resizes images to fit cell heights, copies formatting styles, and fills finding details.

---

## 3. 生物資訊、基因體與醫學資料庫 (Bioinformatics & Medical Databases)

These specialized databases support molecular biology, pharmacology, clinical trials, and genetics research.

### A. Proteins & 3D Structures
*   **[alphafold-database-fetch-and-analyze](file:///C:/Users/User/.gemini/config/plugins/science/skills/alphafold_database_fetch_and_analyze/SKILL.md)**: Retrieves AlphaFold structures by UniProt ID, analyzing structural confidence (pLDDT) and disorder.
*   **[foldseek-structural-search](file:///C:/Users/User/.gemini/config/plugins/science/skills/foldseek_structural_search/SKILL.md)**: Performs 3D protein structure searches using Foldseek API on `.pdb`/`.cif` coordinate files.
*   **[pdb-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/pdb_database/SKILL.md)**: Queries the Protein Data Bank (PDB) for experimentally-determined 3D biomolecular structures.
*   **[pymol](file:///C:/Users/User/.gemini/config/plugins/science/skills/pymol/SKILL.md)**: Automates PyMOL scripting for structure alignment, distance measurements, binding site marking, and high-quality image rendering.
*   **[protein-sequence-msa](file:///C:/Users/User/.gemini/config/plugins/science/skills/protein_sequence_msa/SKILL.md)**: Runs Clustal Omega to align multiple protein sequences for homology analysis.
*   **[protein-sequence-similarity-search](file:///C:/Users/User/.gemini/config/plugins/science/skills/protein_sequence_similarity_search/SKILL.md)**: Performs MMseqs2 or BLAST similarity searches for homologous proteins.
*   **[string-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/string_database/SKILL.md)**: Queries protein-protein interaction (PPI) networks, physical interactions, and functional enrichments.
*   **[uniprot-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/uniprot_database/SKILL.md)**: Retrieves protein sequence metadata, functional annotations, taxonomy, and literature links.
*   **[interpro-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/interpro_database/SKILL.md)**: Identifies domains, signatures, and families combining 14 databases (CDD, Pfam, etc.).

### B. Genomics, Variants & Expression
*   **[alphagenome-single-variant-analysis](file:///C:/Users/User/.gemini/config/plugins/science/skills/alphagenome_single_variant_analysis/SKILL.md)**: Evaluates genetic variant effects on gene expression, chromatin accessibility (DNASE), and transcription factors.
*   **[clinvar-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/clinvar_database/SKILL.md)**: Looks up human genetic variant clinical significance (Pathogenic, Benign, VUS).
*   **[dbsnp-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/dbsnp_database/SKILL.md)**: Maps single nucleotide polymorphisms (SNPs) between rsIDs, VCF coordinates, and HGVS nomenclature.
*   **[gnomad-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/gnomad_database/SKILL.md)**: Evaluates allele frequencies and gene constraint metrics (pLI/LOEUF) in population data.
*   **[gtex-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/gtex_database/SKILL.md)**: Retreives tissue-specific quantitative RNA expression levels and expression quantitative trait loci (eQTLs).
*   **[human-protein-atlas-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/human_protein_atlas_database/SKILL.md)**: Extracts spatial protein expression levels across tissues and sub-cellular compartments from HPA.
*   **[jaspar-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/jaspar_database/SKILL.md)**: Retrieves Transcription Factor binding profiles, PFMs, and PWMs.
*   **[ucsc-conservation-and-tfbs](file:///C:/Users/User/.gemini/config/plugins/science/skills/ucsc_conservation_and_tfbs/SKILL.md)**: Fetches phyloP/phastCons evolutionary conservation scores and transcription factor binding site tracks.
*   **[unibind-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/unibind_database/SKILL.md)**: Queries experimentally validated direct TF-DNA interaction locations.
*   **[ensembl-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/ensembl_database/SKILL.md)**: Resolves gene/transcript/protein coordinates and predicts variant consequences (VEP).
*   **[encode-ccres-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/encode_ccres_database/SKILL.md)**: Queries ENCODERegistry of cis-Regulatory Elements (cCREs) and raw peak files.
*   **[ncbi-sequence-fetch](file:///C:/Users/User/.gemini/config/plugins/science/skills/ncbi_sequence_fetch/SKILL.md)**: Downloads genomic or protein fasta files directly from NCBI database accessions.

### C. Pharmacology, Clinical Trials & Pathways
*   **[chembl-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/chembl_database/SKILL.md)**: Queries ChEMBL database for bioactive molecules, drug targets, bioactivities, and IC50/Ki values.
*   **[pubchem-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/pubchem_database/SKILL.md)**: Searches PubChem for chemical compounds, SMILES, physical properties, and bioassays.
*   **[clinical-trials-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/clinical_trials_database/SKILL.md)**: Resolves NCT IDs, fetches trial enrollment eligibility, and lists sponsor portfolios.
*   **[openfda-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/openfda_database/SKILL.md)**: Integrates FDA adverse events, product labeling, recalls, and shortages.
*   **[opentargets-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/opentargets_database/SKILL.md)**: Facilitates target-disease association scores and therapeutic tractability evaluation.
*   **[reactome-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/reactome_database/SKILL.md)**: Searches human metabolic and signaling pathways, supporting gene enrichment analysis.
*   **[quickgo-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/quickgo_database/SKILL.md)**: Maps annotations between genes and molecular functions/cellular components (GO).
*   **[embl-ebi-ols](file:///C:/Users/User/.gemini/config/plugins/science/skills/embl_ebi_ols/SKILL.md)**: Queries biomedical ontology terms, definitions, and hierarchies (e.g., HP, DOID, GO).

---

## 4. 學術文獻搜尋與分析 (Academic Literature Search)

These skills retrieve academic papers, citations, and full text PDFs.

*   **[literature-search-arxiv](file:///C:/Users/User/.gemini/config/plugins/science/skills/literature_search_arxiv/SKILL.md)**: Queries arXiv, retrieving abstracts and downloading full-text preprints.
*   **[literature-search-biorxiv](file:///C:/Users/User/.gemini/config/plugins/science/skills/literature_search_biorxiv/SKILL.md)**: Searches bioRxiv and medRxiv preprint databases.
*   **[literature-search-europepmc](file:///C:/Users/User/.gemini/config/plugins/science/skills/literature_search_europepmc/SKILL.md)**: Queries Europe PMC for citations, references, and open-access full-text XML.
*   **[literature-search-openalex](file:///C:/Users/User/.gemini/config/plugins/science/skills/literature_search_openalex/SKILL.md)**: Retrieves works, author h-index, institution metrics, and resolves DOIs.
*   **[pubmed-database](file:///C:/Users/User/.gemini/config/plugins/science/skills/pubmed_database/SKILL.md)**: Searches MEDLINE/PubMed, matching raw citations and linking papers to biological entities.

---

## 5. 影音、語音與多媒體 (Voice & Media Tools)

These tools download transcripts, clone voices, and generate visual artwork.

*   **[use-ho-cloned_voice](file:///C:/Users/User/.gemini/config/skills/use-ho-cloned_voice/SKILL.md)**: Generates audio speech files using the cloned voice of "Ho Sze-chi" (何思齊) via a local VoxCPM2 model.
*   **[voxcpm2-voice-cloner](file:///C:/Users/User/.gemini/config/skills/voxcpm2-voice-cloner/SKILL.md)**: Custom voice cloning, conversation scenario script generation, and recording manager (optimized for low RAM).
*   **[video-audio-downloader](file:///C:/Users/User/.gemini/config/skills/video-audio-downloader/SKILL.md)**: Downloads YouTube subtitles (preferring Traditional Chinese `zh-TW`) and reformats them into structured, readable paragraphs in Markdown.
*   **[draw-free](file:///C:/Users/User/.gemini/config/skills/draw-free/SKILL.md)**: Free AI image generator using Pollinations.ai (requires no API keys or local GPU).
*   **[viral-thumbnail-designer](file:///C:/Users/User/.gemini/config/skills/viral-thumbnail-designer/SKILL.md)**: Analyzes video subtitle text and character photos to design high-click-through-rate (CTR) YouTube thumbnail drafts and layouts.

---

## 6. 開發、系統管理與通用工具 (Development & General Tools)

These scripts manage credentials, run environmental CLI diagnostics, or packages workflows.

*   **[android-cli](file:///C:/Users/User/.gemini/config/plugins/android-cli-plugin/skills/SKILL.md)**: Runs Android SDK diagnostics, configures emulation, and deploys builds.
*   **[uv](file:///C:/Users/User/.gemini/config/plugins/science/skills/uv/SKILL.md)**: Verifies or installs the high-performance Python package installer `uv`.
*   **[credentials](file:///C:/Users/User/.gemini/config/plugins/science/skills/credentials/SKILL.md)**: Safe credential handling procedures to check for API keys.
*   **[workflow-skill-creator](file:///C:/Users/User/.gemini/config/plugins/science/skills/workflow_skill_creator/SKILL.md)**: Distills a completed multi-step chat interaction or workflow into a reusable Antigravity skill template.
*   **[predictingthepast](file:///C:/Users/User/.gemini/config/plugins/science/skills/predictingthepast/SKILL.md)**: Implements Aeneas (Latin) and Ithaca (Ancient Greek) models to restore, date, and attribute ancient epigraphic texts.
*   **[google-sheets-drink-order-app-builder](file:///C:/Users/User/.gemini/config/skills/google-sheets-drink-order-app-builder/SKILL.md)**: Parses menu images/data, builds a responsive web app drink order system, and generates Google Apps Script (GAS) code to sync orders with Google Sheets.
*   **[google-sheets-form-order-builder](file:///C:/Users/User/.gemini/config/skills/google-sheets-form-order-builder/SKILL.md)**: Uses Google Apps Script (GAS) to automatically build a Google Form for order entry and syncs responses back to a Google Sheet.
*   **[science-skills-common](file:///C:/Users/User/.gemini/config/plugins/science/skills/science_skills_common/SKILL.md)** (and **[scienceskillscommon](file:///C:/Users/User/.gemini/config/plugins/science/skills/scienceskillscommon/SKILL.md)**): The shared HTTP library with rate limits and exponential backoffs. (Internal module, do not invoke directly).
