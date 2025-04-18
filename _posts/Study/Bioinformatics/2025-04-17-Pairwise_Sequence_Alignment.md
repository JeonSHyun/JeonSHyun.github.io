---
title: Pairwise Sequence Alignment
author: JSH
date: 2025-04-17 10:55:00 +0800
categories: [Study, Bioinformatics]
tags: [Study, Bioinformatics]
use_math: true
---

# Pairwise Sequence Alignment

## Strings and Exact Matching

### Reads and strings
String: Sequencing reads. sequences of characters. 

The strings are the only hints we get about where the reads came from from with respect to the longer DNA molecules.

### String definition
String $S$ is a finite sequence of characters.

Characters are drawn from alphabet $\Sigma$.
Usually, $\Sigma = \\{A, C, G, T \\}$

$\mid S \mid$ = number of characters in $S$.

$\epsilon$ is empty string ($\mid \epsilon \mid = 0$)

Positions within a string $S$ are referred to with offsets.

Concatenation of $S$ and $T , ST$ = characters of $S$ followed by characters of $T$.

Substring of S is a string occurring inside $S$.
$S$ is a substring of $T$ if there exist (possibly empty) strings $u$ and $v$ such that $T = uSv$.

Prefix of $S$ is a substring starting at the beginning of $S$.
$S$ is a prefix of T if there exists a string $u$ such that $T = Su$.

Suffix is substring ending at end of $S$.
$S$ is a suffix of T if there exists a string $u$ such that $T = uS$.

Usually assume alphabet $\Sigma$ is finite, with $O(1)$ elements
* Nucleic acid alphabet: $\\{A, C, G, T \\}$
* Amino acid alphabet: $\\{A, R, N, D, C, E, Q, G, H, I, L, K, M, F, P, S, T, W, Y, V \\}$

### Exact matching
At what offsets does pattern $P$ occur within text $T$?

#### Naive algorithm
If $n = \mid P \mid, m = \mid T \mid$

*  How many alignments are possible?: $m - n + 1$
*  Greatest # character comparisons possible?: $n(m - n + 1)$
*  Least # character comparisons possible?: $m - n + 1$

#### Boyer-Moore algorithm
A few clever tricks are implemented in the Boyer-Moore algorithm.

## Approximate matching and edit distance
Some widely used approximate matching algorithms for DNA (& other strings) came from the biological community, aiming to bring alignments into closer harmony with biological processes that mutate strings.

### Hamming distance
For $X, Y$ where $\mid X \mid = \mid Y \mid$, hamming distance = minimum # substitutions needed to turn one into the other.

Walking along both strings.
For each position, compare the characters in both strings at that position.
If not equal, increment hamming distance.

### Edit distance
For $X, Y$, edit distance = minimum # edits (substitutions, insertions, deletions) needed to turn one into the other.

editDistance($X, Y$) $\leq$ hammingDistance($X, Y$)

If $x$ and $y$ are different lengths, editDistance($X, Y$) $\geq \mid \mid X \mid - \mid Y \mid \mid$

Knowing distances between substrings of $X, Y$ (or prefixes, suffixes) tells you something about overall distance.

#### Algorithm
$D[i, j]$: edit distance between length-i prefix of $x$ and length-j prefix of $y$

Optimal edit transcript for $D[i, j]$ is built by extending a shorter one by 1 operation.  3 options: 
* Append D to transcript for $D[i-1, j]$
* Append I to transcript for $D[i, j-1]$
* Append M or R to transcript for $D[i-1, j-1]$

$D[i, j]$ and its transcript come from 1 of these 3 choices, whichever has fewest edits.
$D[\mid x \mid, \mid y \mid]$ is the overall edit distance.

#### Memoization
Memoization: Reusing solutions to subproblems.

Subproblems $(D[i, j]s$) are reused many times; no need to recalculate them.

#### Dynamic programming
* Top-down dynamic programming
* Bottom-up dynamic programming

Traceback corresponds to an optimal alignment / edit transcript.
At each step, ask which neighbor gave the minimum?

To find the edit distance and the alignment we did: 
* table filling
  * Filling $(m+1)(n+1)$ cells, each requiring constant work, so $O(mn)$
