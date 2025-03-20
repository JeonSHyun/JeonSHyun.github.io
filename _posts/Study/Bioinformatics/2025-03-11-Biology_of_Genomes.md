---
title: Biology of Genomes
author: JSH
date: 2025-03-11 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
---

# Biology of Genomes

## Maps and Tour Guides

Maps are essential in revealing the organizatoin of the heriditary material.

Different types of map describe different types of observations:
* Linkage maps of genes
* Banding patterns of chromosomes
* Restriction maps
* DNA cleavage fragment patterns
* DNA sequences

### Linkage Maps
Inverse of the recombination rate between two genes in the same chromosome suggest their distance.

### Centromere Positioning
Centromere position can be described three ways: metacentric, submetacentric, acrocentric.

In metacentric chromosomes, the centromere lies near the center of the chromosome.

Submetacentric chromosomes have a centromere that is off-center, so that one chromosome arm is longer than the other.
The short arm is designated "p" (for petite), and the long arm is designated "q" (because it follows the letter "p").

In acrocentric chromosomes, the centromere is very near one end.
Human chromosomes 13, 14, 15, 21, 22, and Y are acrocentric.
The p arms of acrocentric chromosomes in humans contain a high density of rDNA genes. 
These genes are involved in development and can flexibly adjust their length.

### Chromosome Banding
Heterochromatic regions, which tend to be rich with adenine and thymine (AT-rich) DNA and relatively gene-poor, stain more darkly with Giemsa and result in G-banding.
Less condensed (open) chromatin, which tends to be GC-rich and more transcriptionally active, incorporates less Giemsa stain, resulting in light bands in G-banding.

Cytogenetic bands are labeled p1, p2, p3, q1, q2, q3, ect., counting from the centromere out toward the telomeres.
At high resolutions, sub-bands can be seen within the bands.

For example, 7q31.2 indicates it is on chromosome 7, q arm, region3, band 1, and sub-band 2.

### Aberrant Karyotypes
Philadelphia chromosome, Trisomy

### High-resolution Maps
Phenotypically observable trait is too sparse for mapping the genome high-resolution.

Detection of DNA markers using 'restriction map' for:
- Variable number tandem repeats (VNTRs), also called minisatellites.
  - The repeat sequence is 10-100 bp long
  - The sequence repeats 5-50 times

### Restriction Fragment Length Polymorphism (RFLP)
Probing VNTRs and/or Short Tandem Repeats (STRs) from DNA sample.
STRs are 2-7bp repeats.

STR and VNTR can have their repeat counts determined using RFLP. 
Both STRs and VNTRs are regions in DNA that contain repetitive sequences, and the differences in the length of these repeating regions can be analyzed to identify individuals. 
RFLP can be a useful method when analyzing these repetitive sequences.

RFLP involves cutting the DNA with restriction enzymes and analyzing the differences in the lengths of the resulting fragments. 
When analyzing regions containing STRs or VNTRs with RFLP, the restriction enzymes cut the DNA at specific sites, and the differences in fragment lengths can reveal variations in an individual's genes.

### Mapping by DNA Sequencing
Because of the decrease in the cost of sequencing, it can now be used to replace practically every method of genetic mapping in modern applications.

DNA sequencing methods:
- Sanger, Lee Hood methods
- Maxam and Gilbert method
- Next generation sequencing
- Third generation sequencing

### Personal Identification and Ethics

#### Legal application of DNA sequencing
The genomes of all individuals are unique.
Like fingerprints, genomes provide a unique personal identification.
Unlike fingerprints, genomes can indicate familial relationships.
Genome contains some recognizable features such as eye and skin colors.

Genome provides more than just personal identification.
It contains much more information.

### DNA Fingerprint

#### DNA Microsatellite
Short, repetitive sequences of 2-6 base pairs of DNA that are repeated multiple times in tandem. 
Microsatellites are highly variable between individuals and are often used in genetic studies and forensic analysis.

#### Flanking Sequence
The DNA sequences located directly upstream and downstream of a specific target gene or region. 
Flanking sequences are important for identifying and amplifying target regions, such as in PCR, where primers are designed to bind to these sequences.

#### CODIS
The FBI selected 20 unique STRs to be used for comparison and analysis in their DNA fingerprint database (Combined DNA Index System - CODIS). 
Based on population frequency data for each STR allele in CODIS, the probability of specificity can be calculated when STRs match. 
Since there can be significant differences in frequency across different populations, such as race and region, the assumptions about the population can change, which in turn can affect the probability.

