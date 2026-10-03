# S. aureus USA300 WGS Variant-Calling Pipeline

An end-to-end whole-genome sequencing variant-calling workflow for *Staphylococcus aureus* USA300, implemented in Google Colab. Covers read acquisition, quality control, trimming, reference alignment, BAM processing, variant calling, filtering, validation, and gene-level annotation.

---

## Biological Question

> What high-confidence genomic variants are present in a sequenced *S. aureus* USA300 isolate relative to the USA300_FPR3757 reference genome?

---

## Dataset & Reference

| Item | Value |
|------|-------|
| Sample | ERR17521341 (paired-end Illumina WGS) |
| Reference | USA300_FPR3757 |
| Reference accession | NC_007793.1 / GCF_000013465.1 |
| Organism | *Staphylococcus aureus* subsp. aureus USA300 |

---

## Tools & Stack

| Tool | Version | Purpose |
|------|---------|---------|
| SRA Toolkit | 3.0.3 | Read acquisition |
| FastQC | 0.11.9 | Sequencing quality assessment |
| Trimmomatic | 0.39 | Adapter trimming and quality filtering |
| BWA-MEM | 0.7.17 | Read alignment to reference |
| SAMtools | 1.13 | SAM/BAM processing, sorting, indexing |
| FreeBayes | 1.3.6 | Haplotype-based variant calling |
| Python | 3.x | Filtering, validation, annotation |
| Pandas | — | Results processing and output |

---

## Workflow

```
ERR17521341 paired-end reads
          │
          ▼
      FastQC
   quality assessment
          │
          ▼
    Trimmomatic
  adapter trimming
  SLIDINGWINDOW:4:15
  MINLEN:36
          │
          ▼
     BWA-MEM
  read → reference
  alignment
          │
          ▼
    SAMtools
  SAM → BAM
  sort → index
          │
          ▼
  Alignment QC
  99.88% mapped
  99.19% properly paired
          │
          ▼
    FreeBayes
  variant calling
  (--ploidy 1)
          │
          ▼
  465 raw variants
          │
          ▼
  QUAL > 1000
  AF = 1
  DP > 10
          │
          ▼
  57 high-confidence
      variants
          │
          ▼
  57/57 validation
      PASS
          │
          ▼
  GFF3 gene annotation
  37 genic / 20 intergenic
```

---

## Results

### Alignment Statistics

| Metric | Value |
|--------|-------|
| Total reads | 12,249,987 |
| Mapped reads | 12,235,896 |
| Mapping rate | **99.88%** |
| Properly paired | **99.19%** |

### Variant Calling

| Stage | Count |
|-------|-------|
| Raw FreeBayes variant records | 465 |
| After filtering (QUAL>1000, AF=1, DP>10) | **57** |
| Validation pass (57/57) | ✅ PASS |

### Filtering Criteria

| Filter | Threshold | Rationale |
|--------|-----------|-----------|
| QUAL | > 1000 | High variant-call quality |
| AF | = 1 | Fixed alternate allele (homozygous variant) |
| DP | > 10 | Minimum read depth coverage |

### Gene Annotation

| Category | Count |
|----------|-------|
| Genic variants | 37 |
| Intergenic variants | 20 |
| Total annotated | 57 |

**Selected genes with variants:**

| Gene | Function |
|------|----------|
| `rpoC` | RNA polymerase β' subunit |
| `recF` | DNA repair and recombination |
| `agrC` | Accessory gene regulator C (quorum sensing / virulence) |
| `hemE` | Heme biosynthesis |
| `dnaJ` | Heat shock chaperone |
| `mnhD1` | Multidrug resistance efflux |
| `bioA` | Biotin biosynthesis |
| `rrf` | Ribosomal RNA |

> **Important:** These are sequence-based genomic variants relative to the reference genome. Gene annotations indicate the genomic location of each variant. Functional consequence (synonymous/nonsynonymous) and phenotypic impact have not been experimentally validated.

---

## How to Run

This pipeline runs in Google Colab. No local installation required.

1. Open the notebook in Google Colab
2. Run all cells sequentially (Runtime → Run all)
3. Total runtime: approximately 3–4 hours

> **Note:** Google Colab resets the environment between sessions. All tool installations and file downloads are included in the notebook and will re-run automatically.

---

## Output Files

| File | Description |
|------|-------------|
| `results/USA300_ERR17521341.annotated.tsv` | 57 high-confidence variants with gene annotation |

The notebook also generates the raw VCF (465 variants) and the
filtered VCF (57 variants) when run. These are not stored in this
repository; their results are shown in the notebook outputs.

---

## Limitations

- Duplicate reads were not marked prior to variant calling
- Variant annotation identifies genomic location (genic/intergenic) but does not predict functional consequence
- Results represent computational predictions and require experimental validation
- `agrC` and other virulence-associated gene variants require phenotypic confirmation before biological interpretation

---

## Author

Vandana Saini
[github.com/vandanasaini04](https://github.com/vandanasaini04)
