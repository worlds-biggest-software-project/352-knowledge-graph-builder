# Standards & API Reference

> Project: Knowledge Graph Builder · Generated: 2026-05-04

## Industry Standards & Specifications

### ISO Standards

**ISO/IEC 39075:2024 — Information Technology: Database Languages — GQL**
- URL: https://www.iso.org/standard/76120.html
- The first ISO/IEC standard for property graph query languages, published April 2024. GQL (Graph Query Language) defines data structures and basic operations on property graphs, including creating, accessing, querying, maintaining, and controlling property graphs. Inspired by Cypher and SQL; openCypher is evolving to become GQL-conformant. Directly relevant to any knowledge graph tool that stores or queries property graphs.

**ISO/IEC 13249-7 — SQL/MM Spatial (Graph Extensions)**
- URL: https://www.iso.org/standard/67383.html
- Defines graph extensions within the SQL standard family. While less widely implemented than GQL, it establishes formal precedent for graph data within relational/SQL contexts. Relevant background for tools that bridge relational and graph storage.

**ISO 81346 — Industrial Reference Designation System**
- URL: https://www.iso.org/standard/82745.html
- An industrial standard being converted to OWL ontologies by the W3C Ontologies and Knowledge Graphs in Industry Community Group, enabling data interoperability in energy, aerospace, and manufacturing knowledge graphs. Relevant for enterprise knowledge graph deployments in industrial sectors.

---

### W3C & IETF Standards

**RDF 1.1 (Resource Description Framework)**
- URL: https://www.w3.org/RDF/
- The foundational W3C standard for representing information as subject-predicate-object triples. Forms the basis of semantic web knowledge graphs and triple stores. RDF 1.2 is in development with RDF-star and SPARQL-star extensions improving reification for representing facts about facts (provenance, confidence scores).

**RDFS — RDF Schema**
- URL: https://www.w3.org/TR/rdf-schema/
- Provides a vocabulary for describing RDF vocabularies, including classes, properties, and subclass/subproperty hierarchies. The foundational layer below OWL for defining ontologies used in knowledge graphs.

**OWL 2 (Web Ontology Language)**
- URL: https://www.w3.org/TR/owl2-overview/
- W3C standard for defining rich ontologies with formal semantics. OWL 2 enables reasoning: inferring implicit facts from declared class relationships, property restrictions, and equivalences. Used extensively in enterprise knowledge graphs for interoperability. The most expressive standard ontology language for knowledge graphs, based on description logics.

**SPARQL 1.1 (SPARQL Protocol and RDF Query Language)**
- URL: https://www.w3.org/TR/sparql11-query/
- The W3C standard query language for RDF graphs. SPARQL 1.1 includes query, update, federated query (SERVICE keyword), and protocol specifications. Essential for any tool targeting standards-compliant RDF/triple-store backends. SPARQL-star (under development) adds syntax for querying RDF-star triples.

**SHACL (Shapes Constraint Language)**
- URL: https://www.w3.org/TR/shacl/
- W3C Recommendation for validating RDF graphs against a set of conditions expressed as "shapes." SHACL is the primary standard for data quality assurance in knowledge graphs: ensuring ingested entities conform to schema constraints, catching extraction errors, and enforcing business rules. SHACL 1.2 (in development) extends rules capabilities. Directly applicable for validating LLM-extracted entities before committing to the graph.

**SKOS (Simple Knowledge Organisation System)**
- URL: https://www.w3.org/TR/skos-reference/
- W3C Recommendation for representing thesauri, taxonomies, and classification schemes in RDF. Widely used for representing domain vocabularies and ontology skeletons. Relevant for schema inference outputs that can be represented as SKOS concept schemes.

**JSON-LD 1.1**
- URL: https://www.w3.org/TR/json-ld11/
- W3C Recommendation for encoding linked data in JSON. Provides a context mapping JSON keys to RDF URIs, enabling graph data to be exchanged in a JSON-native format. Important for knowledge graph APIs targeting web developers unfamiliar with Turtle or N-Triples serialisation formats.

**RFC 7807 — Problem Details for HTTP APIs**
- URL: https://www.rfc-editor.org/rfc/rfc7807
- IETF standard for machine-readable error responses in HTTP APIs. Relevant for the REST API design of any knowledge graph builder service exposing ingestion and query endpoints.

