# Fungalise

**Fungalise** is an automated Snakemake-based pipeline for de novo assembly, polishing, and quality evaluation of fungal Oxford Nanopore Technology (ONT) sequencing data.

The pipeline integrates quality control, adapter trimming, read filtering, genome assembly, polishing, telomere visualisation, and assembly completeness assessment into a single reproducible workflow.


## Pipeline overview

```
raw reads (.fastq.gz)
    |
    |- NanoPlot (raw QC)
    |- Porechop_abi (adapter trimming)
    |- Filtlong (read filtering)
    |- NanoPlot (filtered QC)
    |- Flye (genome assembly)
    |- Medaka (polishing)
    |- TeloVision (telomere-to-telomere analysis)
    |- BUSCO (completeness assessment)
```

## Requirements

The follwing tools must be installed and available in your environment:
| Tool | Version |
|---|---|
| Snakemake | 9.17.3 |
| NanoPlot | 1.46.2 |
| Porechop_ABI | 0.5.1 |
| Filtlong | 0.3.1 |
| Flye | 2.9.6 |
| Medaka | 2.2.1 |
| TeloVision | 0.3.2.1 |
| BUSCO | 6.0.0 |

Porechop_abi and BUSCO each require their own conda environment (`porechop_env` and `busco_env`). These are refenced in the Snakefile using the `conda:` directive.

## Setup

### 1. Preparation of the input files

### 2. Configure the Snakefile

## Usage

## Output

## Author (???)

Moet ook nog citaties naar de tools vermeld worden?
