---
title: "Pre-processing of scRNA-seq using Cellranger"
teaching: 15
exercises: 5
questions:
- "How do pre-process scRNA-seq data using Cellranger?"
objectives:
- "Identify the available tools to preprocess cRNA-seq."
- "Understand how to use Cell Ranger."
keypoints:
- "scRNA-seq requires much pre-processing before analysis can be performed."
---

## Dataset:

Expression data from scRNA-seq experiments represent thousands of reads for thousands of cells. Therefore, the data output can be very large and hard to store in your local machine. YOu will also need higher amounts of memory to analyze.

In this tutorial, We will use Human peripheral blood mononuclear cells (PBMCs) of a healthy female donor aged 25-30 were obtained by 10x Genomics from AllCells.

Libraries were generated from ~16,000 cells (11,996 cells recovered) as described in the Chromium Single Cell 3' Reagent Kits User Guide (v3.1 Chemistry Dual Index) (CG000315 Rev C) using the Chromium X and sequenced on an Illumina NovaSeq 6000 to a read depth of approximately 40,000 mean reads per cell.

##


{% include links.md %}
