# Knowledge Graph Builder — Feature & Functionality Survey

> Candidate #352 · Researched: 2026-05-04

## Solutions Analysed

| Tool | Type | Licence / Model | URL |
|------|------|-----------------|-----|
| Neo4j LLM Graph Builder | Web app + open-source | Apache 2.0 (Labs) | https://github.com/neo4j-labs/llm-graph-builder |
| Neo4j GraphRAG Python Package | Python library | Apache 2.0 | https://github.com/neo4j/neo4j-graphrag-python |
| Microsoft GraphRAG | Python library | MIT | https://github.com/microsoft/graphrag |
| LangChain LLMGraphTransformer | Python library | MIT | https://python.langchain.com/ |
| LlamaIndex PropertyGraphIndex | Python library | MIT | https://docs.llamaindex.ai/ |
| FalkorDB GraphRAG SDK | Python SDK | Apache 2.0 | https://github.com/FalkorDB/GraphRAG-SDK |
| Graphiti (Zep) | Python library / SaaS | Apache 2.0 (lib) / Commercial (cloud) | https://github.com/getzep/graphiti |
| Diffbot Knowledge Graph | SaaS API | Commercial | https://www.diffbot.com/ |
| Ontotext GraphDB / Graphwise | Enterprise platform | Commercial (free tier) | https://www.ontotext.com/ |
| spaCy + spacy-llm | Python library | MIT | https://github.com/explosion/spacy-llm |
| ReLiK (Sapienza NLP) | Python library | Apache 2.0 | https://github.com/SapienzaNLP/relik |
| Amazon Neptune + Bedrock | Managed cloud service | Commercial (AWS) | https://aws.amazon.com/neptune/ |

---

## Feature Analysis by Solution

### Neo4j LLM Graph Builder

**Core features**
- Upload documents from local files, cloud storage (S3, GCS), or web URLs
- Multi-format ingestion: PDF, DOCX, TXT, YouTube videos, web pages, Wikipedia
- LLM-driven entity and relationship extraction via configurable prompts
- Graph schema definition (optional) for semantically constrained extraction
- Community detection and community summary generation (GraphRAG pattern)
- kNN chunk similarity graph via SIMILAR relationships between overlapping chunks
- Natural language question answering using local and global retrievers in parallel
- Multi-LLM support: GPT-5.x, Claude 4.5, Gemini 2.5, Groq, Fireworks, Bedrock Nova
- Web UI for document management, graph browsing, and Q&A
- Self-hostable via Docker; managed cloud deployment also available

**Differentiating features**
- Tight Neo4j integration: directly writes to a live Neo4j Aura or self-hosted instance
- Chunk-to-entity provenance: every entity linked back to source chunk and document
- Parallel retriever evaluation for Q&A (runs multiple RAG strategies, picks best)
- Backend services no longer expose Neo4j credentials to the frontend (security hardening, 2026)
- Detailed graph analytics: chunk, entity, and community node counts per document

**UX patterns**
- Drag-and-drop file upload; S3/GCS bucket browser for bulk ingestion
- Progress indicators per document during extraction
- Graph visualisation panel with zoom/pan, node inspection, and filtering
- Chat panel alongside the graph for contextual Q&A
- Schema editor for constraining node labels and relationship types

**Integration points**
- Neo4j Aura and self-hosted Neo4j databases
- LangChain for LLM orchestration and chain building
- AWS S3, Google Cloud Storage for document sources
- YouTube Data API for transcript ingestion
- Docker Compose for local deployment

**Known gaps**
- Schema reduction heuristics (auto-clustering labels) acknowledged as imperfect by maintainers
- No built-in entity resolution / deduplication across documents
- Limited temporal graph support; no time-aware relationship modelling
- No collaborative annotation or human-in-the-loop correction workflow

**Licence / IP notes**
- Apache 2.0 open-source licence. No known patent concerns.

---

### Neo4j GraphRAG Python Package

**Core features**
- `SimpleKGPipeline`: one-call abstraction from raw text/PDF to populated Neo4j graph
- Configurable entity and relationship extraction via LLM prompts and structured output
- Embedding generation and storage alongside graph nodes for hybrid retrieval
- Multiple built-in retrievers: VectorRetriever, VectorCypherRetriever, HybridRetriever, HybridCypherRetriever
- Pipeline abstraction for advanced orchestration of extraction, embedding, and storage components
- Full Python API with async support
- Comprehensive API reference and user guides maintained by Neo4j

