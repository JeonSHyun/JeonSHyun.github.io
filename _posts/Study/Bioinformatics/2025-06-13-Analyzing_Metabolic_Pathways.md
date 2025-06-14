---
title: Analyzing Metabolic Pathways
author: JSH
date: 2025-06-13 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
use_math: true
---

# Analyzing Metabolic Pathways

## Pathway and Network Analysis
* Any analysis involving pathway or network information
* Most commonly applied to interpret lists of genes
* Most popular type is pathway enrichment analysis
* Helps gain mechanistic insight into omics data

### Pathways vs. Networks
#### Pathway
* Detailed, high-confidence consensus
* Biochemical reactions
* Small-scale, fewer genes
* Concentrated from decades of literature

#### Network
* Simplified cellular logic, noisy
* Abstractions: directed, undirected
* Large-scale, genome-wide
* Constructed from omic data integration

### Types of Pathway/Network Analysis

#### Enrichment of fixed gene sets
* Goal: Identification of pre-built pathways or networks that are enriched in a set of mutated or differentially expressed genes.
* Tools: GSEA, g:Profiler, KEGG Colorizer, Gitools, SLEA, CAMERA
* Output: Enriched network, Depleted network
* Question: What biological processes are altered in this cancer?

#### De novo sub-network construction and clustering
* Goal: Construction of specific sub-networks from the set of mutated or differentially expressed genes to identify an extended list of putative cancer genes.
* Tools: STRING, GeneMANIA, Reactome FI Viz, MEMo, ResponseNet
* Output: Mutated (seed) proteins, Extended network
* Question: Are new pathways altered in this cancer? Are there clinically-relevant tumour subtypes?

#### Pathway-based modeling
* Goal: Evaluation of potential network rules that would be consistent with the identified set of mutated, differentially expressed or amplified and deleted genes.
* Tools: Paradigm, HotNet, SPIA, TieDIE, Pathifier
* Output: Loss-Of-Function Network Signature, Gain-Of-Function Network Signature
* Question: How are pathway activities altered in a particular patient? Are there targetable pathways in this patient?

## Benefits of Pathway Data (vs. transcripts, proteins, SNPs)
Improves statistical power due to fewer tests.

More reproducible (e.g., gene expressio signatures).

Easier to interpret since it uses familiar concepts (e.g., cell cycle).

Identifies mechanism and can explain cause.

Predicts new roles to genes.

## Before Analysis
* Normalization
* Background adjustment
* Quality control (garbage in, garbage out)
* Use statistics that will increase signal and reduce noise specifically for experiment
* Gene list size
* Make sure gene IDs are compatible with software

## Pathway analysis workflow
* Collect genomics data (e.g., mRNA expression)
* Normalize and score (e.g., compute differential expression)
* Generate gene list
* Learn about underlying cellular mechanism using pathway and network analysis
  * Visualize and identify interesting pathways and netowkrs
  * Drill down to understand molecular mechanism
  * Publish model explaning data

## Summarizing pathway analysis with Enrichment Map
Nodes: gene sets reflecting pathways, processes

Edges: sets share many common genes.

Network clustering groups processes/pathways as themes.

## Gene lists
### Where do gene lists come from?
* Molecular profiling (e.g., mRNA, protein)
  * Identification - Gene list
  * Quantification - Gene list + values
  * Ranking, Clustering (biostatistics)
* Interactions: Protein interactions, microRNA targets, transcription factor binding sites (ChIP)
* Genetic screen (e.g., knock out library)
* Association studies (genome-wide)
  * Single nucleotide polymorphisms (SNPs)
  * Copy number variants (CNVs)

### What Do Gene Lists Mean?
* Biological system: complex, pathway, physical interactors
* Similar gene function (e.g. protein kinase)
* Similar cell or tissue location
* Chromosomal location (linkage, CNVs)

## Biological Questions & Answers

### Biological Questions
What do you want to accomplish with your list
* Summarize biological processes or other aspects of gene function in your dataset
* Perform differential analysis - what pathways are different between samples?
* Find a controller for a process (TF, miRNA)
* Find new pathways or new pathway members
* Discover new gene function
* Correlate with a disease or phenotype (candidate gene prioritization)

### Biological Answers
Computational analysis methods we will cover
* Pathway enrichment analysis: summarize and compare
* Network analysis: predict gene function, find new pathway members, identify functional modules (new pathways)
* Regulatory network analysis: find controllers

## Gene and Protein Identifiers
Identifiers (IDs) are ideally unique, stable names or numbers that help track database records (e.g., Social Insurance Number, Entrez Gene ID).

