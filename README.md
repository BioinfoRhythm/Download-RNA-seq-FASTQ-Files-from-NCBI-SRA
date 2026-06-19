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

The option --max-size u removes the default download size limit.

```bash
ls SRR15403782
```

You should see:

```bash
SRR15403782.sra
```

## 3. Download Multiple SRR Samples

Create a file called sra.txt and add one accession per line:
```bash
SRR15403001
SRR15403002
SRR15400003
SRR15400004
SRR15400005
```

Download all runs with:

```bash
mkdir -p sra

prefetch \
    --option-file sra.txt \
    --max-size u \
    --output-directory sra
```

## 4. Parallel Download with GNU Parallel

Install GNU Parallel:

```bash
sudo apt install parallel
```

Run multiple downloads at the same time:

```bash
cat sra.txt | parallel -j 12 \
'prefetch --max-size u {} --output-directory sra'
```

Notes:

-j 12 runs up to 12 downloads at once.

Downloading is usually network-limited, not CPU-limited.

Having more CPU cores does not always make downloads faster.

## 5. Convert SRA to FASTQ

Convert the single .sra file to FASTQ:

```bash
fasterq-dump \
  --split-files \
  --threads 30 \
  SRR15403782
```
For paired-end data, this creates:

```bash
SRR15403782_1.fastq
SRR15403782_2.fastq
```
Convert multiple  .sra file to FASTQ:

```bash
mkdir -p fastq

cat sra.txt | parallel -j 5 \
'fasterq-dump \
    --split-files \
    --threads 6 \
    --outdir fastq \
    sra/{}/{}.sra'
```

project/

├── sra/

│   ├── SRR15403782/

│   ├── SRR15403783/

│   └── ...

├── fastq/

│   ├── SRR15403782_1.fastq

│   ├── SRR15403782_2.fastq

│   ├── SRR15403783_1.fastq

│   └── ...

└── sra.txt



