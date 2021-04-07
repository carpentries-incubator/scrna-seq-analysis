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
For this, we are using the dataset provided in 

{% include links.md %}
