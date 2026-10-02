---
layout: default
title: RAG Techniques — A Survey of Approaches and Papers
---

# RAG Techniques — A Survey of Approaches and Papers

*A short survey of foundational and recent approaches to Retrieval-Augmented Generation (RAG), with an abstract of each and a link to the source paper or blog.*

[← Back to Resources](index.md)

## 1. RAG (Original Framework)

Introduces the foundational retrieval-augmented generation architecture: a pre-trained seq2seq model (parametric memory) is combined with a dense vector index over a document corpus (non-parametric memory), accessed via a learned neural retriever. The retriever fetches relevant passages at generation time, letting the model ground its outputs in external knowledge without having to encode all facts in its weights. This paper established the retrieve-then-generate paradigm that nearly all later RAG variants build on.

**Reference:** Lewis et al., ["Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"](https://arxiv.org/abs/2005.11401) (NeurIPS 2020).

## 2. HyDE (Hypothetical Document Embeddings)

Addresses zero-shot dense retrieval without relevance labels: given a query, an instruction-following LLM first generates a "hypothetical" answer document that captures plausible relevance patterns (even if it contains hallucinated specifics). This hypothetical document is then embedded, and the embedding — not the original query — is used to search the real corpus. The encoder's dense bottleneck filters out the hallucinated detail while keeping the relevance signal, often outperforming direct query embedding for retrieval.

**Reference:** Gao et al., ["Precise Zero-Shot Dense Retrieval without Relevance Labels"](https://arxiv.org/abs/2212.10496) (ACL 2023).

## 3. FLARE (Forward-Looking Active Retrieval)

Moves beyond single-shot retrieval by iteratively predicting the next sentence the model is about to generate, using that prediction as a retrieval query, and re-retrieving whenever the generated tokens show low confidence. This lets the system continually gather new information throughout long-form generation rather than retrieving once up front — important for tasks where the information need shifts as the answer unfolds.

**Reference:** Jiang et al., ["Active Retrieval Augmented Generation"](https://arxiv.org/abs/2305.06983) (EMNLP 2023).

## 4. Self-RAG (Self-Reflective Retrieval-Augmented Generation)

Trains a single LM to adaptively decide *when* to retrieve, and to critique both the retrieved passages and its own generations using special "reflection tokens." Retrieval tokens signal whether retrieval is needed at all for a given step; critique tokens assess whether retrieved passages are relevant and whether the generated output is actually supported by them. This lets the model skip retrieval for easy queries and apply tighter scrutiny on harder ones, improving factuality over fixed-retrieval RAG.

**Reference:** Asai et al., ["Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection"](https://arxiv.org/abs/2310.11511) (ICLR 2024).

## 5. Corrective RAG (CRAG)

Adds a lightweight retrieval evaluator that grades the quality of retrieved documents for a given query and assigns a confidence level. Depending on that grade, CRAG triggers different downstream actions: using the retrieved documents as-is, falling back to a large-scale web search when retrieval confidence is low, or combining both. A decompose-then-recompose step then filters retrieved documents down to their key, query-relevant content before it reaches the generator — explicitly correcting for weak or irrelevant retrieval rather than trusting it blindly.

**Reference:** Yan et al., ["Corrective Retrieval Augmented Generation"](https://arxiv.org/abs/2401.15884) (arXiv 2024).

## 6. RAPTOR (Recursive Abstractive Processing for Tree-Organized Retrieval)

Builds a tree over a document corpus by recursively embedding, clustering, and summarizing chunks from the bottom up, producing summaries at multiple levels of abstraction. At query time, RAPTOR retrieves from across this tree rather than only from short contiguous chunks, letting it integrate both fine-grained details and document-level themes — this is particularly effective for multi-step reasoning over long documents, where flat chunk retrieval misses the big picture.

**Reference:** Sarthi et al., ["RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval"](https://arxiv.org/abs/2401.18059) (ICLR 2024).

## 7. GraphRAG

Extracts a knowledge graph from an unstructured document corpus using an LLM, builds a hierarchical community structure over that graph, and generates summaries for each community. At query time, GraphRAG can answer both local, fact-specific questions and global, sensemaking questions (e.g., "what are the main themes in this dataset?") by traversing and summarizing over the graph — something flat vector-similarity RAG struggles with at the dataset-wide scale.

**Reference:** Edge et al., ["From Local to Global: A Graph RAG Approach to Query-Focused Summarization"](https://www.microsoft.com/en-us/research/publication/from-local-to-global-a-graph-rag-approach-to-query-focused-summarization/) (Microsoft Research, 2024); project site: [microsoft.github.io/graphrag](https://microsoft.github.io/graphrag/).

## 8. RAG-Fusion

Generates multiple reformulated/sub-query variants of the user's original query, runs retrieval independently for each variant, and fuses the resulting ranked lists using Reciprocal Rank Fusion (RRF) — rewarding documents that rank consistently well across variants. This surfaces relevant material that a single phrasing of the query would miss, particularly when the user's vocabulary doesn't match how the corpus is indexed.

**Reference:** Rackauckas, ["RAG-Fusion: a New Take on Retrieval-Augmented Generation"](https://arxiv.org/abs/2402.03367) (arXiv 2024).
