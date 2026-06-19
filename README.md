# Download-RNA-seq-FASTQ-Files-from-NCBI-SRA
A concise guide for downloading RNA-seq sequencing data from the NCBI Sequence Read Archive (SRA) using the SRA Toolkit. This tutorial covers downloading SRA files, converting them to FASTQ format, and managing multiple samples efficiently for downstream bioinformatics analyses.

This tutorial covers:

- Downloading `.sra` files from NCBI
- Converting SRA files to FASTQ
- Downloading multiple SRR accessions
- Parallel downloads with GNU Parallel
- Using multiple CPU cores efficiently
- Common troubleshooting tips
## Features

| Feature | Description |
|----------|-------------|
| Download SRA files | Download sequencing data using `prefetch` |
| FASTQ conversion | Convert `.sra` files using `fasterq-dump` |
| Parallel downloads | Download multiple SRR runs simultaneously |
| Multi-core processing | Utilize all available CPU cores |
| Progress monitoring | Track downloads and conversions |
| Troubleshooting | Fix common SRA Toolkit errors |

## 1. Install SRA Toolkit

## Using conda
```bash
conda install -c bioconda sra-tools
```

## Verify Installation

```bash
prefetch --version
```
```bash
fasterq-dump --version
```

## 2. Download a Single SRR Sample

Download one sample with prefetch:
```bash
prefetch --max-size u SRR15403782
```  