**RFC 6749 / RFC 6750 — OAuth 2.0 and Bearer Token Usage**
- URL: https://www.rfc-editor.org/rfc/rfc6749
- The IETF standard for delegated authorisation. Relevant for knowledge graph APIs exposing multi-tenant access to graph data, where users authenticate to query or modify specific graph namespaces.

---

### Data Model & API Specifications

**openCypher**
- URL: https://opencypher.org/
- An open specification of the Cypher property graph query language, used by Neo4j, Memgraph, Amazon Neptune, and other graph databases. openCypher is converging towards ISO/IEC 39075 GQL conformance. The most widely implemented property graph query language; a knowledge graph builder targeting Neo4j or Memgraph should use Cypher for graph writes and queries.

**OpenAPI 3.1**
- URL: https://spec.openapis.org/oas/v3.1.0
- The de-facto standard for describing REST APIs, enabling automatic generation of client SDKs, documentation, and validation. Any knowledge graph builder exposing a REST ingestion or query API should provide an OpenAPI 3.1 specification.

**JSON Schema (Draft 2020-12)**
- URL: https://json-schema.org/specification
- Standard for validating JSON documents. Relevant for defining and validating the structured output format of LLM entity extraction (entity-relation triple JSON schemas) and for API request/response validation.

**GraphQL**
- URL: https://spec.graphql.org/
- A query language and runtime specification for APIs. Ontotext GraphDB and other graph platforms expose GraphQL endpoints as a developer-friendly alternative to SPARQL or Cypher. Relevant for knowledge graph builders targeting application developers who prefer GraphQL over graph-native query languages.

**RDF-star / SPARQL-star (W3C Community Group)**
- URL: https://w3c.github.io/rdf-star/
- An extension to RDF enabling triples to be subjects or objects of other triples, enabling compact representation of metadata about facts (provenance, confidence, timestamps). Directly relevant for attaching provenance and confidence scores to extracted knowledge graph triples without reification verbosity.

**Turtle / N-Triples / N-Quads**
- URL: https://www.w3.org/TR/turtle/
- W3C-standardised serialisation formats for RDF data. Turtle is human-readable; N-Triples and N-Quads are line-based formats suited for bulk import/export. A knowledge graph builder should support at least one of these formats for data portability.

---

### Security & Authentication Standards

**OAuth 2.0 (RFC 6749) and OpenID Connect 1.0**
- URLs: https://www.rfc-editor.org/rfc/rfc6749 · https://openid.net/connect/
- Industry standards for API authorisation and user authentication. Required for any multi-tenant cloud deployment of a knowledge graph builder where different teams or organisations access isolated graph namespaces.

**OWASP Top 10 (2021)**
- URL: https://owasp.org/www-project-top-ten/
- The foundational web application security risk list. Particularly relevant: A03 (Injection — Cypher/SPARQL injection via natural language queries), A01 (Broken Access Control — multi-tenant graph isolation), and A05 (Security Misconfiguration — exposing graph database credentials to frontends, a known issue in Neo4j LLM Graph Builder that was fixed in 2026).

**NIST SP 800-53 (Security and Privacy Controls)**
- URL: https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final
- US federal standard for security controls. Relevant for enterprise deployments of knowledge graph systems handling sensitive document content (HR, legal, financial). Particularly applicable to access control, audit logging, and data provenance requirements.

**GDPR (EU General Data Protection Regulation)**
- URL: https://gdpr-info.eu/
- EU regulation governing personal data. Highly relevant when knowledge graph builders extract personal information (People entities, relationships) from documents. Data provenance features (linking nodes to source documents) are directly applicable for GDPR right-to-erasure compliance: identifying and deleting all graph nodes derived from a specific document or data subject.

---

### MCP Server Specifications

**Model Context Protocol (MCP)**
- URL: https://spec.modelcontextprotocol.io/
- An open protocol (initiated by Anthropic) for connecting AI agents to external data and tool providers through a standardised server interface. Neo4j, FalkorDB/Graphiti, and Memgraph all now publish MCP servers allowing AI agents (Claude, Cursor, Copilot) to query and update knowledge graphs through natural language. An AI-native knowledge graph builder should expose an MCP server for agent integration. The 2025 H1 MCP roadmap includes OAuth 2.0 authentication, hierarchical agents, and real-time streaming.

---

## Similar Products — Developer Documentation & APIs

### Neo4j GraphRAG Python Package

