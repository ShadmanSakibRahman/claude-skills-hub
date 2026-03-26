---
description: Set up Retrieval Augmented Generation with document chunking, embeddings, vector stores, and citation tracking
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in building RAG (Retrieval Augmented Generation) systems. When setting up or improving a RAG pipeline, follow these steps:

1. **Document ingestion and preprocessing**:
   - Support multiple formats: PDF (use `pypdf` or `pdfplumber`), DOCX (`python-docx`), HTML (`BeautifulSoup`), Markdown, plain text.
   - Extract text while preserving structure (headings, tables, lists).
   - Clean the text: remove headers/footers, page numbers, excessive whitespace, and boilerplate.
   - Store source metadata: filename, page number, section heading, URL, last modified date.

2. **Chunking strategy**:
   - **Recursive character splitting**: Split by paragraph, then sentence, then character. Default chunk size 500-1000 tokens with 100-200 token overlap.
   - **Semantic chunking**: Split at topic boundaries using embedding similarity between consecutive sentences.
   - **Document-structure-aware**: Split by headings/sections to keep related content together.
   - Keep chunks self-contained — each chunk should make sense without context.
   - Prepend section headings or document title to each chunk for context.
   - Test different chunk sizes against your retrieval quality — smaller chunks are more precise, larger chunks provide more context.

3. **Generate embeddings**:
   - **OpenAI**: `text-embedding-3-small` (cost-effective) or `text-embedding-3-large` (higher quality). Dimension: 1536 or configurable.
   - **Cohere**: `embed-english-v3.0` with `input_type="search_document"` for indexing, `"search_query"` for queries.
   - **Open source**: `sentence-transformers` with models like `all-MiniLM-L6-v2` (fast) or `bge-large-en-v1.5` (quality).
   - Batch embedding calls (e.g., 100 chunks per request) to reduce API overhead.
   - Cache embeddings — do not re-embed unchanged documents.

4. **Set up the vector store**:
   - **Pinecone**: Managed service, serverless or pod-based. Create index with correct dimension and metric (cosine).
   - **Chroma**: Local/embedded, great for development. Persistent storage with `chromadb.PersistentClient`.
   - **pgvector**: PostgreSQL extension — good when you already use Postgres. Create index with `ivfflat` or `hnsw`.
   - Store chunk text, embedding, and metadata (source, page, section) together.
   - Create appropriate indexes for your query patterns.

5. **Implement retrieval**:
   - Embed the user query with the same model used for documents.
   - Retrieve top-k results (start with k=5, tune based on quality).
   - Apply metadata filters (e.g., by document type, date range, or access level).
   - **Hybrid search**: Combine vector similarity with keyword search (BM25) for better recall. Use Reciprocal Rank Fusion to merge results.
   - **Re-ranking**: Use a cross-encoder model (e.g., Cohere Rerank, `cross-encoder/ms-marco-MiniLM-L-6-v2`) to re-score top results for higher precision.

6. **Context injection into the LLM prompt**:
   - Format retrieved chunks clearly with source attribution: `[Source: document.pdf, page 3]`.
   - Place context before the question in the prompt.
   - Instruct the LLM: "Answer based only on the provided context. If the context doesn't contain the answer, say so."
   - Limit total context to fit within the model's context window with room for the response.

7. **Implement citation tracking**:
   - Assign a unique ID to each chunk.
   - Ask the LLM to reference chunk IDs in its response: "Cite your sources using [1], [2], etc."
   - Map citations back to original documents, pages, and sections.
   - Return source metadata alongside the answer for verification.

8. **Evaluate and iterate**:
   - Measure retrieval quality: Mean Reciprocal Rank (MRR), Recall@k, Precision@k.
   - Measure answer quality: faithfulness (grounded in context), relevance, completeness.
   - Use RAGAS or similar frameworks for automated evaluation.
   - Test with questions that require single-chunk answers and multi-chunk synthesis.
   - Log queries, retrieved chunks, and answers for ongoing quality monitoring.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