**Differentiating features**
- Official, long-term-support library directly from Neo4j
- Structured pipeline DAG model enabling custom component injection at any step
- Tight typing and schema validation via Pydantic models
- Works directly from text strings or PDF file paths without preprocessing

**UX patterns**
- Code-first API; no UI
- Well-documented configuration YAML for reproducing pipelines
- Integration with Jupyter notebooks for prototyping

**Integration points**
- Neo4j graph database (all versions)
- OpenAI, Anthropic, Cohere, and other LLM providers via LiteLLM
- LangChain and LlamaIndex components as drop-in sub-components

**Known gaps**
- No graphical interface; purely programmatic
- Entity resolution not built-in; requires custom components
- Community detection not included (unlike the web app variant)

**Licence / IP notes**
- Apache 2.0. Supported by Neo4j, Inc.

---

### Microsoft GraphRAG

**Core features**
- End-to-end pipeline: text chunking, entity and relationship extraction, community detection, community summarisation
- Hierarchical community structure (Leiden algorithm) enabling local and global search modes
- Local search: answers entity-specific questions by traversing community context
- Global search: answers dataset-wide thematic questions using community summaries
- LazyGraphRAG variant: defers expensive summarisation until query time, reducing indexing cost
- Output stored as Parquet files or in Azure AI Search; no graph database required
- Configurable LLM prompts for entity/relationship extraction and summarisation
- Supports Azure OpenAI and local Ollama models

**Differentiating features**
- Hierarchical community-based search is a distinctive architectural pattern not found in most competitors
- LazyGraphRAG reduces upfront cost by ~99% while preserving multi-hop reasoning quality
- Available through Microsoft Discovery for scientific research on Azure
- GraphRAG-Bench benchmark comparisons publicly available

**UX patterns**
- CLI-driven workflow (`graphrag index`, `graphrag query`)
- Configuration via YAML/TOML files
- No UI; outputs are flat files or Azure Search indexes

**Integration points**
- Azure OpenAI Service and Azure AI Search
- Local Ollama models for air-gapped deployments
- Python API for programmatic integration

**Known gaps**
- Requires a graph database separately for persistent storage beyond Parquet files
- No interactive graph visualisation
- Index rebuild required for new documents (no incremental ingestion)
- No entity resolution across documents

**Licence / IP notes**
- MIT licence. Microsoft Research project; no patent concerns identified.

---

### LangChain LLMGraphTransformer

**Core features**
- `LLMGraphTransformer`: converts LangChain `Document` objects into graph triples
- Two extraction modes: tool-based (structured output, property extraction) and prompt-based (few-shot, no tools needed)
- Configurable allowed node types, allowed relationship types, and property extraction
- `convert_to_graph_documents()` method returns list of `GraphDocument` objects for downstream use
- Integrates with Neo4j, Memgraph, and Apache AGE via graph store wrappers
- `GraphCypherQAChain`: translates natural language questions to Cypher, executes them, returns NL answers
- Works with any LangChain-compatible LLM (OpenAI, Anthropic, Cohere, Mistral, etc.)

**Differentiating features**
- Fits natively into existing LangChain pipelines and agent frameworks
- Schema constraints reduce hallucination of non-existent entity/relation types
- Composable with other LangChain retrievers and memory components
- Property extraction from relationships (e.g., confidence, date)

**UX patterns**
- Code-first, Python notebook-friendly
- Extensive documentation with runnable examples on LangChain Hub
- Easily combined with `RecursiveCharacterTextSplitter` for chunking

**Integration points**
- All LangChain-compatible LLM providers
- Neo4j, Memgraph, Apache AGE graph stores
- LangSmith for tracing and debugging extraction quality
- LangGraph for agentic workflows over graphs

**Known gaps**
- No entity resolution or deduplication
- Prompt-based mode does not support property extraction
- No built-in visualisation
- Graph schema constraints must be manually specified; no schema inference

**Licence / IP notes**
- MIT licence. No patent concerns identified.

---

### LlamaIndex PropertyGraphIndex

