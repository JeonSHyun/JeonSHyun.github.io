---
title: Single-Cell RNA Analysis
author: JSH
date: 2025-06-08 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
use_math: true
---

# Single-Cell RNA Analysis

## Droplet-based single cell RNAseq (scRNAseq, drop-seq)
Droplet-based single-cell RNA-seq captures and sequences mRNA from individual cells by encapsulating them into nanoliter-sized oil droplets along with barcoded beads, enabling high-throughput transcriptomic profiling of thousands of cells simultaneously.

10x workflow
* Master mix + Sample
* Gel Beads
* Oil

<!-- 
droplet 하나에는 bead가 하나 들어가있고 cell들이 하나씩 들어가있다
완성된 droplet은 GEM이라고 부른다.

dorp-seq은 cell, reagent, bead가 따로 들어오고 마지막에 oil이 들어와서 합류
모든 single cell rnaseq에서 oil이 마지막에 들어와서 droplet을 끊어주는건 공통적임
-->

### Droplet
Component
* Read 1 sequence 
  * primer
* 10x Barcode
  * Unique to each bead (cell)
* UMI
  * Unique to each molecule
* Poly(dT)VN
  * mRNA capture (Poly(A) tail recognition)
* mRNA

<!--
Poly(dT)VN: PolyA의 끝을 잡는다
10x Barcode: cell barcode. 같은 bead에 붙어있는건 seq가 전부 같다. 이 cell은 누구였다 하는걸 대변.
UMI: 모든 molecule에 다 다른다. UMI가 같으면 같은 molecule이다. 같은 cell이라도 다르다.

single cell에서는 PCR이 과도하게 될 때 있다. 그래서 UMI가지고 똑같은 UMI와 똑같은 cell barcode인 애들은 같이 묶어준다.
-->

### Library Preb in Droplet
* Reverse transcription
* Priming of TSO
* Template Switch, Completion of Trancript Extension

