---
icon: brain-circuit
---

# KAI Instance

### The Foundation of Intelligent Document Understanding

Traditional RAG systems use vector similarity to retrieve text chunks, but they can't truly understand how information relates across documents. This limitation leads to incomplete answers, hallucinations, and missed connections.

**What if the retrieval component of your RAG system could understand semantic relationships between all your documents—giving your AI the context it needs to generate accurate, well-informed responses?**

### What is KAI Instance?

**KAI Instance** is a semantic retrieval engine that transforms your document repositories into an intelligent, interconnected knowledge graph. Unlike traditional vector databases used in RAG systems, KAI Instance creates a proprietary semantic neural network that maps relationships between information across all your documents, serving as the **retrieval component** of your RAG architecture—enabling your AI to understand context, avoid hallucinations, and provide accurate, well-informed answers.

#### The Core Concept

A KAI Instance is a dedicated semantic index that:

* **Indexes** multiple document repositories that share a common knowledge domain
* **Connects** information semantically across documents using a proprietary neural graph
* **Serves** AI systems via API with semantic nodes and relationships, not just text chunks
* **Scales** automatically in both compute and storage—no thresholds, no limits

Think of it as the intelligent brain that powers your AI applications, giving them true understanding rather than just pattern matching.

### How It Works

#### Semantic Graph Architecture

Unlike vector databases or traditional graph databases (Neo4j, Graph RAG, ...), KAI Instance uses a **proprietary semantic neural network** that:

* **Maps relationships** between concepts, facts, and information across documents
* **Understands context** through semantic connections, not just similarity scores
* **Prevents hallucinations** by providing AI systems with actual semantic relationships
* **Connects information** that might be worded differently but means the same thing

#### The Indexing Process

**Initial Indexing (Batch Complete)**

When you first connect a KAI Instance to your document repositories:

1. **Connection:** We connect to your document sources (Confluence, SharePoint, Git, file systems, etc.)
2. **Full Analysis:** The instance analyzes every document in your repositories
3. **Semantic Mapping:** Our neural network builds semantic relationships between all information
4. **Graph Construction:** Creates the interconnected knowledge graph
5. **Ready to Serve:** Your instance is ready to answer queries via API

**Incremental Updates**

Once indexed, the instance continuously monitors for changes:

* **Detects updates** in your knowledge bases automatically
* **Re-indexes partially** only the changed documents and their relationships
* **Maintains consistency** of the semantic graph without full re-indexing
* **Stays current** with minimal compute overhead

#### API Consumption

When your RAG system queries a KAI Instance via API (as the retrieval component), it receives:

* **Semantic nodes** representing concepts and information
* **Relationships** between those nodes across documents
* **Context** that helps the AI understand how information connects
* **Structured data** that prevents hallucinations by showing actual relationships

Unlike traditional vector retrieval that returns text chunks, KAI Instance returns semantic understanding—giving your generation layer the context it needs to create accurate responses.

### Supported Formats & Sources

#### Document Formats

KAI Instance supports all common document formats:

* **Microsoft Office:** `.docx`, `.pptx`, `.xlsx`
* **PDF:** `.pdf` files
* **Markdown:** `.md` files
* **Web:** `.html` files
* **Text:** `.txt` files

_Note: Audio and video files are not currently supported._

#### Document Sources

Connect to virtually any document repository:

* **Confluence**
* **SharePoint**
* **Notion**
* **File systems**
* **Any system with API access**

#### Segmentation Strategy

**One Instance, Multiple Repositories**

A single KAI Instance can index multiple document repositories, but they should share a common knowledge domain. This segmentation strategy ensures:

* **Relevant connections** are made between related documents
* **Domain coherence** in the semantic graph
* **Optimal performance** by keeping related knowledge together
* **Logical organization** that matches how your teams work

**Example:** You might have one KAI Instance for "Product Documentation" (indexing Confluence, and SharePoint) and another for "Customer Support Knowledge Base" (indexing Zendesk, internal wikis, etc.).

### Deployment Options

#### SaaS (Software as a Service)

Deploy a KAI Instance in our cloud infrastructure:

* **Zero infrastructure management** for you
* **Automatic scaling** and maintenance
* **Fast setup** and deployment
* **Managed service** with full support

#### On-Premises

Deploy a KAI Instance in your own infrastructure:

* **Full control** over data and infrastructure
* **Compliance** with strict data residency requirements
* **Custom integration** with your existing systems
* **Enterprise security** standards

#### Snowflake Marketplace

Deploy directly from the Snowflake Marketplace:

* **Native integration** with Snowflake ecosystem
* **Leverage Snowflake** compute and storage
* **Seamless data** pipeline integration
* **Enterprise-grade** deployment

### Key Differentiators

#### 🧠 True Semantic Understanding vs. Vector Similarity

**Traditional Search:**

* Finds documents containing keywords
* Returns text chunks
* No understanding of relationships
* High risk of hallucinations

**Vector RAG Retrieval:**

* Finds similar text embeddings
* Returns similar chunks
* Limited relationship understanding
* Still prone to hallucinations
* You must handle both retrieval and generation

**KAI Instance (Semantic RAG Retrieval):**

* Understands semantic relationships
* Returns semantic nodes with connections
* Maps how information relates across documents
* Prevents hallucinations by showing actual relationships
* **You focus on generation and UX** while we handle retrieval

#### 🔗 Semantic Graph vs. Vector Similarity

Unlike vector databases that measure similarity, KAI Instance's semantic graph:

* **Maps actual relationships** between concepts
* **Connects information** even when worded differently
* **Understands context** through semantic connections
* **Provides structure** that AI systems can reason with

#### ⚡ Auto-Scaling Architecture