**Core features**
- `PropertyGraphIndex`: constructs a labeled property graph from documents using LLM-driven extractors
- Multiple extractor modules: `SimpleLLMPathExtractor` (free-form), `SchemaLLMPathExtractor` (constrained), `ImplicitPathExtractor` (dependency-based)
- Property graph representation with typed node labels, node/edge properties
- Multiple retriever strategies: `LLMSynonymRetriever`, `VectorContextRetriever`, `TextToCypherRetriever`, `CypherTemplateRetriever`
- Retrievers can be composed and run concurrently for ensemble retrieval
- Supports Neo4j, Memgraph, Nebula, and in-memory `SimplePropertyGraphStore`
- Embedding storage alongside graph nodes for hybrid retrieval

**Differentiating features**
- Highly modular: swap out extractors, graph stores, and retrievers independently
- Ensemble retrieval combining semantic similarity and graph traversal in parallel
- LlamaIndex Workflow abstraction for agentic graph queries

**UX patterns**
- Python API; LlamaIndex-style index/query engine pattern
- Extensive Jupyter notebook examples
- Compatible with LlamaIndex's document loaders (100+ formats)

**Integration points**
- LlamaIndex document ecosystem (PDF, DOCX, HTML, etc.)
- Neo4j, Memgraph, NebulaGraph, in-memory store
- Any LlamaIndex-compatible LLM and embedding model
- ReLiK integration available for high-performance entity linking

**Known gaps**
- No built-in UI or visualisation
- Entity resolution not built-in
- Schema inference is free-form by default; constrained schemas must be defined manually

**Licence / IP notes**
- MIT licence. No patent concerns identified.

---

### FalkorDB GraphRAG SDK

**Core features**
- Automated ontology generation from unstructured data (PDF, CSV, HTML, TXT, JSON, URLs)
- Ontology import from pre-defined JSON configurations or existing graph schemas
- Document ingestion pipeline from diverse sources to FalkorDB property graph
- Natural language Q&A over the constructed graph via GraphRAG pattern
- Multi-LLM support: OpenAI, Gemini, Groq, and others
- LLM-agnostic framework; swappable LLM backend
- Ranked #1 on GraphRAG-Bench Novel and Medical dataset categories (2025)
- Sub-10ms query latency; up to 90% reduction in hallucinations (claimed)
- Native multi-tenancy

**Differentiating features**
- Ontology-first approach: builds and manages a formal ontology before constructing the graph
- From raw documents to cited answers in under 5 minutes (claimed)
- Predictable cost model with sensible defaults
- FalkorDB as backend: purpose-built for performance and multi-tenancy

**UX patterns**
- Python SDK, code-first
- Configuration via Python objects and JSON ontology files

**Integration points**
- FalkorDB graph database
- OpenAI, Gemini, Groq LLM providers
- Graphiti MCP server for exposing the graph to AI agents

**Known gaps**
- Tightly coupled to FalkorDB; limited portability to other graph databases
- No web UI for non-developers
- Smaller community and ecosystem than Neo4j or LangChain

**Licence / IP notes**
- Apache 2.0 for open-source SDK. FalkorDB cloud is commercial.

---

### Graphiti (Zep)

**Core features**
- Temporal knowledge graph: every entity edge carries event time and ingestion time
- Incremental episode ingestion: processes conversation turns, documents, or structured data as discrete episodes
- Entity deduplication and resolution across episodes using LLM-driven comparison
- Hybrid search: semantic (vector) + BM25 full-text search with proximity reranking
- Point-in-time historical queries: retrieve the state of the graph at any past moment
- Custom entity type definitions for domain-specific knowledge representation
- MCP server for exposing graph memory to any MCP-compatible AI agent (Claude, Cursor, etc.)
- Bulk processing with parallelised LLM calls preserving chronological ordering

**Differentiating features**
- Temporal graph is the defining feature: tracks fact changes over time, not just current state
- Built specifically for AI agent memory, not general document knowledge bases
- Entity resolution as a first-class feature (LLM-based deduplication across episodes)
- Source provenance maintained per entity and relationship

**UX patterns**
- Python library + optional Zep cloud API
- Simple episode-ingestion API: `client.add_episode(name, episode_type, content)`
- MCP server for zero-code integration with AI agent frameworks

**Integration points**
- Neo4j or FalkorDB as graph backend
- Any LLM provider via LiteLLM
- MCP protocol for AI agent integration
- LangGraph and LlamaIndex agent frameworks

**Known gaps**
- Optimised for conversational/agent memory, not large-document corpus ingestion
- No web UI for non-developers
- Cloud service (Zep) is commercial; self-hosting requires Neo4j or FalkorDB infrastructure