### Genome Size Ranges
C-value paradox refers to the phenomenon where the size of an organism's genome (i.e., the total amount of DNA) does not necessarily correlate with its complexity or the number of genes.


## Genome Assembly

### Genome Assembly with de Bruijn Graph
Using kmers list and looking up overlapping (Burrows-Wheeler transform).

Finding a Eulerian path.
- Visit each box only once
- Prune improbable paths using sequence depth and paired ends

* Paired sequencing: a type of DNA sequencing technology where the DNA fragments are read from both ends simultaneously.


### Problems with de Bruijn Assembly

#### Sequence is fragmented due to lack of overlap
Get high coverage sequencing (50X+)

#### Read errors cause bubbles (false edges and nodes)
Hard to distinguish from natural variation (heterozygosity).

Kmer count distinguishes errors can identify random errors.

#### Kmer issues
If kmer is too short, many bubbles and false overlaps occurrs.
If kmer is too long, overlaps missed due to sequence errors.
Kmers should be long enough to be unique in coding regions.

#### Repeats

### Assembly Difficulties with Repeats
If sequence is shorter than repeat, you cannot assemble past the repeat.
Repeats are the single biggest cause of errors in assembly.

### Finishing Shotgun Assembly: Scaffolding
#### Scaffolding
Start with highest quality contigs with unique coverage.
Kmer count tells you depth.

* Contig: a continuous DNA sequence created by aligning and joining multiple short DNA fragments based on overlapping regions (connected sequence). Contigs are used in genome sequencing to reconstruct longer, continuous DNA sequences from shorter reads.

Use mate-pairs - 1000 - 9000 base separation.
Sizing errors make estimate of gap less accurate.

Mate pairs allow neighboring contigs and direction to be established.

* Mate pair sequencing:a DNA sequencing technology that involves cutting the DNA and reading both ends of the fragments. This technique is similar to paired-end sequencing, but there are two main differences. First, in mate-pair sequencing, longer DNA fragments are generated, and the two ends of the fragments are located further apart. Second, the two ends of each DNA fragment are sequenced with a fixed distance between them.


#### Scaffolding and gap filling/closing
Scaffold - contigs with defined order and spacing, but with sequence gaps.

Gap filling is the process of obtaining additional sequences to fill in gaps within scaffolds, while gap closing involves sequencing and connecting those gaps to complete the full genome sequence.

It uses paired end and mate pair information.

### Estimating Genome Size from kmers
To estimate the genome size, you divide the total number of base pairs sequenced (total reads × read length) by the average coverage. 
This gives you the total size of the genome, as coverage indicates how many times each base pair was read during sequencing.


## Genomes of Prokaryotes
### Genomes of Prokaryotes
A large single circular double-stranded genome < 5Mb long, in most cases.
Bacterial coding genes do not contain introns.
Many prokaryotic protein-coding regions are organized into operons, where a single mRNA molecule under common transcriptional control encodes multiple polypeptide chains.
In Archaea, some tRNA genes contain introns (conserved mechanism in Eukarya).
Typical prokaryotic genome contains only a small amount of noncoding DNA. (E. coli has only ~11% noncoding fraction.)

## Introduction to Metagenomics
### Metagenomics
Classical microbiology: identifying pathogenic organisms responsible for infectious disease.
- Isolation, cloning and characterization of pure strain is essential.

To understand general principles of microbial ecology and evolution, an alternative approach is need by studying the entire microbial communities.

Subjects of metagenomic sequencing include:
- General environmental samples: oceans, glaciers, soils, mine tailings, ect.
- Human microbiome
- Agricultural samples

### Difficulties in Metagenomic Sequencing
Sequencing the complex mixture of diverse sources introduces many dificulties.
BLAST searches may identify sources of fragments and some function.
Understanding the functional relationships and interactions is challenging.

16S rRNA sequencing:
16S rRNA sequencing is a method used to identify and classify bacteria and archaea by analyzing the 16S rRNA gene. 
This gene is common across all bacteria and archaea, but specific regions vary by species, making it useful for microbial identification and diversity studies.
- Advantages: Efficient and straight-forward
- Disadvantages
  - Copy-number variation problem
  - Insufficient resolution in the species or strain level
  - Viruses are invisible to this method

Whole metagenome sequencing

