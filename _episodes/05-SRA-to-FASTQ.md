---
title: "Extract FASTQ files from SRA files"
teaching: 20
exercises: 10
questions:
- "What is The Sequence Read Archive (SRA)?"
- "How to convert SRA to FASTQ using NCBI SRA Tools"
objectives:
- "Describe FASTQ file"
keypoints:
- "FIXME"
---
FIXME

{% include links.md %}

## What is the Sequence Read Archive (SRA)?
The [NCBI SRA](https://www.ncbi.nlm.nih.gov/sra) store raw DNA and RNA sequencing data as SRA files, as well as alignment files. These SRA files are compressed forms of FASTQ data to save storage space. These FASTQ raw sequencing data have been produced by various sequencing platforms from Illumina, Oxford Nanopore, PacBio, BGISEQ, Ion Torrent, and Roche (discontinued 454 sequencers).

## What is FASTQ?
In contrast to FASTA, FASTQ contains an extra line per sequence that corresponds to the quality scores of each of the nucleotides. The FASTQ format was originally developed at the Wellcome Trust Sanger Institute, which has became the de factor standard for next-generation sequencing. Further details are explained at the [NCBI File Format Guide page](https://www.ncbi.nlm.nih.gov/sra/docs/submitformats/) and the [Wikipedia page](https://en.wikipedia.org/wiki/FASTQ_format).
~~~
@<identifier and expected information>
<sequence>
+<identifier and other information OR empty string>
<quality>
~~~

## How to extract FASTQ files from SRA files using the NCBI SRA Toolkit?
Let's download the NCBI SRA toolkit from [GitHub](https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit). The pre-built binaries are available for Linux (CentOS and Ubuntu), MacOS and Windows. Let's copy the URL and run the following commands.

~~~
$ mkdir bin
$ cd bin
# MacOS https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.11.0/sratoolkit.2.11.0-mac64.tar.gz
# Windows https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.11.0/sratoolkit.2.11.0-win64.zip
$ wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.11.0/sratoolkit.2.11.0-ubuntu64.tar.gz
$ tar zxvf sratoolkit.2.11.0-ubuntu64.tar.gz
$ cd ~/sratoolkit.2.11.0-ubuntu64/bin/
$ ls
~~~

We are going to use prefetch to download a SRA file (e.g., SRR000001) and fasterq-dump to convert SRA to FASTQ format. Further details are available at the [documentation page](https://github.com/ncbi/sra-tools/wiki/08.-prefetch-and-fasterq-dump).

~~~
$ prefetch SRR000001
$ fasterq-dump SRR000001
~~~

These will create a directory SRR000001 and write three fastq files into SRR000001 (i.e., SRR000001.fastq, SRR000001_1.fastq, SRR000001_2.fastq).


## Could we download FASTQ files straightaway, using R instead of terminal?
We could directly download FASTQ files from EBI using the SRAdb Bioconductor package through ftp protocol. Let's install SRAdb in an R console session.
~~~
> if (!requireNamespace("BiocManager", quietly = TRUE))
+     install.packages("BiocManager")
> BiocManager::install("SRAdb")
> library(SRAdb)
~~~
In contrast to SRA toolkit, SRAdb requires the SRAmetadb sqlite database that is available at the [Amazon cloud](https://s3.amazonaws.com/starbuck1/sradb/SRAmetadb.sqlite.gz). However, this database is very large (~40GB).
~~~
# sqlfile <- getSRAdbFile()
~~~
For demonstration purpose, we will use a demo database.
~~~
> sqlfile <- file.path(system.file('extdata', package='SRAdb'), 'SRAmetadb_demo.sqlite')
> sra_con <- dbConnect(SQLite(),sqlfile)
> getSRAfile( c("SRR000648","SRR000657"), sra_con, fileType = 'fastq')
# or
# getFASTQinfo( c("SRR000648","SRR000657"), sra_con, srcType = 'ftp')
~~~
Alternatively, we could use fasp protocol to download large files at a faster speed. This requires the [IBM Aspera Connect](https://www.ibm.com/aspera/connect/) that has to be separately installed. Further details are available at the [SRAdb vignettes](https://bioconductor.org/packages/release/bioc/vignettes/SRAdb/inst/doc/SRAdb.pdf).