- **Description:** The official Neo4j library for building GraphRAG applications. Provides `SimpleKGPipeline` for one-call knowledge graph construction from text/PDF, multiple retriever implementations (vector, hybrid, Cypher), and a composable Pipeline DAG for advanced workflows.
- **API Documentation:** https://neo4j.com/docs/neo4j-graphrag-python/current/api.html
- **SDKs/Libraries:** Python — https://github.com/neo4j/neo4j-graphrag-python · PyPI: `pip install neo4j-graphrag`
- **Developer Guide:** https://neo4j.com/docs/neo4j-graphrag-python/current/user_guide_kg_builder.html
- **Standards:** REST (Neo4j Bolt protocol), Cypher/openCypher, OpenAPI (Neo4j HTTP API)
- **Authentication:** Username/password, Neo4j Aura API keys, OAuth 2.0 (Aura Enterprise)

### Neo4j LLM Graph Builder (Web Application)

- **Description:** Web application (self-hosted or managed) for uploading documents and constructing a knowledge graph in Neo4j via LLM extraction. Includes graph visualisation, natural language Q&A, and community summary generation.
- **API Documentation:** https://neo4j.com/labs/genai-ecosystem/llm-graph-builder-features/
- **SDKs/Libraries:** https://github.com/neo4j-labs/llm-graph-builder (Docker Compose deployment)
- **Developer Guide:** https://neo4j.com/labs/genai-ecosystem/llm-graph-builder-deployment/
- **Standards:** REST/JSON (internal API), openCypher (Neo4j), LangChain integration
- **Authentication:** Neo4j database credentials; backend service isolates credentials from frontend

### Microsoft GraphRAG

- **Description:** Research-originated library implementing hierarchical community-based knowledge graph construction and retrieval. Produces entity/relationship graphs with community summaries enabling both local (entity-specific) and global (dataset-wide) natural language queries.
- **API Documentation:** https://microsoft.github.io/graphrag/
- **SDKs/Libraries:** Python — https://github.com/microsoft/graphrag · PyPI: `pip install graphrag`
- **Developer Guide:** https://microsoft.github.io/graphrag/get_started/
- **Standards:** REST (Azure OpenAI), Parquet (output format), Azure AI Search integration
- **Authentication:** Azure Active Directory / OpenAI API keys

### LangChain LLMGraphTransformer

- **Description:** LangChain component for converting documents into graph triples using any LangChain-compatible LLM. Supports schema-constrained and free-form extraction modes; integrates with Neo4j, Memgraph, and Apache AGE graph stores.
- **API Documentation:** https://python.langchain.com/docs/integrations/graphs/
- **SDKs/Libraries:** Python — `pip install langchain langchain-community`
- **Developer Guide:** https://blog.langchain.com/constructing-knowledge-graphs-from-text-using-openai-functions/
- **Standards:** REST/JSON (LLM providers), openCypher (Neo4j/Memgraph), LangChain LCEL
- **Authentication:** API keys per LLM provider; Neo4j bolt credentials

### LlamaIndex PropertyGraphIndex

- **Description:** LlamaIndex module for building labeled property graphs from documents using modular extractors and retrievers. Supports free-form and schema-constrained extraction; ensemble retrieval combining vector and graph-traversal strategies.
- **API Documentation:** https://docs.llamaindex.ai/en/stable/module_guides/indexing/lpg_index_guide/
- **SDKs/Libraries:** Python — `pip install llama-index llama-index-graph-stores-neo4j`
- **Developer Guide:** https://www.llamaindex.ai/blog/introducing-the-property-graph-index-a-powerful-new-way-to-build-knowledge-graphs-with-llms
- **Standards:** REST/JSON (LLM providers), openCypher (Neo4j/Memgraph), Gremlin (NebulaGraph)
- **Authentication:** API keys per LLM and graph database provider

### FalkorDB GraphRAG SDK

- **Description:** Python SDK for building ontology-first knowledge graphs from diverse document formats. Ranked #1 on GraphRAG-Bench benchmarks. Provides automated ontology generation, multi-LLM support, and native multi-tenancy.
- **API Documentation:** https://docs.falkordb.com/genai-tools/graphrag-sdk.html
- **SDKs/Libraries:** Python — https://github.com/FalkorDB/GraphRAG-SDK · PyPI: `pip install graphrag-sdk`
- **Developer Guide:** https://www.falkordb.com/graphrag-sdk/
- **Standards:** REST/JSON, FalkorDB query protocol (Cypher-compatible), OpenAI API format
- **Authentication:** API keys per LLM provider; FalkorDB connection credentials

