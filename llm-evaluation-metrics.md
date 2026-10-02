---
layout: default
title: Metrics for Evaluating LLM Responses — Ragas Overview
---

# Metrics for Evaluating LLM Responses — Ragas Overview

*A short survey of metrics for evaluating LLM and RAG-system outputs, based on the [Ragas](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/) metrics catalogue.*

[← Back to Resources](index.md)

## RAG (Retrieval-Augmented Generation) Metrics

Metrics targeted at pipelines that retrieve context before generating a response — they separately score the retrieval step and the generation step so failures can be localized to one or the other.

- **[Context Precision](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/context_precision/)** — measures the proportion of retrieved context that is actually relevant to the query, penalizing retrieval of irrelevant chunks.
- **[Context Recall](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/context_recall/)** — evaluates how completely the retrieved context covers the information needed to answer the query, i.e. whether retrieval missed anything important.
- **[Context Entities Recall](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/context_entities_recall/)** — checks whether specific named entities present in the ground-truth answer were actually retrieved.
- **[Noise Sensitivity](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/noise_sensitivity/)** — tests how robust the generated response is when irrelevant or distracting content is mixed into the retrieved context.
- **[Response Relevancy](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/answer_relevance/)** — determines whether the generated response actually addresses the user's question, independent of factual correctness.
- **[Faithfulness](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/faithfulness/)** — validates that claims in the response are grounded in the retrieved context, catching hallucinated content not supported by the source material.
- **[Multimodal Faithfulness](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/multi_modal_faithfulness/)** — extends faithfulness checks to responses grounded in image or video content.
- **[Multimodal Relevance](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/multi_modal_relevance/)** — evaluates whether retrieved multimodal content (images/video) is relevant to the query.

## Nvidia Metrics

A set of metrics contributed for evaluating accuracy and groundedness in RAG/Q&A pipelines.

- **[Answer Accuracy, Context Relevance, Response Groundedness](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/nvidia_metrics/)** — compares generated answers against expected correct responses (Answer Accuracy), checks whether retrieved passages match query intent (Context Relevance), and confirms responses are supported by the provided context (Response Groundedness).

## Agent / Tool-Use Metrics

Metrics for evaluating LLM agents that call tools or operate over multiple turns toward a goal, rather than single-shot Q&A.

- **[Topic Adherence, Tool Call Accuracy, Tool Call F1, Agent Goal Accuracy](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/agents/)** — Topic Adherence measures whether the agent stays within its intended scope; Tool Call Accuracy and Tool Call F1 evaluate correct selection/invocation of available tools (F1 combining precision and recall of tool-use decisions); Agent Goal Accuracy assesses whether the agent actually achieves its specified objective.

## Natural Language Comparison Metrics

Metrics that compare a generated response against a reference answer — useful when ground-truth answers exist, independent of any retrieval step.

- **[Factual Correctness](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/factual_correctness/)** — compares factual claims in the response against a reference answer.
- **[Semantic Similarity](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/semantic_similarity/)** — measures semantic overlap between generated and reference text using embeddings, rather than exact wording.
- **[Traditional metrics: Non-LLM String Similarity, BLEU, CHRF, ROUGE, String Presence, Exact Match](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/traditional/)** — classic NLP string/n-gram overlap metrics; String Presence checks for expected phrases in the output, Exact Match requires character-for-character correspondence with the reference.

## SQL Metrics

Metrics for evaluating text-to-SQL generation tasks.

- **[Execution-based Datacompy Score, SQL Query Equivalence](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/sql/)** — Datacompy Score compares the *results* of running the generated SQL query for functional equivalence; SQL Query Equivalence evaluates semantic correctness of the generated query itself, independent of execution.

## General-Purpose Metrics

Flexible, often LLM-judge-based frameworks for defining custom evaluation criteria when no off-the-shelf metric fits.

- **[Aspect Critic, Simple Criteria Scoring, Rubrics-based Scoring, Instance-specific Scoring](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/general_purpose/)** — let you define custom aspects, scoring criteria, or rubrics (optionally per-instance) and have an LLM judge score responses against them.

## Summarization Metrics

- **[Summarization Score](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/summarization_score/)** — evaluates the quality and completeness of a generated summary relative to the source document.

**Reference:** Ragas documentation, ["Overview of Available Metrics"](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/).
