# Reproducibility scope and editorial data-access summary

**Associated manuscript:** PONE-D-26-48533R1 (revised title is in `README.md`).

## (a) Third-party source

The starting cohort is the **PDBbind v2020 refined set**, 5,316 complexes, available from the provider at https://www.pdbbind-plus.org.cn/download (original v2020 refined-set complex archive and corresponding index files). The v2020.R1 reprocessed release is **not** a drop-in substitute for the original v2020 cohort. The source was reportedly acquired without special or exclusive access privileges. Any download/access is subject to current provider rules.

## (b) What this repository enables

**Verified from saved artifacts:**

- Exact byte-for-byte restoration of the archived 4,642-record and confirmatory 4,624-record processed feature matrices (3,079 numeric model features; extra metadata columns), using `tools/restore_large_data.py`.
- Alignment of all five historical metadata chunks (4,642 records) to the archived 4,642-row processed matrix, via `code/verify_original_metadata.py`.
- Verification of the 17 conflicting repeated-pair rows and 1 invalid-SMILES exclusion, exact saved sample IDs, 3,699/925 random test partition and the other two validation split files.
- Independent re-calculation of archived prediction-level metrics, SHAP summary checks, ablation results, and 925 post-hoc holdout predictions using the saved rows and `tools/verify_repository.py` and accompanying scripts.
- Optional computational reruns of the downstream models, subject to dependencies and normal numerical/environment variability. The post-hoc training-budget evaluation is **not** a new external validation.

**Not established:**

- A record-by-record historical mapping of **all 674 entries omitted** between the original 5,316-complex source list and 4,642 saved triplets. The notebook documents SDF and PDB checks and parsing exceptions, but did **not** save PDB ID and reason for each omitted entry.
- Complete, bit-for-bit regeneration of the saved ProtT5 embeddings from the raw PDBbind folders: checkpoint revision, long-sequence handling and other upstream extraction details remain uncertain.
- Full independent prospective benchmark validation. The homology-cluster split and external-cohort testing have not been performed.

## (c) Third-party rights and full data access

Source-data download availability and permission to **redistribute derivatives** are not the same thing. The current PDBbind+ terms limit sharing of raw and derived data without written authorization: https://www.pdbbind-plus.org.cn/termofuse . The authors must confirm what terms govern these particular v2020-derived files and obtain any required permission before publicly uploading `data/large_parts/` and row-level materials. A public release of only scripts or aggregate results would not provide the exact minimal processed feature data used for downstream reproduction.

## Fresh-clone check

```bash
python tools/restore_large_data.py
python code/verify_original_metadata.py
python tools/verify_repository.py
```

The versioned GitHub tag/commit and permission/access explanation should match the manuscript's Data Availability Statement and the response to PLOS ONE's data-availability inquiry. Do not claim the code archive is publicly released before these checks are complete.

### November 2026 original-notebook audit addendum

The archived source notebook contains 674 `Could not sanitize molecule` RDKit diagnostics in the initial 5,316-entry extraction pass, matching the 674-record difference to the saved 4,642-row triplet file. This is **aggregate supporting evidence**, not a PDB-level cause audit, and not a reconstruction of ProtT5 embeddings. See `provenance/RDKit_674_log_explanation.md`.
