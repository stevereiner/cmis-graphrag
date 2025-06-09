<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

What libraries support building knowledge graphs, creating vector embeddings, performing vector assisted RAG queries, and performing vector with graph assisted GraphRAG queries?  1. Consider  Neo4j neo4j-graphrag python package (https://neo4j.com/docs/neo4j-graphrag-python/current/  and its doc https://github.com/neo4j/neo4j-graphrag-python Has support for vectors in Neo4j, Weaviate, Pinecone, and Qdrant. KG building with SimpleKGPipeline or support for custom pipelines https://neo4j.com/docs/neo4j-graphrag-python/current/user_guide_kg_builder.html), 2. LangChain,  3. LlamaIndex, 4. Spring AI.  5. LangChain.js, 6. LangChain4j, 7. LangChain.dart . 8. What about others?    9. Create a a table with all libraries:  a. In what specific vector databases, graph databases, and search databases (Elasticsearch, OpenSearch) can it create vectors in (do a complete  a though check) b. List all specific graph databases the library can build  knowledge graphs in. c. What class does the KG building. d. What class does the GraphRAG search.

(Steve: note used Perplexity Pro with Claude 4.0 Sonnet selected for rewrite)

Based on the search results, here's a comprehensive analysis of libraries that support building knowledge graphs, creating vector embeddings, and performing GraphRAG queries:

## Major Libraries for GraphRAG

### **Neo4j GraphRAG Python Package**

The Neo4j GraphRAG Python package provides comprehensive GraphRAG capabilities with support for knowledge graph creation through pipelines that extract entities from unstructured text, generate embeddings, and create graphs in Neo4j[^2]. It includes multiple retrievers for graph search, vector search, and integration with vector databases[^2].

### **LangChain**

LangChain offers extensive GraphRAG capabilities with the `GraphCypherQAChain` for generating Cypher queries and retrieving data from graph databases[^15]. It supports both vector similarity search and graph query bifurcation for property graphs[^15].

### **LlamaIndex**

LlamaIndex provides the **Property Graph Index**, which enables richer modeling, storage, and querying of knowledge graphs compared to traditional knowledge triples[^9]. It supports labeled property graphs with metadata and hybrid search capabilities[^9].

### **Spring AI**

Spring AI integrates with vector databases and provides standardized interfaces for working with vector stores[^11]. It supports knowledge graph integration through specialized query languages like Cypher[^12].

## Comprehensive Comparison Table

| Library | Vector Database Support | Graph Database Support | KG Building Class | GraphRAG Search Class |
| :-- | :-- | :-- | :-- | :-- |
| **Neo4j GraphRAG Python** | Neo4j, Weaviate, Pinecone, Qdrant[^2] | Neo4j | `SimpleKGPipeline`[^4] | `VectorRetriever`, `VectorCypherRetriever`[^2] |
| **LangChain** | Chroma, FAISS, Pinecone, Weaviate, Elasticsearch, many others[^13] | Neo4j, others via connectors[^6] | Custom extractors | `GraphCypherQAChain`[^15] |
| **LlamaIndex** | 50+ integrations including Chroma, FAISS, Pinecone, Weaviate[^8] | Neo4j, others[^9] | `SchemaLLMPathExtractor`, `SimpleLLMPathExtractor`[^9] | `PropertyGraphIndex`, `VectorContextRetriever`[^9] |
| **Spring AI** | Multiple via standard interface[^11] | Neo4j (via Cypher)[^12] | Custom implementations | Custom query engines[^12] |
| **LangChain.js** | Memory, Chroma, FAISS, others[^13] | Neo4j[^14] | Custom extractors[^14] | Similar to Python version |
| **LangChain4j** | Neo4j (embedded)[^16] | Neo4j[^16] | Custom implementations | `Neo4jText2CypherRetriever`[^16] |

## Detailed Vector Database Support

### **Neo4j GraphRAG Python**

- **Native Support**: Neo4j vector indexes[^21]
- **External Vector Stores**: Weaviate, Pinecone, Qdrant[^2]
- **Search Capabilities**: Cosine similarity, Euclidean distance[^21]


### **LangChain**

- **Comprehensive Support**: Over 40 vector store integrations including Chroma, FAISS, Pinecone, Weaviate, Elasticsearch, OpenSearch[^13]
- **Standard Interface**: Unified API across all vector stores with methods like `addDocuments`, `similaritySearch`[^13]


### **LlamaIndex**

- **Extensive Integrations**: 50+ vector store implementations[^8]
- **Notable Stores**: Chroma, FAISS, Pinecone, Weaviate, DeepLake[^8]
- **Flexibility**: Custom vector store implementations supported[^8]


### **Spring AI**

- **Standard Interface**: `VectorStore` abstraction for multiple backends[^11]
- **Integration Examples**: Works with various vector databases through standardized API[^11]


## Graph Database Support Analysis

### **Neo4j-Focused Libraries**

Most libraries primarily support **Neo4j** as their main graph database due to its popularity and Cypher query language support[^2][^6][^9][^12][^15][^16].

### **Multi-Database Support**

- **LlamaIndex**: Supports multiple graph stores through `PropertyGraphStore` abstraction, including in-memory, disk-based, and Neo4j[^9]
- **LangChain**: Primarily Neo4j but extensible architecture allows custom graph database connectors[^6]


## Knowledge Graph Building Classes

### **Neo4j GraphRAG Python**

- **Primary**: `SimpleKGPipeline` - simplifies knowledge graph building from text documents[^4]
- **Custom**: Support for custom pipeline implementations[^2]


### **LlamaIndex**

- **Schema-Guided**: `SchemaLLMPathExtractor` - extracts entities based on predefined schemas[^9]
- **Free-Form**: `SimpleLLMPathExtractor` - infers entities and relationships directly[^9]
- **Implicit**: `ImplicitPathExtractor` - uses node relationships[^9]


### **LangChain**

- **Flexible**: Custom extractor implementations for different use cases[^14]
- **Integration**: Works with various LLMs for entity extraction[^15]


## GraphRAG Search Classes

### **Neo4j GraphRAG Python**

- **Vector Search**: `VectorRetriever` for similarity-based retrieval[^2]
- **Hybrid**: `VectorCypherRetriever` combining vector and graph traversal[^2]
- **Full Pipeline**: `GraphRAG` class for end-to-end workflows[^3]


### **LlamaIndex**

- **Multi-Modal**: `VectorContextRetriever`, `LLMSynonymRetriever`, `CypherTemplateRetriever`[^9]
- **Hybrid Search**: Combines vector similarity with graph structure[^9]


### **LangChain**

- **Primary**: `GraphCypherQAChain` for Cypher query generation and execution[^15]
- **Workflow**: `StateGraph` for complex multi-step GraphRAG workflows[^15]


## Additional Notable Libraries

### **Specialized KG Libraries**

- **PyKEEN**: Knowledge graph embeddings with PyTorch[^19]
- **AmpliGraph**: Machine learning models for knowledge graph embeddings[^19]
- **Pykg2vec**: Knowledge graph embedding algorithms with TensorFlow/PyTorch[^19]

These specialized libraries focus specifically on knowledge graph embeddings but may require additional integration work for full GraphRAG pipelines compared to the comprehensive frameworks listed above.

<div style="text-align: center">⁂</div>

[^1]: neo4

[^2]: https://neo4j.com/labs/genai-ecosystem/graphrag-python/

[^3]: https://neo4j.com/blog/developer/get-started-graphrag-python-package/

[^4]: https://www.i-programmer.info/news/105-artificial-intelligence/18050-graphrag-with-python-and-neoj.html

[^5]: https://www.pluralsight.com/resources/blog/ai-and-data/langchain-local-vector-database-tutorial

[^6]: https://python.langchain.com/docs/tutorials/graph/

[^7]: https://github.com/ksachdeva/langchain-graphrag/blob/main/README.md

[^8]: https://docs.llamaindex.ai/en/stable/community/integrations/vector_stores/

[^9]: https://www.llamaindex.ai/blog/introducing-the-property-graph-index-a-powerful-new-way-to-build-knowledge-graphs-with-llms

[^10]: https://docs.llamaindex.ai/en/stable/examples/cookbooks/GraphRAG_v1/

[^11]: https://docs.spring.io/spring-ai/reference/api/vectordbs.html

[^12]: https://www.linkedin.com/pulse/integrating-spring-ai-knowledge-graphs-varaisys-rtatc

[^13]: https://js.langchain.com/docs/concepts/vectorstores/

[^14]: https://js.langchain.com/docs/how_to/graph_constructing/

[^15]: https://neo4j.com/blog/developer/neo4j-graphrag-workflow-langchain-langgraph/

[^16]: https://neo4j.com/blog/developer/langchain4j-graphrag-vector-stores-retrievers/

[^17]: https://neo4j.com/blog/news/graphrag-python-package/

[^18]: https://github.com/Danielskry/Awesome-RAG

[^19]: https://memgraph.com/blog/best-python-packages-tools-for-knowledge-graphs

[^20]: https://www.youtube.com/watch?v=4Vnf59IqI64

[^21]: https://neo4j.com/docs/neo4j-graphrag-python/current/

[^22]: https://neo4j.com/labs/genai-ecosystem/llamaindex/

[^23]: https://piotrminkowski.com/2025/02/24/using-rag-and-vector-store-with-spring-ai/

[^24]: https://qdrant.tech/documentation/examples/graphrag-qdrant-neo4j/

[^25]: https://neo4j.com/docs/neo4j-graphrag-python/current/user_guide_rag.html

[^26]: https://www.falkordb.com/blog/how-to-build-a-knowledge-graph/

[^27]: https://qdrant.tech/documentation/frameworks/neo4j-graphrag/

[^28]: https://github.com/neo4j/neo4j-graphrag-python

[^29]: https://neo4j.com/videos/graphrag-python-package-accelerating-genai-with-knowledge-graphs-graphdatabase/

[^30]: https://python.langchain.com/docs/integrations/vectorstores/

[^31]: https://js.langchain.com/docs/integrations/vectorstores/

[^32]: https://python.langchain.com/docs/concepts/vectorstores/

[^33]: https://www.reddit.com/r/LangChain/comments/1bf3kjs/can_any_database_be_a_vector_database/

[^34]: https://docs.llamaindex.ai/en/stable/community/faq/vector_database/

[^35]: https://docs.llamaindex.ai/en/stable/module_guides/storing/vector_stores/

[^36]: https://www.reddit.com/r/LlamaIndex/comments/17ydv00/llama_index_vs_vector_databases/

[^37]: https://www.googlecloudcommunity.com/gc/AI-ML/No-support-for-Vector-Search-in-llama-index/m-p/666707

[^38]: https://spring.io/projects/spring-ai

[^39]: https://www.elastic.co/search-labs/blog/spring-ai-elasticsearch-application

[^40]: https://github.com/JMHReif/vector-graph-rag

[^41]: https://blogs.oracle.com/developers/post/spring-ai-10-ga-released-with-oracle-vector-database-support

[^42]: https://www.reddit.com/r/LocalLLaMA/comments/1chmfib/anyone_using_knowledge_graphs_in_their_rag/

[^43]: https://www.databricks.com/blog/building-improving-and-deploying-knowledge-graph-rag-systems-databricks

[^44]: https://www.pinecone.io/learn/vectors-and-graphs-better-together/

[^45]: https://graphacademy.neo4j.com/courses/genai-graphrag-python/

[^46]: https://neo4j.com/blog/developer/graph-traversal-graphrag-python-package/

[^47]: https://graphacademy.neo4j.com/courses/llm-knowledge-graph-construction/

[^48]: https://devblogs.microsoft.com/azure-sql/langchain-with-sqlvectorstore-example/

[^49]: https://blog.langchain.dev/enhancing-rag-based-applications-accuracy-by-constructing-and-leveraging-knowledge-graphs/

[^50]: https://milvus.io/ai-quick-reference/how-do-i-integrate-llamaindex-with-a-vector-database

[^51]: https://milvus.io/ai-quick-reference/how-can-llamaindex-be-used-for-building-knowledge-graphs

[^52]: https://www.youtube.com/watch?v=yPu-WV_00Tk

[^53]: https://neo4j.com/developer/genai-ecosystem/spring-ai/

[^54]: https://js.langchain.com/docs/integrations/vectorstores/pgvector/

[^55]: https://supabase.com/docs/guides/ai/langchain

[^56]: https://blogs.oracle.com/database/post/using-javascript-and-langchain-for-retrieval-augmented-generation-rag-with-oracle-graph

[^57]: https://microsoft.github.io/graphrag/query/overview/

