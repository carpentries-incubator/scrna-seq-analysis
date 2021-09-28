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

`sc.read_10x_mtx` is used for reading expression data matrix. `hg19` is the directory
where `.mtx` file is stored. `var_names` is set to use gene_symbols. `cahe=True` is
the code to write a cache file for faster subsequent reading.

~~~
... reading from cache file cache/data-filtered_gene_bc_matrices-hg19-matrix.h5ad
~~~
{: .output}

Now, it is possible to check out the contents of `adata` object:

~~~
$ adata
~~~
{: .bash}

~~~
AnnData object with n_obs × n_vars = 2700 × 32738
    var: 'gene_ids'
~~~
{: .output}

The output shows that there are 2700 columns containing observations and 32738 rows including
the variables with gene_id information in the reads count expression matrix.

# Preprocessing & Normalization

Expression matrix contains all the genes and their expression levels. As the first step of
filtering, it is possible to find the first twenty genes with highest expression levels using the code below:

~~~
$ sc.pl.highest_expr_genes(adata, n_top=20, )
~~~
{: .bash}


~~~
Figure should be added.
~~~
{: .output}

Usually, filtering is applied on two dimensions of the expression matrix: cells and genes.
For this, scanpy includes four important filteration functions included in `pp` (preprocessing) module: `filter_cells`, 
`filter_genes`, and `filter_highly_variable_genes`, and `normalize_total`. Each function has parameter.
Here, some challenges are required!

> ## Exercise
>
> Which one of the following options can descripe `min_counts` better?
>
> 1) Minimum number of genes required for a count to pass filtering.
> 2) Minimum number of counts required for a cell to pass filtering.
> 3) Minimum number of counts required for a gene to pass filtering.
> 4) Minimum number of cells required to pass filtering.
>
>> ## Solution
>> Option No.2. 
> {: .solution}
{: .challenge}

In the same way, it is possible to explain `min_genes`, `min_cells`, `max_counts`, and `max_genes`, etc,.

> ## Exercise
>
> Which one of the following options can descripe `n_top_genes` better?
>
> 1) Number of highly-variable genes to remove.
> 2) Number of highly expressed genes to keep.
> 3) Number of highly-variable genes to keep. Mandatory if flavor='seurat_v3'.
> 4) Number of highly expressed genes to remove.
>
>> ## Solution
>> Option No.3. 
> {: .solution}
{: .challenge}

Now, basic and actual filtering can be performed.


~~~
$ sc.pp.filter_cells(adata, min_genes=200)
$ sc.pp.filter_genes(adata, min_cells=3)
~~~
{: .bash}


~~~
filtered out 19024 genes that are detected in less than 3 cells
~~~
{: .output}

One main step for quality control of expression matrix is to achieve the information about
the proportion of mitochondrial genes.

> ## Mitochondiral genes a challenge for scRNA-seq 
> Cells with poor quality in scRNA-sq contain high proportions of mitochondrial genes. 
> These cells are assumed to be discarded before entering into the droplet.
> Not filtering mitochondrial genes can cause formation a separate cluster in the further steps.
{: .callout}

Quality control is performed using `calculate_qc_metrics` function in `pp` module of scanpy using the code below:

~~~
$ adata.var['mt'] = adata.var_names.str.startswith('MT-')  
$ sc.pp.calculate_qc_metrics(adata, qc_vars=['mt'], percent_top=None, log1p=False, inplace=True)
~~~
{: .bash}

This code annotates the group of mitochondrial genes as 'mt'.

Now, visualization is possible.

> ## Violin Plots 
> - [Violin plots](https://en.wikipedia.org/wiki/Violin_plot) are used for visualization of quality control results in scRNA-seq.
> - The number of genes expressed in the count matrix, the total counts per cell, and the percentage of counts in mitochondrial genes.
> - These plots are similar to box plots with addition of the probability density of the data at different values.
{: .callout}

~~~
$ sc.pl.violin(adata, ['n_genes_by_counts', 'total_counts', 'pct_counts_mt'],
             jitter=0.4, multi_panel=True)
~~~
{: .bash}

~~~
The figures should be added.
~~~
{: .output}

Scatter plots are applied to visualize data after removal of mitochondrial genes with very high level of expression.

~~~
$ sc.pl.scatter(adata, x='total_counts', y='pct_counts_mt')
$ sc.pl.scatter(adata, x='total_counts', y='n_genes_by_counts')
~~~
{: .bash}

~~~
The figures should be added.
~~~
{: .output}



