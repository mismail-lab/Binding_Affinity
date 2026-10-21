# Computational reproduction and verification

From repository root:

```bash
python tools/restore_large_data.py
python tools/verify_repository.py
```

`tools/restore_large_data.py` verifies and recreates exactly both feature matrices (4,642 and 4,624 rows) before running any model. It uses Python standard library only. `tools/verify_repository.py` confirms hashes of all distributed files, split sizes, prediction rows, and post-hoc metrics without retraining.

For the original Stage 2 analysis (which can be CPU/RAM intensive), create a dedicated Python environment compatible with `requirements_stage2.txt`, then:

```bash
python code/validate_archived_predictions.py
python code/reproduce_stage2.py
```

The original archived outputs came from Python 3.13.5, NumPy 2.3.5, pandas 2.2.3, scikit-learn 1.8.0, LightGBM 4.6.0, CatBoost 1.2.8 and RDKit 2025.09.4. See `results/run_metadata.json` for full metadata. Separate package constraints may require resolution in a given operating system.

For the newer **post-hoc training-budget** experiment, install a separate environment from `requirements_posthoc_jupyter.txt` and run:

```bash
python code/run_posthoc_budget_from_local_features.py
```

It uses the saved 3,699/925 holdout, randomly splits the 3,699 training records into 2,959/740 fitting/validation records (seed 73), selects LightGBM iterations from [100,300,600] and CatBoost iterations from [100,300,600,1000] by lowest validation RMSE, refits the two models on all 3,699 training records and evaluates on the previously examined 925 test cases. The updated user run selected LightGBM 300, CatBoost 1000, and Voting took their mean. Results appear in `recomputed/posthoc_budget/` rather than overwriting archived figures or tables. The originally successful Windows run used the versions in `results/posthoc_training_budget/05_run_metadata.json`.

Original run outputs, row-level predictions, corrected SHAP arrays, and all associated metadata live in `results/`. Test outcome comparisons are **post-hoc descriptive sensitivity estimates**, not unbiased confirmatory model-selection test results nor new external validation. Source ProtT5 embeddings cannot be regenerated end-to-end because upstream provenance is incomplete.

The accompanying notebook `code/PLOS_ONE_Reviewer2_Jupyter_Step_by_Step.ipynb` may expect a source ZIP and the earlier Kaggle-style layout. For the extracted GitHub directory, the Python entry point `code/run_posthoc_budget_from_local_features.py` is the directly supported reproducible rerun.
