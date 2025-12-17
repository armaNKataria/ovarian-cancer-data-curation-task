# Linkage Report — TCGA-OV Universal Dataset

# Canonical Identifier
All datasets were linked using a shared patient-level identifier
(`patient_id_canonical`), corresponding to the TCGA patient ID used
consistently across TCIA collections.

# Join Logic
A left join was performed using the radiology dataset as the reference
population. This preserves all radiology patients while attaching
proteogenomics-derived fields where available as the radiology dataset is bigger than other.

# Match Rate
- Total radiology patients: 143
- Patients with proteogenomics data: 20
- Match rate: ~14%

# Unlinked Records
The majority of patients do not have corresponding proteogenomics data.
This reflects the limited availability of proteogenomic profiling rather
than identifier mismatches or data quality issues.

# Assumptions and Limitations
- Imaging-derived features were aggregated at the patient level.
- The integrated dataset is subject to selection bias, as patients with
  proteogenomics data may not be representative of the full cohort.
- No genomic mutation or transcriptomic data were included, limiting
  molecular coverage.
