# FastQProcessing: RNA-Seq Read-Count Generation and Supporting Scripts

## Overview
This repository contains scripts and pipelines for processing RNA-Seq data, including extracting gene lists, downloading reference genomes, renaming files, and generating read-count TSV files for downstream analysis using DESeq2 in R. The scripts are designed to run on an HPC using the SLURM job scheduler, except where noted otherwise.

## Subdirectories and Scripts

### 1. `Pipeline/`
- **Scripts**:  
  - `FastQ-to-ReadCounts_Pipeline.txt` (step-by-step documented interactive commands)
  - `FastQ-to-ReadCounts_Pipeline.sh` (**optional, automated SLURM batch script**)
- **Purpose**: Processes paired-end RNA-Seq data from FastQ files into read-count TSV files. This includes genome indexing, read alignment, BAM file processing, and read counting.
- **Execution**:  
  - The `.txt` file documents the original interactive workflow, suitable for stepwise or manual execution.
  - The `.sh` script provides an **optional, fully automated alternative** for running the entire pipeline as a single SLURM batch job on an HPC.
- **Dependency**: Requires the reference genome and annotation files generated by the `GetReference/Get_Reference_Genome.sh` script.
- **Output**: Read-count TSV files for each sample.

> **Note:**  
> The `Pipeline/` directory now supports both the original interactive approach (`FastQ-to-ReadCounts_Pipeline.txt`) and an **optional, fully automated approach** (`FastQ-to-ReadCounts_Pipeline.sh`).  
> Use the `.sh` script if you prefer to run the entire workflow as a single SLURM job, or follow the `.txt` for stepwise/manual execution.

### 2. `ExtractGenes/`
- **Script**: `Extract_Genes.sh`
- **Purpose**: Extracts gene lists for specific chromosomes (e.g., X, Y, autosomes, mitochondrial genome) from a GTF file, used for filtering and characterization in MaleLimitedEvo/DESeq2Run/DESeq2Run.R.
- **Execution**: Runs on an HPC using SLURM.
- **Output**: Chromosome-specific gene lists in TSV format.

### 3. `GetReference/`
- **Script**: `Get_Reference_Genome.sh`
- **Purpose**: Downloads and prepares the Drosophila melanogaster reference genome and annotation files. It also generates indices for BWA, samtools, and STAR.
- **Execution**: Runs on an HPC using SLURM.
- **Output**: Reference genome files, GTF annotation file, and genome indices.

### 4. `tsvFileRenaming/`
- **Script**: `renameTSVfiles.sh`
- **Purpose**: Renames TSV files based on their sample name components for easier sorting and analysis in R.
- **Execution**: Runs on an HPC using SLURM.
- **Output**: Renamed TSV files.

### 5. `fastqFileRenaming/`
- **Script**: `renameFASTQfiles.sh`
- **Purpose**: Renames FastQ files based on a predefined mapping for consistency and clarity.
- **Execution**: Does not require SLURM; can be run locally or on a server or an HPC.
- **Output**: Renamed FastQ files.

## Software Requirements
- **STAR**: v2.7.9a or later
- **GATK**: v4.2.3.0-1 or later
- **HTSeq**: v0.13.5 or later
- **GNU parallel**: Required for parallelizing sample processing
- **SLURM**: Required for job scheduling on an HPC
- **rename**: Required for renaming files in `renameFASTQfiles.sh`

## Reference Genome and Annotation
- **Reference Genome**: Drosophila melanogaster BDGP6.28, release 102
- **Annotation File**: GTF file from the same release

## Notes
- Ensure all required software is installed and accessible in your environment before running the scripts.
- Some scripts are designed to run on an HPC using SLURM. Modify the SLURM directives as needed for your system.
- The `Pipeline/` directory now provides both a stepwise documented workflow and an **optional, fully automated SLURM script** for RNA-Seq processing.  
  Choose the approach that best fits your workflow: interactive/manual (`.txt`) or automated batch (`.sh`).

## Contact
For questions or issues, contact [Karl Grieshop](https://github.com/karlgrieshop).