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

Single cell RNA sequencing (scRNA-seq) is a novel technique for extracting more detailed information from genome.
Technically, scRNA-seq includes two parts of experimental design and data analysis.
As it was mentioned before, scRNA-seq is useful in case if heterogenity of cells and development studies. For example,
imagine brain tissue with tens of types of cells with tens of different expression profiles. For extracting transcriptome
of each cell, it is necessary to isolate each cell from the tissue properly.
> ## Note
> 
> A challange in experiment design of scRNA-seq is to isolate cells and prepare a comprehensive library. 
{: .callout}

Several methods have been developed to overcome this challange from which STRT-seq, SMART-seq, CEL-seq, MARS-seq, Fluidigm C1, CytoSeq, Drop-seq, inDrop, 10x Genomics, SPLiT-seq, sci-RNA-seq, DronC-seq, and Seq-Well can be mentioned. The development process of sequencing techniques has been mentioned by [Svensson](https://www.nature.com/articles/nprot.2017.149) which can be assessed. For data analysis, there are few terms in scRNA-seq dictionary. Lets check them out!



{% include links.md %}
