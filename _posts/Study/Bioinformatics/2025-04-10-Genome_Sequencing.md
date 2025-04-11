---
title: Genome Sequencing
author: JSH
date: 2025-04-10 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
---

# Analysis of NGS Sequencing of Genome

## Overview

### A workflow for whole genome sequencing (WGS) of individual genomes
1. Select proband(s)
2. Purify genomic DNA
3. Generate paired-end library
4. Design capture beads (e.g., Agilent SureSelect) (optional; used for whole exome sequencing)
5. Hybridize in solution (optional; used for whole exome sequencing)
6. Elute enriched genomic DNA (optional; used for whole exome sequencing)
7. Amplify (optional; used for whole exome sequencing)
8. Next-generation sequencing
9. Align sequence to a human genome reference
10. Determine coverage (e.g. 30-fold)
11. Identify variants: SNPs, indels (distinguish true variants from sequencing errors)
12. Prioritize variants
13. Validate variants

<!-- genomic DNA를 뽑을 때 최대한 germline과 비슷한게 좋다. 
그래서 피부는 자외선 등에 의해 mutation이 많이 되어서 안되고, 혈액이나 침에서 많이 뽑음.
침에서는 다른 미생물에 의한 영향이 있다는게 문제지만 생각보다 잘 나옴 -->

### Next-generation sequencing workflow
![Image](https://github.com/user-attachments/assets/c7ad77ea-1632-41dc-a27a-5717cc97b667)

### Genome Analysis Tookit (GATK) workflow

#### Phase 1: data processing
* Raw reads (input) <!-- 갓 나온 seqeunce. base calling 한 후. -->
* Mapping  <!-- BWA 등 이용. chromosome의 어디에 있는지 확인 -->
* Local realignment  <!-- 어디에 변이가 있는지 등. 보통 mapping과 local realignment는 BWA를 이용해서 한번에 처리 -->
* Duplicate marking  <!-- PCR에서 duplicate가 많이 생기기 때문에 밸런스를 맞춤. 이걸 안하면 통계 문제가 생김 -->
* Base quality recalibration <!-- sequence의 quality 확인. 리드들을 reference에 mapping해서 정확도 측정. -->
* Analysis-ready reads (output)

<!-- 
GATK 기준으로 용어, 순서 결정.
-->

#### Phase 2: variant discovery and genotyping
* Sample 1 reads, ..., Sample N reads (input)
* SNPs, Indels, Structural variation (SV)
* Raw variants (output)

#### Phase 3: integrative analysis
* Raw indels, Raw SNPs, Raw SVs (input)
* External data
  * Pedigrees, Population structure, Known variation, Known genotypes
* Variant quality recalibration, genotype refinement
* Analysis-ready variants (output)

## FASTQ
### Base calling: the conversion of signal to a nucleotide sequence
Errors happen.
Hopefully infrequently.

### FASTQ format
A standard format for storing and defining sequences from next-generation sequencing technologies.

* Sequence ID: @SEQ_ID
* Sequence: GATTTGGGGTTCA
* Separator: +
* Quality score: !''*((((***+)

### FASTQ quality scores
Estimate of confidence in each base.

Qualities are based on the Phred scale and are encoded.

Q = -10 * log_{10} (P_{err})

FASTQ has had different encoding schemes for encoding PHRED quality scores.

Quality score encoding based on ASCII table.

Formula for getting PHRED quality from encoded quality: Q = ascii(char) - 33

### SRA and ENA
SRA and ENA are the major repositories for the sequencing data.
* SRA: https://www.ncbi.nlm.nih.gov/sra
* ENA: https://www.ebi.ac.uk/ena

## Assembly

### Genome assembly
Genome assembly is the process of converting short reads into a detailed set of sequences corresponding to the chromosome(s) of an organism.

### Genome assembly methods
Overlap graph, de Bruijn graph, string graph

## Alignment

### Next-generation sequence: the problem of alignment
Recent software tools allow the mapping (alignment) of millions or billions of short reads to a reference genome.
For the human genome, this would take thousands of hours using BLAST.
Reads may come from regions of repetitive DNA (exacerbated by sequencing errors)

<!-- BWA가 압도적으로 많이 쓰인다 -->

### Alignment to a reference genome: example of short-read alignment (Bowtie) results
Format
* Read name
* Strand (+, -)
* Reference to which reads match
* Read sequence
* Quality scores

### Pileups
Format
* Reference sequence
* Read depth
* Reference sequence
  * . and , denote agreement with reference on top, bottom strands

### BWA: a popular short-read aligner
Aligns short reads (<200 base pairs) to a reference genome.
Fast and accurate.

### Reads (FASTQ format) can be mapped to a reference genome using software tools such as BWA
BWA is a popular aligner.
It stands for "Burroughs-Wheeler Aligner" referring to the algorithmic approach.

Considerations are speed and sensitivity.

For all software, we measure error rates:
using some gold standard we define true positive (TP) and true negative (TN) results, and we then define sensitivity and specificity.

A standard format has been introduced called Sequence Alignment/Map (SAM).
Its binary version is called BAM.



