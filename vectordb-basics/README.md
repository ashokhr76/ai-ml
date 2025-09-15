# ai-ml
# What is Vector DB ? 

Vector DB is specialized type of database designed to store and search vector embeddings -- numerical representation of data (text, image, audio, etc..) that capture their semantic meaning.
Instead of matching exact words or values like traditional databases, Vactor DB finds items that are most similar in meaning to a given query by comparing their positions in a high-dimensional vector space

# How it works ? 
    1) Embedding Generation - Data (e.g.. A sentence or image) is converted into a vector using models like BERT, CLIP or Word2Vec.
    2) Indexing - These vectors are stored in specialized indexes optimized for high-dimensional search, such as HNSW graphs or IVF indexes
    3) Similarity Search - When you Query, your input is also converted into a vector, and the database finds the nearest neighbor based on distance metrics like cosine similarity or Euclidean distance
    4) Result Ranking - Matches are ranked by similarity score, often combined with filters (e.g data, category) for precision

# Challanges with Using Only a Similarity Search Library : if you rely solely on a library like FAISS or Annoy without VectorDB, you may face : 

    1) Scalability Limits : Hard to manage millions of vectors efficiency
    2) No Persistency : Many libraries store vectors in memory; you must handle saving/loading yourself
    3) Complex Filtering : Combining vector similarity with metadata filters is cumbersome
    4) Operational overhead : You must build API's to handle replication, sharding and backup manually
    5) Real-time updates : Inserting, deleting or updating vector dynamically can be slow or complex

# How VectorDB Solves these Problems : Vector databases like Chroma, Pinecorn, Milvus, Qdrant integrates similarity search with database-grade features:

    1) Persistency & Durability - Data is stored on disk with automatic backup
    2) Hybrid Search - Combine vector similarity with keyword or metadata filters in one query
    3) Distributed & Scalable - Handle billions of vectors with horizontal scaling
    4) Real-time indexing - Insert or update vectors instantly without full re-indexing.
    5) APIs & Integrations - ready to use REST/gRPC APIs, SDKs and connectors for frameworks like Langchain.
    6) Performance Optimization - Built in Approximate nearest neighbor (ANN) algorithms tuned for speed and accuracy

Example: If you’re building a semantic search for a product catalog:
    • FAISS‑only: You’d need to manage storage, metadata filtering, and scaling yourself.
    • VectorDB: You just send your query vector + filters, and it returns relevant products in milliseconds — even if the exact keywords don’t match.

# Architecture of VectorDB : purpose-built to store and search high-dimensional embeddings efficiently, and its architecture is quite different from traditional relational NoSQL database.

# Core Architectural Components

    1) Storage Layer
        a. Vector data store - Holds the actual high-dimensional vectors (e.g - 768 dimensional embeddings from BERT)
            i. Can be in-memory for speed or on-disk for persistence and large datsets.
            ii. Often uses compression to reduce storage footprint
        b. Metadata Storage - Stores extra info linked to each vector (IDs, timestamps, tags, categories)
            i. Enables hybrid search (vector similarity + metadata filters)
        c. Index data storage - Persists the specialized index structures used for fast retrieval
    2) Indexing Layer
        a. Purpose - Avoid brute-force comparison with every vector by narrowing the search space
        b. Common ANN (Approximate Nearest Neighbor) Index Types
            i. HNSW (Hierarchical Navigable Small World graphs) - Graph-based, very fast for large datasets
            ii. IVF (Inverted File Index) - Clusters vectors input partitions for faster lookup
            iii. LSH (Locality Sensitive Hashing) - Hashes similar vectors into the same buckets.
        c. Index Management - Handles updates, rebuilds and optimization as new vectors are added or removed.
    3) Query Processing Layer
        a. Vectorization - incoming queries (text, image, etc..) are converted into vectors using the same embedding model as the storage data
        b. Similarity Search - Finds the nearest neighbors using metrics like:
            i. Cosine similarity - measures angles between vectors (good for semantic similarity)
            ii. Euclidean distance - measures straight-line distance (good for magnitude-sensitive data)
        c. Filtering & Ranking - combines similarity scores with metadata filters, then ranks results
    4) Scalability & Reliability Layer
        a. Sharding - splits data across multiple nodes for horizontal scaling
        b. Replication - keeps copies of data for fault tolerance
        c. Load Balancing - distributes queries evenly across nodes
        d. Caching - stores recent results or hot vectors in memory for speed

# High‑Level Flow
    • Data Ingestion → Embedding model converts raw data into vectors.
    • Storage & Indexing → Vectors + metadata stored; ANN index built.
    • Query → User input vectorized; ANN search finds nearest neighbors.
    • Filtering & Ranking → Apply metadata filters; rank by similarity score.
    • Results → Return top‑K most relevant items.


#in short: 
A VectorDB is essentially three engines working together — a storage engine for vectors + metadata, an indexing engine for fast similarity search, and a query engine for combining semantic relevance with filters. The rest of the architecture ensures it’s scalable, reliable, and easy to integrate into AI pipelines

Vector Databases
Entension : Add-Ons to existing databases

1) redis
2) cassandra
3) mongoDB
4) elasticsearch
5) PgVector

Purpose built vectordb

1) Pinecone
2) Chroma
3) LanceDB
4) Weaviate
5) Drant
6) Milvus
7) Vespa
8) Vald
9) Zilliz

