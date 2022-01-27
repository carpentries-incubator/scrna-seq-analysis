---
title: "Pre-processing of scRNA-seq using Cellranger"
teaching: 15
exercises: 5
questions:
- "How do pre-process scRNA-seq data using cellranger?"
objectives:
- "Identify the available tools to preprocess cRNA-seq."
- "Understand how to use Cell Ranger."
keypoints:
- "scRNA-seq requires much pre-processing before analysis can be performed."
---

## Dataset:

Expression data from scRNA-seq experiments represent thousands of reads for thousands of cells. Therefore, the data output can be very large and hard to store in your local machine. You will also need higher amounts of memory to analyze.

In this tutorial, We will use Human peripheral blood mononuclear cells (PBMCs) of a healthy female donor aged 25-30 were obtained by 10x Genomics from AllCells.

Libraries were generated from ~16,000 cells (11,996 cells recovered) as described in the Chromium Single Cell 3' Reagent Kits User Guide (v3.1 Chemistry Dual Index) (CG000315 Rev C) using the Chromium X and sequenced on an Illumina NovaSeq 6000 to a read depth of approximately 40,000 mean reads per cell.

## Generation of count matrix:

In this part, we will generate the count matrix from the raw sequencing data. After sequencing, the output generated from the sequencing machine will be either output the raw sequencing data as BCL or FASTQ format. Using this raw sequence, we will generate the count matrix.

When using 10X Genomics library preparation method, then the Cell Ranger pipeline is most ideal way to pre-process the data. Make sure that you installed the Cell Ranger version 6.1 (see the instructions). Using `cellranger`, we can genome mapping, UMI filtering, UMI dedeplication and cell filtering. We will start with  

FIXME: We need to add image cellranger pipeline where we shows different steps (e.g. extraction, filtering, ..) and also how to correct the naming of the input file

FIXME: Need to subset the dataset for the use only for this part of the lesson.

in order to align the fastqs to the reference genome and count how many reads per gene per cell. We ca use `cellranger count` command.

```{bash eval =FALSE}
cellranger count --id=bcl \
                   --transcriptome=/opt/refdata-cellranger-GRCh38-3.0.0 \
                   --fastqs=/home/test/outs/fastq_path/HAWT7ADXX/test_sample/ \
                   --sample=mysample\
                   --expect-cells=8000
```

> ## Question
>
> What do you do if your input from sequencing machine is bcl file?
>
> > ## Solution
> >
> > `cellranger` wraps the illumina [`bcl2fastq`](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html) command into `cellranger mkfastq` to convert it to fastq files for single-cell RNAseq data.
> {: .solution}
{: .challenge}

### What is the output of `cellranger count`?

In the `outs` folder, and you will find the `filtered_feature_bc_matrix` folder, which contains 3 files :

```
ls filtered_feature_bc_matrix/
  barcodes.tsv.gz   features.tsv.gz   9 matrix.mtx.gz

 ```

 We can look into individule files using `head` command. The `barcodes.tsv.gz` should contains all the cell barcodes that passed the `cellranger` filter

> FIXME: Fix all the names/sequences when you subset the files

```
zcat barcodes.tsv.gz | head -5
AAAAAAACCCCCCCCC-1
AAAAAAACCCCCCCCC-1
AAAAAAACCCCCCCCC-1
AAAAAAACCCCCCCCC-1
AAAAAAAACCCCCCCCC-1

````

We can count how many cell/barcodes in `barcodes.tsv.gz`
```
zcat barcodes.tsv.gz | wc -l
11544
```

The second file is the `features.tsv.gz`, which contains the ENSEMBLE id and gene symbol

```
zcat features.tsv.gz | head -5
ENSG00000222222 MPRRCCC     Gene Expression
ENSG00000222222 MPRRCCC Gene Expression
ENSG00000222222 MPRRCCC   Gene Expression
ENSG00000222222 MPRRCCC      Gene Expression
ENSG00000222222 MPRRCCC      Gene Expression
```

> ## Question
>
> How can you count the genes?
>
> > ## Solution
> >
> > We can use `zcat features.tsv.gz | wc -l` to count the number of genes.
> {: .solution}
{: .challenge}

The third output is `matrix.mtx.gz` which is a sparse matrix which contains the non-zero counts. Sparse matrix efficiently save the disk space by only recording the non-zero entries.


{% include links.md %}
