---
name: context-engineering
description: 'Domain knowledge, mathematical facts, and empirical heuristics about LLM context windows, attention mechanisms, and context rot. Use when authoring or reviewing context engineering talks.'
---

# Context Engineering Domain Facts

<workflow>

Reference these verified facts and formulations when authoring context engineering talks:

## 1. Softmax Attention Equation

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

- Weights normalize to exactly 1.0 (100% budget).
- Growing the denominator crushes individual token attention weights toward zero.

## 2. Rotary Position Embeddings (RoPE) & U-Curve

- Liu et al. (2023) "Lost in the Middle": LLMs attend heavily to the start (primacy) and end (recency) of context.
- Information placed between 20% and 80% suffers significant degradation.

## 3. The 3 Pathologies of Context Rot

1. **Zombie Code (Negative Priming)**: Autoregressive repetition of buggy patterns in prior chat turns.
2. **Constraint Bleed (Denominator Dilution)**: Early instructions losing attention mass over long conversations.
3. **Multi-Hop Reasoning Collapse**: Exponential difficulty in cross-referencing disparate facts across large contexts.

## 4. The Model Routing Matrix

- Minimal Context (<16k) + High Reasoning: Surgical code, TDD, refactoring, security reviews.
- Massive Context (1M+) + Low Reasoning: Repository scanning, API drift, code search, summarization.
- **Anti-pattern**: Massive Context (1M+) + High Reasoning -> extreme latency, runaway cost, reasoning collapse.

## Example

For a slide explaining normalized attention, use the formulation and delivery notes in the [softmax attention slide](../../../talks/context-engineering/slides/02-the-math/01-softmax-attention.md).

</workflow>
