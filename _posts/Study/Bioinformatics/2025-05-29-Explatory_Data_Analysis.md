---
title: Exploratory Data Analysis & Data Visualization
author: JSH
date: 2025-05-29 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
use_math: true
---

# Exploratory Data Analysis & Data Visualization

## Exploratory Data Analysis

### Research Paradigms
* Hypothesis-Driven Research
  * Background Research
  * Develop hypothesis
  * Select System and Design Experiment
  * Apply Assay(s)
  * Interpret Data, Refine, And Extend Hypothesis
* Hypothesis-Generating Research
  * Background Research
  * Select System
  * Generate High Throughput Data + Gather Related Public Dataset
  * Explore Data for Patterns
  * Refine, Extend, And Validate Hypothesis

### Exploratory Data Analysis (EDA)
Data analysis approach prioritizing investigation and understanding over immediate confirmation.

* Process: Analyzing datasets to summarize characteristics, often using visualization methods.
* Core Idea: Examine data thoroughly before making assumptions or proceeding with formal modeling.
* Focus
  * Examining data for inherent patterns
  * Identifying outliers/anomalies
  * Understanding variable distributions
  * Uncovering underlying structure
* Contrast: Less concerned with rigid statistical modeling or formal inference initially

### The Philosophy of EDA
John Ukey's Emphasis: EDA is more than just techniques

* Attitude: Be open-minded, let the data guide
* Flexibility: Adapt the analysis based on what the data reveals
* Reliance on Display: Use graphical methods extensively to see patterns

### EDA vs. Confirmatory Data Analysis
#### Confirmatory Data Analysis
Goal: Test pre-defined hypotheses.

Questions: Answer specific, preformulated questions.

Role: Formal statistical testing and inference.

#### Exploratory Data Analysis
Goal: Discovery, pattern finding, understanding the data.

Questions: Formulate the right questions to ask.

Role: Crucial precursor; helps determine if planned statistical methods are appropriate.

### Core Goals
#### Maximize Insight
Develop a comprehensive understanding of the dataset.

Familiarize with structure, variable distributions, key characteristics, and context.

#### Pattern Discovery
Identify underlying trends and correlations.

Find clusters of similar observations.

Uncover other hidden structures.

#### Anomaly Detection
Spot outliers, errors, inconsistencies.

Identify unusual events needing investigation or cleaning.
(Could be errors or interesting biological phenomena)

#### Hypothesis Generation
Use visualizations and summarizes to formulate data-driven, testable hypotheses.

Ensure research questions are relevant and informed by the data.

#### Data Quality Assessment
Check assumptions for later statistical tests (Identify assumptions in the experimental design!).

Identify issues: missing values, systematic biases (e.g., batch effects, GC bias)

Assess overall data fidelity and reliability (Avoid “Garbage In, Garbage Out”).

#### Inform Feature Selection & Engineering
Gain insights to guide selection of important variables (features).

Suggest potential data transformations to improve models.

### Specific Roles in Bioinformatics
#### Hypothesis Generation from -Omics Data
Sift through vast, noisy data to generate plausible, data-driven biological hypotheses.

Example: Visualizing gene expression → clusters of co-expressed genes → hypothesis about shared regulation.

#### Quality Control (QC)
Assess quality of experimental data (e.g., sequencing runs).

Identify technical artifacts (e.g., batch effects).

Check quality scores, mapping rates, ensure reliability before downstream analysis.

#### Guiding Downstream Analysis
EDA findings (distributions, variance, outliers, batch effects) directly inform choices about: 
* Data normalization
* Data clearance
* Specific parameters for processing
* Statistical test selection (parameteric vs. non-parametric)
* Need for batch correction
* Feature engineering / model techniques

### Iterative Nature of EDA
Why is iterative especially vital in bioinformatics?
* Complex biological data.
* Potential for unexpected technical variations
* Intricate biological structures hidden in high dimensions
* Beyond Linearity: A strictly linear analysis is often insufficient
* Feedback Loop Example
  * Discover potential batch effect (e.g., via PCA)
  * Revisit data → Apply corection methods → Re-explore corrected data

### Importance of Context: Linking Data to Biology
Apply Techniques Meaningfully: Use visualization and summarization not just on numbers, but on entities with biological meaning (genes, proteins, pathways, variants).

Interpret Patterns Biologically
* Uncover potential biological mechanisms reflected in data patterns.
* Identify technical artifacts that might obscrue biology.

Metadata is Key: Linking experimental data with corresponding sample/feature metadata is essential for interpreting patterns

Goal: Translate observed data patterns into potential biological knowledge and testable hypotheses.

## Revealing Insights from Data

### Numerical Summarization
Using statistical measures to describe the main features of a dataset with numbers. 

Purposes in EDA:
* Condense large amounts of data into a few meaningful values.
* Objectively describe data distributions and variability
* Provide a basis for comparison between different groups or conditions.
* Identify potential issues (e.g., extreme values)

Helps Understand
* Central Tendency: Typical or central value
* Dispersion: Spread or variability of data points
* Distrubution Shape: Symmetry, skewness, tails
* Relationships: How variables related (correlation)

### Dimensionality Reduction
* Reduces the number of features while preserving the essential information in the data
* Helps in visualizing high-dimensional data, removing redundant or correlated features, and improving computational efficiency
* Examples: PCA, NMF, t-SNE, UMAP

### Clustering
Groups similar samples or features in a bioinformatics dataset based on their intrinsic properties or patterns.

Helps in discovering subgroups or subtypes within the data, such as different cell populations, disease subtypes, or functional modules.

Examples: k-means, hierarchical clustering, DBSCAN, Louvain method.

### Correlation Analysis
Measures the strength and direction of the relationship between variables in a bioinformatics dataset.

Helps in identifying patterns, dependencies, and potential interactions among biological entities such as genes, proteins, or metabolites.

Examples: Pearson correlation, Spearman rank correlation, Kendall’s tau

## Data Visualization