Gene and protein information stored in many databases.
Therefore, genes have many IDs.

Records for: Gene, DNA, RNA Protein.
Important to recognize the correct record type.

### Common Identifiers
* Gene: Ensembl, Entrez Gene, Unigene
* RNA transcript: GenBank, RefSeq, Ensembl
* Protein: Ensembl, RefSeq, UniProt, IPI, EMBL, PDB
* Species-specific: HUGO HGNC, MGI, RGD, ZFIN, FlyBase, WormBase, SGD
* Annotations: InterPro, OMIM, Pfam, Gene Ontology, SNPs
* Experimental Platform: Affymetrix, Agilent, CodeLink, Illumina

<!--
ensembl 버전은 크게 문제가 되지 않는다.
사람은 ENSG로 시작하고, 나머지 종에서는 종 이름이 중간에 들어간다
entrez gene: 숫자로 되어있음. otholog 분석 (종간 분석) 을 많이 한다
unigene: 잘 안쓰고 앙상블을 더 많이씀

refseq: NM으로 시작함. XM, BC 이렇게 단계가 다르게 있다
최근에는 앙상블도 많이 씀. ENST로 시작.
refseq는 보수적으로 annotation, 앙상블은 과감하게 해서 조금 다름. refseq는 자꾸 바뀌어서 앙상블이 낫다

protein은 앙상블이 ENSP로 시작. Refseq은 NP로 시작
Uniprot도 많이 쓰임. 

InterPro는 INteractome
OMIM은 질병
-->

### Identifier Mapping
* So many IDs
  * Software tools often recognize only a handful
  * Map from your gene list IDs to standard IDs
* Four main uses
  * Searching for a favorite gene name
  * Link to related resources
  * Identifier translation (proteins to genes, Affy ID to Entrez Gene)
  * Merging data from different sources (find equivalent records)
   
### ID Challenges
* Avoid errors: map IDs correctly
  * Beware of 1-to-many mappings
* Gene name ambiguity - not a good ID
  * Better to use the standard gene symbol
* Excel error-introduction
* Problems reaching 100% coverage
  * E.g., due to version issues
  * Use multiple sources to increase coverage

### ID Mapping Services
g:Convert, Ensembl Biomart

### Recommendations
* For proteins and genes
  * doesn't consider splice forms
* Map everything to Entrez Gene IDs or Official Gene Symbols using a spreadsheet
* If 100% coverage desired, manually curate missing mappings
  * Use multiple resources - geneCards, Ensembl, species DBs
* Be careful of Excel auto conversions - especially when pasting large gene lists
  * Remeber to format cells as 'text' before pasting

<!-- david에서 에러가 잘 나는 경우가 있어서 주의해야 한다 -->

## Pathways and other gene function attributes
* Available in databases
* Pathways
  * Gene ontology biological process, pathway databases
* Other annotations
  * Gene Ontology molecular function, cell location
  * Chromosome position
  * Disease association
  * DNA properties
    * TF binding sites, gene structure (intro/exon), SNPs
  * Transcript properties
    * Splicing, 3' UTR, microRNA binding sites
  * Protein properties
    * Domains, secondary and tertiary structure, PTM sites
  * Interactions with other genes

## Gene Ontology (GO)
Ontology: A formal system for describind knowledge

### GO Structure
* Terms are related within a hierarchy
  * is-a   <!-- 일종이다 -->
  * part-of   <!-- 구성품 -->
* Describes multiple levels of detail of gene function
* Terms can have more than one parent or child

### GO is really three different ontologies
* Cellular Component (CC)
  * Where is the gene product localized?
* Biological Process (BP)
  * What function(s) does it perform in that location?
* Molecular Function (MF)
  * How does it carry out that function (via which molecular mechanisms)?

### Terms
Where do GO terms come from?
* GO terms are added by editors at EBI and gene annotation database groups
* Terms added by request
* Experts help with major development

### Annotations
Genes are linked, or associated, with GO terms by trained curators at genome databases
* Known as gene associations or GO annotations
* Multiple annotations per gene

Some GO annotations created automatically (without human review)

#### Hierarchical annotation
Genes annotated to specific term in GO automatically added to all parents of that term.

<!--
여러가지 전략이 있겠지만 p-value가 가장 좋은걸 선택하고 나머지 위를 다 날려버리는 전략을 쓴다.
어쨌거나 동일한 유전자들이 영향을 미치고 희석이 되기 때문에
-->

