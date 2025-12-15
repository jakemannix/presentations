# Program Map: Unified Relevance Platform

### Slide text

- Goal: converge Search, P13N, Ads, and Sparky on a shared relevance platform
- We have a mix of:
  - Programs already underway that need evolutionary adjustments
  - New or significantly expanded programs we must stand up
- This section maps the work into two buckets:
  - Underway, directionally right
  - New / major expansion required

---
Diagrams:
- Two-column visual:
  - Left: "Underway / Evolutionary" with a few program names.
  - Right: "New / Major Expansion" with corresponding program names.
- Arrow from both columns toward a central "Unified Relevance Platform" box.

Layout and styling:
- Title at top, bullets on left.
- Two-column block or simple table to visually separate the buckets.

## Bucket A: Underway, Mostly Evolutionary

### Slide text

- Programs in this bucket:
  - Feature Store → + event transforms & indexing
  - Tiered Hybrid Search (Solr → Vespa, broaden to all catalog)
  - Multi-head / multi-task rankers in Search + P13N
  - Search E/E learnings → Arbitration Engine
  - Model inference on GTP with Hydra integrated
- These are largely **directionally correct**
  - Require scope extension and cross-team alignment
  - Do **not** require a fundamental rethink

---
Diagrams:
- List of 5 program boxes under a header "Bucket A".
- Each box with a small label indicating primary owner(s) (e.g. Search, P13N, GTP).

Layout and styling:
- Use color coding (e.g. green) for "underway".
- Keep bullets simple; details go to per-program slides.

## Feature Store: Extend to Events & Indexing

### Slide text

- Current status
  - Feature Store program is already underway
  - Focused on defining and serving features online/offline
- Required evolution
  - Add a robust event transformation layer:
    - clicks, views, orders, chat, ads → feature tables & training sets
  - Integrate tightly with indexing pipelines:
    - feature definitions drive Vespa indexing for all catalog data sources
- Target state
  - Feature Store becomes the **data backbone**:
    - single source of truth for features used by Search, P13N, and later Ads
    - powering both training and serving paths

---
Diagrams:
- Pipeline: Event Bus → Event Transforms → Feature Store → (a) Training, (b) Vespa Indexes, (c) Online Serving.
- Icons for "Search ranker", "P13N ranker" reading from the same Feature Store.

Layout and styling:
- Emphasize "already underway" and highlight the new attachments (event transforms, indexing hooks).

## Tiered Hybrid Search: Vespa for All Catalog Data

### Slide text

- Current status
  - Tiered Hybrid Search is migrating Solr → Vespa for Search
  - Primarily focused on SERP use cases today
- Required evolution
  - Treat Vespa as the **canonical retrieval substrate**
    - expand beyond Search to P13N rec pools
    - eventually serve all catalog data sources in CP
  - Support multiple retrieval recipes:
    - query-based (Search SERP)
    - context-based (P13N)
    - hybrid query + profile
- Target state
  - One unified retrieval layer:
    - single indexing path for catalog
    - shared infrastructure used by Search and P13N (and later Ads)

---
Diagrams:
- Left: "Solr → Vespa migration" for Search.
- Right: Vespa with arrows from:
  - Search SERP,
  - P13N recs,
  - future Ads and Sparky flows.
- Caption: "One Vespa-based Tiered Hybrid Search for all catalog retrieval."

Layout and styling:
- Highlight the “scope expansion” from Search-only to multi-domain.

## Multi-Task Rankers: Joint Search + P13N Program

### Slide text

- Current status
  - Multi-head / multi-task rankers exist separately:
    - in Search
    - in P13N
- Required evolution
  - Operate these as **one program**, not two:
    - shared trunk / representation model
    - Search and P13N as separate heads/tasks
  - Unify:
    - training data pipelines,
    - evaluation dashboards and metrics,
    - serving infrastructure (GTP)
- Target state
  - A shared ranking model family:
    - Search ranker head and P13N ranker head on the same backbone
    - easier to add future heads (e.g. Ads) without new bespoke stacks

---
Diagrams:
- Neural net sketch with:
  - Shared trunk labeled "Search+P13N trunk".
  - Two heads labeled "Search head" and "P13N head".
- Arrow from Data Lake / logs into the shared training pipeline.

Layout and styling:
- Visually emphasize that current “two programs” become “one shared program with multiple heads”.


## Search E/E → Unified Arbitration Engine

### Slide text

- Current status
  - P13N Arbitration Engine: online-learning / bandits for rec modules
  - Search E/E: explore/exploit experiments applied to SERP/rankers
- Required evolution
  - Merge learnings from Search E/E into the Arbitration Engine
  - Make Arbitration Engine a **shared platform**:
    - can handle carousels and pointwise result lists (SERPs)
    - can manage ranking variants for Search and module mixes for P13N
- Target state
  - One cross-domain online-learning platform:
    - shared policy engine and logging format
    - configurable per surface (SERP, home, PDP) and per slot/module

---
Diagrams:
- Current: two boxes labeled "P13N arbitration" and "Search E/E" in parallel.
- Future: single "Arbitration & E/E Engine" box feeding:
  - SERP ranker selection,
  - rec module selection.

Layout and styling:
- Use arrows to show consolidation.
- Label the future engine as "shared across Search + P13N (and extensible to Ads)".

## Model Inference on GTP with Hydra Integration

### Slide text

- Current status
  - GTP already operates a model serving platform
  - Hydra exists as a concrete ranking/model stack within Search/P13N