* traceback
  * Worst case: tracback never moves diagonally, so $O(m+n)$

Matrix-filling dynamic programming algorithm is $O(mn)$ time and space.
FillIng matrix is $O(mn)$ space and time, yields edit distance.
Traceback is $O(m + n)$ time, yields optimal alignment / edit transcript.

### Approximate matching with edit distance
Can we search for the occurrence of $$P in $T$ with least edits?
* Initialize first row with 0’s rather than increasing integers, then fill matrix
* Pick lowest edit distance in the bottom row, traceback to top row
* $D[i, j]$ equals the optimal edit distance between the length-i prefix of $P$ and a substring of $T$ ending at position $j$

## Global Alignment
It doesn’t make sense for every edit to cost 1.

### Generalizing edit distance
Transitions are A-G and C-T changes.
Transversion are A-C, A-T, C-G, C-T.
For random mutations, transitions should be half as frequent as transversions, but if you compare two humans, transition to transversion ratio (ti/tv) is ~2.1.

Keep basic edit distance idea and algorithm, but give different weights to different events according to likelihood.

### Global alignment
Traceback works just as it did for edit distance.

Matrix-filling dynamic programming algorithm is $O(mn)$ time and space
* FillIng matrix is $O(mn)$ space and time, yields global alignment value
* Traceback is $O(m + n)$ time, yields optimal alignment

### Affine gap penalty
Affine gap penalty: 

## Local Alignment
Given strings $x$ and $y$, what is the optimal global alignment value of a substring of $x$ to a substring of $y$.
This is local alignment.

Assume scoring function where: (a) similarities get scores > 0, (b) dissimilarities get scores < 0, (c) global alignment value for $x = \epsilon, y = \epsilon$ is 0

What roughly is # substring pairs, where $\mid x \mid = n, \mid y \mid = m$? $O(mn)$

#### Algorithm
As for edit distance, there are only so many possibilities:
* Empty: let both substrings be empty, global alignment value = 0
* Vertical: append D to transcript for $V[i-1, j]$, add penalty
* Horizontal: append I to transcript for $V[i, j-1]$, add penalty
* Diagonal: append M or R to transcript for $V[i-1, j-1]$, add match bonus or replacement penalty as appropriate

What’s different from global alignment?
* First row, column initialized to 0s
* 0 is one of the arguments of the max (because of $\epsilon, \epsilon$)
* Scoring function with differences < 0, matches > 0

Dynamic-programming implementation of this is called Smith-Waterman

#### Smith-Waterman
Backtrace: 
* start from maximal cell
* stop upon reaching cell with score = 0

## Searching Databases
### Database search may need a massive number of alignments
Looking for local alignments between a query sequence and any sequence in the database
* Identifying a newly determined DNA or protein sequence
* Searching for homologs
* Retrieving full sequences using a partial fragment

### K-mer indexing narrows down the search
Searching for perfect matches of a fixed-length sequence can be implemented very efficiently (allows very small number of mismatches in many aligners.) 
Once the candidates are picked by matching k-mer profiles, an alignment algorithm can refine the results.
Achieves similar sensitivity with dramatically reduced computation.

### Different versions of BLAST for idfferent problems
* blastp
  * Query: peptide
  * Database: peptide
* blastn
  * Query: nucleotide
  * Database: nucleotide
* tblastn
  * Query: peptide
  * Database: nucleotide
* blastx
  * Query: nucleotide
  * Database: peptide
* tblastx
  * Query: nucleotide
  * Database: nucleotide
  * Notes: matches by translated sequences
* megablast
  * Query: nucleotide
  * Database: nucleotide
  * Notes: high similar seqs.

### Profile-based database search
Distant homologs can’t be easily found using a single sequence. 
Conservation profile among the known homologs enable higher sensitivity while keeping the false negative rate low. 

Biologically interesting features are revealed during the profile refinement
* Domain identification
* Evolutionary analysis
* Fold recognition

Major implements:
* PSI-BLAST: Position Specific Iterative BLAST, position-specific model
* JackHMMER: Jack hidden Markov Modeler, HMM-based model

