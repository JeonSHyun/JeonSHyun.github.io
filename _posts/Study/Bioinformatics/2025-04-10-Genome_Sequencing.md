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

### Other problems
As repeat regions share lower identity, read mapping gains higher confidence.

There is ambiguity mapping a read with a mismatch versus a deletion.

## SAM/BAM
<!-- alignment와 SAM/BAM은 중간고사에 항상 나오는 토픽 -->

### SAM format
A text-based standard for representing sequence alignments.

In the dark ages, sequence aligners used disparate output formats.
1000 Genomes Project sought to standardize.
The result is imperfect, but it’s a huge improvement.

Strengths of the SAM and BAM formats
* Compressed: less disk hungry
* Indexed: fast viewing, slicing, etc.
* Single-end and paired-end
* Relatively simple to produce
* Good toolkits available

### SAM format overview
* QNAME
  * Read or Pair name
* FLAG
  * Bitwise Flag
* RNAME
  * Reference sequence name
* POS
  * 1-based alignment start coordinate
* MAPQ
  * Mapping quality
* CIGAR
  * Extended CIGAR string
* MRNM
  * If paired, the mate's reference seq
* MPOS
  * If paired, the mate's alignment start
* ISIZE
  * If paired, the insert size
* SEQ  <!-- reference 방향을 따른다 -->
  * The sequence of the query/mate
* QUAL
  * The quality string for the query/mate
* OPT
  * Optional Tags

### Edit distance
How many edits (changes) must be made to a word or kmer to make it match (aligh) to another word or kmer?

### The CIGAR string: endcode the details of the alignment
Operation
* M: match <!-- indel이 아니고 하나에서 다른걸로 바뀌면 match로 친다 -->
* D: deletion w.r.t. reference
* I: insertion w.r.t. reference
* N: split or spaced alignment <!-- deletion이 너무 클 때 점수에는 들어가지 않게 처리 -->
* S: soft-clipping <!-- alignment 하는것보다 안하는게 더 점수 상 이득이라고 할 때. 끝부분에서. 한 리드에는 반드시 두번까지 나타날 수 있다. (왼쪽 끝, 오른쪽 끝) 대부분이 끝부분 에러가 많이 나서 끝부분 제거를 그냥 하는 편 -->
* H: hard-clipping <!-- 거의 안쓰임 -->
* P: padding

### The extended CIGAR string: M become = and X
Operation
* =: Exact match
* X: Mismatch

<!-- 사실상 요즘은 잘 안 쓴다 -->

### The FLAG column
<!-- 2진법 encoding. 4번과 16번을 제일 많이 사용함 -->

### SAMTools
Use samtools to convert SAM to BAM
* Create BWT of reference genome
* Align paired-end FASTQ to BWT index
* Convert SAM to BAM

SAMTools tview visualization of reads from a BAM file.

Integrative Genome Viewer (IGV): display of a BAM file (at two resolutions) and a VCF.

## Variant Calling: SNVs
Goal: find all inherited variants in an individual's diploid genome.
To find inherited genetic variation by sequencing DNA from millions of cells.

Each DNA cluster is amplified from a single strand from a single haploid chromosome from a single cell.

<!-- Q: Heterozygous SNP을 포함한 샘플의 그 특정 위치에서 FASTQ 파일에 포함된 quality는 주변에 비해 낮게 나오는 경향이 있다? -> A: 아니다. 차이가 없다. (이유 다시 확인하기) -->

Scenarios
* An individual is homozygous for the reference allele
* An individual is homozygous for an alternate allele
* An individual is heterozygous for an alternate allele

At least 30X (30 fold sequence coverage) genome is recommended.
It confers sufficient power to find the majority of heterozygous allele.
With 30 tosses (reads), we are much more likely to see an even mix of alternate and reference alleles at a heterozygous locus in a genome

<!-- Heterozygous allele을 특히 더 분석하기 힘든 조건은?: somatic mutation analysis가 germline mutation analysis보다 더 어렵다. somatic은 발달 단계에서 생기거나 살면서 생기는 cell이 많기 때문에 binomial 분포로는 알 수가 없음. 통계적인 어려움 -->

Depth tackles the allele sampling issue and lower quality scores.
<!-- 요즘은 퀄리티가 상향평준화되었고, depth도 충분하기 때문에 퀄리티 낮은 read는 버리고 분석해도 문제가 없는 수준이 됨. -->

<!-- IGV로 확인하는 부분은 다시 확인하면서 어떤 점을 중점으로 봐야 하는지 보기 -->

* Random versus systemic error
* Strand bias from PCR
* Pileups of many differences from paralogy
* Calling INDELs is much harder than SNPs

## Variant Calling: SVs

