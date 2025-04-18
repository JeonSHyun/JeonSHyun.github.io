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
* 











