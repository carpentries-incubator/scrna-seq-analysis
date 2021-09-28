---
title: "Quality Control & Normalization"
teaching: 15
exercises: 5
questions:
- "What is the aim of normalization?"
objectives:
- "To understand the structure of expression matrix."
- "To use the `Scanpy` package for normalization."
- "To create an object containing expression matrix, barcodes, and cell IDs."
- "Understanding the necessity of normalizing counts for accurate comparison between cells."
keypoints:
- "scRNA-seq requires much pre-processing before analysis can be performed."
---


# Generating Expression Metadata

Sequencing centers deliver the results of scRNA-seq in three formats including `BCL`, `fastq`, and `.mtx`. Raw data for scRNA-seq data are received as `BCL2` or `fastq` files. BCL2 files should be converted into FASTQ files using a command line software called [bcl2fastq](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html). Analysis of data in FASTQ format includes `Quality Control`, `Trimming`, `Alignment`, `Mapping` which are mainly similar to bulk RNA-seq analysis and you can find in   [Data Carpentry Genomics Lessons](https://datacarpentry.org/wrangling-genomics/). Quantification analysis uses statistical analysis and machine learning methods to detect the number of each transcript and count them per cell. Some of the methodologies normalize the counts of transcripts and filter the genes with no significantly different expression levels among which edgeR, DESeq, DESeq2, etc can be mentioned.
The output of quantification analysis is a text file containing gene IDs in rows and cell IDs in columns which is called an expression matrix.
In this curriculum, we will work on the expression matrix and will apply the analysis steps on it.

# Get Data
The dataset which we use for this workshop includes 6 files in `.tsv` format with information about cell barcodes, metadata, cell IDs and gene IDs and one file in `.mtx` format which includes the number of RNAs per cell.


> ## Project Directory
> 
> scRNA-seq analysis workflow begins with a few files and will produce a lot of files. 
> So it is a big data project and it is useful to manage our files and directories.
> For this, create a directory called `scRNA-seq` and four subdirectories called data, scripts, output, and docs.
> 
> ~~~
> $ mkdir -p scRNA/{data,docs,output,scripts}.
> $ ls
> $ cd scRNA/data
> ~~~
> {: .bash}
> 
> As we do for all big data projects, for a better data management in here,
> we can add the date of files generation at the first part of files names. For example, 2021-09-20-normalization.txt.
{: .callout}

> ## Exercise
> 
> Discuss your results with your classmate. What are the advantages and disadvantages of
> file name system suggested? 
> Which system do you suggest for file names which helps for better management of scRNA-seq as a big data project?
> 
>> ## Solution
>> - Advantages:
>> Reproducibility.
>> Easy to track the project progress.
>> Disadvantage:
>> Not all of the collaborators use the same manner for the data management. It makes hard to merge files and data.
> {: .solution}
{: .challenge}

Please download dataset using the link in setup (should be linked) into the data directory using the command below:

~~~
$ wget -c data-link
$ ls
~~~
{: .bash}

~~~
barcodes.tsv.gz  deng-reads.rds  features.tsv.gz  matrix.mtx.gz  molecules.txt reads.rds  reads.txt  TPs.txt  umi.rds
~~~
{: .output}



# Preprocessing

The first step using expression matrix is preprocessing divided into two main steps of preprocessing and normalization.


> ## SCANPY
> [Scanpy](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-017-1382-0) is a 
> large scale toolkit for analysis of single-cell gene expression data. 
> The methods for preprocessing, visualization, clustering, pseudotime and trajectory inference, 
> differential expression testing, and simulation of gene regulatory networks are included. 
> The Python-based implementation of SCANPY efficiently deals with data sets of more than one million cells.
{: .callout}

You can see that there are different data structures. For this lesson, `scanpy` is used in combination with
`pandas` and `numpy` libraries. In the following steps, `matplotlib` will be needed for visualization, too.
For this, the libraries should be imported as below:

~~~
$ import scanpy as sc
$ import pandas as pd
$ import numpy as np
~~~
{: .bash}

Now, configuration settings of scanpy should be performed. Verbosity is
an attribute for management of warning messages. The second line is used
for creating a log file and the thهrd line is the method for general settings
of the graph.


~~~
$ sc.settings.verbosity = 3             # verbosity: errors (0), warnings (1), info (2), hints (3)
$ sc.logging.print_header()
$ sc.settings.set_figure_params(dpi=80, facecolor='white')
~~~
{: .bash}

Which will give you the following output:
~~~
scanpy==1.6.0 anndata==0.7.5.dev7+gefffdfb umap==0.4.2 numpy==1.18.1 scipy==1.4.1 pandas==1.0.3 scikit-learn==0.22.1 statsmodels==0.11.0 python-igraph==0.7.1 leidenalg==0.7.0
~~~
{: .output}


A file is generated to store the analysis results:

~~~
$ results_file = 'write/pbmc3k.h5ad'
~~~
{: .bash}

Based on the different types of files, it is needed to create an object which
contains data of count matrix, annotations, barcodes, etc.
The object is called [`AnnData`](https://anndata.readthedocs.io/en/latest/anndata.AnnData.html).
AnnData stores data in its special format called `h5ad`.
The object named as `adata` is created using the code below:
~~~
$ adata = sc.read_10x_mtx(
$   'data/filtered_gene_bc_matrices/hg19/',  # the directory with the `.mtx` file
$   var_names='gene_symbols',                # use gene symbols for the variable names (variables-axis index)
$   cache=True)                              # write a cache file for faster subsequent reading
~~~
{: .bash}
