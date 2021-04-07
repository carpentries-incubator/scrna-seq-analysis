---
title: "Management of Expression Matrix"
teaching: 40
exercises: 20
questions:
- "What is SingleCellExperiment class?"
- "How to filter genes with zer expression level?"
objectives:
- "Define control features of the expression matrix"
- "Calculate the quality matrix"
keypoints:
- "In scRNA-seq data analysis, there are always a number of genes with zero expression levels."
- "Quality control for genes and cells in this analysis is important."
---
Expression matrix is created after mapping and quanitifation of expression levels of genes.
The quality control is applied on expression matrix in scRNA-seq analysis to filter all cells and genes with poor quality.
Inadequate filteration leads to noise and biase in biological assessments in the downstream stages.
This stage is performed using different approaches and metrics because it has no standard way. However, we are aiming to do this 
in an optimal approach but one should be careful following the codes in each experiment.
For this, we are using the dataset provided in <a href="https://figshare.com/articles/dataset/Single-cell_RNA-seq_data_from_microfluidic_emulsion/5715025">figshare</a>.

<h2 id="general">SingleCellExperiment</h2>

<a href="https://bioconductor.org/packages/release/bioc/html/SingleCellExperiment.html">SingleCellExperiment</a> is a S4 class developed by Bioconductor to stor data obtsined
from single cell RNA sequencing experiments. This includes methods required for different steps of scRNA-seq data processing and analysis including dimensionality reduction, library size, and cells and genes data management. 


{% include links.md %}
