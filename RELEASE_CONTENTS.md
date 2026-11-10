# Consolidated GitHub release contents — November 2026

This is the **single consolidated** source package for the PLOS ONE revision, combining the original 66-file GitHub reproducibility release and the later historical-provenance add-on. Older ZIP packages are superseded; upload **these extracted repository files only**.

## Contents by directory

| Path | Purpose |
|---|---|
| `code/` | Model-reproduction and validation code, notebooks, historical metadata verification and PDBbind extraction rerun |
| `data/` | Exact 4,624/4,642 source-derived matrices as reconstructable compressed chunks, exclusions, sample mapping and partitions |
| `provenance/` | Five original metadata CSV chunks; original extraction logic; source-folder audits and reduction summaries |
| `results/` | All archived ablation, statistical, SHAP, prediction and post-hoc iteration-budget results |
| `figures/` | Seven publication TIFF figures plus one supplementary figure |
| `tools/` | Checksum validation and exact dataset reconstruction |
| Root files | License scope, citation draft, requirements, upload notes, source-data rights and reproducibility scope |

## Exact structure and checks

- **6 compressed feature-data chunks**; each tracked item is below GitHub's 25 MiB browser-upload limit.
- **4,642 original rows** and **4,624 confirmatory rows**, each reconstructed byte-for-byte.
- **5 original metadata chunks**: 1,000 + 1,000 + 1,000 + 1,000 + 642 = 4,642 rows.
- Original random test partition: **3,699 train / 925 test**.
- Post-hoc model budgets selected: LightGBM 300, CatBoost 1,000; 925 saved test predictions.
- **Do not upload reconstructed ~94 MB raw CSVs separately**: the 6 tracked parts restore them.
- The public repository release has **not been independently verified by this ZIP**; upload and check a fresh clone.
- **Rights approval is required** before publishing PDBbind-derived data: `DATA_RIGHTS_AND_PROVENANCE.md`.

## Test commands

```bash
python tools/restore_large_data.py
python code/verify_original_metadata.py
python tools/verify_repository.py
```

`SHA256SUMS.tsv` lists a SHA-256 for every tracked content file except itself. Python's verification script checks all of them.