#### Annotation Sources
Manual annotation
* Curated by scientists
  * High quality
  * Small number (time-consuming to create)
* Reviewed computational analysis

Electronic annotation
* Annotation derived without human validation
  * Computational predictions (accuracy varies)
  * Lower quality than manual codes

Key point: be aware of annotation origin

#### Evidence type
* Experimental Evidence Codes
  * EXP: Inferred from Experiment
  * IDA: Inferred from Direct Assay
  * IPI: Inferred from Physical Interaction
  * IMP: Inferred from Mutant Phenotype
  * IGI: Inferred from Genetic Interaction
  * IEP: Inferred from Expression Pattern
* Computational Analysis Evidence Codes
  * ISS: Inferred from Sequence or Structural Similarity
  * ISO: Inferred from Sequence Orthology
  * ISA: Inferred from Sequence Alignment
  * ISM: Inferred from Sequence Model
  * IGC: Inferred from Genomic Context
  * RCA: Inferred from Reviewed Computational Analysis
* Author Statement Evidence Codes
  * TAS: Traceable Author Statement
  * NAS: Non-traceable Author Statement
* Curator Statement Evidence Codes
  * IC: Inferred by Curator
  * ND: No biological Data available
* IEA: Inferred from electronic annotation

<!-- Human, mouse에선 IEA를 다 빼고 보는게 일반적이다

내가 생각하는 genome size에 비해 annotation이 너무 적으면 IEA를 적절히 추가해서 보는게 옳다.

DAVID를 압도적으로 많이 쓴다. 쉽기 때문. 그런데 정확도를 희생했기 때문에 주의가 필요하다.
-->

## Pathway Databases
Pathway Commons is a network biology resource and acts as a convenient point of access to biological pathway information collected from public pathway databases, which you can search, visualize and download.

<!--
Pathway commons를 시작점으로 쓴다.
-->

## What have we learned?
Pathways and other gene attributes in databases.
* Pathways from Gene Ontology (GO) and pathway databases
* Gene Ontology (GO)
  * GO is a classification system and dictionary for biological concepts
  * Annotations are contributed by many groups
  * More than one annotation term allowed per gene
  * Some genomes are annotated more than others
  * Annotation comes from manual and electronic sources
  * GO can be simplified for certain uses (GO Slim)
* Many gene attributes available from genome databases such as Ensembl

# Gene Set Enrichment Analysis

## Types of enrichment analysis

### Gene list (expression change with p < 0.05)
* Answers the question: Are any gene sets surprisingly enriched (or depleted) in my gene list?
* Statistical test: Fisher's Exact Test (aka Hypergeometric test)

