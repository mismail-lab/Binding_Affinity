# Structure-free protein–ligand affinity regression — research reproducibility

**Associated manuscript:** *Structure-Free Protein–Ligand Binding Affinity Regression Using ProtT5 and Ligand Features: Ablation, Explainability, and Similarity-Aware Validation*

**Manuscript ID:** PONE-D-26-48533 (PLOS ONE, revision)

**Repository:** https://github.com/mismail-lab/Binding_Affinity

This repository contains the **original and confirmatory processed feature matrices**, row-level exclusions and dataset splits, matched predictions, seven feature-ablation experiments, corrected LightGBM SHAP outputs, publication figures, source code, and an additional **post-hoc training-budget sensitivity comparison** performed using the same original 925-case test partition.

> **Rights notice — verify before public posting.** The matrices were derived from PDBbind v2020 source data. The PDBbind+ terms of use restrict redistribution of original **and derived** data without written permission. The responsible authors must verify which terms governed the exact 2020 data acquisition and obtain any required authorization before publishing these data, not merely acknowledge this notice. See `DATA_RIGHTS_AND_PROVENANCE.md`. All nonrestricted author-generated code and aggregate analyses may be released separately.

## What is inside

| Directory | Contents |
|---|---|
| `code/` | Reanalysis scripts, original Stage 2 notebook, independent Jupyter budget-sensitivity notebook and execution script |
| `data/` | Exclusion audits, exact random/scaffold/protein splits, row mapping and group metadata |
| `data/large_parts/` | Exact 4,642-row and 4,624-row processed feature CSVs, **gzip-compressed and split into GitHub-compatible parts** |
| `results/` | Original model metrics, five-fold ablations, matched saved predictions, corrected SHAP arrays and statistics |
| `results/posthoc_training_budget/` | New selection table, holdout metrics, per-case predictions, significance tests, environment metadata |
| `figures/` | Seven TIFF figures and S1 Morgan-bit example figure |
| `tools/` | Reconstruct data matrices and verify the uploaded repository |

## First steps

1. Clone/download the **entire** repository after release. All `data/large_parts/*.part*` files are required.
2. Run `python tools/restore_large_data.py` from any directory (Python stdlib only). It checks all component hashes and recreates both original CSVs **byte-for-byte** under `data/`.
3. Run `python tools/verify_repository.py` to check saved outputs, splits, figures, package contents and reconstructed matrices.
4. Install environment requirements, and rerun as outlined in `REPRODUCE.md`.

## Verified headline results

| Study | LightGBM R² | CatBoost R² | Voting R² |
|---|---:|---:|---:|
| Original fixed 100-iteration holdout | 0.600 | 0.438 | 0.558 |
| Post-hoc training-only-selected budgets on same reused holdout | 0.6134 (300) | 0.6033 (1,000) | 0.6238 (300/1,000) |

Post-hoc Voting had a numerically smaller test MAE than LightGBM (0.9413 vs 0.9514); the paired Wilcoxon p-value ≈0.235 and 95% bootstrap CI for paired MAE difference crossed zero, so no statistically significant advantage is claimed. These new experiments are **post-hoc analyses on an already examined test holdout**, not prospectively independent validation. The 1,000-iteration CatBoost budget was the upper candidate tested, not an established global optimum.

Corrected LightGBM SHAP group totals: ProtT5 **64.26%**, Morgan **14.69%**, RDKit **21.05%** on 250 holdout observations. This is model-specific, dependent on group sizes and original feature names.

## Important scientific limits

- The reasons for the 674 upstream exclusions between the original 5,316 PDBbind entries and first 4,642 processed rows cannot be reconstructed from the retained feature matrix.
- Original ProtT5 checkpoint and feature-extraction details were not all preserved; only downstream prediction-level reproducibility is demonstrable from these files.
- An exact-protein-sequence-disjoint split does not constitute homology-cluster generalization.
- CatBoost original fixed-100 predictions did not replay identically in an independent refit, so do not claim bitwise full retraining reproducibility.
- The post-hoc experiment environment differs from the original Stage 2 software environment.

## Documentation

- `REPRODUCE.md` — execution commands, model selection procedure, data layout, and caution on interpretation.
- `DATA_RIGHTS_AND_PROVENANCE.md` — permissions and provenance.
- `UPLOAD_TO_GITHUB.md` — GitHub Desktop and browser upload instructions.
- `LICENSE_CODE_ONLY` — license text for author-generated code, **subject to author confirmation of rights**. Data are not licensed under this text.
- `CITATION.cff` — author listing needs author approval.

**No DOI is assigned by this package.** Use a fixed GitHub commit or tagged release only after public upload and verification.
