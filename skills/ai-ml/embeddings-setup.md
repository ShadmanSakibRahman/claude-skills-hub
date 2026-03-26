---
description: Set up vector embeddings and similarity search with embedding models, vector databases, and indexing strategies
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in vector embeddings and similarity search systems. When setting up embeddings infrastructure, follow these steps:

1. **Choose the embedding model based on the use case**:
   - **Text embeddings (API)**: OpenAI `text-embedding-3-small` (1536d, cost-effective), `text-embedding-3-large` (3072d, highest quality), Cohere `embed-english-v3.0` (1024d, supports search/clustering input types).
   - **Text embeddings (open source)**: `sentence-transformers/all-MiniLM-L6-v2` (384d, fast), `BAAI/bge-large-en-v1.5` (1024d, high quality), `intfloat/e5-large-v2` (1024d).
   - **Image embeddings**: OpenAI CLIP (`openai/clip-vit-base-patch32`), SigLIP for image-text matching.
   - **Multimodal**: CLIP variants for joint image-text embeddings in the same vector space.
   - Consider: dimension size (affects storage/speed), max input length, quality on your domain, and cost.

2. **Generate embeddings**:
   - Preprocess text: clean, normalize, and truncate to model's max token limit.
   - For OpenAI: `client.embeddings.create(model="text-embedding-3-small", input=texts)`. Batch up to 2048 inputs per call.
   - For sentence-transformers: `model.encode(texts, batch_size=32, show_progress_bar=True, normalize_embeddings=True)`.
   - Normalize embeddings to unit length for cosine similarity (many models do this by default).
   - Cache embeddings to avoid redundant computation — hash input text as the cache key.

3. **Select and configure a vector database**:
   - **Pinecone**: Fully managed, serverless option available. Create index: `pinecone.create_index(name, dimension, metric="cosine", spec=ServerlessSpec(...))`.
   - **Chroma**: Lightweight, embedded. `chromadb.PersistentClient(path="./chroma_db")`. Good for prototyping and small-medium datasets.
   - **pgvector**: PostgreSQL extension. `CREATE EXTENSION vector; ALTER TABLE items ADD COLUMN embedding vector(1536);`. Best when you already use Postgres.
   - **Qdrant**: High-performance, supports filtering. Docker or cloud deployment.
   - **Weaviate**: GraphQL API, supports hybrid search natively.
   - Choose based on: dataset size, query latency requirements, filtering needs, managed vs self-hosted preference.

4. **Indexing strategies**:
   - **HNSW (Hierarchical Navigable Small World)**: Default for most vector DBs. Best for datasets up to ~10M vectors. Parameters: `M` (connections per node, default 16), `ef_construction` (build quality, default 200). Higher values = better recall, more memory.
   - **IVF (Inverted File Index)**: Better for very large datasets (10M+). Partitions vectors into `nlist` clusters. At query time, searches `nprobe` nearest clusters. Trade-off: more clusters = faster search, lower recall.
   - **Product Quantization (PQ)**: Compresses vectors for memory savings. Combine with IVF for large-scale deployments. Accept ~5-10% recall loss for 4-8x memory reduction.
   - **Flat/brute-force**: Exact search, best recall. Only viable for <100K vectors.
   - Start with HNSW defaults, then tune based on benchmarks.

5. **Batch processing and ingestion**:
   - Process documents in batches of 100-500 for embedding generation.
   - Upsert to the vector database in batches of 100-1000.
   - Implement retry logic with exponential backoff for API rate limits.
   - Track progress and support resumption for large ingestion jobs.
   - Use async/parallel processing to speed up ingestion: `asyncio.gather()` for API calls, multiprocessing for local models.

6. **Build the semantic search API**:
   - Accept a query string and optional filters (metadata filters, date range, category).
   - Embed the query using the same model and preprocessing as the documents.
   - Search the vector database with top-k (default 10) and similarity threshold (e.g., cosine > 0.7).
   - Return results with: matched text, similarity score, and metadata.
   - Implement pagination for browsing results beyond top-k.

7. **Optimize search quality**:
   - Use query expansion: generate multiple query variations and merge results.
   - Implement hybrid search: combine vector similarity with BM25 keyword search using Reciprocal Rank Fusion.
   - Add a re-ranking step with a cross-encoder for the top 20-50 candidates.
   - Filter by metadata before or after vector search depending on the database's capabilities.
   - A/B test retrieval configurations with a labeled relevance dataset.

8. **Monitor and maintain**:
   - Track search latency (P50, P95, P99), query volume, and result relevance.
   - Set up index rebuilding for databases that need it (IVF after significant data changes).
   - Monitor embedding model versioning — re-embed all documents if you change models.
   - Implement a feedback loop: let users flag irrelevant results to improve the system.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