### Ranked list (differential expression)
* Answers the question: Are any gene sets ranked surprisingly high in my ranked list of genes?
* Statistical test: minimum hypergeometric test (+ others we won't discuss)

<!--
Expression change로 유전자 고르기: expression level이 높을수록 조금만 변해도 p-value가 과해진다. 
그래서 expression level에서의 bias가 생김… 조심해서 해야 한다.
Fold change로 고르기
-->

## Gene list

### Two-class design for gene lists
* Expression Matrix
  * Cases vs. Controls
* Genes Ranked by Differential Statistics
  * Fold change
  * Log (ratio)
  * t-test
  * Significance analysis of gene expression
* Selection by threshold

<!-- DAVID 등 사용할때도 background를 꼭 지정해줘야 한다. -->

### Recipe for gene list enrichment test
* Define your gene list and your background list
* Select your gene sets (pathways) to test for enrichment
* Run enrichment tests and correct for multiple testing, if necessary
* Interpret your enrichments

<!--
보통은 enrichment 결과를 바탕으로 validation 실험을 한다. 3~4점 논문은 여기도 받아주는데 그 이상은 더 요구를 한다.
-->

## Ranked list
### Possible problems with gene list test
* No natural value for the threshold
* Different results at different threshold settings
* Possible loss of statistical power due to thresholding
  * No resolution between significant signals with different strengths
  * Weak signals neglected

### Recipe for ranked list enrichment test
* Rank your gene list and your background list
  * Select up/down regulated genes separately
  * Use a lenient threshold
* Select your gene sets (pathways) to test for enrichment
* Run enrichment tests and correct for multiple testing, if necessary
* Interpret your enrichments

## Outline of theory component
* Gene lists
  * Hypergeometric test for calculating enrichment P-values for gene lists (Fisher's Exact Test).
  * Others: Binomial and Chi-squared
* Ranked list (semi-quantitative)
  * Minimum hypergeometric test for computing enrichment P-values for ranked lists.
  * Others: GSEA, Wilcoxon ranksum, Mann-Whitney U, Kolmogorov-Smirnov

Multiple test corrections: Bonferroni, Benjamini-Hochberg FDR.

## Hypergeometric test (a.k.a., Fisher's exact test)
Hypothesis
* Null hypothesis: List is a random sample from population
* Alternative hypothesis: More black genes than expected

2x2 contingency table for Fisher's Exact Test

### Important details
To test for under-enrichment of "black", test for over-enrichment of "red".

Need to choose background population appropriately
* If only certain genes are tested in the experiment
* If only certain genes are part of the annotation (part of any pathway)

To test for enrichment of more than one independent types of annotation (red vs black and circle vs square), apply Fisher’s exact test separately for each type.

## Minimum hypergeometric test (mHG)

### Steps
* Calculate P-value at multiple thresholds
* Correct for multiple testing

### Rationale
Each gene-set (pathway) tested separately for ranked gene list
* Few highly ranked genes in the list associate to smaller, specific pathways
* General pathways with many genes apparent in analysis of larger subsets of the ranked list

mHG determines the optimal threshold for every pathway in the input gene list.
Stronger as well as weaker gene signals considered.

<!--
Minimum hypergeometric test는 모든 가능한 thrshold에 대해서 다 hypergeometric test를 쓴다 (맞는지 확인!) optimal threshold를 잡을 수 있다!
많이 계산하니까 p-value를 multiple correction은 해야한다.
강한 것도 잘 잡아내고 약한 시그널도 잘 잡아낸다.. (왜?)
-->

## GSEA

### How is significance determined for GSEA?
Permutation is frequently used to determine if an enrichment score is statistically significant
* Permuting samples is preferred, but large n required (more than 7 per group)
* Permuting genes is a common alternative, but is subject to inter-gene correlations which can inflate type 1 error

<!-- 
GSEA에서 phenotype = condition이라고 생각하면 된다.
ES를 어떻게 계산하는건지 이해 못했음 ㅜ gpt에게 물어보자. 겹치면 + 안겹치는건 -로 해서 계산한다던데. 그이후에 normalize한다고 했음
-->

<!--
10번 permutation하면 최소 p-value는 0.1, 10만번하면 10만분의 1. 그래서 많이 셔플링해야하는데 샘플 개수가 적으면 그냥 gene을 permutation한다.
-->

### MSigDB
The Molecular Signatures Database (MSigDB) is a collection of annoted gene sets for use with GSEA software.

# Multiple testing corrections

## Bonferroni
If $M$ is number of annotation tested,
Corrected p-value = $M \times$ original p-value.

Corrected P-value is greater than or equal to the probability that at least one (or more) of the observed enrichments is due to random draws.

The jargon for this correction is controlling for the Family-Wise Error Rate (FWER).

### Bonferroni correction caveats
Bonferroni correction is very stringent and can wash away real enrichments leading to false negatives.

Often one is willing to accept a less stringent condition, the false discovery rate (FDR), which leads to a gentler correction when there are real enrichments.

## False discovery rate (FDR)
FDR is the expected proportion of the observed enrichments due to random chance (e.g. 5%).

Compare to Bonferroni correction which is a bound on the probability that any one of the observed enrichments could be due to random chance.

Typically FDR corrections are calculated using the Benjamini-Hochberg procedure.

FDR threshold is often called the q-value.

### Benjamini-Hochberg
* Sort P-values of all tests in increasing order
* Adjusted P-value is nominal P-value times number of tests divided by the rank of the P-value in sorted list
  * Adjusted P-value = P-value x [# of tests] / Rank
* Q-value (or FDR) corresponding to a nominal P-value is the smallest adjusted P-value assigned to P-values with the same or higher ranks.

## Reducing multiple test correction stringency
The correction to the P-value threshold α depends on the # of tests that you do, so, no matter what, the more tests you do, the more sensitive the test needs to be.

Can control the stringency by reducing the number of tests: e.g. restrict testing to the appropriate GO annotations; or filter gene sets by size.

## Summary
Enrichment analysis
* Statistical tests
  * Gene list: Fisher's Exact Test
  * Ranked list: mHG, GSEA, also see Wilcoxon ranksum, Mann-Whitney U-test, Kolmogorov-Smirnov test
* Multiple test correction
  * Bonferroni: stringent, controls probability of at least one false positive
  * FDR: more forgiving, controls expected proportion of false positives - typically uses Benjamini-Hochberg
