---
title: Gene Expression Analysis
author: JSH
date: 2025-06-04 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
use_math: true
---

# Gene Expression Analysis

*  Identifying differentially expressed genes between different experimental conditions or samples, such as comparing cancerous and non-cancerous tissue.
*  Characterizing gene expression patterns in various cell types or tissues, such as identifying genes that are specifically expressed in brain cells.
*  Discovering novel transcripts and alternative splicing events, which can lead to the identification of new protein-coding genes and non-coding RNAs.
*  Quantifying gene expression levels for functional genomics studies, such as identifying genes involved in specific biological pathways or determining the effects of genetic mutations.
*  Assessing the quality and integrity of RNA samples, such as detecting contamination or degradation of samples.
*  Study of gene expression in non-model organisms, such as studying the gene expression of a plant species which is not well studied.
*  Study of the expression of viral genes in host organisms, such as studying the expression of viral genes in a host organism infected with a virus.

<!-- 약물을 처리했을 때 여러 pathway가 켜지거나 꺼지는 것도 확인 가능 -->

## RNA vs. DNA
Functional Study: While the genome generally does not change, gene expression can vary greatly depending on experimental conditions
* Cell lines treated vs. untreated with drugs
* Wild-type vs. knockout mice

In genome sequencing, it is difficult to accurately predict transcript sequences.
With the advent of RNA-seq, gene annotation has been revolutionized.

Some molecular features are only observable through RNA. (Alternative isoforms, fusion transcripts, RNA editing)

When interpreting synonymous mutations that do not change the protein sequence.
* Regulatory synonymous mutations can affect how much mRNA is produced

When prioritizing among protein-coding missense mutations
* Synonymous mutations in non-expressed genes are less informative.
* Loss-of-function mutations are more likely to be detected in wild-type alleles
* If the mutant allele is expressed, it may be considered a potential drug target

## RNA vs. Protein

| Category             | RNA Profiling                                                                 | Protein Profiling                                           |
|----------------------|--------------------------------------------------------------------------------|--------------------------------------------------------------|
| Coverage             | Can observe nearly all expressed RNAs easily                                  | Usually only partially observable                           |
| Alternative splicing | Can be examined in detail                                                     | Much more difficult                                          |
| Experimental issues  | Less prone to bias, more reproducible, and lower error rates                  | Relatively high bias, lower reproducibility, higher error    |
| Scalability          | Cost-effective and easy to scale                                              | Scaling up is more burdensome                               |
| Novel transcript     | Sometimes possible even without a reference genome                            | Requires high-quality reference                             |

<!-- 단백질의 경우에는 화학적인 성질이 모두 다르지만 RNA는 그렇지 않다 (실험적 문제) -->

## Bulk vs. single-cell
| Category                    | Bulk RNA-seq                                                                 | Single-cell RNA-seq                                                                 |
|-----------------------------|------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Cost & Effort               | Relatively simple and inexpensive                                            | More expensive and burdensome                                                       |
| Sample Quality & Quantity   | Can work even with low-quality or small-quantity samples                     | Requires relatively strict standards for quality and quantity                        |
| Representation in Profile   | Can capture average expression with less external influence                  | Requires minimal delay even without sorting, up to cell lysis                       |
| Scalability                 | Easy to handle even with large sample numbers                                | Limited scalability for increasing sample numbers                                   |
| Customization               | Easy to adjust based on target of interest                                   | Protocol changes are limited                                                        |

<!-- single cell은 cell끼리 분리하는 과정이 필요하다. 그래서 cell이 분리되려고 스트레스 받은 그 상태로 스냅샷을 얻는다 -->

