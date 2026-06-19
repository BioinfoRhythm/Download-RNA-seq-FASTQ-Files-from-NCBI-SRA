# Download-RNA-seq-FASTQ-Files-from-NCBI-SRA
A concise guide for downloading RNA-seq sequencing data from the NCBI Sequence Read Archive (SRA) using the SRA Toolkit. This tutorial covers downloading SRA files, converting them to FASTQ format, and managing multiple samples efficiently for downstream bioinformatics analyses.

1. Install SRA Toolkit
Conda
```conda install -c bioconda sra-tools ```
Verify Installation
prefetch --version
fasterq-dump --version

Example:
prefetch : 3.x.x
fasterq-dump : 3.x.x
