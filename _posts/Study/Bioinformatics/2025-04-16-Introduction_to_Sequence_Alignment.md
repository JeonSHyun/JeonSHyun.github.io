---
title: Introduction to Sequence Alignment
author: JSH
date: 2025-04-16 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
use_math: true
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

### Substitution Matrix

### BLOSUM62
Blocks Substitution Matrix (BLOSUM62).
It is the default matrix for BLAST.

<!-- 성질이 너무 다르거나 진화적으로 다르면 음수가 나온다 -->

#### BLOSUM matrices
Derives from the BLOCKS database where ungapped alignments are stored.

BLOSUMnn is constructed using alignments with ≤ nn% identity.
<!-- 예를들어 BLOSUM62면 62퍼센트보다 낮거나 같은 identity를 사용한다는 의미. 비슷하게 과도하게 많이 샘플링되는걸 방지하기 위해서 -->

#### Collecting BLOSUM statistics
Count amino acids pairs in each column.
Then, normalize results to obtain probabilities.

Compute log-odds score matrix from probabilities: $S(a, b) = [2 \log_2 \frac{q_{a,b}}{p_a p_b}]$ (rounding)
<!-- q_a,b는 a와 b가 같이 나온 실제 확률 -->

### PAM vs. BLOSUM
* PAM
  * Developed by Margaret Dayhoff, 1978
  * Model: Evolutionary
  * Original name: Point Accepted Mutation
  * Number: Number of accepted point mutations per 100 amino acids
  * PAM100 is more closely related than PAM250 
* BLOSUM
  * Developed by Steven & Joria Henikoff, 1992
  * Model: Sequence identity <!-- BLOSUM은 진화적 유연관계 안봄 -->
  * Original name: Blocks Substitution Matrix
  * Number: Sequence identity (%) to be eliminated from database
  * BLOSUM90 is more closely related than BLOSUM45

## Inserting Gaps

Gap opening penalty is higher than gap extension penalty.

### Pairwise alignment algorithm
Dynamic programming

## Types of Alignment

* Needleman-Wunsch
  * Needleman-Wunsch can be suboptimal in some cases
* Local alignment
  * Local alignments reveal partial overlaps
* Multiple sequence alignment
  * Structure, function, evolution
  * Multiple sequence alignment is highly sensitive to the strategy
  * Progressive alignment <!-- Progressive alignment에는 심각한 문제가 있다. 한번 gap이 생기면 계속 생김.. 그래서 다른 tool을 많이 쓴다. (e.g., ClustalW) -->
  * ClustalW
    * Constructing a guide tree
    * (1) Pairwise alignments (2) Distance matrix (3) Hierarchical clusters (guide tree)

### Every combination has its use
Local and pairwise alignment: homolog search

Local and multiple alignment: structural analysis <!-- 어디가 보존되어있는지 찾을 때 사용 -->

Global and pairwise alignment: comparison between close homologs

Global and multiple alignment: cluster analysis of 16S rRNA

<!-- 왜 이런 방법 쓰는지 한번 확인하면 좋겠당 -->

