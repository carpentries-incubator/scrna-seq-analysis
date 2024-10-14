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

RNA sequencing uses all RNA content of cells including mRNAs and non-coding RNAs in a specific conditions such as a diseases or a stage of disease
to find the alterations in functionality of those cells under that specific condition. 
Single cell RNA sequencing (scRNA-seq) is a novel technique applied to achieve the expression profile of each cell type under specific condition.
Technically, scRNA-seq includes two parts of experimental design and data analysis.
Considering that single cells in a tissue are used for sequencing, it is important to design sample preparation, cell capturing,
RNA extraction and sequencing in a way that not only provides the information of each cell type, but also helps to compare expression
profiles of various cell types. The main workflow of scRNA-seq includes `Single Cell Isolation`, `Secondary Strand Synthesis`, `Full length DNA Synthesis`,
`Barcode Adding`, `Pooling Befor Library`, `Library Amplification`, `Sequencing`, `Data Analysis`.
The required steps are more than bulk RNA-seq and subsequently a collection of specific phrases are created for scRNA-seq. 
Here is a specific terminology for scRNA-seq which we should know for analysis of data. Lets check them out!

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


> ## Note
>
> # To achieve transcriptome of each cell individually, it is required to separate cells of a tissue or a sample into single cells.
> - `Several methods have been developed since the introduction of scRNA-seq technique. Different steps are performed for this including`:
> - ## Single Cell Isolation:
>  The first step which determines the quality of scRNA-seq. This step is performed to increase the number of cells captured per experiment:
> `Primary methods`: These methods rely on manual picking and FACS to  isolate single cells into plates or microfluidic chips to capture single cells in nanoliter chambers and subsequently generate sequencing libraries. However, these techniques are difficult and error prone.
> `Robotics methods`: These methods automate single cell isolation procedures. Droplet-based microfluidics and nanowell-based technologies were developed to randomly capture single cells into isolated nanoliter compartments (droplets or nanowells), increasing the throughput to tens of thousands of cells while at the same time significantly reducing manual labor.
>-  ## Second Strand Generation: 
>  There are three methods for this:
> `Adding poly-A tail`: In this method, after adding a ploy-A tail, a poly-T primer is used to amplify cDNA. Quartz-Seq and Quartz-Seq2.
> `MMLV terminal transferase`: This enzyme adds cytosines to 3' end of RNA and ploy-G is added to 3' end and a complementary strand is synthesized.
   STRT-seq, SMART-seq, SMART-seq2, Drop-seq, Seq-Well, Chromium, and SPLiT-seq.
> `Combination of ribonuclease (RNase) H and DNA polymerase I from Escherichia coli`: In this method, RNase H first cuts mRNA in the mRNA-DNA duplex.
    Then, the RNA-primed first strand cDNA is used as template, and second strand cDNA is synthesized by DNA polymerase I.
    CEL-seq, CEL-seq2, MARS-seq, inDrop, and sci-RNA-seq. 
> 
{: .callout}





 [Svensson and colleagues](https://www.nature.com/articles/nprot.2017.149). 
![Fig1](https://user-images.githubusercontent.com/30586852/130464788-8f2e1c8e-bb5d-43d7-95a9-5d8e9adbe39d.png)

> ## Full Length DNA Synthesis?
> - `PCR-based methods for library amplification due to simplicity and speed
> - In vitro transcription (IVT) achieves linear amplification of the library, resulting in less amplification bias but requiring more steps and time than PCR.
  CEL-seq, CEL-seq2, and inDrop. 
> 
> -  STRT-seq, STRT-seq-2i, Drop-seq, Chromium (10x Genomics), Seq-Well, and SPLiT-seq all perform full-length cDNA synthesis like SMART-seq and SMART-seq2, but STRT-seq and STRT-seq-2i only sequence the 5′ end of the transcripts, while the others focus on 3′ sequencing of the mRNA.
{: .callout}


<div style="background-color: white; padding: 15px; border-radius: 5px;">
    <h3 style="background-color: lightblue; color: white; padding: 10px; border-radius: 5px;">Full Length DNA Synthesis?</h3>
    <p> `PCR-based methods for library amplification due to simplicity and speed`.
  - `In vitro transcription (IVT)` achieves linear amplification of the library, resulting in less amplification bias but requiring more steps and time than PCR.
  CEL-seq, CEL-seq2, and inDrop.</p>
    <p> - STRT-seq, STRT-seq-2i, Drop-seq, Chromium (10x Genomics), Seq-Well, and SPLiT-seq all perform full-length cDNA synthesis like SMART-seq and SMART-seq2, but STRT-seq and STRT-seq-2i only sequence the 5′ end of the transcripts, while the others focus on 3′ sequencing of the mRNA.</p>
</div>

![Figure2](https://github.com/user-attachments/assets/e81f3706-8f25-44a5-977b-544b0500d870)


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
