---
title: Vision Transformer
author: JSH
date: 2024-09-02 9:00:00 +0800
categories: [Study, Artificial Intelligence]
tags: [Study, Artificial Intelligence]
use_math: true
---

# Vision Transformer

## Self-attention
$Attention(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V$

### Query(Q), Key(K), Value(V)
Attention value is the weighted average of values, where each weight is proportional to the relevance between the query and the corresponding key
* Query: context
* Key-value: Reference
