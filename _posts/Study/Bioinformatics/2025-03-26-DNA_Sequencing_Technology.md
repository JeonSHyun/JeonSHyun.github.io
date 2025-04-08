---
title: DNA Sequencing Technology
author: JSH
date: 2025-03-26 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
---

# DNA Sequencing Technology

## First Generation DNA Sequencing

### Sanger DNA Sequencing
Sanger DNA sequencing uses ddNTPs and capillary electrophoresis to determine the nucleotide sequence of DNA.
* ABI Prism 3700
  * The ABI Prism 3700 uses fluorescently labeled ddNTPs and capillary electrophoresis to analyze DNA sequences.
  * In capillary electrophoresis, DNA fragments are separated by size as they move through a capillary under an electric field, with smaller fragments moving faster than larger ones.
* Lee Hood automation
  * Used fluorescently labeled ddNTPs to synthesize DNA and analyzes it with automated machines

### Maxam-Gilbert method
The Maxam-Gilbert method is a DNA sequencing technique based on degradation, where 5′ ends are radiolabeled and various chemical treatments are used: formic acid for A+G, dimethyl sulfate for G, hydrazine for C+T, and hydrazine+NaCl for C.
It often requires concentration adjustments.

## Second Generation DNA Sequencing

### The process of second-generation sequencing
* Library preparation
* Cluster formation
* Sequencing reaction and imaging
* Image analysis and base calling

### 454 Sequencing
* Share DNA
* Add adaptors
* Attach to beads. Trap in oil droplet micro-reactors
* Amplify w/PCR
* Trap DNA-coated beads in wells (up to 1 million)

### Pyrosequencing: luciferase from fireflies
Protocol
* Hybridize sequencing primer
* Add DNA polymerase, ATP sulfurylase, luciferase, apyrase & substrates (adenosine 5' phosphosulfate (APS) and luciferin)
* Nucleotide incorporation catalyzes chain reaction that results in light
* Add bases sequentially, and repeat ~500 times

### 454 sequencing: summary
First post-Sanger technology (2005).

Used to sequence may microorganisms & Jim Watson's genome (for $2M in 2007).

Longer reads than Illumina, but much lower yield (~500bp).

Rapidly outpaced by other technologies - now essentially obsolete.

### Illumina sequencing

### Bridge-PRC
#### Sequencing Library Preparation Stage
* DNA fragmentation
* Adapter ligation, size selection, and PCR amplification
* Denaturation <!-- DNA 분자가 두 가닥으로 분리되는 과정 -->
* Loading onto the flow cell
#### Inserting single molecules into the flow cell and amplifying them through bridge PCR
* DNA folds over into a bridge-like shape
* Complementary (reverse) strand is made using primer
* Clonal copies of both forward and reverse strand in a cluster

### Solexa/Illumina Sequencing-by-synthesis (SBS)
<!-- 이후 sequencing 과정 -->

* Incorporate all four nucleotides, each label with a different dye
* Wash, four-colour imaging
* Cleave dye and terminating groups, wash  <!-- 색이 계속 쌓이지 않도록 wash과정 거침 -->

<!-- 여기서 합성이 중단되어야 하는데, terminal blocker 이용. Fluorescently-labeled nucleotides를 사용하는 시퀀싱 과정에서, terminal blocker는 염기 추가 후 fluorescent 신호가 정확히 감지될 수 있도록 도와 -->

### Illumina SBS: 2- and 4-Channel Sequencing
<!-- 현재는 4채널 말고 2채널 사용함. 생각보다 잘 나오고, 비용도 저렴 -->
<!-- 2채널일 때, A 색, B 색, A+B 색, 색x 이렇게 하면 됨 -->

### Illumin SBS: 1-Channel Sequencing
<!-- 장점: 카메라가 색 구분 안해도 된다. 비용이 많이 저렴해짐. -->
<!-- 두번 나눠서 sequencing. 첫번째에는 A, T, 두번째에는 T, C. 두번 깜빡거리면 T. 한번도 안했으면 G. -->

### Paired-end sequencing
A molecular hack to sequence longer fragments
<!-- 양쪽으로 sequencing. 중간을 겹치게 디자인하면 중간 seqeuncing이 아주 높은 퀄리티로 된다 -->

<!-- paired-end sequencing에서 read 횟수는 몇 번까지 갈 수 있을까요?: 4번 이상. -->
<!-- 합성하고 떼고, sequencing 하고.. 할 수 있어서 여러번 시퀀싱 할 수 있다 (?) -->

