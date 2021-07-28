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
The NCBI SRA store raw DNA and RNA sequencing data as SRA files. These SRA files are compressed forms of FASTQ data to save storage space. These FASTQ raw sequencing data have been produced by various sequencing platforms from Illumina, Oxford Nanopore, PacBio, BGISEQ, Ion Torrent, and LS454.

## What is FASTQ?
In contrast to FASTA, FASTQ contains an extra line per sequence that corresponds to the quality scores of each of the nucleotides. Further details are explained at the [NCBI File Format Guide page](https://www.ncbi.nlm.nih.gov/sra/docs/submitformats/) and the [Wikipedia page](https://en.wikipedia.org/wiki/FASTQ_format).
~~~
@<identifier and expected information>
<sequence>
+<identifier and other information OR empty string>
<quality>
~~~

## How to extract FASTQ files from SRA files using the NCBI SRA Tools?
Let's download the NCBI SRA tools from [GitHub](https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit). The pre-built binaries are available for Linux (CentOS and Ubuntu), MacOS and Windows. Let's copy the URL (Ubuntu in my case) and run the following commands.

~~~
$ mkdir bin
$ cd bin
$ wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.11.0/sratoolkit.2.11.0-ubuntu64.tar.gz
$ tar zxvf sratoolkit.2.11.0-ubuntu64.tar.gz
$ cd ~/sratoolkit.2.11.0-ubuntu64/bin/
$ ls
~~~

We are going to use prefetch to download a SRA file (e.g., SRR000001) and fasterq-dump to convert SRA to FASTQ format. Further details are available at the official [Wiki page](https://github.com/ncbi/sra-tools/wiki/08.-prefetch-and-fasterq-dump).

~~~
$ prefetch SRR000001
$ fasterq-dump SRR000001
~~~

These will create a directory SRR000001 and write three fastq files into SRR000001 (i.e., SRR000001.fastq, SRR000001_1.fastq, SRR000001_2.fastq).
