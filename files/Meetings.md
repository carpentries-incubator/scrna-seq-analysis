RNA-seq Lesson Development
===

###### tags: `RNA-seq` `Meeting`

:::info
- **Location:** Online
- **Date:** Feb 5, 2021

:::

## RNA-seq Lesson Development 

The process of developing the RNA-seq lesson in the Carpentries.


:closed_book: Batool's Draft for bulk RNA-seq
--
- **Intro to RNA-seq**
	- Principle
	- Library
- **Intro to Bioconducor**
- **How to get help**
	- in R - `?DEseq` or `vignette("DEseq2")`
	- Bioconductor Forum
- **Convert SRA to FASTQs?**
	- What is the best way to do it? e.g. use `fastq-dumb` from SRA Toolkit.
- **Quality Control of FASTQ files using `fastqc`.**
	- Do we show anything about adpater trimming?
	- Do add UMI extraction (`UMI-tools`) or Removal of ribosomal RNA (`SortMeRNA`). It might causes confusion!
- **Salmon**
	- Pseudo-alignment and quantification
	- Command line tool
	- Improves the accuracy of abundance estimates and the reliability of  differential expression analysis
- **Import the data to `tximeta/tximport`**
	- Maybe it's better to only mention `tximeta`
	- Show how tximeta automatically adds annotation metadata when the RNA-seq data has been quantified with `salmon`
- **Convert the quantification from `tximeta` to `DESeq2`**
	- Design the conditions of the experiment
	- Do we need to show other tools like `fishpond`/`Swish` or `DTU`. This may causes confusion! 
- **Normalisation**
	- Why normalise? 
		- gene length
		- library depth
		- gene expression
	- Size factor
	- Estimate Dispersion
	- Wald test (shrinkage)
- **Explore the data (data viz)**
	- MA plot
	- Volcano Plot
	- Extract the top differentiated genes
	- Heatmaps
 	- GO enrichments
 	- PCA (rlog transformation)
	- Boxplot
	- k-means clustering
	- Hierarchical clustering
- **Cloud-scale (e.g. AWS) or HPC**
  - Maybe usng [nf-core RNA-seq](https://nf-co.re/rnaseq)!
  >"The pipeline is built using Nextflow, a workflow tool to run tasks across multiple compute infrastructures in a very portable manner. It comes with docker containers making installation trivial and results highly reproducible".

:question: Questions
---

- What is the prerequisites? familiarity with command line and R
- What datasets/what organism (e.g.Homo-sapien)/paired-end RNA-seq?
- Do we only address differential expression analysis?
- How long the lesson (hours/days)?
- Do we use rworkflow (e.g. seeds) to show best practice/reproducibility? Do we use rmarkdown? Do show example of using workflow manager in the end?

:books: Notes
---

- I think it's crucial to include data viz even if it spans more than one episode. 

![](https://i.imgur.com/gqmTZLM.png)

<!-- Other important details discussed during the meeting can be entered here. -->

###### tags: `scRNA-seq` `Meeting`

:::info
- **Location:** Online
- **Date:** Feb 14, 2021
- **Participants** Batool and Elnaz
:::

:books: Notes
---

- We changed the lesson to scRNA-seq. 
- We'll add a part about nf-core piplines for scRNA-seq.
- It'll be two days workshop.
- We'll only use bioconductor (R and the command line).

###### tags: `scRNA-seq` `Meeting`

:::info
- **Location:** Online
- **Date:** Feb 27, 2021
- **Participants** Batool and Elnaz
:::

:books: Notes
---

- We created a new issue in the carpentries incubator.
- We created a new template using the incubator template
- We are preparing for outlines.
- We'll use pseudo-alignment with Salmon or kallisto rather than alignment with STAR.
- Prerequisites: The course is intended for those who have basic familiarity with Unix and the R scripting language
- Docker image for the materials and packages
- We have to choose the dataset ([Link](https://scrnaseq-course.cog.sanger.ac.uk/website/index.html))
- Review the genomic carpentries lesson (intro to package, most recommanded path, functionality of the package and the output)

:closed_book: Batool's Draft
--
- **Intro to scRNA-seq**
	- Principle
	- Library
	- difference between bulk RNA-seq and scRNA-seq
- **Intro to Bioconducor**
    - How to get help**
	    - in R - `?clusterExperiment` or `vignette("clusterExperiment")`
	    - Bioconductor Forum
- **Convert SRA to FASTQs?**
	- What is the best way to do it? e.g. use `fastq-dumb` from SRA Toolkit.
- **Quality Control of FASTQ files using `fastqc`.**
	- Do we show anything about adpater trimming?
- **Pseudo-alignment with Salmon or kallisto**
- **Read counts**
- **Normalisation**
- **Dimensionality Reduction**
- **Clustering**
- **DE analysis**
- **nf-core scRNA-seq pipeline**
    - containers 
    - run HPC/AWS/Azure 

:closed_book: Elnaz's Draft
- **Introduction to scRNA-Seq**
      Workflow 
      Computational analysis
- **Processing raw scRNA-Seq data.**
      File formats
      FastQC
      Trimming
      Demultiplexing
      Kallisto and pseudoalignment
- **Construction of expression Matrix.**
      Reads quantification
      Unique molecular identifiers
      SingleCellExperiment
- **Dealing with Expression Matrix.**
      Cleaning expression matrix(UMI)
- **Biological Analysis including clustering and DE analysis.**


:traffic_light: To Do list:
- Dataset determination.
- Trying the workflow for ourselves.
--

:traffic_light: Dataset and Setup
---
- For every step, there's a file with all the solutions for this episode, so students won't struggles.
- Register in the nf-core hackathon.
- Need to run all the pipeline with this new dataset before 6th of March - check the versions of the softwares, record all the notes.
- Contact the author/bioconductor why we used some of its materials.


:link: Resources
---
- [Analysis of single cell RNA-seq data](https://scrnaseq-course.cog.sanger.ac.uk/website/index.html)- we'll use this dataset.
- [Materials from 2017: Bioconductor workflow for single-cell RNA sequencing: Normalization, dimensionality reduction, clustering, and lineage inference](https://www.bioconductor.org/help/course-materials/2017/BioC2017/Day2/Workshops/singleCell/doc/workshop.html)
- [An introduction to scRNA-seq data analysis](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/scrna-intro/slides.html#1)
- [Pre-processing of 10X Single-Cell RNA Datasets](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/scrna-preprocessing-tenx/tutorial.html)
- [Pre-processing of Single-Cell RNA Data](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/scrna-preprocessing/tutorial.html)
- [Introduction to Single-cell RNA-seq](https://hbctraining.github.io/scRNA-seq/schedule/)
- [Bioconductor conference 2020 videos](https://www.youtube.com/user/bioconductor/video)


