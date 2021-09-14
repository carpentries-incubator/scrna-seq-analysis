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

Sequencing centers deliver the results of scRNA-seq in three formats including `BCL`, `.fastq`, and `.mtx`. Raw data for scRNA-se data are recieved as `BCL2` or `fastq` files. BCL2 files should be converted into .fastq files using a commandline software called [bcl2fastq](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html). Analysis of data in .fastq format includes Quality Control, Trimming, Alignment, Mapping which are mainly similar with bulk RNA-seq analysis and you can find in [Data Carpentry Genomics Lessons] (https://datacarpentry.org/wrangling-genomics/). Quantification analysis uses statistical analysis and machine learning methods to detect the number of each transcript and count them. Some of the methodologies normalize the counts of transcripts and filter the genes with no significantly different expression levels amongwhich edgeR, DESeq, DESeqq2, etc can be mentioned.
The output of quantification analysis is a text file containing gene IDs in rows and cell IDs in columns.

The first step is to 
