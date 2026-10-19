# CRC-scRNA-Seq-Analysis
scRNA-seq analysis of colorectal cancer organoids treated with YAP activator and/or TGF-β (GSE333618). QC, clustering, cell-state annotation, GSEA and replicate-level pseudobulk in R/Seurat. Independent reanalysis of public data.

# YAP and TGF-β cell-state shifts in colorectal cancer organoids (scRNA-seq)

An independent reanalysis of public single-cell RNA-seq data
([GSE333618](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE333618)):
a patient-derived colorectal cancer organoid line grown in collagen and treated
with a YAP activator, TGF-β1, both, or neither (2 replicates per condition,
~28,000 cells before QC, BD Rhapsody).

**Question:** how do YAP activation and TGF-β, alone and combined, reshape
cell states in CRC organoids?

## Main findings
- YAP activation is the largest source of transcriptional variation; replicates
  show no batch effect.
- Adding TGF-β to YAP shifts cells from a *TAC3*-high state to an
  *ANKRD1*/*TAGLN*-high state. Both replicates of each condition agree.
- The shifted state is enriched for Hallmark EMT genes, both in a cluster
  comparison and in a cluster-independent pseudobulk comparison of conditions.
- TGF-β alone produced only a modest change relative to control.

## Methods
Cell-level QC with thresholds chosen from the data (mitochondrial content is
high in this chemistry, so standard 5-10% cutoffs were not used), normalisation,
PCA, graph-based clustering and UMAP, marker-based state annotation, cell-state
composition per replicate, GSEA (clusterProfiler, MSigDB Hallmark), and
pseudobulk differential expression (edgeR/limma-voom).

## Robustness checks
- Clustering at two resolutions (0.3 and 0.5) gave the same main states.
- Mitochondrial cutoff of 40% vs 50% removed a similar fraction from every sample.
- EMT enrichment was tested before and after removing cluster-defining genes.
- A low-depth cluster was identified and handled explicitly.

## Limitations
One organoid line and two replicates per condition, so results are descriptive
and not generalisable. Cluster-vs-cluster p-values treat cells as independent
and are inflated. Reanalysis of an unpublished dataset: no published figures
to compare against, and conclusions are mine, not the original authors'.

## Reproducing
Run scripts in `scripts/` in order. Raw data are downloaded by
`scripts/00_download.R` and are not stored in this repo.
