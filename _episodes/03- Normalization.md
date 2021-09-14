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

Raw data for scRNA-se data are recieved as `BCL2` or `fastq` files. BCL2 files should be converted into .fastq files using a commandline software called [bcl2fastq] https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html
