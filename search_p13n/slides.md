# Program Map: Unified Relevance Platform

- **Goal:** Converge Search, P13N, Ads, and Sparky on a shared relevance platform
- We have a mix of:
  - Programs already underway that need evolutionary adjustments
  - New or significantly expanded programs we must stand up

| Underway / Evolutionary | New / Major Expansion |
|-------------------------|----------------------|
| Feature Store | Unified Cross-Surface Memory |
| Tiered Hybrid Search | Unified Embedding Architecture |
| Multi-Task Rankers | Shared Agent Tools |
| Search E/E → Arbitration | Inference Graph Orchestrator |
| Model Inference on GTP | |

---

# Bucket A: Underway, Mostly Evolutionary

| Program | Evolution Needed |
|---------|------------------|
| Feature Store | + event transforms & indexing |
| Tiered Hybrid Search | Solr → Vespa, broaden to all catalog, all RT recommenders |
| Multi-head / multi-task rankers | Joint Search + P13N program |
| Search E/E | → Arbitration Engine |
| Model inference | GTP owns Hydra+Element |

These are **directionally correct** — require scope extension and cross-team alignment, but do **not** require a fundamental rethink.

---

# Feature Store: Extend to Events & Indexing

**Current status**
- Feature Store program is already underway
- Focused on finding some features to share

**Required evolution**
- Add a robust event transformation layer:
  - clicks, views, orders, chat, ads → feature tables & training sets
- Integrate tightly with CDC/indexing pipelines:
  - feature definitions drive Vespa indexing for all catalog + signal data sources
- Only diff of "indexing" / "feature hydration": Vespa vs Cassandra

**Target state**
- Feature Store pipelines become the **data backbone**:
  - Single source of truth for features used by Search, P13N, and later Ads
  - Powering both training, serving, indexing paths

---

# Tiered Hybrid Search: Vespa for All Catalog Data

**Current status**
- Tiered Hybrid Search is migrating Solr → Vespa for Search
- Primarily focused on Embedding use cases today

**Required evolution**
- Treat Vespa as the **canonical retrieval substrate**
  - Expand beyond Search to (non-batch) P13N rec pools
  - Eventually serve all catalog data sources in CP
- Support multiple retrieval recipes:
  - Query-based (Search SERP)
  - Context-based (P13N)
  - Hybrid query + profile

**Target state**
- One unified retrieval layer with single indexing path for catalog
- Shared infrastructure used by Search and P13N (and later Ads)
- *Not* to be handed to GTP: complex NRT + filters + shard-local ranking

---

# Multi-Task Rankers: Joint Search + P13N Program

**Current status**
- Multi-head / multi-task rankers exist separately:
  - In Search
  - In P13N

**Required evolution**
- Operate these as **one program**, not two:
  - Shared trunk / representation model
  - Search and P13N as separate heads/tasks
- Unify:
  - Training data pipelines
  - Serving infrastructure (Element/GTP)

**Target state**
- A shared ranking model family:
  - Search ranker head and P13N ranker head on the same backbone
  - Easier to add future heads (e.g. Ads) without new bespoke stacks
  - note: also, can we kill as many tree-based models as possible?

---

# Search E/E → One Unified Arbitration Engine

**Current status**
- P13N Arbitration Engine: generic multi-objective online-learning for modules
- Search E/E: explore/exploit applied to secondary stacks

**Required evolution**
- Merge learnings from Search E/E into the Arbitration Engine
- Expand Arbitration Engine a single **shared platform**:
  - Can handle carousels *and* pointwise result lists (SERPs)
  - Can manage ranking variants for Search and module mixes for P13N

**Target state**
- One cross-domain online-learning platform:
  - Shared policy engine and logging format
  - Configurable per surface (SERP, home, PDP) and per slot/module

---

# Model Inference on Element / Hydra

**Current status**
- GTP already operates Element (low-latency Ads models)
- We've walked through P13N's Hydra, can handle Search already

