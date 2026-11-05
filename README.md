# H3K9me3 ChIP-seq Analysis of HDAC7 Knockdown in Glioblastoma Stem Cells.
**An R/Bioconductor workflow exploring HDAC7-associated changes in repressive chromatin in patient-derived glioblastoma stem cells.**


## Project Overview
Glioblastoma (GBM) exhibits extensive epigenetic plasticity that contributes to tumor-cell identity and therapeutic resistance. My doctoral research investigated HDAC7 as an epigenetic regulator connecting histone H3.3 organization, chromatin state, and stem-like transcriptional programs in patient-derived glioblastoma stem cells (GSCs).

This repository explores publicly available **H3K9me3 ChIP-seq data following HDAC7 knockdown**. H3K9me3 is a repressive histone modification associated with heterochromatin. Comparing its genomic distribution between control and knockdown conditions provides insight into local changes in repressive chromatin.

The analysis forms part of a broader research program integrating epigenomic, transcriptomic, and functional approaches to investigate HDAC7 biology in GBM.


## Research Question

How does HDAC7 knockdown alter the genomic distribution and local enrichment of the hitone repressive mark,H3K9me3, in patient-derived GSCs?

## Hypothesis

HDAC7 inhibition alters the H3K9me3 landscape, including local enrichment of repressive chromatin that may contribute to transcriptional reprogramming in GSCs.

## Data and Experimental Context

| Component | Description |
|---|---|
| Biological model | Patient-derived GB2 glioblastoma stem cells |
| Perturbation | siRNA-mediated HDAC7 knockdown |
| Comparison | siHDAC7 versus siControl |
| Histone modification | H3K9me3 |
| Assay | ChIP-seq |
| Reference genome | Human hg38 |
| Analysis inputs | Deposited BED region files and BigWig signal tracks |
| Background control | Input DNA BigWig track |

Public data are available through [GEO accession GSE286178](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE286178), including the [ChIP-seq subseries GSE286176](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE286176).

| Sample | GEO accession |
|---|---|
| GB2 siControl, H3K9me3 ChIP | [GSM8720290](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM8720290) |
| GB2 siHDAC7, H3K9me3 ChIP | [GSM8720291](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM8720291) |
| GB2 input DNA | [GSM8720292](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM8720292) |


# Full Analysis

**[View the complete rendered CHIP-seq analysis →](https://olahassan000.github.io/HDAC7-GBM-Epigenomics--R/)**

The full R Markdown workflow includes H3K9me3 enrichment analysis in HDAC7-knockdown versus control GSCs, identification and comparison of regions with differential H3K9me3 signal, genome-wide signal profiling and heatmap visualization, genomic annotation of enriched regions, and biological interpretation of HDAC7-associated heterochromatin remodeling.

## Analysis Workflow

### 1. Import and Inspect Genomic Regions

- Import the public control and knockdown BED files.
- Check chromosome labels, coordinates, and interval widths.
- Convert BED coordinates to genomic ranges for downstream analysis.

### 2. Compare Called-Region Coverage

- Summarize interval counts and widths.
- Calculate total genomic coverage.
- Identify shared, control-only, and knockdown-only genomic sequence.

### 3. Construct a Common Region Set

- Merge overlapping regions from both conditions.
- Create a consistent set of **46,511 common regions** for signal comparison.

### 4. Quantify and Compare H3K9me3 Signal

- Extract mean BigWig signal across each common region.
- Calculate knockdown/control signal ratios and log2 fold changes.
- Select regions using an exploratory **1.5-fold linear change threshold**:
  - **Higher in knockdown:** ratio ≥ 1.5.
  - **Lower in knockdown:** ratio ≤ 1/1.5.
  - **Between thresholds:** ratios between these cutoffs.

### 5. Visualize Signal Distributions

- Compare control and knockdown signals using scatter plots.
- Generate region-centered aggregate profiles and heatmaps.
- Include input profiles to inspect background signal.
- Display individual loci and genes of interest using genome-browser-style tracks.

### 6. Annotate Genomic Context

- Annotate common regions using hg38 gene models.
- Compare promoter, exon, intron, UTR, and intergenic assignments.
- Examine associated genes and distances to transcription start sites.
- Interpret selected loci in their genomic context.

## Selected Outputs

The exploratory 1.5-fold selection identified:

| Signal group | Number of regions |
|---|---:|
| Higher in HDAC7 knockdown | 399 |
| Lower in HDAC7 knockdown | 2,484 |
| Between thresholds | 43,628 |

Both selected groups were predominantly assigned to intronic or distal intergenic locations. Aggregate profiles and individual locus tracks illustrate local differences in H3K9me3 signal between conditions.

These outputs distinguish changes in **signal intensity**, **called-region coverage**, and **genomic context**, which address different aspects of chromatin remodeling.

## Tools

| Tool | Purpose |
|---|---|
| R and R Markdown | Analysis, documentation, and report generation |
| GenomicRanges and IRanges | Genomic interval operations |
| rtracklayer | BigWig import and signal extraction |
| ggplot2 | Signal profiles, comparisons, and locus visualization |
| ChIPseeker | Genomic feature and gene annotation |
| GenomicFeatures | Gene coordinates and annotation queries |
| TxDb.Hsapiens.UCSC.hg38.knownGene | hg38 transcript models |
| org.Hs.eg.db and AnnotationDbi | Gene identifier mapping |

## Analysis Scope and Biological Interpretation

This notebook explores one publicly deposited ChIP track per condition together with an input track. It focuses on genomic coverage, signal visualization, and annotation, providing a reproducible workflow for examining the deposited data.

The 1.5-fold cutoff selects regions by effect size. Results are descriptive; replicate-based statistical testing is outside this notebook’s scope. This linear cutoff is distinct from a log2 fold-change threshold of 1.5.

Genomic annotations identify candidate gene associations. Local H3K9me3 changes alone do not establish altered gene expression, direct HDAC7 targets, or heterochromatin spreading. Interpretation considers the location, intensity, and extent of the observed signal alongside the broader study.

## Explore the Analysis

The rendered R Markdown report contains the analysis code, figures, tables, and biological interpretation:

[**Open the complete H3K9me3 ChIP-seq analysis →**](https://olahassan000.github.io/HDAC7-GBM-Epigenomics--R/)



## Study context and disclosure

This repository accompanies the [published HDAC7 study in the Journal of Biological Chemistry](https://www.jbc.org/article/S0021-9258(25)02584-0/fulltext). Interpret this portfolio analysis alongside the paper's methods, data-access information, and experimental findings.

A patent application, **PCT/US2022/077910**, concerns HDAC7-specific inhibitors. Homer Therapeutics, Inc. is developing cancer therapeutics targeting HDAC7.


## Author

**Ola Hassan, PhD**  
Cancer epigenomics · Computational biology · Translational oncology

[GitHub](https://github.com/olahassan000)
