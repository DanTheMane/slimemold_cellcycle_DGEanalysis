# Reference-based cell-cycle transcriptomics in a slime mold

## Project status

This is an exploratory, reference-based analysis package prepared from the supplied project files. It has not been independently rerun end to end. The repository is staged locally for review; no files have been uploaded.

## Overview

The project examines transcript-level expression across developmental cell-cycle stages in a slime mold using Salmon quantification and DESeq2, with sequence-similarity-based annotation and exploratory prioritization of replication, DNA repair/genome maintenance, chromatin-associated, and nucleotide-metabolism candidates. Candidate assignments are hypotheses for review, not experimentally confirmed protein identities.

## Dataset and samples

The available metadata records SRA study `SRP412754` and run accessions `SRR22704993`–`SRR22705006` (with `SRR22704997` excluded from the retained DE analysis because a single-paired read could only be retrieved). The verified analysis manifest contains 13 retained samples: 3 early S, 2 mid S, 3 late S, 2 early G2, and 3 late G2. The sample manifest and run metadata are included under `results/differential_expression/` and `data/metadata/`.

A saved SRA experiment-summary JSON contains invalid-UID errors; it is retained in the audit source inventory only and is not part of the staged data. Cite the source study and verify metadata/accessions against a current SRA record before publication.

## Differential-expression design and results

The supplied R script uses a DESeq2 design of `~ stage`, sets early S-phase as the reference stage, imports transcript-level Salmon estimates through tximport (`txOut=TRUE`, `countsFromAbundance="no"`), and filters to transcripts with counts >=10 in at least two samples. The saved analysis summary reports 31,729 transcripts before filtering and 23,287 after filtering. Pairwise results use `alpha=0.05`; significance counts below are rows with saved `padj < 0.05` (DESeq2 adjusted p-values).

| Contrast (numerator vs denominator) | Tested transcripts | padj < 0.05 |
| --- | ---: | ---: |
| early G2 phase vs early S-phase | 23,287 | 885 |
| mid S-phase vs early S-phase | 23,287 | 1,566 |
| late S-phase vs early S-phase | 23,287 | 2,587 |
| late G2 phase vs early S-phase | 23,287 | 25 |

These counts were recomputed from the copied CSV tables by counting non-NA adjusted p-values below 0.05 and agree with the row counts and saved analysis summary. They describe the saved results; the analysis was not rerun here. The R script's comparison direction is the stage named first relative to early S-phase. The separate replication-progression outputs use additional sequential contrasts and must be interpreted according to their own file/script definitions.

## Workflow and software evidence

The scripts are not publicly available and can be shared on request.

The saved DESeq2 session record documents R 4.5.3 on Ubuntu 26.04.1 LTS and reports installed package/session details. The separate library uncertainty note reports Salmon 2.8.0 for pilot runs; exact Salmon version and parameters for every retained quantification should be confirmed in per-sample command records before publication. No complete environment lockfile was present.

## Contents

- `scripts/`: source shell, R, and Python scripts available in the supplied project.
- `results/differential_expression/`: four full result tables, candidate tables, analysis summary, sample sheet, verified manifest, and R session record.
- `results/quality_control/`: selected PCA/correlation plots and QC summaries.
- `results/genome_maintenance/`: 15-candidate report and curated replication/repair/nucleotide candidate tables.
- `results/enrichment/`: selected GO and genome-maintenance summary tables.
- `results/figures/`: DESeq2 PCA figure.
- `data/`: selected transcriptome and targeted protein reference material (provisional pending provenance/license review), accession list, and uncertainty notes.
- `docs/inventory.tsv`: file-by-file inclusion/exclusion/inspection recommendations for the supplied source tree.
- `docs/audit-and-validation.md`: audit findings, checks, and release checklist.

Raw FASTQ reads, generated Salmon indices and quantification directories, bundled SRA Toolkit, large local protein databases, caches, and redundant intermediate outputs are excluded. Obtain reads through their SRA accessions and regenerate derived files from documented inputs where needed.

## Reproduction and limitations

The staged R scripts and result tables document substantial analysis steps, but the package is not yet a complete reproducible release. Several scripts use fixed `/home/dan/...` paths or depend on files and software not staged. Required references, exact BLAST/DIAMOND database snapshots, retrieval dates, all parameters, and complete software versions need documentation. Validate dependency versions and expected input/output paths before attempting a rerun.

Library strandedness remains unresolved in the project notes. The note reports higher mapping under IU than ISF/ISR in pilot runs, while explicitly stating that this does not prove an unstranded library protocol. Verify the original library preparation method and confirm per-sample Salmon library settings.

Similarity-based annotations are candidate assignments, not confirmed identities. Differential expression alone does not establish causal regulation, chromatin modification, epigenetic memory, or molecular coordination. These data support exploratory hypothesis generation only.

## Data availability, citations, and license

The recorded study accession is `SRP412754`; listed run accessions and the verified analysis subset are described above. Verify the study record and cite the associated source publication before release. The project has no license selected. Confirm reuse terms for all scripts, transcriptome/protein references, and third-party database-derived annotations before adding a repository license or redistributing reference sequences.

## Before upload

Resolve the manual-review items in `docs/audit-and-validation.md`, especially sample metadata conflicts, strandedness, reference provenance/licensing, portability, and dependency records. Do not describe the full workflow as reproduced until it has been rerun and checked.

