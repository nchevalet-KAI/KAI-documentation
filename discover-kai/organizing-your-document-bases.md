---
description: >-
  How to structure the governance of your unstructured knowledge — and why
  structured data approaches don't apply.
icon: sitemap
---

# Organizing your document bases

### The Fundamental Misconception

Most organizations approach document management with reflexes borrowed from the world of **structured data**: centralize, normalize, deduplicate into a single repository. This approach, effective for SQL tables or data warehouses, consistently fails when applied to document bases.

Why? Because a document is not a row in a table. It's a **living object**, contextual, meaning-bearing — and often contradictory with other documents without anyone knowing.

***

### Structured Data vs. Document Knowledge

#### What Fundamentally Changes

|                            | Structured Data                                     | Document Knowledge                                                     |
| -------------------------- | --------------------------------------------------- | ---------------------------------------------------------------------- |
| **Format**                 | Rows, columns, fixed schema                         | Free text, tables, images, diagrams                                    |
| **Truth**                  | One value per field — the latest is the correct one | Multiple documents can cover the same topic with different information |
| **Contradiction**          | Detectable by constraint (unique key, type…)        | Invisible without semantic analysis                                    |
| **Obsolescence**           | Managed by versioning or timestamps                 | Rarely tracked — outdated documents coexist with current ones          |
| **Traditional governance** | Data catalog, lineage, quality rules                | No mature equivalent before K-AI                                       |
| **Owner**                  | The DBA, the data engineer                          | Often nobody — or everybody                                            |
| **Duplication**            | `SELECT DISTINCT`                                   | Two documents saying the same thing with different words               |
| **Impact of an error**     | A wrong number in a dashboard                       | An incorrect AI response sent to a customer or employee                |

#### In Short

Structured data lives in a world **constrained by design**: schemas, types, primary keys, indexes. These constraints mechanically prevent most inconsistencies.

Document knowledge lives in a world **free by nature**: anyone can create a document, duplicate it, modify it, contradict it. **No mechanical constraint protects consistency.** This is exactly the problem K-AI solves.

***

### The Pitfalls of Applying a "Data" Approach to Documents

#### ❌ Pitfall 1 — "We'll centralize everything into a single repository"

In the data world, centralization works (data warehouse, data lake). For documents, it's an illusion:

* Teams use different tools (SharePoint, Confluence, Notion, Google Drive…)
* Forcing migration creates resistance and content loss
* A poorly maintained central repository becomes a document graveyard

**The K-AI approach:** We don't centralize documents. We **connect** to existing repositories via API and build a semantic intelligence layer on top. Each repository stays where it is.

#### ❌ Pitfall 2 — "We'll deduplicate like in a database"

In SQL, a duplicate is identical bit for bit. In a document repository, duplication is **semantic**:

* Two documents with different titles explaining the same procedure
* A Word version and a PDF version of the same content, with minor edits
* Three onboarding guides created by three teams, partially overlapping

**The K-AI approach:** The Neural Semantic Graph detects duplicates by **meaning**, not by form. Two documents saying the same thing with different words are identified as semantic duplicates.

#### ❌ Pitfall 3 — "We'll apply automated quality rules"

Data quality rules (null check, format validation, range check) have no direct equivalent for documents. You can't write a rule that says: _"This paragraph contradicts another document published 6 months ago."_

**The K-AI approach:** Contradiction detection relies on contextual understanding of content, not declarative rules. K-AI identifies that one document says _"The return policy is 30 days"_ while another says _"Returns are accepted within 14 days"_ — without any rule being configured.

#### ❌ Pitfall 4 — "A data catalog will suffice"

A data catalog inventories datasets, their lineage, and their metadata. It's essential for structured data. But for documents:

* Metadata is often missing or incorrect
* The actual content of a document goes far beyond its title
* Document lineage (who created what, from what) is rarely tracked

**The K-AI approach:** The AI-Ready Knowledge Score provides a living diagnostic of the health of each document base — far beyond a simple inventory.

***

### How to Organize Your Document Bases with K-AI

#### Core Principle: One Instance per Coherent Domain

The unit of organization in K-AI is the **instance**. Each instance corresponds to a **homogeneous document domain** — a set of documents sharing a common business context.

```
Example for a large retail group:

Instance 1 — Store procedures (POS, checkout, inventory)
Instance 2 — HR policies (leave, payroll, recruitment)
Instance 3 — Product documentation (specs, catalogs, data sheets)
Instance 4 — IT support (guides, troubleshooting, FAQ)
```

> **Rule:** If two sets of documents are not meant to be compared against each other for contradiction detection, they belong to separate instances.

#### 3 Dimensions of Analysis per Base

Before creating an instance, analyze each document base along three axes:

**📐 Dimension 1 — Usage**

What is the primary need?

| Need                | K-AI Module                 | When to Use                                     |
| ------------------- | --------------------------- | ----------------------------------------------- |
| Deep cleanup        | **K-AI Audit**              | Complex base, never audited, critical stakes    |
| Ongoing maintenance | **K-AI Document Companion** | Already relatively clean base, needs monitoring |
| Both                | **Audit → then Companion**  | Most common scenario: clean first, then monitor |

**👥 Dimension 2 — Stakeholders**