## Bulk RNA-seq vs. Spatial transcriptome
| Category                    | Bulk RNA-seq                                                                 | Spatial Transcriptomics                                                                |
|-----------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Cost & Effort               | Relatively simple and inexpensive                                            | More expensive and burdensome                                                         |
| Sample Quality & Quantity   | Can work even with low-quality or small-quantity samples                     | Requires relatively strict standards for quality and quantity                          |
| Coverage                    | Can observe nearly all expressed RNAs                                        | Limited observation depending on quantity, length, location, and sequence              |
| Scalability                 | Easy to handle even with large sample numbers                                | Limited scalability for increasing sample numbers                                      |
| Customization               | Easy to modify protocols (like changing recipes)                             | Many restrictive conditions for protocol modification                                  |

## RNA profiling library preparation steps

### RNA-seq Library Preparation
mRNA $\rightarrow$ Library Preparation $\rightarrow$ Sequencing-ready library

### Illumina TruSeq Small RNA
* mRNA
* Fragmentation
* Ligation of 3' pre-adenylated adapter
* Ligation of 5' adapter <!-- 아는 sequence를 붙이기 위해서. -->
* Sequencing-ready library

<!-- 이후 Reverse transcription 및 PCR 과정 거친다. -->
<!-- 3', 5' adapter는 single strand이다. (중요) -->
<!-- sequencing할 때 방향을 알 수 있다 -->

### Vanilla RNA-seq
<!-- 최초의 RNA seq -->
* PolyA + RNA captured
* RNA fragmented and primed
* First strand cDNA synthesized
* Second strand cDNA synthesized
* 3' end adenylated and 5' ends repaired
* DNA sequencing adapters ligated
* Ligated fragments PCR amplified

<!-- 
first strand: RNA와 반대쪽. 그림 상으로 2)의 빨간색.
이후 first stand 만들고 RNA 없애고 second strand만든다.
문제: strand를 알 수 없다. 왜냐면 first, second 만들고 나서 double strand가 되는데 어디가 first, second인지 알 수 없다. adapter가 똑같은게 대칭으로 붙어있기 때문에.
일부 겹쳐있는 유전자 구분을 하거나 annotation이 안되어있는 유전자는 분석이 어렵다는 문제가 있었다.
-->

### Stranded RNA-seq (dUTP-based)
<!-- Vanilla RNA seq의 strand 알 수 없는 문제 보완 -->

* mRNA
* Fragmentation
* 1st strand synthesis (U) and 2nd strand synthesis (T) dutf
* Adapter ligation
* Degradation of labeled strand <!-- U가 있는 1st strand 없앰 -->
* PCR amplification
* Sequencing

<!-- first strand는 U만 있고, second strand는 T만 사용함
이후에 U를 잘라주는 enzyme을 활용. 이후 second strand만 이용해서 PCR함. 그러면 방향성 알 수 있다. -->

### The Peregrine Method
* Fragmented RNA
* RT & 3' extension
  * Reverse transcription is initiated using an oligo(dT) or random primer
  * The reverse transcriptase synthesizes the first-strand cDNA and adds a few non-templated cytosines (C) at the 3′ end of the cDNA
* Template switching
  * A template switching oligo (TSO) with guanosine (G) overhangs hybridizes to the extended C residues, allowing the reverse transcriptase to continue synthesis and append a defined adaptor sequence to the 5′ end
* 2nd strand synthesis
* Sequencing-ready library

<!-- stranded rna-seq의 경우에는 끝부분은 depletion되고 가운데가 많이 나오는 경향이 있다. size가 끝부분이 좀 작게 나온다. 그래서 나중에 sequencing이나 PCR에서 필터링됨.
하지만 이 방법은 5'쪽으로 좀 쏠린다. 
이 의미는 일반적인 RT는 5' 말단까지 도달하지 못하는 경우가 많은데, template switching RT는 효소가 5' 말단에 도달해야만 TSO가 붙고 adaptor가 붙으므로, 성공한 cDNA들은 대부분 5' end까지 잘 복원된 transcript이기 때문이다. -->

### Modern RNA-seq variants: SMART-seq2
<!-- 모든 RNA를 균일한 품질로 full length cDNA를 만드는 게 목적이다. -->
<!-- fragmentation 안하고 RT, PCR부터 시작함 -->

