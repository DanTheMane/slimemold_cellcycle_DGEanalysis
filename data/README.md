# Data notes

`SRP412754_runinfo.csv` is the run-info table copied from the supplied project. Verify it against the current SRA study record before citing. `SRA_experiment_summary.json` is a failed retrieval response containing invalid-UID errors; it is included only to document the provenance problem and must not be treated as valid experiment metadata.

The source project contains a verified sample manifest under `results/differential_expression/verified_sample_manifest.csv`. The older `sample_manifest.csv` in the source tree has conflicting stage assignments and is not staged.

The transcriptome and targeted protein sequences in this directory require provenance and redistribution-license review. `GDRG01.fasta` and `GDRG01.fasta.gz` are duplicate representations; retain one after review.