**No Thresholds, No Limits**

* **Compute scaling:** Automatically adjusts based on query load
* **Storage scaling:** Grows seamlessly as you add documents
* **No configuration needed:** The instance manages itself
* **Transparent to users:** You just use the API

#### 🎯 Zero Maintenance

**Completely Transparent**

* **No manual tuning** required
* **No index optimization** needed
* **No performance monitoring** on your side
* **Just use the API** and it works

### How KAI Document Compagnon Uses KAI Instance

KAI Document Compagnon is built on top of KAI Instance. Here's how they work together:

#### Phase 1: Indexing & Duplicate Detection

1. **KAI Document Compagnon** connects a **KAI Instance** to your document repositories
2. **KAI Instance** performs the full semantic indexing
3. **KAI Document Compagnon** queries the instance to identify duplicate documents by analyzing semantic relationships
4. **Result:** You get a clean, deduplicated repository

#### Phase 2: Conflict Detection

1. **KAI Document Compagnon** receives user queries from your AI system
2. **KAI Document Compagnon** queries **KAI Instance** via API with those queries
3. **KAI Instance** returns semantic nodes and relationships for relevant information
4. **KAI Document Compagnon** analyzes the semantic connections to detect:
   * **Contradictions** between documents
   * **Outdated information** that doesn't match user expectations
   * **Missing topics** that users are asking about
5. **Result:** You get alerts about conflicts and content gaps

#### The Power of Semantic Understanding

Because KAI Instance provides semantic relationships (not just text), KAI Document Compagnon can:

* **Detect contradictions** even when documents use different wording
* **Understand context** to identify when information conflicts
* **Cluster topics** semantically, not just by keywords
* **Generate better content** recommendations based on semantic gaps

### Technical Architecture

```
┌─────────────────────┐
│  Document           │
│  Repositories       │
│  (Multiple Sources) │
└──────────┬──────────┘
           │
           │ Connection
           ▼
┌─────────────────────┐
│  KAI Instance       │
│  (Semantic Index)   │
│                     │
│  • Proprietary      │
│    Neural Graph     │
│  • Auto-scaling     │
│  • Incremental      │
│    Updates          │
└──────────┬──────────┘
           │
           │ REST API
           │ (Semantic Nodes
           │  & Relationships)
           ▼
┌─────────────────────┐
│  RAG Systems        │
│  (Generation Layer) │
│                     │
│  • LLM              │
│  • Agents/Agentic   │
│  • Document         │
│    Compagnon        │
└─────────────────────┘

```

### How KAI Instance Fits in Your RAG Architecture

#### The RAG Components

A typical RAG system has two main components:

1. **Retrieval:** Finding relevant information from your knowledge base
2. **Generation:** Using that information to generate responses for users

**KAI Instance is the Retrieval Component**

Instead of using vector similarity search, use KAI Instance as your retrieval engine:

```
┌─────────────────┐
│  User Query     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐      ┌──────────────────┐
│  KAI Instance   │─────▶│  Semantic Nodes  │
│  (Retrieval)    │      │  & Relationships │
└────────┬────────┘      └────────┬─────────┘
         │                        │
         │                        ▼
         │              ┌──────────────────┐
         │              │  Your LLM        │
         │              │  (Generation)    │
         │              └────────┬─────────┘
         │                       │
         └───────────────────────┘
                   │
                   ▼
         ┌──────────────────┐
         │  User Response   │
         └──────────────────┘
```

#### Benefits for Your RAG System

**Focus on What Matters**

* **You handle retrieval:** KAI Instance provides semantic understanding
* **You focus on generation:** Optimize your LLM prompts and UX
* **Better context:** Your generation layer receives semantic relationships, not just text chunks
* **Fewer hallucinations:** Structured semantic nodes prevent the LLM from making up connections

**Separation of Concerns**

* **Retrieval optimization:** We handle semantic indexing and relationship mapping
* **Generation optimization:** You focus on prompt engineering, response formatting, and user experience
* **Clear API boundary:** Simple integration, clear responsibilities

### Use Cases

#### Enhancing RAG Systems

Use KAI Instance as the retrieval component of your RAG:

* **Better context** through semantic relationships
* **Fewer hallucinations** with structured semantic nodes
* **Improved accuracy** by understanding document connections
* **Focus on UX** while we handle retrieval complexity

#### Knowledge Base Management

Use KAI Instance to understand your knowledge base:

* **Find relationships** between articles
* **Identify gaps** in coverage
* **Detect contradictions** across documents
* **Map knowledge domains** semantically

#### Powering Agents and Agentic Systems

When used by agents or agentic systems, KAI Instance provides:

* **Better context understanding:** Agents receive semantic relationships, not just text
* **Improved accuracy:** Agents can reason with actual document connections
* **Reduced hallucinations:** Structured semantic nodes prevent agents from inventing relationships
* **Enhanced decision-making:** Agents understand how information relates across documents

**Example:** An agentic system needs to understand product dependencies. Instead of retrieving disconnected text chunks, KAI Instance provides semantic nodes showing how features relate, dependencies connect, and components interact—giving the agent the context it needs to make accurate decisions.

#### Enterprise Documentation

Index and understand enterprise documentation:

* **Technical documentation** across multiple repositories
* **Product documentation** with semantic connections
* **Internal wikis** and knowledge bases
* **Compliance documentation** with relationship mapping

### Ready to Enhance Your RAG with Semantic Retrieval?

Stop relying on vector similarity for retrieval. Use KAI Instance as your RAG's retrieval component and focus on what you do best—creating great user experiences and optimizing your generation layer.

_KAI Instance - The semantic foundation for intelligent AI applications._
