# Audit and validation report

Audit date: 2026-10-23. Scope: the copied project tree, including the newly supplied `01_reference_based` directory. Original analysis files were not modified. No pipeline was rerun and no external upload was made.

## Inventory and curation

The supplied project tree contains 689 files (~5.31 GB), including scripts, metadata, Salmon quantifications, reference indices/databases, logs, and reports. `inventory.tsv` records each observed source file with type, byte size, probable role, recommended action, rationale, and manual-review flag.

The staging package now includes the available shell/R/Python analysis scripts, verified sample manifest, analysis sample sheet and summary, full DE result and candidate tables for all four contrasts, selected QC figures and tables, selected genome-maintenance/candidate and enrichment outputs, and selected references. Staging currently contains 68 files (~69.5 MB). Raw reads, bundled executables, generated Salmon index and per-sample quantification directories, large third-party databases, logs, caches, and redundant intermediate matrices are excluded.

## Statistical checks

The saved DE analysis summary reports 13 samples, 31,729 transcripts before filtering, and 23,287 after filtering. The copied DESeq2 script filters with `rowSums(counts(dds) >= 10) >= 2`, uses design `~ stage`, and sets early S-phase as the reference. Four saved result tables each contain 23,287 rows. Directly counting non-NA `padj < 0.05` values gives:

| Contrast (numerator vs early S-phase) | Significant rows |
| --- | ---: |
| early G2 phase | 885 |
| mid S-phase | 1,566 |
| late S-phase | 2,587 |
| late G2 phase | 25 |

These results agree with the saved table dimensions and summary. This validates those saved counts only; no model was rerun.

## Issues found

1. **Metadata conflict:** `reports/sample_manifest.csv` is stale/inconsistent: it uses broad `late phase` labels for samples that are split into late S and late G2 in `verified_sample_manifest.csv`, and its stage assignments disagree with that verified manifest for some runs. The DESeq2 script explicitly uses the verified manifest, so the staged README summarizes that manifest. The inconsistent sample manifest is excluded and flagged in the inventory; review it before deleting from any public source archive.
2. **Quantification availability:** the verified manifest excludes `SRR22704997` as unavailable, while other runs have quantifications. The initial copied project directory contained a lone FASTQ mate for some runs; this subset is not a complete paired-read dataset. Use SRA accessions and verified metadata rather than infer samples from those partial FASTQ files.
3. **Invalid SRA summary:** `metadata/SRA_experiment_summary.json` contains NCBI invalid-UID errors for the experiment accessions. It is retained in `data/metadata/` only to document the failed retrieval, not as evidence. `SRP412754_runinfo.csv` is staged, but confirm records against the SRA study and cite the source publication.
4. **Library strandedness:** the project note says library type is unresolved and documents pilot Salmon mapping behavior. Confirm the original library preparation and per-sample quantification settings.
5. **Portability/reproducibility:** scripts contain hard-coded `/home/dan/slime_mold_synchrony` paths and assumptions about directories/software. Targeted annotation and enrichment scripts depend on unstaged databases/inputs. No complete environment lockfile or full provenance manifest is present.
6. **Reference provenance/licensing:** the staged transcriptome and targeted protein files require source accessions, retrieval dates, licensing/redistribution review, and de-duplication of compressed/uncompressed transcriptome copies.
7. **Interpretation:** sequence similarity supports candidate annotations only. It does not confirm protein identity or function; differential expression does not establish causality or epigenetic/chromatin mechanisms.

## Validation performed

- Inspected the supplied analysis scripts, verified manifest, saved result tables, candidate report, metadata files, and library uncertainty note.
- Counted all four DE table rows and computed `padj < 0.05` counts from the underlying CSVs.
- Confirmed staged paths and file sizes; full source inventory is present.
- Did not execute scripts or computational pipelines. Existing results were copied without modification; no claim of end-to-end reproducibility is made.

## Remaining manual review and GitHub checklist

- Resolve the stale/inconsistent sample manifest and verify the final run-to-stage mapping from primary records.
- Confirm SRA study and run accessions and cite the associated publication.
- Resolve library strandedness and check Salmon command records and version for each sample.
- Provide reference/database provenance, retrieval dates, parameters, and redistribution terms; select one transcriptome FASTA representation.
- Make scripts portable and document complete dependencies, exact commands, parameters, and required external inputs.
- Decide whether additional selected annotation/QC outputs should be staged and verify any summary against source tables.
- Choose a license after rights review; inspect the complete staging tree for secrets, private paths, accidental raw data, and unexpected large files.
- Only after review, create/upload the repository yourself. No remote, commit, authentication, or upload was performed here.


