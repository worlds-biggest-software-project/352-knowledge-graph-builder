# Knowledge Graph Builder

> Part of the [worlds-biggest-software-project](https://github.com/worlds-biggest-software-project) initiative.
>
> Auto-construct queryable knowledge graphs from unstructured documents using LLM-driven entity and relationship extraction.

Knowledge Graph Builder turns document corpora — PDFs, Word files, web pages, emails, support tickets — into navigable, queryable property graphs without months of manual annotation or predefined schemas. It is aimed at engineering teams, data platform owners, and domain experts who need to unlock relational knowledge buried in text but lack the budget for specialist NLP pipelines.

---

## Why Knowledge Graph Builder?

- Traditional knowledge graph construction required months of manual annotation, predefined ontologies, and specialised NLP expertise — out of reach for most teams.
- Open-source incumbents like Neo4j LLM Graph Builder, Microsoft GraphRAG, LangChain `LLMGraphTransformer`, and LlamaIndex `PropertyGraphIndex` ship strong extraction primitives but leave entity resolution, schema inference, and human-in-the-loop curation as exercises for the user.
- Commercial offerings such as Diffbot, Ontotext GraphDB Enterprise, and Amazon Neptune + Bedrock GraphRAG are either tied to public web data, expensive at scale, or opaque about the extraction pipeline.
- Cross-document entity deduplication, confidence-scored extractions, and incremental ingestion without full reprocessing remain underserved across the surveyed tools.
- LLMs now make schema-free extraction practical — research from HKUST's ATLAS demonstrated 900M+ nodes and 5.9B edges built from 50M documents with 95% semantic alignment to human-crafted schemas and zero manual intervention.

---

## Key Features

### Ingestion and Extraction

- Multi-format document ingestion: PDF, DOCX, TXT, HTML, web URLs.
- LLM-driven entity and relationship extraction with configurable schema constraints.
- Chunk-to-entity provenance: every node and edge linked to its source sentence and document.
- Multi-LLM provider support (OpenAI, Anthropic, open-source models via Ollama).

### Graph Construction and Quality

- Entity resolution and deduplication across documents using LLM-based candidate comparison.
- Relationship confidence scoring with a review UI for borderline extractions.
- Automated schema inference with iterative refinement from observed entities.
- Incremental document ingestion without full graph reprocessing.

### Querying and Exploration

- Natural language Q&A using the GraphRAG retrieval pattern.
- Interactive graph visualisation with node/edge filtering and cluster exploration.
- Domain-specific extraction prompt templates (legal, biomedical, financial, cybersecurity).
- Python SDK with a one-call `build_graph(docs, schema)` interface.

### Advanced Capabilities (Backlog)

- Temporal graph support: time-stamped entity and relationship facts with point-in-time queries.
- Community detection and hierarchical community summarisation (Microsoft GraphRAG pattern).
- Collaborative annotation UI for team review, correction, and few-shot feedback loops.
- MCP server exposing the graph as AI agent memory.
- Export to RDF/SPARQL-compatible formats and optional ontology alignment to Wikidata or Schema.org.

---

## AI-Native Advantage

LLMs replace brittle fuzzy-matching heuristics for entity resolution, propose and refine graph schemas autonomously, and assign confidence scores to extracted triples so reviewers can prioritise borderline cases. Few-shot prompting with frontier models achieves accuracy comparable to fully supervised traditional NLP without thousands of labelled training examples, and natural-language-to-Cypher/SPARQL translation makes the resulting graph accessible to non-technical users.

---

## Tech Stack & Deployment

Targeted as a self-hostable Python SDK with a property graph backend (Neo4j as default, pluggable adapters for FalkorDB, Memgraph, or Neptune). Vector embeddings are stored alongside graph nodes to support hybrid semantic + graph-traversal retrieval (the GraphRAG pattern). Optional RDF/SPARQL export aligns with W3C standards and ISO/IEC 39075 GQL for interoperability with standards-based tooling.

---

## Market Context

Knowledge graph construction reached production maturity in 2024–2025, with reported 300–320% ROI on graph-based knowledge systems. The space spans free open-source libraries (LangChain, LlamaIndex, Microsoft GraphRAG), commercial SaaS (Diffbot, Zep cloud), and managed cloud services (Amazon Neptune + Bedrock). Primary buyers are data platform teams, AI engineering groups, and domain organisations in legal, biomedical, financial, and cybersecurity sectors that need to mine internal document corpora.

---

## Project Status

> This project is in the **research and specification phase**.  
> Contributions, feedback, and domain expertise are welcome.

---

## Contributing

We welcome contributions from developers, domain experts, and potential users.
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Important:** All contributions must be your own original work or clearly attributed
open-source material with a compatible licence. Copyright infringement and licence
violations will not be tolerated and will result in immediate removal of the offending
contribution. If you are unsure whether a piece of code, text, or other material is
safe to contribute, open an issue and ask before submitting.

---

## Licence

Licence to be determined. All major open-source tools surveyed in this space are released under permissive licences (Apache 2.0 or MIT), so no licence-compatibility blockers were identified.
