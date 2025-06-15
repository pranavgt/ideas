# ReguGraph: Graph-Augmented Compliance Rules Engine

## ⚙️ Overview
**ReguGraph** is a Java-based compliance and risk analysis engine that combines traditional SQL databases with a graph-augmented, proximity-aware lookup layer. It allows for efficient rule evaluation, dependency tracing, and dynamic risk flagging in regulated data environments, such as financial transactions, shipments, or KYC profiles.

The system draws inspiration from Hierarchical Navigable Small World (HNSW) graphs ([Malkov & Yashunin, 2016](https://arxiv.org/abs/1603.09320)) to simulate efficient multi-layer traversal and proximity-based rule application.

---

## 📁 Key Features
- **Hybrid Data Layer**: Structured SQL for persistence + in-memory graph model for dependency exploration
- **Compliance Rule Engine**: Define and execute custom regulatory rules (e.g., OFAC, export restrictions)
- **Graph Traversal Engine**: HNSW-style proximity search to flag indirect risks or dependencies
- **Audit Logging**: Full traceability of decisions, including traversal paths and rule matches
- **Risk Attribution**: Assign risk scores and labels based on direct and indirect exposures

---

## 🤷 Use Cases
- Flagging shipments involving restricted countries or entities
- Tracing indirect ownership to sanctioned entities
- Identifying suspicious transaction patterns across linked accounts
- Visualizing exposure graphs for compliance review

---

## 👨‍💼 Target Users
- Compliance officers at financial institutions
- Developers building RegTech tools
- Risk analysts and auditors
- Fintech startups in trade compliance or AML/KYC

---

## 🚀 Tech Stack
- **Language**: Java 17+
- **Database**: PostgreSQL or MySQL
- **Graph Library**: [JGraphT](https://jgrapht.org/) or [Apache TinkerPop](https://tinkerpop.apache.org/)
- **ORM (optional)**: Hibernate
- **Caching (optional)**: Guava or Redis
- **API (optional)**: Spring Boot

---

## 📊 Data Model (SQL)
### Tables:
- `entities` (id, name, type, jurisdiction)
- `relationships` (from_id, to_id, relation_type)
- `transactions` (id, entity_id, amount, timestamp)
- `rules` (id, description, logic_sql, priority)
- `flags` (entity_id, rule_id, risk_score, path_json)

---

## 🔀 Graph Layer
- Nodes: Entities (e.g., companies, vendors, people)
- Edges: Relationships (ownership, transaction, logistics)
- Search: HNSW-style traversal prioritizing recent, high-weight, or high-risk connections

---

## 🔢 Example Rule
> If a company is in a jurisdiction under export control, or linked within 2 hops to a flagged entity, raise a compliance alert.

```sql
SELECT e.id FROM entities e
JOIN jurisdictions j ON e.jurisdiction = j.code
WHERE j.export_controlled = TRUE;
```

Graph Layer will then:
- Traverse 2-hops from flagged nodes
- Match entities by proximity, weight, and timestamp

---

## 🔧 Architecture Outline
```
Client
  └── REST API (Spring Boot, optional)
        └── Rule Engine (Java)
              ├── SQL Adapter (JDBC or Hibernate)
              └── Graph Module (JGraphT / TinkerPop)
                        └── In-memory HNSW traversal
```

---

## 🔁 Example Workflow
1. Load entities and relationships from SQL
2. Build in-memory graph at runtime
3. Define compliance rules (SQL + graph-aware)
4. Execute queries and graph traversals
5. Flag risky nodes and store flags in database
6. Provide audit trail with graph paths

---

## ✨ Stretch Features
- Rule DSL for non-dev users
- Batch mode for large transaction audits
- Graph visualizer (e.g., D3.js frontend)
- Alerts system (email, webhook) on new flags
- Integration with real sanctions datasets (OFAC, EU)

---

## 🏆 Why This Project
- Demonstrates systems thinking with hybrid architectures
- Applies graph theory to real-world compliance problems
- Built in Java: industry-friendly, battle-tested
- Emphasizes performance, traceability, and explainability

---

## 📚 References
- HNSW paper: [https://arxiv.org/abs/1603.09320](https://arxiv.org/abs/1603.09320)
- JGraphT: [https://jgrapht.org/](https://jgrapht.org/)
- OFAC Sanctions List: [https://sanctionssearch.ofac.treas.gov/](https://sanctionssearch.ofac.treas.gov/)

---

Ready to make compliance scalable, explainable, and fast.
