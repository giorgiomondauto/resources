---
layout: default
title: Sampling Techniques for Building Golden Datasets for LLMs
---

# Sampling Techniques for Building Golden Datasets for LLMs

*A short survey of recent methods for curating high-confidence reference datasets used in LLM fine-tuning and evaluation.*

[← Back to Resources](index.md)

## 1. Rejection Sampling with Verifiers (STaR / ReST / ReSTEM)

Generates many candidate completions per prompt and keeps only those confirmed correct by an external verifier — a unit test, symbolic math checker, or reward model. The verified subset becomes the golden training/eval set, and the cycle can be repeated iteratively to bootstrap increasingly capable models from their own filtered outputs. This is the dominant technique behind reasoning-focused golden datasets used for chain-of-thought and math/coding fine-tuning.

**Reference:** Zelikman et al., "STaR: Bootstrapping Reasoning With Reasoning" (NeurIPS 2022); Gulcehre et al., "Reinforced Self-Training (ReST) for Language Modeling" (arXiv 2023); Singh et al., "Beyond Human Data: Scaling Self-Training for Problem-Solving with Language Models" (ReST-EM, arXiv 2023).

## 2. Self-Consistency Sampling

Samples k independent reasoning paths for the same question (typically at non-zero temperature) and selects the majority-vote or verifier-agreed final answer as the "golden" label. This produces high-confidence labels at low cost, without human annotation, by exploiting agreement across diverse decoding paths rather than a single greedy output.

**Reference:** Wang et al., "Self-Consistency Improves Chain of Thought Reasoning in Language Models" (ICLR 2023 / arXiv 2022).

## 3. LLM-as-Judge Consensus Filtering

Uses one or more LLM judges — often at different temperatures or with different prompts — to score candidate examples for correctness, helpfulness, or style. Only examples with high judge scores and strong inter-judge agreement are retained in the golden set, reducing noise from any single judge's bias or miscalibration. Widely used in recent large-scale synthetic data pipelines (e.g., Nemotron).

**Reference:** Zheng et al., "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena" (NeurIPS 2023); NVIDIA, "Nemotron-4 340B Technical Report" (2024).

## 4. Diversity + Quality Joint Sampling (Deita)

Embeds candidate examples, clusters them in embedding space, and selects a subset that is simultaneously diverse (non-redundant across clusters) and high-quality (per a learned complexity/quality scorer). This avoids golden sets that are accidentally dominated by near-duplicate or trivially easy examples, a common failure mode of naive top-k selection.

**Reference:** Liu et al., "What Makes Good Data for Alignment? A Comprehensive Study of Automatic Data Selection in Instruction Tuning" (Deita, ICLR 2024 / arXiv 2023).

## 5. Importance Resampling (DSIR)

Reweights a large candidate pool toward a target domain distribution using importance weights estimated from n-gram or embedding features, then resamples according to those weights. Rather than uniform random sampling, this biases selection toward examples that are most representative of the target evaluation distribution.

**Reference:** Xie et al., "Data Selection for Language Models via Importance Resampling" (DSIR, NeurIPS 2023).

## 6. Active / Uncertainty Sampling

Prioritizes examples for which the current model shows high disagreement, high output entropy, or high judge-score variance across repeated samples. These are the examples most informative for both evaluation and further training, since the model's behavior on "easy" consensus cases is already well characterized.

**Reference:** Settles, "Active Learning Literature Survey" (University of Wisconsin–Madison, 2009) — foundational framework, adapted in recent LLM data-curation pipelines for uncertainty-based example selection.

## 7. Difficulty-Stratified / Curriculum Sampling

Buckets candidate examples by empirical difficulty (e.g., solve rate under repeated sampling, perplexity, or step-level verifier pass rate) and samples across buckets so the golden set spans easy, medium, and hard cases rather than skewing toward what the model already answers correctly. Step-level process reward models have recently been used to stratify difficulty at the reasoning-step level, not just the final answer.

**Reference:** Lightman et al., "Let's Verify Step by Step" (ICLR 2024); Xu et al., "WizardLM: Empowering Large Language Models to Follow Complex Instructions" (Evol-Instruct, arXiv 2023).
