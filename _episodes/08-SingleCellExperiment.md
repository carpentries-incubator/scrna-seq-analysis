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
- "Filtering cells and genes with poor quality"
keypoints:
- "There are cells with poor quality of gene expression in expression dataset."
- "There are genes with zero expression level in expression matrix."
- "Expression matrix should be cleaned before downstream analysis."
- "Cleaning of expression matrix helps to improve results and remove noises and bias during the analysis."
---

The important point dealing with scRNA-seq data is to understand the difference between UMI and no-UMI datasets. This makes it aeasy to deal with each type of dataset.
# First of all I had downloaded data from the link.
#Then put all data into the data folder.
# Then I set the orking directory to the current one.
setwd('/home/eli/Desktop/scRNS-Seq-data')

#and checked if I have done this right.
getwd()

#Then for pre-processing I used the following variable:
molecules <- read.table("molecules.txt", sep = "\t")

## For installation of "SingCellExperiment",
#first I should install the BiocManager. SO I ran this command.
if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")

# In the following, I want to install the class.
BiocManager::install("SingleCellExperiment")

{% include links.md %}

