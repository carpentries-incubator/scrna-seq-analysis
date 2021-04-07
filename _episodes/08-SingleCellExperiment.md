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
After quantification analysis, we have an expression matrix in which each row represent one gene and column represents one cell.
Most of the time there are cells with poor quality and cells with zero expression levels in all of the cells.
If we dont filter cells and genes with low quality, this will cause noise and biase in downstream stages of the analysis.
One of the most popular packages for filtering, dimentionality reduction, checking for spike-in information, and methods for metadata analysis is
<a href="https://bioconductor.org/packages/release/bioc/html/SingleCellExperiment.html">SingleCellExperiment</a>.
This is a S4 class developed by <a href="https://www.bioconductor.org/">Bioconductor</a> for storing data obtained from scRNA-seq analysis.
This class includes methods for analysis of single cell RNA-seq. For using SingleCellExperiment, it should be installed. The installation method is explained in
<a href="https://carpentries-incubator.github.io/scrna-seq-analysis/setup.html">Setup</a> page of the lasson.
Two files including molecules.txt and annotation.txt will be used in this section that you can download from figshare in Setup page.

For the analysis, the directory should be set up. 'setwd' will direct you to the directory containing scRNA-Seq-data which is the working directory.
Snter the exact directory:
setwd('the/path/to/scRNS-Seq-data')

Now, check if you are in the right directory:
getwd()

As you can see in the 'scRNS-Seq-data' directory, the format of molecules.txt and annotation.txt files is '.txt'.
For reading this file, a function is used called  <a href="https://www.rdocumentation.org/packages/utils/versions/3.6.2/topics/read.table">read.table()</a>. This function reads a file into data frame in table format. The file can be comma delimited or tab or any other delimiter specified by parameter "sep=". If the parameter "header=" is "TRUE", then the first row will be treated as the column names. To know more about the arguments of read.table() function, use this code:
 ~~~
?read.table
~~~
{: .bash}

To import the data of molecules and annotation files, use this code:
 ~~~
?read.table
molecules <- read.table("molecules.txt", sep = "\t")
anno <- read.table("annotation.txt", sep = "\t", header = TRUE)
~~~
{: .bash}

Now, 'head' will help to checkout data in the file:
 ~~~
head(reads[ , 1:3])
head(anno)
~~~
{: .bash}

In order to standardize our dataset, SingleCellExperiment object should be created.
For this, create a SCE object using the code below:

 ~~~
 
 
umi <- SingleCellExperiment(
    assays = list(counts = as.matrix(molecules)), 
    colData = anno
)
~~~
{: .bash}

To remove genes with 0 expression the matrix, run the code below:

~~~
keep_feature <- rowSums(counts(umi) > 0) > 0
umi <- umi[keep_feature, ]
~~~
{: .bash}

{% include links.md %}

