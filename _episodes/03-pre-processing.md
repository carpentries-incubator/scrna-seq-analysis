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

Expression data from scRNA-seq experiments represent thousands of reads for thousands of cells. Therefore, the data output can be very large and hard to store in your local machine. You will also need higher amounts of memory to analyze.

In this tutorial, We will use Human peripheral blood mononuclear cells (PBMCs) of a healthy female donor aged 25-30 were obtained by 10x Genomics from AllCells.

Libraries were generated from ~16,000 cells (11,996 cells recovered) as described in the Chromium Single Cell 3' Reagent Kits User Guide (v3.1 Chemistry Dual Index) (CG000315 Rev C) using the Chromium X and sequenced on an Illumina NovaSeq 6000 to a read depth of approximately 40,000 mean reads per cell.

## Generation of count matrix:

In this part, we will generate the count matrix from the raw sequencing data. After sequencing, the output generated from the sequencing machine will be either output the raw sequencing data as BCL or FASTQ format. Using this raw sequence, we will generate the count matrix.

When using 10X Genomics library preparation method, then the Cell Ranger pipeline is most ideal way to pre-process the data. Make sure that you installed the Cell Ranger version 6 (see the instructions). Using `cellranger`, we can genome mapping, UMI filtering, UMI dedeplication and cell filtering. We will start with  

```
cellranger count --id=sample345 \
                   --transcriptome=/opt/refdata-gex-GRCh38-2020-A \
                   --fastqs=/fastq_path \
                   --sample=cell \
                   --expect-cells=1000 \

```

{% include links.md %}
