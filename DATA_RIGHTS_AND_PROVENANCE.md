# Dataset rights, provenance and release gate

**Read before making this full repository public.** The matrices in this package are **derived from PDBbind 2020** and contain protein sequence, ligand SMILES, processed embeddings/fingerprints and affinity labels. The current PDBbind+ terms restrict redistribution of raw and derived data without specific written authorization from its named rights holders: https://www.pdbbind-plus.org.cn/termofuse .

**The author must verify whether those terms apply to the PDBbind v2020 files actually acquired for this study**, which may depend on the version, acquisition date and agreed license. Having original source data or a public URL does not automatically grant the right to republish derivatives. If written permission is required, obtain and retain it first. If not permitted, do NOT upload `data/large_parts/`, `data/analysis_sample_index.csv`, row-level split/audit labels, and row-level prediction files until an appropriate agreement or alternative approved access route exists. Consult the PLOS ONE editorial office for a restricted-third-party-data disclosure and equivalent access mechanism.

The scripts, figures and aggregates can form a narrower public code-only release. The MIT text in `LICENSE_CODE_ONLY` is a *proposed* author-generated code license, not a data redistribution license; confirm that all code authors approve it.

## Exact feature-data provenance

The original saved processed matrix contains 4,642 records. Seventeen records in eight conflicting repeated-pair groups plus one unparseable-SMILES record were removed in a separately logged confirmatory analysis, leaving 4,624 records. These two files are preserved byte-for-byte inside reassemblable gzip parts; checksums are in `data/large_parts_manifest.json`.

The reproducibility materials contain exact random holdout (3,699/925), ligand-scaffold-disjoint and exact-protein-sequence-disjoint splits. They do not contain PDB structure files or the full original 5,316-entry upstream exclusion audit.

Do not publicly claim that upstream ProtT5 embeddings can be independently regenerated from this package, because the checkpoint revision and all extraction/preprocessing details are unavailable.
