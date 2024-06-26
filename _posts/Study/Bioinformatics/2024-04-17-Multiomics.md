---
title: Multiomics
author: JSH
date: 2024-04-17 20:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
---

## Multiomics
Multiomics is a biological analysis approach in which the data sets are multiple "omes", such as the genome, proteome, transcriptome, epigenome, metabolome, and microbiome; in other words, the use of multiple omics technologies to study life in a concerted way. By combining these "omes", scientists can analyze complex biological big data to find novel associations between biological entities, pinpoint relevant biomarkers and build elaborate markers of disease and physiology. In doing so, multiomics integrates diverse omics data to find a coherently matching geno-pheno-envirotype relationship or association.


![image](https://github.com/JeonSHyun/JeonSHyun.github.io/assets/86886562/04f3a639-e45c-4bc3-9ddc-9c4ed5b37502)


## Omics data types
### Genome
In the realm of medical research, genomics focuses on identifying genetic variants associated with disease, response to treatment, or future patient prognosis. GWAS is a successful approach that has been used to identify thousands of genetic variants associated with complex diseases in multiple human populations. In such studies, thousands of individuals are genotyped for more than a million genetic markers, and statistically significant differences in minor allele frequencies between cases and controls are considered evidence of association. GWAS studies provide an invaluable contribution to our understanding of complex phenotypes. Associated technologies include genotype arrays, NGS for whole-genome sequencing, and exome sequencing.

### Proteome
Proteomics is used to quantify peptide abundance, modification, and interaction. The analysis and quantification of proteins has been revolutionized by MS-based methods and, recently, these have been adapted for high-throughput analyses of thousands of proteins in cells or body fluids. Interactions between proteins can be detected by classic unbiased methods such as phage display and yeast two-hybrid assays. Affinity purification methods, in which one molecule is isolated using an antibody or a genetic tag, can also be used. MS is then used to identify any associated proteins. Such affinity methods, sometimes coupled with chemical crosslinking, have been adapted to examine global interactions between proteins and nucleic acids (e.g., ChIP-Seq). Finally, the functions of a large fraction of proteins are mediated by post-translational modifications such as proteolysis, glycosylation, phosphorylation, nitrosylation, and ubiquitination. Such modifications play key roles in intracellular signaling, control of enzyme activity, protein turnover and transport, and maintaining overall cell structure. MS can be used to directly measure such covalent modifications by defining the corresponding shift in the mass of the protein (in comparison to the unmodified peptide). There are efforts to develop genome-level analyses of such modifications. Associated technologies include MS-based approaches to investigate global proteome interactions and quantification of post-translational modifications.

### Transcriptome
Transcriptomics examines RNA levels genome-wide, both qualitatively (which transcripts are present, identification of novel splice sites, RNA editing sites) and quantitatively (how much of each transcript is expressed). The central dogma of biology viewed RNA as a molecular intermediate between DNA and proteins, which are considered the primary functional read-out of DNA. Other examples of RNA function, such as structural (e.g., ribosomal complexes), or regulatory (e.g., Xist in ChrX inactivation) have often been regarded as odd exceptions to the general rule.

The advent of large transcriptomic studies in the past decade has shown that while only ~3% of the genome encodes proteins, up to 80% of the genome is transcribed. RNA-Seq studies identified thousands of novel isoforms and showed a larger than previously appreciated complexity of the protein-coding transcriptome. However, an even more significant contribution of these studies was the development of the non-coding RNA field. It is now clear that thousands of long non-coding RNAs transcribed play essential roles in many physiological processes and various diseases. In addition to long non-coding RNA, NGS allows interrogation of short RNAs (microRNAs, piwi-interacting RNAs, and small nuclear RNAs) and identification of circular RNAs. Much like long non-coding RNAs, a growing body of evidence points to dysregulation of short and circular RNAs in disease and the potential use thereof as biomarkers or as therapeutic targets. Associated technologies include probe-based arrays and RNA-Seq.

### Epigenome
Epigenomics focuses on genome-wide characterization of reversible modifications of DNA or DNA-associated proteins, such as DNA methylation or histone acetylation. Covalent modifications of DNA and histones are major regulators of gene transcription and subsequently of cellular fate. Those modifications can be influenced both by genetic and environmental factors, can be long lasting, and are sometimes heritable. While the role of epigenetic modifications as mediators of transgenerational environmental effects remains controversial, their importance in biological processes and disease development is evident from many epigenome-wide association studies that have been reported. Epigenetic signatures are often tissue-specific, and several large consortia are focusing on establishing comprehensive epigenomic maps in multiple human tissues. Thus, in addition to insight gained from identifying epigenetic modifications correlating with diseases, data generated by these studies has great potential to enhance our functional interpretation of genetic variants residing in those regions or of epigenetic markers associated with disease independently of genetic variation. Associated technology includes assessment of DNA modifications using NGS.

### Metabolome
Metabolomics simultaneously quantifies multiple small molecule types, such as amino acids, fatty acids, carbohydrates, or other products of cellular metabolic functions. Metabolite levels and relative ratios reflect metabolic function, and out of normal range perturbations are often indicative of disease. Quantitative measures of metabolite levels have made possible the discovery of novel genetic loci regulating small molecules, or their relative ratios, in plasma and other tissues. Associated technologies include MS-based approaches to quantify both relative and targeted small molecule abundances.

### Microbiome
Microbiomics is a field in which all the microorganisms of a given community are investigated together. Human skin, mucosal surfaces, and the gut are colonized by microorganisms, including bacteria, viruses, and fungi, collectively known as the microbiota (and their genes constituting the microbiome). There are substantial variations in microbiota composition between individuals resulting from seed during birth and development, diet and other environmental factors, drugs, and age. Many studies have implicated perturbations in gut bacteria in a variety of disorders, including diabetes, obesity, cancer, colitis, heart disease, and autism. The microbiome can be profiled by amplifying and then sequencing certain hypervariable regions of the bacterial 16S rRNA genes followed by clustering the sequences into operational taxonomic units. Shotgun metagenomics sequencing, in which total DNA is sequenced, can provide additional resolution for distinguishing genetically close microbial species. Associated technologies include NGS application for 16S ribosomal abundance and metagenomics quantification.

## Reference

[1] https://en.wikipedia.org/wiki/Multiomics

[2] Hasin, Y., Seldin, M. & Lusis, A. Multi-omics approaches to disease. Genome Biol 18, 83 (2017). https://doi.org/10.1186/s13059-017-1215-1
