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

## What's Happening in the Illumina Sequencing?
<!-- 이 챕터는 시험에는 내지는 않을 예정 -->

### Flowcell - one channel (lane)
MiSeq, HiSeq

### Data Processing
* Image capture (.tif)
* Template Generation (.close)
* Intensities (.cif)
* Base Calls (.bcl) <!-- sequence와 quality score가 있는 파일. 이거로 fastq 파일을 만든다 -->

### Key Steps in Illumina Sequencing
* Cycle 0
  * Focus Calibration
  * First Base Report
* Cycle 1
  * Run infomration
  * Cluster number estimate
* Cycle 5
  * Accuarate cluster number
* Cycle 25
  * CHASTITY % passing filter (PF)
* Cycle 26
  * Q-score

### Fluorescence Signal Cross-talks

### Phasing and Pre-phasing Correction
Phasing, <!-- 하나 뒤쳐짐 -->
prephasing <!-- 하나 더 들어감 -->

### PhiX Spike-in Control

### Base calling

### Quality score
Representation of probability of base called incorrectly.

#### Phred scaled
-10 * log_{10} (prob. error)

Readable from ascii character: Q + 33

## Third Generation DNA Sequencing
<!-- 원래 reference genome에서는 centromere가 없었다. 똑같은 서열이 반복되는 특징이 있어서 assembly하기 힘들었음 -->

<!-- 2세대와 비교해서 3세대 서열분석기의 가장 큰 차이점은? -->

* 2nd generation
  * short read
  * very precise (~99.99%)
  * need to be amplified
  * read does not correspond to the molecule one-to-one
  * low price
* 3rd generation
  * long read
  * less accurate
  * no need for amplification
  * Each read reflects a monomolecule
  * high in price

### short read vs. long read
Long-read sequencing enables more accurate and contiguous genome assemblies by spanning repetitive regions and reducing fragmentation.
(e.g., centromere)

<!-- long read seq의 예시
Friedreich's Ataxia. Repite expansion. methylation 증가로 볼 수도 있다. 증폭하지 않으니 methylation도 볼 수 있다.
RNA-seq를 long read로 보면 isoform을 확신을 가지고 볼 수 있다. -->

### Pacific Biosciences

#### Single-Molecule Real-Time DNA Sequencing (SMRT)
<!-- 민감도를 엄청 높여서 증폭 안하고도 detection 가능하게 -->
DNA polymerase + ZMW Confinement + Phospholinked Nucleotides

#### Methylation
<!-- methylation 있는 부분은 합성이 느리게 되니까 그걸 기반으로 알아냄. -->
Detect base modifications using the kinetics of the polymerization reaction during normal sequencing.

#### SMRT bell
<!-- 여러번 읽은것 중 신호가 깨끗한 것만 골라서 이용해서 정확도를 높임 -->

#### SMRT Sequencing correction
* Intramolecular correction: Circular Consensus Sequence (CCS) <!-- 하이파이리드 -->
* Multimolecular correction <!-- 요즘은 잘 안씀 -->

### Oxford Nanopore Technologies
Portable

#### Nanopore Direct Sequencing
Nanopore sequencing involves passing single-stranded DNA through a nanopore—an extremely small hole typically around 1 nanometer in diameter. 
As each nucleotide (A, T, C, or G) passes through the pore, it causes a characteristic change in the electrical current. 
These changes are measured and used to determine the DNA sequence.

The nanopore is narrow enough that double-stranded DNA cannot pass through directly. 
Therefore, enzymes such as helicases are used to unwind the DNA into single strands before sequencing.

Methylation can also be distinguished.

* Ultra-Long Reads
<!-- single molecule sequencer는 공통적으로 read가 매우 길다. short read seqeunce에서는 phasing과 pre phasing이 있어서 길어지면 뿌옇게 되는데 얘들은 signal을 지저분하게 만들지 않는다 -->

* a lot of errors
* Unless it's SNV analysis, there's usually no big problem <!-- SNV 분석에서는 하나 변이가 매우 중요하기 때문에 -->
* easy to distinguish isoform

#### Problems with Nanopore basecalling
* Multiple bases influence the current passing through the pore
* Through simulation with Brownian Dynamics, we calculated the contribution from triplets of DNA in a solid-state nanopore - 64 current levels
* Not all of these different currents are distinguishable

#### Adaptive Sampling
<!-- 전기를 거꾸로 걸어서 다시 빼거나 할 수 있다. 실시간 제어 가능 -->

Strand approaches nanopore

Region of interest
* Strand is sequenced and analysed in real time
* Region of interest found. Sequencing continues
* Nanopore completes sequencing, available for next strand

Not region of interest
* Strand is sequenced and analysed in real time
* Sequence seens is not in region of interest. Strand ejected. Nanopore available for next strand
* Subsequent strand sequenced

### Comparison 
||Illumina NextSeq|PacBio Sequel 2|Oxford Nanopore Tech. MinION Mk1c|
|------|---|---|---|
|read leangth|150+150 (paired-end)|~20kbp|~50kbp|
|error rate|~0.05%|~0.5%|~1%|
|size|large|huge|small|
|operating time|~2 days|~2 days|~2 days|
|cost (10 Gbp)|~50|~200|~100|
|Usage|Clinical diagnosis, research|sequencing project|real-time diagnosis, sequencing project|

<!-- 2세대가 3세대에 의해 대체되고 하는게 아니라 동시에 사용된다. 3세대는 아직 임상 허가를 받지 못함 등등 -->

## Next Generation Sequencers of 2020
<!-- pre phasing과 phasing 문제 해결 시도들-->

### Element Bioscience Avidity Sequencing
* Bind avidite
* Wash
* Detect base
* Remove avidite
* Step with block
* Remove block

### PacBio Onso: Sequencing-by-binding (SBB)
* Initiate
* Interrogate
* Activate
* Incorporate

<!-- imaging하는 구간과 합성 구간의 환경 등 조건을 다르게 해서 각각의 단계가 잘되게 했다 -->

## "Next" Generation Sequencers

In situ sequencing
* FISSEQ (Fluorescent in situ sequencing)

Single-molecule protein sequencing

Protein Fingerprinting by FRET

Massively parallel Edman degradation

Nanopore Protein Sequencing
