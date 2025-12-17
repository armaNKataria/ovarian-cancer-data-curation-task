# Ovarian Cancer Multimodal Data Integration Project

## Project Overview

This project explores the identification, auditing, analysis, and integration of open ovarian cancer datasets with a focus medical imaging and proteogenomics. The objective is to demonstrate a reproducible, well-documented data engineering and exploratory analysis workflow, rather than to develop predictive models.

The project follows a structured pipeline:
- Dataset discovery and cataloging
- Ethical data loading and auditing
- Exploratory analysis and visualization
- Patient-level dataset integration
- Schema and metadata documentation

All datasets used are **open-access** and publicly licensed.

---

## Project Structure

- medical-data-analysis/
  - data/
    - raw/
      - tcga-ov/
      - tcga_ov_proteogenomics/
    - processed/
      - ovarian_universal.csv
  - notebooks/
    - 01_load_and_audit.ipynb
    - 02_analysis_and_viz.ipynb
    - 03_integration_strategy.ipynb
  - reports/
    - linkage_report.md
  - schema.json
  - metadata.json
  - curated_sources.md
  - README.md

---

## Part A — Dataset Discovery & Cataloging

Multiple open ovarian cancer datasets were identified across diverse modalities, including:
- Radiology (CT/MR imaging metadata)
- Proteogenomics
- Clinical and molecular datasets (cataloged but not fully integrated)

Each dataset is documented in `curated_sources.md`, including:
- Dataset name and source
- Modality and size
- Access method
- License and terms
- Identifier systems
- Known limitations and biases

Key gap identified:  
Somatic mutation, copy number variation, and transcriptomic data were not integrated and represent opportunities for future expansion.

---

## Part B — Dataset Selection & Loading

Two datasets with distinct but linkable modalities were selected:

1. TCGA-OV Radiology (TCIA)  
   - 143 patients  
   - 844 imaging series  
   - Predominantly CT imaging metadata  

2. TCGA-OV Proteogenomics (TCIA)  
   - 20 patients  
   - 87 imaging series  
   - Subset of TCGA-OV with proteogenomic profiling  

Raw metadata files were downloaded ethically and stored under `data/raw/`.

---

## Part C — Data Audit & Exploratory Analysis

### Notebook: `01_load_and_audit.ipynb`

Performed:
- Row and column counts
- Unique patient counts
- Missingness analysis (% missing per column)

Key observations:
- Radiology data provides broad imaging coverage but has substantial demographic missingness
- Proteogenomics data is smaller and more selective
- Missingness reflects real-world clinical data collection practices

### Notebook: `02_analysis_and_viz.ipynb`

Exploratory analyses included:
- Number of studies per patient
- Total image count per patient
- Relationship between studies and images
- Scanner manufacturer distribution

Key insights:
- Imaging coverage is highly uneven across patients
- CT imaging dominates both datasets
- Scanner vendor bias (GE Medical Systems, Siemens) is present
- Proteogenomics cohort has limited longitudinal imaging depth

---

## Part D — Universal Dataset Integration

### Notebook: `03_integration_strategy.ipynb`

A patient-level universal integrated dataset was constructed by:
- Aggregating radiology and proteogenomics metadata to one row per patient
- Defining a canonical identifier: `patient_id_canonical`
- Merging datasets using a **left join**

Output file:
- `data/processed/ovarian_universal.csv`

Linkage summary:
- Total radiology patients: 143
- Patients with proteogenomics data: 20
- Match rate: ~14%

Integration assumptions, join logic, and limitations are documented in:
- `reports/linkage_report.md`

---

## Part E — Schema & Metadata Documentation

To ensure transparency and reproducibility, the following documentation files were created:

### `schema.json`
Defines the structure of `ovarian_universal.csv`, including:
- Column names and data types
- Descriptions and allowed values
- Data provenance for each field

### `metadata.json`
Summarizes:
- Data sources and licenses
- Processing and transformation steps
- Dataset versioning and creation date
- Known limitations

These files treat the integrated dataset as a **reusable data product**.

---

## Summary

This project demonstrates a complete, end-to-end workflow for:
- Discovering and evaluating biomedical datasets
- Auditing and visualizing real-world clinical data
- Integrating heterogeneous modalities at the patient level
- Producing reproducible, well-documented outputs

