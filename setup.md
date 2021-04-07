---
title: Setup
---
<h3 id="general">Overview</h3>
This workshop is developed to be run using <a href="https://www.bioconductor.org/">Bioconductor</a> in the R programming environement. For this, Rstudio is required in general. However, this lesson is run on pre-imaged Amazon Web Services (AWS) instances. With the exception of analysis of spreadsheet data files, all of the software and data used in the workshop are hosted on an Amazon Machine Image (AMI). Please follow the instructions below to prepare your computer for the workshop.

<h3 id="general">Software</h3>

This lesson is designed using Bioconductor packages which work in R programming environment.
For this, Rstudio will be used. For downloading and installation, go to <a href="https://www.rstudio.com/">Rstudio</a> and download the desired
version based on your operation system.

<h3 id="general">SingleCellExperiment</h3>
For installation of SingleCellExperiment class, it is recommended to refer to <a href="https://bioconductor.org/packages/release/bioc/html/SingleCellExperiment.html"> here</a>
  and follow uo the instruction. However, in this workshop, it is possible to install SingleCellExperiment in Rstudio using the following code:
  ~~~
if (!requireNamespace("BiocManager", quietly = TRUE)) 
  install.packages("BiocManager")
  BiocManager::install("SingleCellExperiment")
~~~
{: .bash}

   
{% include links.md %}
