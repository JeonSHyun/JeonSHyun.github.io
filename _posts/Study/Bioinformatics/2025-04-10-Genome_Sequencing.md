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

