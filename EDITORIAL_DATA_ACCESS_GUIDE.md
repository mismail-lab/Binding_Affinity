# Minimal data needed for the PLOS ONE editorial check

Original PDBbind v2020 refined set: https://www.pdbbind-plus.org.cn/download (original v2020, items 1 and 3; not v2020.R1).

**Study-specific archived inputs:**
- `data/large_parts/analysis_features_4624.csv.gz.part001...003`: exact 4,624-row/3,079-feature analysis matrix (reconstruct with `python tools/restore_large_data.py`).
- `data/large_parts/original_processed_features_4642.csv.gz.part001...003`: earlier 4,642-row processed matrix.
- `data/analysis_sample_index.csv`, `data/split_random_80_20.csv`, other `data/split_*.csv`: case information and exact experiment partitions.
- `results/holdout_predictions.csv`, `results/posthoc_training_budget/`, `results/ablation_cv_summary.csv`: output values supporting reported summaries.
- `code/`, `requirements*.txt`, `REPRODUCE.md`, `REPRODUCIBILITY_SCOPE.md`: code and reuse instructions.
- `provenance/`: original extraction audit, 674 RDKit sanitization messages, and intermediate metadata.

**Recommended verification on a clean clone:**
```
python tools/restore_large_data.py
python tools/verify_repository.py
python code/verify_original_metadata.py
python code/verify_rdkit_extraction_log_summary.py
```

**Scope:** Supports checking/repeating downstream analyses from archived vectors; not exact, end-to-end historical regeneration of embeddings. The 674 messages do not individually identify PDB IDs.

**Public release gate:** Public redistribution of PDBbind-derived sequence/SMILES/affinity features and metadata must be approved under the applicable source agreement. Do NOT upload before verifying permission or an authorized alternative access route. See DATA_RIGHTS_AND_PROVENANCE.md.