**Licence / IP notes**
- Graphiti library: Apache 2.0. Zep cloud platform: commercial SaaS. No patent concerns identified.

---

### Diffbot Knowledge Graph

**Core features**
- Pre-built web-scale knowledge graph: 10+ billion entities, 1 trillion facts
- Entities: People, Organisations, Products, Articles, Events, and more
- Continuous web crawl across 60+ billion pages; graph updated automatically
- Diffbot Query Language (DQL) for filtering, sorting, and faceting entities
- Visual query builder (no-code) and pure DQL API access
- Natural Language API: entity extraction, relationship/fact extraction, sentiment analysis
- Data provenance: source and transformation records for all ~200 billion facts
- Integrations: Excel, Google Sheets, Tableau, REST API

**Differentiating features**
- No ingestion pipeline required: the graph already exists and is continuously updated
- Web-scale: one of only three Western entities crawling a majority of the public web
- Proven data provenance system for compliance and auditing

**UX patterns**
- Web-based query interface with visual DQL builder
- REST API for programmatic access
- Spreadsheet integrations for non-technical users

**Integration points**
- REST API
- Excel and Google Sheets plugins
- Tableau connector
- Enhance API for enriching custom entity sets against the Diffbot graph

**Known gaps**
- Read-only for private/custom data: cannot ingest proprietary enterprise documents into the graph
- Expensive for high-volume API access
- Limited customisation of entity types and relationship schemas
- Data is public-web-only; not suitable for internal knowledge management

**Licence / IP notes**
- Commercial SaaS. Proprietary data and crawling infrastructure.

---

### Ontotext GraphDB / Graphwise

**Core features**
- RDF triple store with OWL reasoning and SPARQL 1.1 query support
- SHACL constraint validation for data quality assurance
- GraphQL interface (via Semantic Object service) for developer-friendly access
- OntoRefine: no-code data cleaning, transformation, and RDF conversion tool
- No-code RAG chat feature (chat with your graph via GraphDB Workbench)
- Taxonomy Advisor: automated taxonomy creation and enrichment for KG building
- Full-text search, semantic similarity, and SPARQL-based reasoning
- Enterprise clustering and replication for large-scale deployments

**Differentiating features**
- Standards-first: built on W3C RDF/OWL/SPARQL, ensuring interoperability
- OWL reasoning engine: infers implicit facts from declared ontologies
- Graphwise (merger of Ontotext + Semantic Web Company) positions as semantic layer between data and AI
- OntoRefine provides no-code ETL into RDF for non-developers

**UX patterns**
- GraphDB Workbench: full web UI for repository management, querying, import, and visualisation
- No-code OntoRefine for data transformation
- GraphQL API for application developers
- SPARQL endpoint for standards-based tooling

**Integration points**
- SPARQL 1.1 endpoint (standards-based; compatible with all RDF tools)
- GraphQL API
- REST API
- OntoRefine for ETL from CSV, JSON, XML, spreadsheets

**Known gaps**
- RDF/OWL learning curve is steep for teams unfamiliar with semantic web standards
- LLM-driven entity extraction is not a native feature; requires third-party pipelines
- Enterprise pricing can be prohibitive for small teams

**Licence / IP notes**
- GraphDB Free edition available. Enterprise edition is commercial. No patent concerns identified.

---

### spaCy + spacy-llm

**Core features**
- Industrial-strength NLP pipeline: tokenisation, POS tagging, dependency parsing, NER
- Pre-trained models for 60+ languages
- spacy-llm: integrates LLMs into spaCy pipelines for NER, REL (relation extraction), text classification, and coreference resolution
- REL task: define custom relationship types extracted via prompted LLM calls
- Prodigy annotation tool for efficient training data creation
- Entity linking: maps extracted mentions to knowledge base entries
- Custom component API for adding project-specific extractors

**Differentiating features**
- Battle-tested production NLP library; not primarily a KG tool but foundational to many pipelines
- spacy-llm enables custom NLP task definitions with few-shot examples
- Prodigy integration lowers the cost of human annotation for fine-tuning

**UX patterns**
- Python API, pipeline composition pattern
- CLI for training and evaluation
- No built-in UI; Prodigy provides annotation UI

**Integration points**
- Neo4j (via community tutorials and integrations)
- Hugging Face models for entity linking
- Any LLM provider via spacy-llm task definitions

