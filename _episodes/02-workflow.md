---
title: "scRNA-seq Workflow"
teaching: 15
exercises: 5
questions:
- "What is the standard workflow of scRNA-seq?"
objectives:
- "Understanding the main steps in scRNA-seq experiments."
- "Understand the main steps in scRNA-seq data analysis."
- "Understanding the main protocols in scRNA-seq and the differences between them."
- "Experimental challenges in preparation of samples for scRNA-seq data analysis."
  
keypoints:
- "scRNA-seq requires much pre-processing before analysis can be performed."
---

# scRNA-Seq Experimental Workflow

Single cell RNA sequencing (scRNA-seq) is a novel technique for extracting more detailed information from genome.
Technically, scRNA-seq includes two parts of experimental design and data analysis.
As it was mentioned before, scRNA-seq is useful in case of heterogeniety of cells and developmental studies. For example,
imagine brain tissue with tens of cell types with tens of different expression profiles. For extracting transcriptome
of each cell, it is necessary to isolate each cell from the tissue properly.
# To achieve transcriptome of each cell individually, it is required to separate cells of a tissue or a sample into single cells.
For this, several methods have been developed since the introduction of scRNA-seq technique. Several steps are performed for this including:
- Single Cell Isolation: The first step which determines the quality of scRNA-seq. This step is performed to increase the number of cells which
are analyzed 
> ## Note
> 
> A challange in experiment design of scRNA-seq is to isolate cells and prepare a comprehensive library. 
{: .callout}

Several methods have been developed to overcome this challange from which STRT-seq, SMART-seq, CEL-seq, MARS-seq, Fluidigm C1, CytoSeq, Drop-seq, inDrop, 10x Genomics, SPLiT-seq, sci-RNA-seq, DronC-seq, and Seq-Well can be mentioned. The developmental process of sequencing techniques has been mentioned by [Svensson and colleagues](https://www.nature.com/articles/nprot.2017.149). 
![Fig1](https://user-images.githubusercontent.com/30586852/130464788-8f2e1c8e-bb5d-43d7-95a9-5d8e9adbe39d.png)


There is a specific terminology for scRNA-seq which we should know for analysis of data. Lets check them out!

> ## scRNA-seq dictionary
> - `Unique Molecular Identifiers (UMI)`: Short random molecular tags which are added to DNA fragments in library preparation process before PCR amplification.
> UMIs are used to identify input DNA molecules. 
> 
> -  `External RNA Controls Consortium (ERCC) spike-in`: A short RNA sequence which is used to calibrate measurements of RNA hybridization assays. ERCC spike-ins bind to DNA molecules with matching as control probes.
> 
> - `Cell Barcode`: unique nucleic acid sequences, termed barcodes, which are used to label individual cells, so that they can be tracked through space and time in scRNA-seq.
> 
> - `Flourescence-activated cell sorting (FACS)`: A flowcytometry method for cell isolation in which fluorescent tags are used to detect each cell.
> 
> - `laser capture microdissection (LCM)`: Cell sorting method under direct microscopic visualization.
{: .callout}

[Here](http://data-science-sequencing.github.io/Win2018/lectures/lecture16/), you can see the order and construction of reads in scRNA-seq:
![biasedreads2](https://user-images.githubusercontent.com/30586852/130571826-79ac907f-0c14-4367-a010-51d88a3140f0.png)

Cell barcodes are used to determine each read belongs to which cell and UMI is used for identification of each RNA molecule and enales counting the frequency of reads.


> ## scRNA-Seq Computational Workflow
>
> scRNA-seq raw data includes reads with cell barcode and UMIs. Before alignment of reads to genome, reads can be grouped using cell barcodes and the frequency of each read is estimated per cell per gene using UMIs.
> After alignment and frequency calculations, we have a gene expression table containing cells represented in the columns and genes represented in the rows.
This is what we analyze in scRNA-seq comlutational workflow.
{: .callout}

> Here You can see the bioinformatics workflow for analysis of scRNA-seq data.

![Workflow](https://user-images.githubusercontent.com/30586852/132938128-c0bdc3ea-c8e0-4752-8c0e-267b586e7381.png)

{% include links.md %}