### The Sorcerer II Global Ocean Sampling Expedition

### Questions of Metagenomics
- Who is there?
  - What is the relative proportion of communitiy members?
  - How rich is the community?
  - How evenly distributed?
- What are they doing?
  - What functional chemistry is being carried out?
  - What environmental products are consumed and what is excreted?
- How are they doing it?
  - Which enzyme pathways are present?
  - How is pathway activity stratified within the sample?

### Applications of Metagenomics
Human health, agriculture, environmental remediation, anthropology, biotechnology

## Genomes of Eukaryotes

### Eukaryotic Genomes
Majority of DNA is in the nucleus, separated into bundles of nucleoprotein, the chromosomes.
Each is a linear double-stranded DNA.

Organellar genomes are in the circular dsDNA from in mitochondria and chloroplasts.

Chromosome structure variations:
- Polyploidization
- Translocation, fragmentation or joining
  - Human 2 = chimpanzee 12 + 13
  - Thought to contribute to reproductive isolation in species separation

### Gene Families
Termed by the type of separation event
- Ortholog: genes in different species that evolved from a common ancestor
- Paralog: genes within the same species that result from a duplication event
- Xenolog: genes transferred between species via horizontal gene transfer
- Analog: traits in different species that perform similar functions but do not share a common evolutionary origin

Pseudogenes: duplicated by retrotransposition from mRNA, followed by the accumulation of mutations.
- mRNA is reverse-transcribed into DNA by reverse transcriptase and inserted back into the genome. This new DNA copy lacks a promoter and other essential elements, so it is not expressed or loses its function.

## The Human Genome

### The Human Genome
3.2 Gbp (30 times larger than C. elegans or D. melanogaster)

22 Chromosomes plus X and Y. (also the mitochondrial genome)

Coding sequence ~5%, 20-25k genes.

35% of human genes are alternatively spliced.

Many genes contain large introns: dytrophin, coding 3685 a.a., is >= Mbp long.

### Repeat Sequences in Human genome
55% of non-transposable elements

### Types of Transposable Elements
Elements
- Short interspersed nuclear elements (SINE)
- Long interspersed nuclear elements (LINE)
- Long terminal repeats (LTR)
- DNA transposon fossils

Retrotransposons use a copy and paste mechanism.
DNA transposons use a cut and paste mechanism.

TEs are thought to drive evolution by rewiring the genomic circuits including:
- Gene inactivation/activatoin
- Changing gene regulation
- Changing gene products

### RNA Genes in Human Genome
- 497 tRNA genes: one large cluster in chr6 (140 genes in 4Mbp regions)
- Ribosomal DNA genes: 18S, 28S, 5.8S appear in 44kb tandom repeat unit of 150-200 copies. 5S rRNA genes also appear in tandem arrays containing 200-300 genes.
- Small nucleolar RNAs (snoRNAs): cleave and process rRNAs.
- Spliceosomal snRNAs: U1, U2, U4, U5, and U6 snRNAs appear in clusters of tandom repeats of nearly identical or inverted repeats
- Regulatory small RNAs: small interfering RNAs (siRNAs), microRNAs (miRNAs), PIWI-interacting RNAs (piRNAs)
- Other non-coding RNAs: 7SL RNA (sprRNA), RNase P, vault RNA, etc.

### Single-nucleotide polymorphism (SNP)
Two unrelated individuals iffer in ~0.1% of the whole genome.
Many of the differences are SNPs.
There are also many deletions.

SNP is a genetic variation limited to a single base pair that can be substituted, inserted, or deleted.

Most SNPs are not linked to diseases.
Many are not even within functional regions.

Ex) Sickle-cell anemia: a disease caused by A>T mutation in beta-globin gene, changes Glu to Val.

### Types of SNPs
- Missense
- Nonsense
- Silent

### Treatment of Diseases by Defective or Absent Proteins
Providing normal protein: Insulin for diabetes, human growth hormone for developmental delays

Lifestyle adjustments that makes the functional unnessary: Phenylketonuria (PKU), a deficiency in phenylalanine hydroxylase (converts Phe to Tyr), causes developmental defects including mental retardation

Gene therapy: to replace absent proteins, viral vectors, mRNA drugs, CRIPR technology could be used.

### Systematic Collection of SNPs: HapMap
Internation HapMap project has collected and curated haplotype distributions from more than 1571 individuals from 11 population groups.
