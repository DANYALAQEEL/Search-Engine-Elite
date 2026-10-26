# 🔍 Search Engine Elite // Information Retrieval Architecture

[![Status](https://img.shields.io/badge/Status-Production%20Active-10B981?style=for-the-badge&logo=statuspage)](https://github.com/DANYALAQEEL)
[![License](https://img.shields.io/badge/Access-Proprietary%20%2F%20NDA-0A0A0A?style=for-the-badge&logo=lock&labelColor=0A0A0A&color=10B981)](https://github.com/DANYALAQEEL)
[![Focus](https://img.shields.io/badge/Focus-Academic%20Paper%20Indexing-blue?style=for-the-badge)](https://github.com/DANYALAQEEL)

> [!NOTE]
> **PROPRIETARY ARCHITECTURE // SOURCE UNDER NON-DISCLOSURE AGREEMENT (NDA)**  
> This repository serves as the public technical documentation and architectural whitepaper for the Search Engine 2.0 and arXiv scientific indexing ecosystem. Full source code is maintained in a private production repository.

---

## 🏛️ Ingestion & Indexing Pipeline Topology

```mermaid
flowchart LR
    Crawler["arXiv OAI-PMH Harvester"] --> Filter["Metadata & Abstract Normalizer"]
    Filter --> Tokenizer["BM25 Stemmer & Lemmatizer"]
    Tokenizer --> Vectorizer["Dense Embedding Generator"]
    
    subgraph Hybrid Search Engine
        Tokenizer --> InvertedIndex[("Inverted BM25 Index")]
        Vectorizer --> VectorStore[("HNSW Vector Index")]
    end
    
    Query["User Search Query"] --> HybridRanker["Hybrid Reciprocal Rank Fusion (RRF)"]
    InvertedIndex --> HybridRanker
    VectorStore --> HybridRanker
    HybridRanker --> Results["Ranked Technical Citations"]
```

---

## 🛠️ Technical Specifications & Algorithms

- **Corpus Target:** 117,000+ scientific preprints and technical publications from arXiv and open access repositories
- **Ranking Function:** Hybrid RRF (Reciprocal Rank Fusion) combining dense vector similarity with sparse BM25 token frequencies
- **Indexing Structure:** Memory-mapped inverted posting lists with delta-encoding compression
- **Query Latency:** Sub-80ms median response time for boolean and vector similarity queries

---

## 📑 System Design Overview

1. **Crawler Resiliency:** Implements exponential backoff rate-limiting adhering strictly to arXiv API terms of service.
2. **Deduplication:** MinHash LSH (Locality-Sensitive Hashing) applied to preprint versions to eliminate duplicate index entries.
3. **Continuous Deployment:** Containerized microservice deployable with isolated worker pods.

---
*Maintained by [Danyal Aqeel](https://github.com/DANYALAQEEL) // Systems & Search Architecture*