### Graphiti (Zep)

- **Description:** Open-source temporal knowledge graph engine for AI agent memory. Ingests episodes (conversations, documents, structured data), resolves entities across episodes, supports point-in-time historical queries, and exposes an MCP server for zero-code agent integration.
- **API Documentation:** https://help.getzep.com/graphiti/getting-started/overview
- **SDKs/Libraries:** Python — https://github.com/getzep/graphiti · PyPI: `pip install graphiti-core`
- **Developer Guide:** https://help.getzep.com/graphiti/
- **Standards:** MCP (Model Context Protocol), REST/JSON (Zep cloud API), openCypher (Neo4j backend)
- **Authentication:** Zep API keys (cloud), Neo4j/FalkorDB credentials (self-hosted)

### Diffbot Natural Language API

- **Description:** Commercial REST API for extracting entities, relationships, facts, categories, and sentiment from unstructured text. Backed by a pre-built 10B-entity / 1T-fact knowledge graph continuously updated from web crawls.
- **API Documentation:** https://docs.diffbot.com/reference/extract-analyze
- **SDKs/Libraries:** REST API; community SDKs in Python, JavaScript
- **Developer Guide:** https://docs.diffbot.com/docs/tutorial-quickstart-with-knowledge-graph-search
- **Standards:** REST/JSON, DQL (Diffbot Query Language)
- **Authentication:** API token (Bearer token in HTTP header)

### Amazon Neptune + Bedrock Knowledge Bases GraphRAG

- **Description:** Fully managed AWS service combining Neptune (property graph and RDF databases) with Amazon Bedrock's GraphRAG capability for automatic knowledge graph construction and maintenance from S3 documents.
- **API Documentation:** https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-build-graphs.html
- **SDKs/Libraries:** AWS SDK for Python (Boto3), AWS SDK for JavaScript/Go/Java
- **Developer Guide:** https://aws.amazon.com/blogs/database/build-and-explore-knowledge-graphs-faster-with-amazon-neptune-using-graph-build-and-g-v-part-2/
- **Standards:** openCypher, Gremlin, SPARQL 1.1, REST/JSON (Neptune HTTP API), AWS SigV4 auth
- **Authentication:** AWS IAM (SigV4 request signing), VPC security groups

### Ontotext GraphDB / Graphwise

- **Description:** Enterprise-grade RDF triple store with OWL reasoning, SPARQL 1.1, SHACL validation, and a GraphQL interface. The Graphwise platform (Ontotext + Semantic Web Company merger) adds AI-driven taxonomy creation and KG-enhanced RAG.
- **API Documentation:** https://graphdb.ontotext.com/documentation/
- **SDKs/Libraries:** Java SDK, Python RDFLib integration; REST API
- **Developer Guide:** https://www.ontotext.com/products/graphdb/
- **Standards:** SPARQL 1.1, RDF 1.1, OWL 2, SHACL, JSON-LD, GraphQL
- **Authentication:** Username/password, LDAP/AD integration, token-based auth (Enterprise)

---

## Notes

**Emerging standards to watch:**
- **RDF 1.2 / SPARQL 1.2**: The W3C RDF Working Group is finalising RDF-star and SPARQL-star extensions. RDF-star enables attaching metadata (provenance, confidence, timestamps) to triples without verbose reification, making it highly relevant for LLM-extracted knowledge graphs where every fact carries a confidence score and source reference.
- **GQL evolution**: ISO/IEC 39075 GQL (2024) is still being adopted by graph database vendors. Neo4j, Amazon Neptune, and Microsoft Fabric are adding GQL support. openCypher will incrementally converge to GQL conformance. Tools built today on Cypher will remain relevant; GQL compatibility should be tracked.
- **MCP standardisation**: The Model Context Protocol is maturing rapidly. The 2025 roadmap includes OAuth 2.0 authentication, hierarchical agent support, and real-time streaming — all directly applicable to knowledge graph MCP servers. Tracking the MCP specification closely is advisable.
- **Property Graph Schema (PG-Schema)**: ISO SC32 is working on a schema language for property graphs (a SHACL equivalent for the property graph world). Early drafts exist; production readiness is 2–3 years out. Relevant for future data validation in non-RDF knowledge graphs.