**Known gaps**
- Not a complete KG builder: provides building blocks, not end-to-end pipeline
- No graph storage or visualisation
- Requires significant custom glue code to produce a queryable knowledge graph

**Licence / IP notes**
- spaCy and spacy-llm: MIT licence. Prodigy annotation tool is commercial.

---

### ReLiK (Sapienza NLP)

**Core features**
- Retrieve-Read-Link architecture: fast entity linking and relation extraction
- Retriever stage: retrieves candidate entities from a knowledge base
- Reader stage: extracts entities and relations from text using retrieved candidates
- Closed Information Extraction models combining entity linking and relation extraction in one pass
- Pre-trained models available on Hugging Face (Large, Small variants)
- Achieves high extraction accuracy at a fraction of LLM-based approaches' cost

**Differentiating features**
- Academic-origin, state-of-the-art accuracy without requiring large LLM inference at extraction time
- Blazing fast: designed for high-throughput extraction on academic budgets
- LlamaIndex integration for drop-in use in existing pipelines

**UX patterns**
- Python library; code-first
- Hugging Face model hub for pre-trained model download

**Integration points**
- LlamaIndex PropertyGraphIndex (official integration)
- Neo4j (community tutorials)
- Hugging Face model hub

**Known gaps**
- Requires pre-defined entity and relation type sets; not schema-free
- Not designed as an end-to-end KG builder
- Smaller community than LangChain or LlamaIndex

**Licence / IP notes**
- Apache 2.0. Academic project from Sapienza University of Rome.

---

### Amazon Neptune + Bedrock GraphRAG

**Core features**
- Managed graph database service (property graphs via Gremlin/openCypher; RDF via SPARQL)
- Amazon Bedrock Knowledge Bases GraphRAG: fully managed pipeline from documents to KG with embeddings
- Automatic graph and embedding maintenance; no manual pipeline management
- Neptune ML: graph neural networks for node classification, link prediction, regression tasks
- NeptuneOpenCypherQAChain: natural language to openCypher query translation
- G.V() graph IDE: visual query builder and graph explorer for Neptune
- Scales to very large graphs; managed clustering and replication

**Differentiating features**
- Only fully managed end-to-end GraphRAG service in a major cloud (AWS) as of 2026
- Deep integration with AWS ecosystem (IAM, VPC, CloudWatch, SageMaker)
- Neptune Analytics: in-memory graph analytics engine for complex graph algorithms

**UX patterns**
- AWS Console for cluster management
- G.V() desktop/Marketplace IDE for visual exploration
- Bedrock console for Knowledge Base configuration (no-code)

**Integration points**
- AWS Bedrock (foundation models), SageMaker (ML), S3 (data sources)
- LangChain NeptuneGraph integration
- openCypher and SPARQL query interfaces

**Known gaps**
- Vendor lock-in to AWS; portability is limited
- Bedrock GraphRAG is opaque: limited control over extraction pipeline
- High cost at scale compared to self-hosted alternatives
- Limited entity resolution; deduplication not built-in

**Licence / IP notes**
- Commercial AWS service. No open-source component.

---

## Cross-Cutting Feature Themes

### Table-Stakes Features
- LLM-driven entity and relationship extraction from unstructured text (no manual annotation)
- Support for common document formats: PDF, DOCX, TXT, HTML, CSV
- Storage in a property graph database (Neo4j, FalkorDB, Memgraph, or Neptune)
- Natural language Q&A over the constructed graph (GraphRAG pattern)
- LLM provider flexibility (OpenAI, Anthropic, Google, open-source models)
- Chunk-to-entity provenance linking extracted facts to source sentences
- Vector embeddings stored alongside graph nodes for hybrid semantic retrieval
- Python SDK/library as the primary developer interface

### Differentiating Features
- **Temporal graph modelling** (Graphiti): tracking how facts change over time
- **Hierarchical community summarisation** (Microsoft GraphRAG): enabling global dataset-level questions
- **Entity resolution** (Graphiti, Diffbot): deduplicating references to the same real-world entity
- **Automated ontology generation** (FalkorDB): schema-first pipeline from documents to formal ontology
- **Fully managed cloud pipeline** (Amazon Bedrock GraphRAG): zero infrastructure for extraction and storage
- **Web-scale pre-built graph** (Diffbot): no ingestion pipeline; query an existing trillion-fact graph
- **MCP server integration** (Graphiti, Memento MCP): zero-code memory for AI agents
- **Standards compliance** (Ontotext GraphDB): full W3C RDF/OWL/SPARQL/SHACL conformance
- **High-speed lightweight extraction** (ReLiK): retrieve-read-link without large LLM calls

