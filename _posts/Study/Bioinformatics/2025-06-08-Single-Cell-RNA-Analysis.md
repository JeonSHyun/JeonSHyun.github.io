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
