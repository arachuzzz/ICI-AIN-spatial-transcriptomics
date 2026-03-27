# 20260327 Integrated Spatial and Single-Cell Transcriptomics of Matched Human Kidney Biopsies Reveals Distinct Immune Architecture in Immune Checkpoint Inhibitor-Associated Acute Kidney Injury

## Overview

This repository contains the analysis code for the above manuscript. We performed integrated CosMx high-plex spatial transcriptomics (319,141 cells; 1,000-gene panel) and single-cell FFPE RNA sequencing (scFFPE; ~51,247 cells post-doublet removal) on matched formalin-fixed, paraffin-embedded (FFPE) kidney biopsy specimens from four cases:

| Sample | Condition | Abbreviation |
|--------|-----------|--------------|
| S0 | T-cell-mediated rejection (TCMR) | Rejection |
| S1 | ICI-associated acute interstitial nephritis | ICI-AIN |
| S2 | Drug-induced acute interstitial nephritis | Drug-AIN |
| S3 | ICI-associated acute interstitial nephritis | ICI-AIN |

## Repository Structure

All analysis scripts are R Markdown (`.Rmd`) files, numbered in recommended execution order:

### scFFPE Single-Cell Analysis Pipeline

| # | File | Description | Manuscript |
|---|------|-------------|------------|
| 01 | `01_scFFPE_preprocessing.Rmd` | Quality control, SCTransform normalization, Harmony integration, doublet removal (scDblFinder), CD45 annotation | Methods |
| 02 | `02_scFFPE_celltype_annotation.Rmd` | Marker-based cell type annotation for major and detailed subtypes | Methods |
| 03 | `03_scFFPE_three_group_DEG.Rmd` | Whole-cell and cell-type-specific DEG analysis across three conditions (ICI-AIN vs Rejection vs Drug-AIN) | Methods |
| 04 | `04_scFFPE_ICI_signature_discovery.Rmd` | Identification of ICI-AIN-specific gene signatures (11 signatures, 43 unique genes); CosMx panel overlap analysis | Figure 2, Suppl Table 1 |

### CosMx Spatial Transcriptomics Pipeline

| # | File | Description | Manuscript |
|---|------|-------------|------------|
| 05 | `05_CosMx_SCTransform_annotation.Rmd` | SCTransform normalization, Harmony batch correction, marker-based hierarchical cell type annotation (module score approach) | Methods, Figure 1 |
| 06 | `06_CosMx_signature_projection.Rmd` | Projection of scFFPE-derived signatures onto CosMx spatial data using AddModuleScore | Methods, Figure 2 |

### Figure Generation

| # | File | Description | Manuscript |
|---|------|-------------|------------|
| 07 | `07_Figure1_Figure2_overview.Rmd` | Study design overview, spatial cell type maps, UMAP visualizations, cell type composition | Figure 1, Figure 2 (A–B) |
| 08 | `08_Figure2C_pseudobulk_heatmap.Rmd` | Pseudobulk heatmap of ICI-specific DEGs across cell lineages and conditions | Figure 2C |
| 09 | `09_Figure3_spatial_niche.Rmd` | Kernel density estimation, immune-tubule distance analysis, DBSCAN clustering, spatial signature distribution, Ripley's K function | Figure 3 |
| 10 | `10_Figure4_T_myeloid_interaction.Rmd` | Nearest-neighbor distance, co-localization index, high-score cell overlap, spatial correlation (Ripley's K) between T cells and myeloid cells | Figure 4 |

### Supplemental Figures

| # | File | Description | Manuscript |
|---|------|-------------|------------|
| 11 | `11_SuppFig5_CXCR3_CXCL9_10.Rmd` | CXCR3-CXCL9/10 chemokine axis expression analysis (CosMx + scFFPE cross-platform validation) | Suppl Figure 5 |
| 12 | `12_SuppFig5_highmag_images.Rmd` | High-magnification spatial images of representative regions with automated ROI selection | Suppl Figure 5 |

## Software and Key Packages

All analyses were performed in R. Key packages and versions:

| Package | Purpose |
|---------|---------|
| **Seurat** (v5.4.0) | Single-cell and spatial data analysis |
| **SCTransform** | Variance-stabilizing normalization |
| **Harmony** | Batch correction across samples |
| **scDblFinder** | Doublet detection and removal |
| **spatstat** | Spatial statistics (Ripley's K, kernel density) |
| **dbscan** | Density-based spatial clustering |
| **ggplot2** / **patchwork** | Visualization |
| **pheatmap** | Heatmap generation |
| **ggpubr** / **rstatix** | Statistical testing |

## Data Availability

- **CosMx spatial transcriptomics data**: [GEO accession to be added]
- **scFFPE single-cell RNA-seq data**: [GEO accession to be added]
- **CosMx gene panel**: NanoString CosMx™ Human Universal Cell Characterization Panel (1,000 genes)

## Notes

- All Rmd files were developed and executed in RStudio with `renv` for package management.
- CosMx data was normalized with SCTransform and batch-corrected with Harmony (replacing earlier NormalizeData-based pipelines).
- Cell type annotation used a marker-based module score approach rather than label transfer, due to limited gene overlap (~8%) between scFFPE and the CosMx 1,000-gene panel.
- File paths in the scripts are specific to the original analysis environment and will need to be updated to run on a different system.

## Contact

Hiroyuki Arai  
[Washington University in St. Louis]  
[araih@wustl.edu]

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