<!--
droplet 안에서 뭘 하는지?
* RT (3' 끝에서부터 시작)
* CCC를 붙임 -> TSO 붙임 (template switch)
* switch oligo 상보적인 서열 합성

여기까지 droplet 안에서 끝!
여기서 droplet을 깨도 되는 이유는 합성한 cDNA에 바코드가 붙어있기 때문에 섞여도 찾을 수 있기 때문이다!
-->

Droplets can now be broken, and remaining steps carried out in bulk.

### Library Preb after Droplet
* Double strand cDNA
* cDNA Amplication (PCR #1)
* Enzymatic Fragmentation
* End Repair, A-Tail, Ligation <!-- 뒤에 DNA adapter 붙이기 위한 방법 -->
* Clean up
* Sample index PCR (PCR #2) <!-- sample index 붙인다. 따라서 sample index, cell barcode, umi. 바코드 총 세개 -->

### Sequencing
* Read 1 (28 bp):
  * Cell Barcode – identifies the individual cell (typically 16 bp)
  * UMI (Unique Molecular Identifier) – identifies unique transcripts (typically 10–12 bp)
* Read 2 (91 bp):
  * Contains the cDNA insert, derived from the original mRNA transcript.
* Index Read (Sample Index, typically 8 bp):
  * Contains the sample barcode.

<!--
P5, P7: flow cell에 붙여주는 부분
Read 1: 10xBC와 UMI가 먼저 나오고, Poly(dT)VN나온다
Read 2: 3' UTR 앞쪽, gene body 안쪽이 먼저 sequencing됨

sample index는 Read 2의 반대쪽으로 읽는 방식으로.
-->

### Cellular Indexing of Transcriptomes and Epitomes by Sequencing (CITE-seq)
CITE-seq allows simultaneous measurement of gene expression and protein abundance at the single-cell level by using DNA-barcoded antibodies that mimic mRNA.

Antibodies are conjugated with a unique DNA barcode and a polyA tail.
These tagged antibodies bind to surface proteins on cells.
Cells are encapsulated with barcoded beads in droplets.
After lysis, both mRNAs and antibody-oligos hybridize to the beads' RT primers.
As a result, both transcriptome and protein (epitope) information are captured and indexed with the same cell barcode.

<!-- cell 표면에 어떤 게 붙어있는지 정보를 함께 제공하는 방법 -->

### scATAC-seq
<!-- scATAC-seq은 transposome을 이용해서 open chromatin을 식별하는 방법 -->
 
scATAC-seq enables genome-wide profiling of chromatin accessibility at single-cell resolution.
It identifies regulatory DNA regions by targeting open chromatin using Tn5 transposase within droplets containing isolated nuclei and barcoded beads.

### Multiplexed assays
TEA-seq: a trimodal assy for measurement of transcripts, epitopes, and accessibility in thousands of single cells.
* T: poly-A capture. 3' cDNA library <!-- RNA expression -->
* E: poly-A capture. ADT library <!-- antibody -->
* A: Tn5-inserted oligo capture. ATAC-seq library <!-- open chromatin -->

# Spatial Transcriptomics

## What are the uses of spatial transcriptomics?
* Preserves native tissue architecture.
* Maps gene expression to exact locations.
* Reveals tissue domains & microenvironments.
* Captures cell-cell interactions in context.

<!-- 뇌와 발생생물학에서 spatial transcriptome 연구를 많이 한다 -->

## Sequencing-based ST (sST)
A sequencing-based technique that determines the spatial localization of cells and their gene expression profiles within a tissue section.
* Slide-seq, Q0X Visium, Stereo-seq
* Standard NGS libraries
* Computational spot deconvolution
* Lower resolution, higher sensitivity

Workflow
* A tissue slide is prepared with spatially barcoded capture probes (usually arranged as a fixed oligonucleotide array).
* A tissue section is placed on the slide and subjected to fixation and permeabilization to preserve RNA and allow it to diffuse.
* mRNAs from the tissue hybridize to the capture probes on the slide surface.
* Reverse transcription is performed to synthesize cDNA from the captured mRNA.
* The cDNA is sequenced along with the spatial barcodes embedded in the slide, linking gene expression to specific positions.
* A spatial gene expression map is reconstructed, showing where in the tissue each gene is expressed.

<!--
slie에다가 티슈를 올린다.
특정 지역 스팟에 바코드가 있다.
바코드를 빽뺵하게 깔면 resolution이 더 좋아진다

디컨볼루션은 공간 전사체 데이터에서 각 spot에 어떤 세포 유형이 얼마나 섞여 있는지를 추정하는 계산 과정

resolution이 낮다 = 바코드가 cell보다 훨씬 크기 때문
sensitivity가 높다 = 발현량이 낮은 유전자도 detection 가능
-->

## Imaging-based ST (iST)
Imaging-based Spatial Transcriptomics (iST) refers to a group of technologies that use fluorescence microscopy and in situ hybridization to visualize and quantify RNA transcripts directly within tissue sections.

* MERFISH, seqFISH, RNAscope, Xenium
* In situ hybridization + imaging
* Single-molecule detection
* Multiplexed combinational labeling
* Higher resolution but fewer genes

Workflow
* Tissue preparation and fixation
* In situ hybridization using gene-specific probes that bind to target mRNAs
* Fluorescence labeling – either:
  * Using different fluorophores per gene (limited multiplexing)
  * or, using combinatorial barcoding with multiple rounds of imaging (high multiplexing)
* Microscopy imaging – collecting fluorescence signals
* Image processing to reconstruct gene expression maps at single-cell or subcellular resolution

<!--
cell을 fixiation하고 거기서 readout probe를 붙여서 깜빡거리게 한다.
시간이 오래걸리지만 해상도 매우좋다! 어떤것은 cell resolution 이하까지 볼 수 잇다. (어떤 유전자는 핵 안에 있더라..)
readout probe: 미리 지정해야만 detection 가능. 미리 어떤 유전자를 잡을지 결정해야한다. (pannel)
multiplexed combinatorial labeling: 내가 detection하고 싶은 유전자 probe들을 여러 조합으로 해서 경우의 수에 따라서 하는 것.. -> gpt에게 물어보기 2^n-1개만큼.
error correction 때문에 실제로는 조금 더 많이 피룡하다.
단점: 유전자 개수가 제한된다
-->

Multiplexed combinatorial labeling is a strategy where gene-specific probes are labeled with combinations of fluorophores across multiple imaging rounds. 
By decoding the unique sequence of colors (a barcode), many genes can be simultaneously detected beyond the limit of available fluorophores.

## From Tissues to cell types and back again
* Bulk analysis
* Single-cell analysis
* Spatial analysis

<!--
cell 단위를 할것이냐 image base를 할것이냐

세개 다 같이 진행이 되어야 한다.
bulk - 가격이 싸고, 발현량이 낮은것도 잘 잡는다. preliminary study에 사용. gene pannel을 잡기 위한 기본 데이터
single-cell - clustering 쉽다. cell type과 종류 알아보기 좋다. sensitivity 좋다. 
spatial - 공간정보 좋다. detection하는 유전자 개수 떨어진다.

single-cell + spatial 같이 보는게 좋다.
-->