### Scale of the sequence search
Smith-Waterman, SSEARCH < BLAST, FASTA, BLAT < BWA, bowtie, STAR < Kallisto, sailfish < Archive search engines

## Index-assisted Approximate Alignment

### Dynamic programming summary
A powerful set of tools:
*  DP deals naturally with both mismatches and gaps
*  DP scoring can take into account variation, sequencing error, etc

### Pigeonhole principle

### Index-assisted approximate matching
Use index for exact-matching subproblems, follow up with DP.

Index is identifying diagonal stretches of matches.

### Neighborhood search
Use index to find exact occurrences of strings in P’s neighborhood

Neighborhood = set of strings within some Hamming / edit distance

## Searching with Nucleic Acid or Protein Sequences with BLAST

### BLAST outline
* Seeding: Find common subwords between query and database sequences (seeds)
* Extension: Starting from seeds, extend alignment in both directions - high-scoring segment pairs (HSP)
* Evaluation: Assess the statistical significance of each HSP

#### Seeding
Build a list $L_1$ of all subwords (factors) of the length W in the query sequence.

Similarity is defined via a substitution matrix- For each subword $w_i \in L_1$ build a neighborhood $N_i$ which includes “similar” subwords.

Similarity is defined via a substitution matrix.
* For proteins, BLOSUM matrices can be used
* For DNA, +2 for a match and -3 for mismatch (or +5/-4)

Only subwords with similarity score above a threshold T are added into the neighborhood.

Scan the database for exact matches of subwords in $L_1$ and neighborhoods.

#### Extension
Try to extend the alignment to the left and to the right from the seed.

Stop if the current total score drops by more than X compared to the maximum seen so far.

Trim alignment back to the maximum score.

#### Evaluation
Are sequences biologically related or are they similar just by chance?

Smith-Waterman alignment scores between two random sequences follow the Gumbel extreme value distribution.

Probability $p$ of observing a score $S$ equal to or greater than $x$ is given by the equation: $p(S \geq x) = 1 - \exp (-e^{\lambda (x - \mu)})$
* Parameters $\lambda$ and $\mu$ depend on the substitution matrix, gap penalties, and sequence length.

### Scores from the database search
#### E-value
Expected count of two random sequences aligning with a score greater than or equal to $S$.
(cutoff range often used: 0.1-10)

Expectation: $E = Km' n' e^{-\lambda S}$
* E: Expected number of alignments by chance
* K: A minor constant
* m': Length of query
* n': Length of database
* $\lambda$: Scaling factor
* S: Raw score

#### Bit-score
$S' = \frac{\lambda S - \ln k}{\ln 2}$
* S': normalized score
* $\lambda$: Scaling factor
* S: Raw score
* k: a minor constant

A log2-scaled version of an alignment score.
Normalized pairwise alignment score independent of query sequence length and database size.
(cutoff range often used: 40–50)

### NGS aligners are the opposite cases
* BLAST: minimally preprocessed
  * Database size: Very large
  * Database updates: Fast evolving
  * NUmber of queries: Relatively small
  * Expected distance: Distant

* NGS aligners: fully indexed
  * Database size: ~1 Genome
  * Database updates: Stable
  * NUmber of queries: very large
  * Expected distance: very close

### Different databases for different problems
* nr: All non-redundant GenBank CDS translations+PDB+SwissProt+PIR+PRF excluding environmental samples from WGS projects
* refseq_protein: NCBI Protein Reference Sequences
* landmark: The landmark database includes proteomes from 27 genomes spanning a wide taxonomic range
* swissprot: Non-redundant UniProtKB/SwissProt sequences
* pataa: Protein sequences derived from the Patent division of GenBank
* pdb: This database consists of sequences from the Protein Data Bank (PDB), which contains information about experimentally-determined structures of proteins, nucleic acids, and complex assemblies
* env_nr: Proteins from WGS metagenomic projects (env_nr)
* tsa_nr: The Transcriptome Shotgun Assembly proteins are produced from CDS features on mRNA sequences in the Transcriptome Shotgun Assembly sequences.
