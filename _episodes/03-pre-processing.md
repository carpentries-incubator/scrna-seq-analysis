---
title: "Pre-processing of scRNA-seq using Cellranger"
teaching: 15
exercises: 5
questions:
- "How do pre-process scRNA-seq data using cellranger?"
objectives:
- "Identify the available tools to preprocess cRNA-seq."
- "Understand how to use Cell Ranger."
keypoints:
- "scRNA-seq requires much pre-processing before analysis can be performed."
---

## Dataset:

Expression data from scRNA-seq experiments represent thousands of reads for thousands of cells. Therefore, the data output can be very large and hard to store in your local machine. You will also need higher amounts of memory to analyse.

In this tutorial, We will use Human peripheral blood mononuclear cells (PBMCs) of a healthy female donor aged 25-30 were obtained by 10x Genomics. Libraries were generated from ~16,000 cells (11,996 cells recovered) as described in the Chromium Single Cell 3' Reagent Kits User Guide (v3.1 Chemistry Dual Index) (CG000315 Rev C) using the Chromium X and sequenced on an Illumina NovaSeq 6000 to a read depth of approximately 40,000 mean reads per cell.

.
![Figure4](https://github.com/user-attachments/assets/7861cebd-2eea-4ed7-853d-5806435b756b)


## Generation of count matrix:

In this part, we will generate the count matrix from the raw sequencing data. After sequencing, the output generated from the sequencing machine will be either output the raw sequencing data as BCL or FASTQ format. Using this raw sequence, we will generate the count matrix.

When using 10X Genomics library preparation method, then the Cell Ranger pipeline is most ideal way to pre-process the data. Make sure that you installed the Cell Ranger version 6.1 (see the instructions). Using `cellranger`, we can genome mapping, UMI filtering, UMI dedeplication and cell filtering.  


{% include links.md %}
