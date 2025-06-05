---
title: Gene Expression Analysis (1)
author: JSH
date: 2025-06-05 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
use_math: true
---

# Gene Expression Analysis (1)

*  Identifying differentially expressed genes between different experimental conditions or samples, such as comparing cancerous and non-cancerous tissue.
*  Characterizing gene expression patterns in various cell types or tissues, such as identifying genes that are specifically expressed in brain cells.
*  Discovering novel transcripts and alternative splicing events, which can lead to the identification of new protein-coding genes and non-coding RNAs.
*  Quantifying gene expression levels for functional genomics studies, such as identifying genes involved in specific biological pathways or determining the effects of genetic mutations.
*  Assessing the quality and integrity of RNA samples, such as detecting contamination or degradation of samples.
*  Study of gene expression in non-model organisms, such as studying the gene expression of a plant species which is not well studied.
*  Study of the expression of viral genes in host organisms, such as studying the expression of viral genes in a host organism infected with a virus.

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

## Bulk vs. single-cell
| Category                    | Bulk RNA-seq                                                                 | Single-cell RNA-seq                                                                 |
|-----------------------------|------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Cost & Effort               | Relatively simple and inexpensive                                            | More expensive and burdensome                                                       |
| Sample Quality & Quantity   | Can work even with low-quality or small-quantity samples                     | Requires relatively strict standards for quality and quantity                        |
| Representation in Profile   | Can capture average expression with less external influence                  | Requires minimal delay even without sorting, up to cell lysis                       |
| Scalability                 | Easy to handle even with large sample numbers                                | Limited scalability for increasing sample numbers                                   |
| Customization               | Easy to adjust based on target of interest                                   | Protocol changes are limited                                                        |

## Bulk RNA-seq vs. Spatial transcriptome
| Category                    | Bulk RNA-seq                                                                 | Spatial Transcriptomics                                                                |
|-----------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Cost & Effort               | Relatively simple and inexpensive                                            | More expensive and burdensome                                                         |
| Sample Quality & Quantity   | Can work even with low-quality or small-quantity samples                     | Requires relatively strict standards for quality and quantity                          |
| Coverage                    | Can observe nearly all expressed RNAs                                        | Limited observation depending on quantity, length, location, and sequence              |
| Scalability                 | Easy to handle even with large sample numbers                                | Limited scalability for increasing sample numbers                                      |
| Customization               | Easy to modify protocols (like changing recipes)                             | Many restrictive conditions for protocol modification                                  |







