# Fungalyse

**Fungalyse** is an automated Snakemake-based pipeline for de novo assembly, polishing, and quality evaluation of fungal Oxford Nanopore Technology (ONT) sequencing data.

The pipeline integrates quality control, adapter trimming, read filtering, genome assembly, polishing, telomere visualisation, and assembly completeness assessment into a single reproducible workflow.


## Pipeline overview

```
raw reads (.fastq.gz)
    |
    ├── NanoPlot (raw QC)
    ├── Porechop_abi (adapter trimming)
    ├── Filtlong (read filtering)
    ├── NanoPlot (filtered QC)
    ├── Flye (genome assembly)
    ├── Medaka (polishing)
    ├── TeloVision (telomere-to-telomere analysis)
    └── BUSCO (completeness assessment)
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

Create an `input/` directory in the same location as the Snakefile and place the raw `.fastq.gz` files there:

```
input/
|- species1.fastq.gz
|- species2.fastq.gz
|- ...
```

Each file should be named after the sample/species (without the `.fastq.gz` extension), as this name is used throughout the pipeline.

### 2. Configure the Snakefile

Open the Snakefile and edit the following variables at the top of the file:


```python
SAMPLES = ["species1", "species2"    # List your sample names here (must match filenames in input/)

GENOME_SIZES = {
    "species1": "40m",               # Estimated genome size per species
    "species2": "12m",
}
```

> **Important:** `SAMPLES` and `GENOME_SIZES` must be filled in manually before running the pipeline. Sample names in `SAMPLES` must exactly match the filenames in the `input/` folder (without `.fastq.gz).
> Genome sizes are used by Flye and should be provided in Flye's notation (e.g. `40m` for 40mb, `12.5m` for 12.5 Mb).

Other parameters that can optionally be adjusted:

```python
COVERAGE = 40    # Coverage limit for Flye (default 40x)
THREADS = 4      # Number of threads per rule
```

## Usage

Run the pipeline from the directory containing the Snakefile:

```bash
snakemake --snakefile Snakemake_Fungalyse --use-conda --cores 4
```

To do a dry run first (recommended):

```bash
snakemake --snakefile Snakemake_Fungalyse --use-conda --cores 4 --dryrun
```

If you encounter a lock error:

```bash
snakemake --unlock
snakemake --use-conda --cores 4 --rerun-incomplete
```

## Output

Results are organised by tool and sample under the `output/` directory:

```
Output/
├── nanoplot_raw/{sample}/
├── porechop_output/{sample}/
├── filtlong_output/{sample}/
├── nanoplot_filtered/{sample}/
├── flye_output/{sample}/
├── medaka_output/{sample}/
├── telovision_assembly/{sample}/
└── busco_output/{sample}/
```

Key output files:
- `output/nanoplot_raw/{sample}/NanoPlot-report.html` — raw read QC report
- `output/nanoplot_filtered/{sample}/NanoPlot-report.html` — filtered read QC report
- `output/medaka_output/{sample}/assembly.fasta` — final polished assembly
- `output/telovision_assembly/{sample}/{sample}.html` — telomere visualization
- `output/busco_output/{sample}/{sample}/short_summary.specific.fungi_odb10.{sample}.txt` — BUSCO completeness summary

## Author

Evi van Gorp - Avans University of Applied Sciences, School of Life Sciences and Technology

[LinkedIn](https://www.linkedin.com/in/evi-van-gorp-719543326/)