- Required evolution
  - Package Hydra models and infra to run on GTP as a first-class tenant
  - Standardize:
    - model registration and versioning
    - SLAs and monitoring for Search/P13N workloads
  - Gradually deprecate bespoke serving paths once GTP parity is confirmed
- Target state
  - One model inference platform (GTP):
    - serving Search and P13N rankers, retrieval-assist models, classifiers
    - easier for future domains (Ads, Sparky) to onboard

---
Diagrams:
- Left: separate "Hydra serving" and "GTP serving" boxes.
- Right: single "GTP model serving" box hosting:
  - Hydra-based rankers,
  - other models.
- Arrow from Search & P13N into GTP serving.

Layout and styling:
- Emphasize convergence onto GTP as the standard runtime.

## Bucket B: New or Major Expansion Programs

### Slide text

- Programs in this bucket:
  - Unified cross-surface memory: agents + Search contextualization
  - Unified embedding architecture & shared semantic space
  - Shared personalized search tools for agents (Sparky + external)
  - Shared inference graph orchestrator (RMS → platform)
- These are **not** just minor scope changes
  - They require new cross-team mandates
  - They materially change how multiple stacks operate

---
Diagrams:
- Four boxes labeled with each program under "Bucket B".
- Arrows from each box into a central “Unified Relevance Platform” to show they are foundational.

Layout and styling:
- Use a different accent color (e.g., orange) to signal these are new/big.
- Keep bullet list short; details on per-program slides.

## Unified Cross-Surface Memory (Agents + Search)

### Slide text

- Current status
  - Memory for agents (Sparky) is underway
  - Search has separate realtime contextualization/session logic
- Required evolution
  - Build a **single journey/memory layer**:
    - shared session/journey model across Search, P13N, Sparky, partners
    - unified view of recent queries, clicks, views, cart, chat turns
  - Expose the same memory to:
    - Search ranking,
    - P13N recs,
    - Sparky and external agents via tools
- Target state
  - One cross-surface memory system:
    - consistent behavior across search bar, home, PDP, Sparky, ChatGPT
    - foundational for “native AI shopping” and long-lived missions

---
Diagrams:
- Central "Journey Memory" / "Session Store" box.
- Arrows from:
  - Search,
  - P13N,
  - Sparky,
  - ChatGPT
  into and out of that memory layer.

Layout and styling:
- Emphasize “one memory” vs separate per-surface memories.

## Unified Embedding Architecture & Shared Semantic Space

### Slide text

- Current status
  - No unified embedding architecture today:
    - multiple embedding spaces across Search, P13N (and potentially Ads)
- Required evolution
  - Define canonical embedding types:
    - user_long, user_session, item_product, item_content, query_intent, context
  - Establish shared training frameworks:
    - multi-task training over Search and P13N signals
    - common dimensionalities, quality metrics, lifecycle
  - Integrate deeply with:
    - Feature Store,
    - Vespa-based retrieval,
    - shared ranking trunk
- Target state
  - A single semantic space (or set of well-defined spaces):
    - used by retrieval, ranking, recs, and agents
    - simplifies cross-domain reuse and multi-task learning

---
Diagrams:
- Embedding boxes for users, items, queries with consistent shapes and arrows into:
  - Retrieval,
  - Rankers,
  - Sparky tools.
- Caption: "One shared semantic space for Search + P13N (and future Ads)".

Layout and styling:
- Visual metaphor of different colored blobs merging into a single coherent embedding space.

## Shared Agent Tools & Sparky Agents for Search/Discovery

### Slide text

- Current status
  - Sparky exists with some tools/integrations
  - No unified, shared tool set specifically for personalized search & recs
- Required evolution
  - Define a common **tool API surface** for agents:
    - search_products, get_recommendations, get_similar_items
    - get_bundles/plan, get_user_profile, etc.
  - Implement these tools on top of:
    - unified retrieval,
    - Feature Store,
    - shared rankers
  - Build **Sparky Agents** specialized for:
    - search & discovery,
    - browsing and planning flows
- Target state
  - Agents (Sparky, ChatGPT, others) all call the **same set of tools**
    - consistent personalization,
    - consistent logging and learning,
    - easy to add new agent capabilities without new bespoke backends

---
Diagrams:
- "Agent Tool Layer" with a set of tool names (search_products, get_recs, etc.).
- Arrows from:
  - Sparky,
  - ChatGPT,
  to the tool layer.
- Tool layer connected down to unified retrieval, rankers, and Feature Store.

Layout and styling:
- Emphasize that tools are “thin wrappers” over the same platform APIs used by Glass.

## Shared Inference Graph Orchestrator (RMS → Platform)

### Slide text

- Current status
  - No unified story; RMS has a version of an inference orchestration layer
  - Each stack has bespoke pipelines / flow control
- Required evolution
  - Turn RMS’ version into a **configuration-driven platform**:
    - a graph/DAG of nodes: feature fetch, retrieval, rankers, rules, bandits, arbitration
    - executed by a shared, stateless runtime
  - Migrate Search and P13N flows to this orchestrator:
    - Search SERP graph templates
    - Homepage / PDP recs graph templates
  - Plan for handoff to GTP once mature enough:
    - so Ads and Sparky internals can also run on the same orchestrator
- Target state
  - A “Relevance Runtime” used by all domains:
    - consistent timeouts, caching, logging, and fallbacks
    - surfaces differ by graph config, not by owning their own code pipelines

---
Diagrams:
- API layer → "Inference Orchestrator" box → nodes:
  - Feature Fetch,
  - Retrieval,
  - Ranker,
  - Arbitration, Bandits
  → Response


