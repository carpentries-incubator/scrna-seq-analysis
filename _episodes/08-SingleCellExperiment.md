---
title: "SingleCellExperiment Construction"
teaching: 45
exercises: 15
questions:
- "What is SingleCellExperiment?"
- "Why it it important to clean expression matrix in scRNA-seq data analysis?"
- "How to assess quality of reads and cells?"

objectives:
- "Explain the SingleCellExperiment class"
- "Create SingleCellExperiment class"
- "Quality control of cells and reads"
- "Filtering cells and genes with poor quality
keypoints:
- "There are cells with poor quality of gene expression in expression dataset."
- "There are genes with zero expression level in expression matrix."
- "Expression matrix should be cleaned before downstream analysis."
- "Cleaning of expression matrix helps to improve results and remove noises and bias during the analysis."
---

The important point dealing with scRNA-seq data is to understand the difference between UMI and no-UMI datasets. This makes it aeasy to deal with each type of dataset. 

{% include links.md %}
