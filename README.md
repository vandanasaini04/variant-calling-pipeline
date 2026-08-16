# S. aureus USA300 Variant Calling Pipeline

## Overview

An end-to-end NGS variant-calling workflow for *Staphylococcus aureus* USA300 whole-genome sequencing (WGS) data.

## Tools Used

- FastQC — sequencing quality assessment
- Trimmomatic — read trimming and quality filtering
- BWA-MEM — alignment to the reference genome
- SAMtools — SAM/BAM processing, sorting and indexing
- FreeBayes — haploid variant calling

## Dataset

- Input: *S. aureus* USA300_FPR3757 paired-end WGS reads — SRA accession `ERR17521341`
- Reference: *S. aureus* USA300_FPR3757 — `GCF_000013465.1`

## Workflow

FASTQ → FastQC → Trimmomatic → BWA-MEM → SAMtools → FreeBayes → VCF → Variant Filtering

## Results

- 99.88% reads mapped to the reference genome
- 99.19% properly paired
- 465 raw FreeBayes variant calls
- 63 filtered variant calls

## How to Run

1. Download the `.ipynb` notebook from this repository.
2. Open the notebook in Google Colab.
3. Install or verify the required bioinformatics tools and dependencies.
4. Run the notebook cells sequentially.

## Author

Vandana Saini