### Categories of structural variation (SV)
<!-- 각각 어떻게 detect하는지 정리해보기 -->

### Deletion
### Novel sequence insertion
### Mobile-element insertion
### Inversion
### Interspersed duplication
### Tandem duplication

## VCF

### VCF format
* VCF header
  * INFO
  * FORMAT
  * Mandatory header lines: file format, CHROM POS REF ALT QUAL FILTER INFO FORMAT SAMPLE...
* Body <!-- variant를 어떤걸 넣어야 한다 이런건 없고, 사용자가 원하는 내용 넣을 수 있다 -->
  * Phased data: phased genotypes distinguish haplotype <!-- |로 구분되어 있으면 엄마한테서 받았는지, 아빠한테서 받았는지 구분해놓았다는 의미. phased가 안된 경우: / 사용 -->
  * AF = allele frequency

<!-- POS는 vcf는 1부터, bcf는 0부터 시작한다 -->
<!-- FORMAT이 GT:DP일 때 1/2:13이면 A, AT를 가지고 depth가 13임 -->

<!-- genotype이 unknown인 경우는 대부분 quality filter에 걸렸거나 read가 부족한 경우임 -->

### Allel frequency spectrum
Most variants are rare.
More than 50% of the 9 million variants discovered were present as a heterozygote in 1 out of the 60706 individuals (a singleton).

Only one person with SNP is called singleton.

### bcftools
Use bcftools to handle VCF files.
<!-- 실습 있음 -->

## Visualizing NGS Data

### Visualizing and tabulating next-generation sequence data
W will next explore BEDtools, a set of programs used to analyze BAM, GTF, BED, VCF, and other file types.
There are many ways to visualize BAM files.
* Try Genome Workbench from NCBI
* Upload your BAM file to a server and point to it using the UCSC Genome Browser
* Use Integrative Genomics Viewer (IGV)
* Use samtools tview

## Significance
Raw VCF files are naked.
Interpretation requires annotation.

### Annotation provides context for interpretation
* UCSC
  * Conservation
  * Repeat elements
  * Genome Gaps
  * Cytobands
  * Gene annotations
  * Mappability
  * DeCIPHER
  * ISCA
* dbSNP
* gnomAD browser
* ClinVar
* OMIM
* 1000 Genomes
* ENCODE
  * Chromatin marks
  * DNA methylation
  * RNA expression
  * TF binding
* Human Protein Reference Database
* HGMD
* KEGG
* Pfam

### Case study
Mom and data are unaffected, kie (proband) is affected with rare, Mendelian disease phenotype.

More than 40% of developmental disorders caused by de novo mutation.

### Find variants that disrupt gene function
Synonymous (silent)

Non-synonymous (missense)
* Impact sometimes hard to predict

Stop-gain (nonsense)

Stop-loss

### Loss of function variants
Nonsense SNP

Frame-shift indel

Splice site SNP

Exon deletion

Whole gene deletion

### Annotating the effect of a variant on a transcript
SnpEff, Variant Effect Predictor (VEP), ANNOVAR, Variant Annotation Tools

Many tools + many transcript annotations = many answers
<!-- 해석이 어렵다. 하나 insertion되었다고 해서 그 function에 어떤 영향이 있는지 보려면 뒤쪽 sequence까지 봐야하고.. -->

### An example of the complexity
Insertion of a singla A.
Then, what is the impact?

Variants overlap multiple transcripts and even genes.

Apparent loss-of-function variants are enriched for error.

If a disease phenotype is rare, the causal variant should also be similarly rare.
<!-- coding gene의 경우에는 rare 유전자 모아서 function에 영향이 있는지 같은 방법 사용 가능 -->

### gnomAD
gnomAD reports the allele frequency from diverse ancestries.

https://gnomad.broadinstitute.org/

# Specialized Applications of NGS

### Specialized next-generation sequence (NGS) application
There are many useful applications of NGS technology.
These include:
RNA-seq to measure RNA levels ("gene expression" of genes and isoforms),
chromatin immunoprecipitation sequencing (ChIP-Seq) to measure protein-DNA interactions,
methyl-seq, FAIRE-seq, and many others.

### Perspective
Next-generation sequencing (NGS) technology is revolutionizing biology.
We are now able to catalog genetic variation at unprecedented depth.

There is rapid growth in the technologies used for NGS. 
There are also vast numbers of software solutions for quality control, sequence alignment, genome assembly, variant calling (including single nucleotide variants, indels, and structural variants), and variant prioritization.
Key file formats include FASTQ (“raw” reads), BAM/SAM (aligned reads), and VCF (variant calls). Many tools are available for the generation, analysis, and visualization of these types of files.
