# Fungalise

**Fungalise** is an automated Snakemake-based pipeline for de novo assembly, polishing, and quality evaluation of fungal Oxford Nanopore Technology (ONT) sequencing data.

The pipeline integrates quality control, adapter trimming, read filtering, genome assembly, polishing, telomere visualisation, and assembly completeness assessment into a single reproducible workflow.

--

## Pipeline overview

```
raw reads (.fastq.gz)
    |
    |- NanoPlot