### Underserved Areas / Opportunities
- **Entity resolution at scale**: deduplication across large corpora is largely absent from open-source tools; users must build their own
- **Collaborative human-in-the-loop curation**: no tool provides a polished UI for teams to review, correct, and annotate extracted facts with corrections fed back as few-shot training examples
- **Temporal knowledge modelling for document corpora**: Graphiti provides this for agent memory, but no tool applies it to static document collections
- **Domain-adaptive extraction templates**: no tool ships pre-built extraction prompts tuned for legal, biomedical, financial, or cybersecurity domains
- **Incremental graph updates without full reprocessing**: most tools require full re-indexing when new documents arrive
- **Schema inference and automatic refinement**: most tools require the user to supply or accept unconstrained schemas; autonomous schema inference (as in ATLAS) is not yet available in production tools
- **Extraction quality visibility**: users cannot easily see which extractions are high vs. low confidence without building custom tooling
- **Non-developer access**: only Ontotext GraphDB and Amazon Bedrock offer genuinely non-technical interfaces

### AI-Augmentation Candidates
- **Entity resolution**: LLMs can compare candidate entity pairs and decide if they refer to the same real-world object — replacing brittle fuzzy-string-matching heuristics
- **Schema inference**: LLMs can propose and iteratively refine a graph schema by observing extracted entities across documents
- **Extraction quality scoring**: LLMs or specialised classifiers can assign confidence scores to extracted triples, enabling review prioritisation
- **Domain prompt engineering**: LLMs can generate and refine extraction prompts tuned to a specific domain given sample documents
- **Temporal fact resolution**: LLMs can identify conflicting facts about the same entity across documents and determine which is more recent or authoritative
- **Natural language graph querying**: generating Cypher, SPARQL, or GQL queries from free-text questions is a natural LLM task that all tools implement but few do well end-to-end

---

## Legal & IP Summary

All major open-source tools in this space are released under permissive licences: Apache 2.0 (Neo4j GraphRAG Python, FalkorDB GraphRAG SDK, ReLiK, Graphiti) or MIT (Microsoft GraphRAG, LangChain, LlamaIndex, spaCy). No patented features were identified across the open-source tools surveyed. Commercial products (Diffbot, Ontotext GraphDB Enterprise, Amazon Neptune, Zep cloud) are proprietary SaaS or managed services but do not restrict use of open standards (RDF, SPARQL, openCypher). W3C standards (RDF, OWL, SPARQL, SHACL) and ISO/IEC 39075 GQL are royalty-free open standards. An AI-native open-source knowledge graph builder can be built without licence compatibility concerns using any combination of the Apache 2.0 / MIT tooling surveyed.

---

## Recommended Feature Scope

**Must-have (MVP)**
- Multi-format document ingestion: PDF, DOCX, TXT, HTML, web URLs
- LLM-driven entity and relationship extraction with configurable schema constraints
- Storage in a property graph database (Neo4j or pluggable via adapter)
- Chunk-to-entity provenance: every node and edge linked to its source sentence and document
- Natural language Q&A using GraphRAG retrieval pattern
- Multi-LLM provider support (OpenAI, Anthropic, open-source via Ollama)
- Python SDK with a simple one-call `build_graph(docs, schema)` interface

**Should-have (v1.1)**
- Entity resolution and deduplication across documents (LLM-based candidate comparison)
- Relationship confidence scoring and a review UI for borderline extractions
- Automated schema inference with iterative refinement from observed entities
- Incremental document ingestion without full graph reprocessing
- Domain-specific extraction prompt templates (legal, biomedical, financial, cybersecurity)
- Interactive graph visualisation with node/edge filtering and cluster exploration

**Nice-to-have (backlog)**
- Temporal graph support: time-stamped entity and relationship facts with point-in-time queries
- MCP server for exposing the graph as AI agent memory
- Export to RDF/SPARQL-compatible formats for standards-compliant interoperability
- Community detection and hierarchical community summarisation (Microsoft GraphRAG pattern)
- Collaborative annotation UI: team review, correction, and few-shot feedback loop
- Ontology alignment: optional mapping to Wikidata, Schema.org, or domain ontologies