* Cell lysis
* Reverse transcription and terminal transferase
* Template switching by reverse transcriptase
* PCR preamplication of cDNA
* PCR cleanup
* Tagmentation (Tn5)
<!-- tagmentation을 한다. double strand DNA에 중간중간 adapter를 넣는다. cDNA fragmentation + adapter insertion 한번에. 
다른 방법들처럼 RNA 상태에서 fragmentation하면 길이도 재각각, 불안정함.
double strand DNA는 훨씬 균일하다. 훨씬 안정적 -->

* Gap repair, enrichment PRC and PCR purification
* Sequencing

<!-- 효율적이다! 초기 single cell RNA seq에서 사용한 방법이다 -->

### Cap Analysis of Gene Expression (CAGE)
CAGE maps where genes start by sequencing the 5' capped ends of mRNA, allowing precise detection of transcription start sites.

<!-- rRNA는 cap이 없으므로 sequencing 안된다. (rRNA 오염 없어서 장점임) -->

### Rapid Amplification of cDNA-Ends (RACE)
* 5' RACE
* 3' RACE

<!-- sequence가 어디서 시작해서 어디서 끝나는지 구조 알 수 있음.
5' RACE는 5' end를 detection, 3' RACE는 3' end를 detection.
RACE는 끝을 detection하기 힘들기 때문에 별로 안좋고 요즘은 잘 안쓴다. -->

### Targeted RNA-seq by dual PCR
Targeted RNA-seq by dual PCR is a method that selectively amplifies specific RNA targets using two rounds of PCR—first to enrich for the genes of interest, and second to add sequencing adapters and indexes.

<!--
16s sequencing, 18s sequencing에 이용함.
primer 2개를 가지고 primer 뒤에 illumina overhang을 붙여서 그걸로 PCR해서 원하는 유전자만 targeting.
targeted meta transcriptome 이런거 할때 사용.
-->

### Targeted RNA-seq by hybridization probes
* Pool stranded RNA-Seq libraries
* Hybridize biotinylated probes to targeted regions
* Capture using streptavidin beads
* Elution from beads

<!--
양이 정말 적은 RNA를 찾기 위해서 이용.
hybridization 이용하는 방법은 PCR이용한 targeted sequencing보다는 효율이 안좋지만 PCR bias는 없다
-->

### Library preparation overview
From tissue, isolate total RNA.

#### Assess RNA quality
* Gel electrophoresis of RNA
* Capillary electrophoresis of total RNA

<!-- Gel electrophoresis of RNA는 퀄리티를 보기 위해서. RIN 값으로도 볼 수 있다.
RIN3은 안쓴다. 어지간하면 RIN9.5 이상의 좋은 RNA를 이용한다. -->

#### Library preparation
<!-- QC한 RNA 빼고 나머지로 rna 프랩 한다. -->

* DNAse treat and enrich
* RNA fragmentation
* cDNA synthesis
* cDNA fragmentation
* Size selection or exclusion
* Add sequencing adapters
* Sequence

## Key Considerations in RNA Analysis
* Sample status
  * Purity: Chemical purity, purity by cell type, etc.
  * Quality: RNA integrity <!-- DEG 분석하는 RNA integrity는 비슷해야 결과가 이상하지 않게 나온다 -->
  * Quantity: < 1 ng, 10–50 ng, 50–500 ng, ≥ 500 ng <!-- 양이 적으면 bias가 엄청 많이 걸린다. 양은 최대한 똑같이, 많이 하는게 좋다 -->
* RNA sequencing shows short exons connected between long introns in the genome.
  * Must consider in advance whether the experimental design allows proper mapping to the genome.
* RNA abundance varies significantly.
  * Differences can be up to 10⁵ to 10⁷-fold
  * RNA sequencing involves random sampling. Highly expressed genes take up the majority of reads.
  * Ribosomal RNA and mitochondrial RNA
  * Ribosomal protein mRNA
