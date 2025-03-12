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
