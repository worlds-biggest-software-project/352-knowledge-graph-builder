# Research: Knowledge Graph Builder

**Date:** 2026-05-02
**Status:** Candidate research

---

## 1. Problem Statement

Organisations accumulate vast stores of unstructured text — documents, reports, emails, research papers, support tickets — that contain valuable relational knowledge which remains locked and unsearchable. Building knowledge graphs traditionally required months of manual annotation by domain experts, predefined schemas, and specialised NLP pipelines. LLMs now make it practical to automatically extract entities and relationships from unstructured data and construct queryable knowledge graphs without extensive manual intervention, opening this capability to teams that previously lacked the resources to pursue it.

---

## 2. Market Landscape

Knowledge graph construction reached production maturity in 2024-2025, with organisations reporting 300-320% ROI on graph-based knowledge systems. What previously required specialist NLP expertise and months of annotation can now be completed in days using LLM-driven pipelines.

Key tools and platforms include:

- **Neo4j LLM Graph Builder** — upload files from local machines, cloud storage (GCS, S3), or web sources, select an LLM, and generate a knowledge graph automatically. ([github.com/neo4j-labs](https://github.com/neo4j-labs/llm-graph-builder))
- **FalkorDB GraphRAG SDK** — described as the highest-performance path from raw documents to a queryable knowledge graph. ([siliconflow.com](https://www.siliconflow.com/articles/en/best-open-source-LLM-for-Knowledge-Graph-Construction))
- **AutoSchemaKG / ATLAS** — research from HKUST demonstrating autonomous KG construction without predefined schemas; the ATLAS system built 900 million+ nodes and 5.9 billion edges from 50 million documents with 95% semantic alignment to human-crafted schemas and zero manual intervention. ([arxiv.org](https://arxiv.org/html/2510.20345v1))
- **LLM-empowered KG construction frameworks** — few-shot prompting with GPT-4 or Claude achieves accuracy comparable to fully supervised traditional models without requiring thousands of labelled training examples. ([arxiv.org](https://arxiv.org/html/2510.20345v1))

Top open-source LLMs for knowledge graph construction in 2026 include DeepSeek-R1, Qwen3-235B-A22B, and GLM-4.5, chosen for reasoning quality and structured output generation. ([siliconflow.com](https://www.siliconflow.com/articles/en/best-open-source-LLM-for-Knowledge-Graph-Construction))

---

## 3. Key Features to Consider

- **Schema-free entity and relationship extraction** — identifying entities, entity types, and relationships from raw text without requiring a predefined ontology
- **Schema inference and refinement** — automatically proposing and iteratively refining a graph schema from observed entities and relationships
- **Multi-source ingestion** — processing PDFs, Word documents, web pages, databases, emails, and structured data exports
- **Entity resolution and deduplication** — merging references to the same real-world entity across documents (e.g. "IBM", "International Business Machines", "Big Blue")
- **Relationship confidence scoring** — surfacing uncertainty so users can review borderline extractions
- **Interactive graph visualisation** — exploring nodes, edges, and clusters in a navigable graph interface
- **Natural language querying** — asking questions in plain English and receiving answers derived from graph traversal
- **Graph export and integration** — exporting to Neo4j, Weaviate, Amazon Neptune, or RDF/SPARQL-compatible formats

---

## 4. Technical Considerations

- **Entity extraction pipeline** — NER (named entity recognition) stage to identify candidate entities, followed by relation extraction and co-reference resolution
- **LLM orchestration** — chunking large documents into overlapping windows, prompting for structured JSON output (entity-relation triples), and merging across chunks
- **Graph database backend** — property graphs (Neo4j, FalkorDB) for flexible schema and traversal performance; RDF triple stores for standards compliance
- **Embedding layer** — storing vector embeddings alongside graph nodes to support hybrid semantic + graph-traversal queries (GraphRAG pattern)
- **Incremental updates** — efficiently adding new documents and entities to an existing graph without full reprocessing
- **Scalability** — distributed processing for large corpora; the ATLAS system demonstrates that 50 million documents is achievable with the right architecture
- **Ontology alignment** — optionally mapping extracted entities to standard ontologies (Wikidata, Schema.org, domain-specific ontologies) for interoperability

---

## 5. Differentiation Opportunities

- **Domain-adaptive prompting** — pre-built extraction prompt templates optimised for legal, biomedical, financial, and cybersecurity domains
- **Provenance tracking** — every node and edge linked back to the exact source sentence and document, enabling auditing and trust verification
- **Collaborative curation** — allowing teams to review, correct, and annotate the extracted graph through a web UI, feeding corrections back as few-shot examples
- **Temporal graph support** — representing how relationships change over time (e.g. a person's role at an organisation changing across documents dated at different times)
- **GraphRAG question answering** — using the knowledge graph as the retrieval backbone for a RAG system, delivering more factually consistent answers than pure vector search

---

## Sources

- [Creating Knowledge Graphs from Unstructured Data — Neo4j Developer Guides](https://neo4j.com/developer/genai-ecosystem/importing-graph-from-unstructured-data/)
- [How to Convert Unstructured Text to Knowledge Graphs Using LLMs — Neo4j Blog](https://neo4j.com/blog/developer/unstructured-text-to-knowledge-graph/)
- [From LLMs to Knowledge Graphs: Building Production-Ready Graph Systems in 2025 — Medium](https://medium.com/@claudiubranzan/from-llms-to-knowledge-graphs-building-production-ready-graph-systems-in-2025-2b4aff1ec99a)
- [LLM-empowered Knowledge Graph Construction: A Survey — arXiv](https://arxiv.org/html/2510.20345v1)
- [Neo4j LLM Graph Builder — GitHub](https://github.com/neo4j-labs/llm-graph-builder)
- [Ultimate Guide: Best Open Source LLMs for Knowledge Graph Construction in 2026 — SiliconFlow](https://www.siliconflow.com/articles/en/best-open-source-LLM-for-Knowledge-Graph-Construction)
- [From Unstructured Text to Interactive Knowledge Graphs Using LLMs — Medium](https://robert-mcdermott.medium.com/from-unstructured-text-to-interactive-knowledge-graphs-using-llms-dd02a1f71cd6)
