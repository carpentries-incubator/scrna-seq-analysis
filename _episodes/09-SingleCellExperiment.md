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
 
 
> umi <- SingleCellExperiment(
    assays = list(counts = as.matrix(molecules)), 
    colData = anno
)

> umi
~~~
{: .bash}

~~~
class: SingleCellExperiment 
dim: 19027 864 
metadata(0):
assays(1): counts
rownames(19027): ENSG00000237683 ENSG00000187634 ... ERCC-00170 ERCC-00171
rowData names(0):
colnames(864): NA19098.r1.A01 NA19098.r1.A02 ... NA19239.r3.H11
  NA19239.r3.H12
colData names(5): individual replicate well batch sample_id
reducedDimNames(0):
spikeNames(0):
altExpNames(0):
~~~
{: .output}

To remove genes with 0 expression, the data matrix should be subset. For this, we can use <a href="http://www.r-tutor.com/r-introduction/basic-data-types/logical">logical values</a> which is a very useful method for subsetting dataframes and comparison between variables. For subsetting our data, run the code below:

~~~
keep_feature <- rowSums(counts(umi) > 0) > 0

keep_feature
~~~
{: .bash}

~~~
ENSG00000237683 ENSG00000187634 ENSG00000188976 ENSG00000187961 ENSG00000187583 
           TRUE            TRUE            TRUE            TRUE            TRUE 
ENSG00000187642 ENSG00000188290 ENSG00000187608 ENSG00000188157 ENSG00000237330 
           TRUE            TRUE            TRUE            TRUE            TRUE 
ENSG00000131591 ENSG00000162571 ENSG00000186891 ENSG00000186827 ENSG00000078808 
           TRUE            TRUE            TRUE            TRUE            TRUE 
ENSG00000176022 ENSG00000184163 ENSG00000160087 ENSG00000162572 ENSG00000131584 
           TRUE            TRUE            TRUE            TRUE            TRUE 
ENSG00000169972 ENSG00000127054 ENSG00000224051 ENSG00000169962 ENSG00000107404 
           TRUE            TRUE            TRUE            TRUE            TRUE 
ENSG00000162576 ENSG00000175756 ENSG00000221978 ENSG00000224870 ENSG00000242485 
           TRUE            TRUE            TRUE            TRUE            TRUE 
ENSG00000235098 ENSG00000205116 ENSG00000179403 ENSG00000215915 ENSG00000160072 
           TRUE            TRUE            TRUE            TRUE            TRUE 
           .
           .
           .
           ENSG00000116752 ENSG00000175984 ENSG00000116748 ENSG00000213281 ENSG00000009307 
           TRUE            TRUE            TRUE            TRUE            TRUE 
 [ reached getOption("max.print") -- omitted 18027 entries ]
~~~
{: .output}

 Since, we want to filter genes with zero expression levels, code will show all the genes with expression levels higher than zero with TRUE and each gene with zero expression levels are demonstrated as FALSE. Now, we can apply filteration by running code below:
~~~
> umi <- umi[keep_feature, ]
> umi
~~~
{: .bash}

~~~
class: SingleCellExperiment 
dim: 18726 864 
metadata(0):
assays(1): counts
rownames(18726): ENSG00000237683 ENSG00000187634 ... ERCC-00170 ERCC-00171
rowData names(0):
colnames(864): NA19098.r1.A01 NA19098.r1.A02 ... NA19239.r3.H11
  NA19239.r3.H12
colData names(5): individual replicate well batch sample_id
reducedDimNames(0):
spikeNames(0):
altExpNames(0):
~~~

{: .output}

Now, you can make a comparison between umi before and after filteration.



There are many alternative sequencing data for different feature types in scRNA-seq experiment such as spike-in transcripts in plate-based experiments, antibody tags in CITE-seq experiments, CRISPR tags, and allele information for tasts including various genotypes. All these features can be managed using a method in the SingleCellExperiment called “alternative Experiments”. This helps to keep and analyze various features separately while synchronization of operations on a single object is also done which makes it easierto interpret the results.
In the dataset of Tung, we have spike-ins and mitochondrial gene which are considered as features for filtering data. Data for each feature are represented in one separate row.




{% include links.md %}
