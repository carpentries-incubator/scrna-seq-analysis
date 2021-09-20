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

Sequencing centers deliver the results of scRNA-seq in three formats including `BCL`, `.fastq`, and `.mtx`. Raw data for scRNA-se data are recieved as `BCL2` or `fastq` files. BCL2 files should be converted into .fastq files using a commandline software called [bcl2fastq](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html). Analysis of data in .fastq format includes Quality Control, Trimming, Alignment, Mapping which are mainly similar with bulk RNA-seq analysis and you can find in   [Data Carpentry Genomics Lessons](https://datacarpentry.org/wrangling-genomics/). Quantification analysis uses statistical analysis and machine learning methods to detect the number of each transcript and count them. Some of the methodologies normalize the counts of transcripts and filter the genes with no significantly different expression levels amongwhich edgeR, DESeq, DESeqq2, etc can be mentioned.
The output of quantification analysis is a text file containing gene IDs in rows and cell IDs in columns which called expression matrix.

# Get Data
The dataset which we use for this workshop includes 6 files in `.tsv` format including information about cell barcodes, metadata, cell IDs and gene IDs, etc., and one file in `.mtx` format which includes the number of RNAs in each cell.

> ## Project Directory 
> scRNA-seq analysis workflow begins with a few files and will produce a lot of files.
> Therefore, it is useful to manage our files and directories.
> For this, create a directory called `scRNA-seq' and transfer the downloaded files into this directory.
> Now, we can check out if we have all the files required for the analysis.
{: .callout}



# Preprocessing

The first step using expression matrix is preprocessing which includes preprocessing and normalization.


