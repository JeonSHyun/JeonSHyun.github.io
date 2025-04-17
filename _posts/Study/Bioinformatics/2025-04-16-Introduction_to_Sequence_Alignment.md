---
title: Introduction to Sequence Alignment
author: JSH
date: 2025-04-16 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
---

# Introduction to Sequence Alignment

## Principles of Sequence Alignment

### Implications of Sequence homology
A good alignment can reveal homology between sequences.

Implications of sequence homology
* Evlutionary selective pressure
* Finding biochemically analogous sites
* Structural conservation

### Similarity does not always imply homology
<!-- similarity: 시퀀스 사이의 유사도, homology: 진화적 거리 -->
Similarity: Measures how alike two sequences are at the nucleotide or amino acid level.

Homology: Indicates an evolutionary relationship based on common ancestry.

### DNA sequences are harder to align than protein sequences
6X degrees of freedom, at least.

Less information: 1/4 vs. 1/20 <!-- DNA는 ATGC, protein은 20종 -->

Redundancy in genetic code (e.g., synonymous mutation)

## Scoring Alignment
A correct alignment is not necessarily the best-scoring alignment.

AN alignment of completely unrelated sequences may not have zero identity.

### Dot-plot
Dot-plot for a visual assessment of alignments.

Larger window reduces noises in dot-plots.
Repeats can be detected using a dot-plot.

### Not all mismatches are equally bad
It's better when things of similar nature are aligned.

The overall alignment score is calculated as the sum of the similarities.

Simple scoring matrix just works for aligning DNA sequences. (not protein)

How much similarity can be accepted as significant for protein sequences? 20 ~ 35%.

## Substitution Matrices