**Required evolution**
- Hand Hydra infra (UX, config setup) so GTP can merge with Element
- GTP gets Hydra-trained *people* who understand Search + P13N perf needs
- It's on *them* to merge/deprecate duplicate parts over time

**Target state**
- One model inference platform (Element)
- Any GTP-internal migrations are transparent to customers

---

# Bucket B: New or Major Expansion Programs

| Program | Scope |
|---------|-------|
| Unified Cross-Surface Memory | Agents + Search contextualization |
| Unified Embedding Architecture | Shared semantic space |
| Shared Agent Tools | Sparky + external agents |
| Inference Graph Orchestrator | RMS → platform |

These are **not** just minor scope changes — they require new cross-team mandates and materially change how multiple stacks operate.

---

# Unified Cross-Surface Memory (Agents + Search)

**Current status**
- Memory for agents (Sparky) is underway
- Search has realtime contextualization/session pipelines+caches

**Required evolution**
- Build a **single journey/memory layer**:
  - Shared session/journey model across Search, P13N, Sparky, partners
  - Unified view of recent queries, clicks, views, cart, chat turns
  - Pluggable rollup/aggregation/summarization pipeline systems
- Expose the same memory to:
  - Search ranking
  - P13N recs
  - Sparky and external agents via tools

**Target state**
- One cross-surface memory system:
  - Consistent behavior across search bar, home, PDP, Sparky, ChatGPT
  - Foundational for "native AI shopping" and long-lived missions

---

# Unified Embedding Architecture & Shared Semantic Space

**Current status**
- No unified embedding architecture today
- Multiple embedding spaces for each of Catalog, Query, User (and Ads)

**Required evolution**
- Define canonical embedding types e.g.:
  - `user_long`, `user_session`, `item_product`, `item_content`, `query_intent`, `context`
- Establish shared training frameworks:
  - Multi-task/multi-tower training over Search and P13N signals
  - Common dimensionalities, quality metrics, lifecycle
- Integrate deeply with Feature Store, Vespa, shared ranking trunk

**Target state**
- A single semantic space (or set of version backwards-compatible spaces):
  - Used by retrieval, ranking, recs, and agents
  - Simplifies cross-domain reuse and multi-task learning
- "It's Representation Learning, not Feature Engineering" as an LLM might say

---

# Shared Agent Tools & Sparky Agents for Search/Discovery

**Current status**
- Sparky exists with some tools/integrations
- No unified, shared tool set specifically for personalized search & recs

**Required evolution**
- Define a common **MCP tools** for agents:
  - `search_products`, `get_recommendations`, `get_similar_items`
  - `get_bundles/plan`, `get_user_profile`, etc.
- Implement these tools on top of unified retrieval, Feature Store, shared rankers
- Build **Shopping Agents** specialized for personalized search & discovery, browsing and planning flows
- Critical: not totally separate p13n and search tools. *Integrated*

**Target state**
- Agents (Sparky, ChatGPT, others) all call the **same set of tools**
  - Consistent personalization
  - Easy to add new agent capabilities without new bespoke backends

---

# Shared Inference Graph Orchestrator (RMS → Platform)

**Current status**
- No unified story; RMS has a version of an inference orchestration layer
- Each stack has bespoke pipelines / flow control

**Required evolution**
- Turn RMS' version into a **configuration-driven platform**:
  - A graph/DAG of nodes: feature fetch, retrieval, rankers, rules, bandits, arbitration
  - Executed by a shared, stateless runtime
- Migrate Search and P13N flows to this orchestrator:
  - Search SERP graph templates
  - Homepage / PDP recs graph templates
- Maybe: handoff to GTP once mature enough (probably ~ 2y out)

**Target state**
- A "Relevance Runtime" used by all domains:
  - Consistent timeouts, caching, logging, and fallbacks
  - Surfaces differ by graph config, not by owning their own code pipelines