Clearly identify who produces and who consumes:

* **Producers**: the subject-matter experts who create and maintain documents. They are the ones who will act on K-AI alerts.
* **Consumers**: the end users who query the base — directly or through an AI system (chatbot, copilot, agent).

> Without an identified and accountable producer, a document base inevitably degrades. This is a GO/NO GO criterion for deployment.

**🎯 Dimension 3 — Scope**

| Situation                  | K-AI Organization                                                    |
| -------------------------- | -------------------------------------------------------------------- |
| Single homogeneous domain  | **1 instance**                                                       |
| Multiple distinct domains  | **1 instance per domain**                                            |
| Cross-domain search needed | **1 instance per domain + 1 umbrella instance** for global retrieval |

***

### Document Governance vs. Data Governance

#### What Data Governance Does Well (and What to Keep)

Some data governance principles translate directly:

* **Ownership**: every document base must have an identified owner, just as every dataset has a data owner
* **Lifecycle**: documents have a validity period, just as data has a freshness date
* **Quality measurement**: the AI-Ready Knowledge Score plays the role of the data quality score, but adapted for documents
* **Continuous improvement**: document quality is a process, not a one-time project

#### What Is Specific to Documents

| Data Concept           | K-AI Document Equivalent                                      |
| ---------------------- | ------------------------------------------------------------- |
| Data quality rules     | Automatic semantic detection (conflicts, obsolescence, gaps)  |
| Data catalog           | Neural Semantic Graph — a living graph of knowledge           |
| Data lineage           | Traceability of relationships between documents and concepts  |
| ETL / data pipeline    | K-AI Cleaning phase (connect → index → clean)                 |
| Data warehouse         | No equivalent — documents stay in their original repositories |
| Monitoring / alerting  | Real-time conflict detection during user queries              |
| Master Data Management | Single Point of Truth — one authoritative document per topic  |

***

### Typical Organization Diagram

```
                    ┌───────────────────────────┐
                    │   Global Governance       │
                    │   • C-Level Sponsor       │
                    │   • Cross-cutting KPIs    │
                    │   • Target AI-Ready Score │
                    └────────────┬──────────────┘
                                 │
            ┌────────────────────┼─────────────────────┐
            │                    │                     │
            ▼                    ▼                     ▼
   ┌─────────────────┐ ┌─────────────────┐  ┌─────────────────┐
   │ KAI Instance    │ │ KAI Instance    │  │ KAI Instance    │
   │ HR Base         │ │ Product Base    │  │ IT Support Base │
   │                 │ │                 │  │                 │
   │ Owner: CHRO     │ │ Owner: Product  │  │ Owner: CIO      │
   │                 │ │ Director        │  │                 │
   │ Repositories:   │ │ Repositories:   │  │ Repositories:   │
   │ • SharePoint HR │ │ • Confluence    │  │ • ServiceNow    │
   │ • Notion Payroll│ │ • Google Drive  │  │ • Confluence IT │
   │                 │ │                 │  │                 │
   │ Score: 72/100   │ │ Score: 58/100   │  │ Score: 81/100   │
   └─────────────────┘ └─────────────────┘  └─────────────────┘
            │                    │                     │
            └────────────────────┼─────────────────────┘
                                 │
                                 ▼
                    ┌───────────────────────────┐
                    │  Umbrella Instance        │
                    │  (cross-domain retrieval) │
                    │                           │
                    │  Used by:                 │
                    │  • Internal chatbot       │
                    │  • Copilot                │
                    │  • AI Agents              │
                    └───────────────────────────┘
```

***

### Checklist — Before Connecting a Document Base

Before creating a K-AI instance for a document base, verify these points:

* [ ] **Owner identified** — Someone is responsible for this base and will act on alerts
* [ ] **Scope defined** — The boundaries of the document domain are clear
* [ ] **Repositories identified** — The list of sources (SharePoint, Confluence, Notion…) is known
* [ ] **Use case clear** — Audit only, search only, or both?
* [ ] **Consumers identified** — Who uses this base? Through which channel (chat, copilot, direct)?
* [ ] **Success KPIs defined** — What AI-Ready Score are we targeting? What business impact are we measuring?
* [ ] **Sponsor engaged** — Management buy-in is secured

> If any of these points is not covered, it's better to resolve it **before** deploying. A tool, however powerful, does not compensate for an organizational gap.

***

### Summary

|                               | Structured Data               | Document Knowledge                    |
| ----------------------------- | ----------------------------- | ------------------------------------- |
| **Reference tool**            | Data warehouse, data catalog  | K-AI Document Companion               |
| **Governance unit**           | The dataset                   | The document base (= 1 K-AI instance) |
| **Quality measurement**       | Data quality score            | AI-Ready Knowledge Score              |
| **Cleanup**                   | ETL, SQL dedup                | Automatic semantic cleaning           |
| **Monitoring**                | Pipeline monitoring           | Real-time conflict detection          |
| **Objective**                 | Single source of truth (data) | Single Point of Truth (documents)     |
| **What protects consistency** | Schema constraints            | K-AI (nothing else does it at scale)  |

***

_Structured data quality is a solved problem. Document knowledge quality is not — not yet. That's exactly why K-AI exists._