<!-- 
DNA는 cell당 개수가 한 copy로 정해져있는데 RNA는 cell당 개수 차이가 엄청나게 많이 날 수 있다. 이러면 라이브러리 프랩할때 다 반영이 되어버린다.
그래서 ribosomal RNA와 mitochondrial RNA는 제거하고 시작한다. 얘들이 너무 많이 나오기 때문.
ribosomal protein mRNA는 반드시 제거하지는 않더라도 많이 나오기 때문에 주의.
-->
* RNA comes in various sizes
  * Small RNAs require completely different preparation methods.
  * For long RNAs, poly(A) selection can cause 3′ end bias.
<!-- RNA는 화학적 성질이 비슷하다고 했지만 길이가 비슷할 때의 얘기. -->
* RNA is more fragile than DNA.

## Selection/depletion
<!-- rRNA를 없애는 방법들 -->

### Total RNA
Includes all RNA species, with rRNA making up the majority; used without rRNA removal.
* Broad transcript representation.
* Abundant RNAs dominate
* High unprocessed RNA
* High genomic DNA
<!-- total RNA: 도저히 rRNA를 제거할 수 없을 때 사용하는 특수 케이스 -->

### rRNA reduction
Selectively removes ribosomal RNA using complementary probes that hybridize to rRNA sequences.
* Broad transcript representation
* Abundant RNAs de-emphasized
* High unprocessed RNA
* High genomic DNA
<!-- rRNA reduction: rRNA에 상보적인 서열 이용해서 제거. 효율 떨어짐 -->

### PolyA selection
Enriches mRNAs with poly-A tails, removing most rRNA and non-polyadenylated RNAs.
* Limited transcript representation (polyA)
* Abundant RNAs de-emphasized
* Low unprocessed RNA
* Low genomic DNA
<!-- poly A selection이 가장 많이 사용됨. poly A가 없는 다른 RNA도 제거된다는 단점이 있다. -->

### cDNA capture
Uses probes to selectively capture cDNA of specific genes or transcripts of interest.
* Limited transcript representation (targeted)
* Abundant RNAs de-emphasized
* Low unprocessed RNA
* Low genomic DNA

<!-- exome에 붙여서 함. exome에 못붙는 rRNA는 제거됨. exome enrichment 키트가 비싸서 잘 사용 안함. -->

## Stranded & Unstranded
In unstranded RNA-seq, the strand of origin (+ or −) of the RNA is not preserved.
In stranded RNA-seq, the strand information of the RNA is retained.
This allows for clear identification of the gene's transcriptional direction and precise genomic location.

## RNA Quality Check
RIN = RNA integrity number.

0(bad) to 10 (good)

<!-- 6만 되어도 깨진 RNA임. -->

## Replicates
### Technical Replicate
Multiple instances of sequence generation
* Flow Cells, Lanes, Indexes
<!-- 같은 샘플인데 기술적으로 다르게 -->

### Biological Replicate
Multiple isolations of cells showing the same phenotype, stage or other experimental condition

Some example concerns/ challenges: Environmental Factors, Growth Conditions, Time

<!-- 다른 샐에서 나온 데이터 -->

## RNA-seq Experimental Design
* What insight is the goal?
* Signal-to-noise ratio
<!-- 원하지 않는 잡음에 해당하는 다른 cell들 때문에 DEG 결과가 안나올 가능성이 많다. 그래서 예시에도 single sorted했을때는 안나왔는데 double sorted하니까 엄청 많이 나와버림 -->
* More sequence or more replication?
<!-- expression level이 낮으면 read가 많이 필요하다. 예시의 y는 variability. 이게 낮은게 좋다.
variability가 높을수록 read count 및 replicate도 많이 필요하다.
-->
* The source and quantity of data distribution vary greatly depending on the type of sample and experiment
<!-- read count가 적어도 pathway를 만들어서 분석하면 잘 될수도 있다.. -->
* Batch effect

<!-- batch correction을 잘 해야한다
서로 비교하는 쌍끼리 맞춰서 sequencing해서 batch를 만들어야 한다. batch balancing해야 한다. -->
