S. aureus Variant Calling Pipeline

Overview

An end-to-end NGS variant-calling workflow for Staphylococcus aureus whole-genome sequencing (WGS) data.

Tools Used

- FastQC — sequencing quality assessment
- Trimmomatic — read trimming and quality filtering
- BWA-MEM — alignment of reads to the reference genome
- SAMtools — SAM/BAM processing, sorting and indexing
- FreeBayes — variant calling

Dataset

- Input: S. aureus paired-end WGS reads — SRA accession "SRR8359173"
- Reference: S. aureus USA300 genome — "GCF_000013425.1"

Workflow

FASTQ → Trimmomatic → BWA-MEM → SAMtools → FreeBayes → VCF

Results

- 58,548 raw variant calls generated using FreeBayes.

«The reported calls represent preliminary variant calls from the implemented workflow and should undergo additional quality filtering and biological validation before being interpreted as confirmed mutations.»

How to Run

1. Download the ".ipynb" notebook from this repository.
2. Open the notebook in Google Colab.
3. Install or verify the required bioinformatics tools and dependencies.
4. Run the notebook cells sequentially.

Author

Vandana Saini
