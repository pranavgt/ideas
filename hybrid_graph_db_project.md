# HybridGraphDB: Multi-Model Query Routing with HNSW Acceleration

## Overview

**HybridGraphDB** is a demonstration of how graph-based approximate nearest neighbor (ANN) search — specifically **Hierarchical Navigable Small World (HNSW)** graphs — can be used to route and optimize queries across multi-model databases. The project explores scalable, efficient, and privacy-aware approaches to querying hybrid data stores that include structured (SQL), graph, document, and vector components.

Inspired by [Malkov & Yashunin's 2016 paper on HNSW](https://arxiv.org/abs/1603.09320), this project repurposes HNSW’s logarithmic complexity and navigable layer design to build a smart meta-query layer capable of quickly identifying relevant data points and choosing the optimal query path — minimizing overhead and maximizing response relevance.

## Motivation

In many AI and analytics applications, data lives across multiple storage models:

- Structured customer or transaction data in SQL
- Relationships in graphs (social networks, supply chains)
- Descriptive text in documents or logs
- Embedding-based similarity in vector stores
- Metrics and trends in time-series data

Traditional query systems struggle to unify these models efficiently. HybridGraphDB demonstrates how HNSW can serve as a *routing index*, enabling fast similarity lookups and guiding downstream engines (SQL, document search, graph traversal) with **context-aware, right-sized searches**.

## Key Features

- ⚡ **HNSW-Powered Search Layer**: Uses `hnswlib` to index hybrid data vectors
- 🌐 **Multi-Model Query Routing**: Routes queries to SQL, document, or graph systems based on proximity results
- 🧠 **Hybrid Embedding Indexing**: Encodes rows, documents, and graph node metadata into shared vector space
- 🧮 **Efficient Join Avoidance**: Uses graph distances to bypass expensive relational joins
- 🧪 **Local-first Inference**: Demonstrates how lightweight vector-first querying can serve AGI/LLM microtasks privately

## Architecture

```
               +----------------------------+
               |    Query/API Entry Point   |
               +-------------+--------------+
                             |
                             v
                   +--------------------+
                   |   HNSW Indexer     |  <- Embedding similarity search
                   +----------+---------+
                              |
              +---------------+---------------+
              |               |               |
              v               v               v
        +----------+     +----------+     +----------+
        | SQL Core |     | Graph DB |     | Doc Store|
        +----------+     +----------+     +----------+
              \              |               /
               \_____________|_____________/
                            |
                            v
                  +---------------------+
                  | Unified Result Set  |
                  +---------------------+
```

## Technologies

- **HNSW**: [`hnswlib`](https://github.com/nmslib/hnswlib) for proximity graph indexing
- **Multi-Model Database**: [`ArcadeDB`](https://github.com/ArcadeData/arcadedb) for SQL + Graph + Document + Search
- **Embeddings**: OpenAI / Sentence Transformers
- **API**: FastAPI (Python) or Express.js (Node.js)
- **Frontend (optional)**: React + Cytoscape/Vis.js

## Demo Use Case

> "Find all customers within 2 hops of a flagged transaction, whose text logs and purchase patterns resemble known fraud cases."

This use case blends:

- Graph queries (neighbor hops)
- Embedding similarity (fraud log patterns)
- SQL joins (customer metadata)
- Time-based filtering (recent transactions)

HybridGraphDB efficiently handles this by using HNSW to prefilter relevant regions before dispatching precise model-specific queries.

## Project Structure

```
HybridGraphDB/
├── engine/                # Core HNSW + routing logic
├── dataloaders/          # Sample hybrid data ingestion scripts
├── query_router.py       # Main routing engine
├── adapters/             # SQL, graph, and doc connectors
├── benchmarks/           # Performance comparison scripts
├── demo/                 # Streamlit or notebook demo UI
├── docs/                 # Diagrams, README assets, theory notes
└── README.md
```

## Goals

- ✅ Demonstrate ANN + graph hybrid search patterns
- ✅ Showcase how HNSW can optimize coarse search across data models
- ✅ Explore composable infra for edge-scale AI agents

## Future Extensions

- Docker-based microservice deployment
- Real-time streaming data index updates
- Integration with private LLM agents for downstream generation

## References

- Malkov, Yu. A., & Yashunin, D. A. (2016). *Efficient and robust approximate nearest neighbor search using Hierarchical Navigable Small World graphs*. [arXiv:1603.09320](https://arxiv.org/abs/1603.09320)
- ArcadeDB: [https://arcadedb.com/](https://arcadedb.com/)
- hnswlib: [https://github.com/nmslib/hnswlib](https://github.com/nmslib/hnswlib)

---

Want to collaborate or try building this? Fork the repo or reach out — always up for designing lean, intelligent systems that scale smartly — not massively.

