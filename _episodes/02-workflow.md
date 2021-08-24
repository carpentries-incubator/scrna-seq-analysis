---
title: "scRNA-seq Workflow"
teaching: 15
exercises: 5
questions:
- "What is the standard workflow of scRNA-seq?"
objectives:
- "Understand the main steps in scRNA-seq experiments."
- "Understand the main steps in scRNA-seq data analysis."
- "Understand the challanges in scRNA-seq data analysis."
keypoints:
- "scRNA-seq requires much pre-processing before analysis can be performed"
---

# scRNA-Seq Experimental Workflow

Single cell RNA sequencing (scRNA-seq) is a novel technique for extracting more detailed information from genome.
Technically, scRNA-seq includes two parts of experimental design and data analysis.
As it was mentioned before, scRNA-seq is useful in case if heterogenity of cells and development studies. For example,
imagine brain tissue with tens of types of cells with tens of different expression profiles. For extracting transcriptome
of each cell, it is necessary to isolate each cell from the tissue properly.
> ## Note
> 
> A challange in experiment design of scRNA-seq is to isolate cells and prepare a comprehensive library. 
{: .callout}

Several methods have been developed to overcome this challange from which STRT-seq, SMART-seq, CEL-seq, MARS-seq, Fluidigm C1, CytoSeq, Drop-seq, inDrop, 10x Genomics, SPLiT-seq, sci-RNA-seq, DronC-seq, and Seq-Well can be mentioned. The development process of sequencing techniques has been mentioned by [Svensson](https://www.nature.com/articles/nprot.2017.149) which can be assessed. 
![Fig1](https://user-images.githubusercontent.com/30586852/130464788-8f2e1c8e-bb5d-43d7-95a9-5d8e9adbe39d.png)


For data analysis, there are few terms in scRNA-seq dictionary. Lets check them out!

> ## scRNA-seq dictionary
> - Unique Molecular Identifiers (UMI): Short random molecular tags which are added to DNA fragments in library preparation process before PCR amplification.
> UMIs are used to identify input DNA molecules. 
> - External RNA Controls Consortium (ERCC) spike-in: A short RNA sequence which is used to calibrate measurements of RNA hybridization assays. ERCC spike-ins bind to DNA molecules with matching as control probes.
> - Cell Barcode: unique nucleic acid sequences, termed barcodes, which are used to label individual cells, so that they can be tracked through space and time in scRNA-seq.
{: .callout}

[Here](http://data-science-sequencing.github.io/Win2018/lectures/lecture16/) which can be assessed. , you can see the order and construction of reads in scRNA-seq:
![biasedreads2](https://user-images.githubusercontent.com/30586852/130571826-79ac907f-0c14-4367-a010-51d88a3140f0.png)

Cell barcodes are used to determine each read belongs to which cell and UMI is used for identification of each RNA molecule.


# scRNA-Seq Computational Workflow

scRNA-seq raw data includes reads with cell barcode and UMIs. Before alignment of reads to genome, reads can be grouped using cell barcodes and frequency if each read per cell per gene can be estimated using UMIs.
After alignment and frequency calculations, we have a gene expression table containing cells represented in the columns and genes represented in the rows.
Analysis of this table has challanges.


{% include links.md %}
