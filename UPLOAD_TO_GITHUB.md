# Upload the entire repo to GitHub

Target: https://github.com/mismail-lab/Binding_Affinity

## Recommended: GitHub Desktop or Git CLI (preserves every directory)

1. **First confirm that you have the necessary permission to redistribute PDBbind-derived data.** See `DATA_RIGHTS_AND_PROVENANCE.md`. If not, use the previously provided public code-only package instead.
2. Extract `PLOS_ONE_Complete_GitHub_Upload_2026_10_20.zip` to a folder. Do **not** upload this ZIP as a single repository file: upload its **contents**.
3. With GitHub Desktop, clone your existing `mismail-lab/Binding_Affinity` repository, then copy these extracted files into the cloned folder, preserving subfolders. Review and commit/push changes; check that no existing README or other work was unintentionally overwritten.
4. Alternatively in the repository folder with Git installed:

   ```bash
   git add README.md DATA_RIGHTS_AND_PROVENANCE.md UPLOAD_TO_GITHUB.md REPRODUCE.md .gitignore .gitattributes data/ code/ results/ figures/ tools/ requirements*.txt CITATION.cff LICENSE_CODE_ONLY SHA256SUMS.tsv
   git commit -m "Add complete PLOS ONE reproducibility release and post-hoc analysis"
   git push origin main
   ```
   Adjust branch/clone configuration as needed. Review author metadata and license first.
5. Clone the public repository afresh; run `python tools/restore_large_data.py` and `python tools/verify_repository.py`.
6. Optionally tag your reviewed release `v1.0.0` and provide the tag/commit URL in the manuscript. **Do not claim GitHub is public until you verify it.**

## Browser upload option

All *individual packaged files* are smaller than 25 MiB. GitHub browser upload may nevertheless require folder-by-folder selection to preserve paths. For a large group of files and complex directories GitHub Desktop is much easier. Do not upload the outer ZIP as a single archive; in that case individual CSV inputs would not be directly reconstructable from a cloned repository until the zip were manually downloaded/extracted.

The two feature matrices are compressed and split as `data/large_parts/*.partNNN`. **Upload all parts** and the matching `data/large_parts_manifest.json`. The reconstruction script verifies their exact original checksums. Do not commit reconstructed `data/analysis_features_4624.csv` or `data/original_processed_features_4642.csv` as redundant large Git files.

## Before PLOS ONE submission

Check public file accessibility, dataset permissions and that the final manuscript's Data Availability Statement accurately describes the actual access route. The GitHub URL alone is not proof of a complete or lawful deposit.
