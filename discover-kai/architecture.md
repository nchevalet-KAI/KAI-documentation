---
description: Technical architecture overview of KAI stack
icon: sitemap
---

# Architecture

### Overview

KAI uses a **hybrid architecture** that combines single-tenant and multi-tenant components to ensure both data isolation and operational efficiency:

* **KAI Instance:** Single-tenant architecture—each instance runs in complete isolation with dedicated compute and storage
* **KAI Document Compagnon:** Multi-tenant architecture—manages multiple client instances while maintaining data segregation

This architecture provides enterprise-grade security through instance-level isolation while enabling efficient management and scaling.

### Core Components

#### KAI Instance

The semantic indexing engine that powers KAI's intelligent document understanding:

* **Architecture:** Single-tenant—each instance is completely isolated
* **Semantic Graph:** Proprietary neural network that maps relationships across documents
* **Indexing Engine:** Processes and indexes documents from client repositories
* **API Layer:** REST API for querying semantic nodes and relationships
* **Auto-scaling:** Automatically adjusts compute and storage based on load
* **Isolation:** Dedicated pod (AKS) and Elastic Cloud database per instance

#### KAI Document Compagnon

The intelligent document maintenance layer built on top of KAI Instance:

* **Architecture:** Multi-tenant—manages multiple client instances
* **Conflict Detection:** Analyzes user queries to detect document inconsistencies
* **Gap Analysis:** Identifies missing topics users are asking about
* **Content Generation:** Creates new documents based on admin responses
* **Alert System:** Provides actionable recommendations for document updates
* **Instance Management:** Orchestrates multiple KAI Instances while maintaining data segregation

#### API Gateway

The integration layer that connects KAI with client systems:

* **REST API:** Standard API for all integrations
* **Authentication:** Secure API key management
* **Rate Limiting:** Ensures fair resource usage

### Integration Architecture

#### How KAI Connects to Your Systems

```
┌─────────────────────────────────────────────────────────┐
│                    Client Infrastructure                │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌───────────────┐         ┌──────────────────┐         │
│  │  Document     │         │  AI Search       │         │
│  │  Repositories │         │  System          │         │
│  │               │         │  (RAG/Agents/    │         │
│  │ • Confluence  │         │   Copilot)       │         │
│  │ • SharePoint  │         │                  │         │
│  │ • Notion      │         │                  │         │
│  │ • Git, etc.   │         │                  │         │
│  └───────┬───────┘         └────────┬─────────┘         │
│          │                          │                   │
│          │ API                      │ API               │
│          │ (Document Access)        │ (User Queries)    │
└──────────┼──────────────────────────┼───────────────────┘
           │                          │
           │                          │
           ▼                          ▼
┌─────────────────────────────────────────────────────────┐
│                    KAI Platform                         │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌───────────────────────────────────────────────┐      │
│  │    KAI Document Compagnon (Multi-Tenant)      │      │
│  │  • Conflict Detection                         │      │
│  │  • Gap Analysis                               │      │
│  │  • Content Generation                         │      │
│  │  • Instance Orchestration                     │      │
│  └───────────────┬───────────────────────────────┘      │
│                  │                                      │
│                  │ API (per client instance)            │
│                  ▼                                      │
│  ┌───────────────────────────────────────────────┐      │
│  │    KAI Instance (Single-Tenant per client)    │      │
│  │  • Semantic Graph                             │      │
│  │  • Indexing Engine                            │      │
│  │  • Query API                                  │      │
│  │  • Isolated Pod + Elastic Cloud               │      │
│  └───────────────────────────────────────────────┘      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

#### Integration Points

**Document Repositories → KAI**

* **Connection:** Via API connectors (Confluence API, SharePoint API, etc.)
* **Access:** Read-only access to documents for indexing
* **Frequency:** Initial full index, then incremental updates as documents change

**AI Search System → KAI Document Compagnon**

* **Connection:** REST API integration
* **Data Flow:** Your AI system sends user queries to KAI Document Compagnon
* **Real-time:** Queries are analyzed as they happen

**KAI → Client Systems**

* **Alerts:** KAI Document Compagnon provides alerts via API
* **Recommendations:** Actionable insights on document conflicts and gaps
* **Generated Content:** New documents ready for your knowledge base

### Data Flow

#### Document Indexing Flow

```
1. Document Source
   └─> Client's Document Repository
   
2. Temporary Storage
   └─> Azure Blob Storage (temporary, during processing)
   
3. Processing
   └─> KAI Instance Indexing Engine
       • Document analysis
       • Semantic relationship mapping
       • Graph construction
   
4. Permanent Storage
   └─> Elastic Cloud (dedicated per instance)
       • Semantic graph storage
       • Indexed relationships
   
5. Reference
   └─> Pointer to original document (via API)
       • No document content stored permanently
       • Only semantic relationships and metadata
```

**Key Points:**

* Documents are temporarily stored during processing only
* After processing, documents are removed from temporary storage
* KAI maintains pointers to original documents, not document copies
* All semantic relationships are stored in the dedicated Elastic Cloud instance

#### Query Processing Flow

```
1. User Query
   └─> Client's AI Search System
   
2. Query Forwarding
   └─> KAI Document Compagnon (via API)
   
3. Semantic Retrieval
   └─> KAI Instance
       • Query semantic graph
       • Retrieve relevant nodes and relationships
       • Return structured semantic data
   
4. Analysis
   └─> KAI Document Compagnon
       • Correlate query with semantic relationships
       • Detect conflicts or gaps
       • Generate recommendations
   
5. Response
   └─> Client System
       • Alerts on conflicts
       • Recommendations for updates
       • Generated content (if applicable)
```

### Security & Data Isolation

#### Hybrid Architecture: Single-Tenant Instances, Multi-Tenant Management

**KAI Instance: Single-Tenant Architecture**

Each KAI Instance operates in complete isolation:

* **Dedicated Compute:** Each instance runs in its own pod on Azure Kubernetes Service (AKS) in France
* **Dedicated Storage:** Each instance has its own Elastic Cloud database
* **No Shared Resources:** No compute, storage, or network resources are shared between instances
* **Data Segregation:** Complete separation ensures no data leakage between clients
* **Complete Isolation:** Each client's semantic graph and indexed data are completely isolated

**KAI Document Compagnon: Multi-Tenant Architecture**

KAI Document Compagnon manages multiple client instances while maintaining strict data segregation:

* **Instance Orchestration:** Manages multiple KAI Instances (one per client)
* **Data Segregation:** Each client's data is isolated at the KAI Instance level
* **No Cross-Instance Access:** KAI Document Compagnon never mixes data between instances
* **API Isolation:** Each client's API calls are routed to their dedicated KAI Instance
* **Operational Efficiency:** Multi-tenant management layer enables efficient operations while maintaining security

**How It Works Together:**

```
KAI Document Compagnon (Multi-Tenant)
    │
    ├──> Client A's KAI Instance (Single-Tenant)
    │    └──> Dedicated Pod + Elastic Cloud
    │
    ├──> Client B's KAI Instance (Single-Tenant)
    │    └──> Dedicated Pod + Elastic Cloud
    │
    └──> Client C's KAI Instance (Single-Tenant)
         └──> Dedicated Pod + Elastic Cloud
```

Each client's data remains completely isolated in their dedicated KAI Instance, while KAI Document Compagnon provides the management and analysis layer across all instances.

#### Data Storage & Privacy

**Where Data is Stored:**

* **Semantic Graph:** Elastic Cloud (dedicated instance per KAI Instance)
* **Temporary Processing:** Azure Blob Storage (documents deleted after processing)
* **Pointers Only:** KAI maintains API pointers to original documents, not document copies

**Data Retention:**

* **Semantic Relationships:** Stored permanently in Elastic Cloud (as long as instance is active)
* **Document Content:** Not stored permanently—only semantic relationships and metadata
* **Temporary Files:** Deleted immediately after processing

#### Security Measures

* **Encryption:** All data encrypted in transit and at rest
* **Access Control:** API key-based authentication
* **Network Security:** Isolated network per instance
* **Compliance:** Designed to meet enterprise security and compliance requirements

### Scalability & Performance

#### Auto-Scaling Architecture

**Compute Scaling:**

* Automatically adjusts based on query load
* No manual configuration required
* Seamless scaling without service interruption

**Storage Scaling:**

* Grows automatically as documents are indexed
* No storage limits or thresholds
* Transparent to users

#### Performance Guarantees

**Availability:**

* **99.95% uptime SLA**
* High availability architecture
* Automatic failover and recovery

**Query Performance:**

* **Semantic graph queries:** Always under 8 seconds
* Performance consistent regardless of:
  * Number of documents indexed
  * Size of document repository
  * Complexity of semantic relationships

**Indexing Performance:**

* Initial indexing: Speed depends on repository size
* Incremental updates: Only changed documents are re-indexed
* Minimal impact on ongoing operations

### Deployment Models

#### SaaS (Software as a Service)

**Infrastructure:**

* Hosted on Azure (France region)
* Managed by KAI team
* Zero infrastructure management for clients

**Benefits:**

* Fast setup and deployment
* Automatic updates and maintenance
* Full support and monitoring

#### On-Premises

**Infrastructure:**

* Deployed in client's own infrastructure
* Full control over data and compute
* Custom integration options

**Benefits:**

* Data residency compliance
* Enterprise security requirements
* Custom network configuration

#### Snowflake Marketplace

**Infrastructure:**

* Native integration with Snowflake
* Leverages Snowflake compute and storage
* Seamless data pipeline integration

**Benefits:**

* Enterprise-grade deployment
* Integrated with existing Snowflake workflows
* Optimized for Snowflake ecosystem

### Architecture Principles

#### Separation of Concerns

* **KAI Instance:** Handles semantic indexing and retrieval
* **KAI Document Compagnon:** Handles conflict detection and content generation
* **Client Systems:** Handle user experience and response generation

#### API-First Design

* All integrations via REST API
* No proprietary protocols or dependencies
* Standard authentication and authorization
* Easy integration with existing systems

#### Stateless Operations

* API calls are stateless
* No session management required
* Horizontal scaling without state synchronization
* Resilient to individual component failures

### Monitoring & Observability

#### What KAI Monitors

* **API Performance:** Response times and throughput
* **Indexing Status:** Document processing progress
* **System Health:** Instance availability and resource usage
* **Query Patterns:** Usage analytics (anonymized)

#### What Clients Can Monitor

* **API Usage:** Track API calls and consumption
* **Indexing Status:** Monitor document indexing progress
* **Alert History:** Review conflict and gap detections
* **Performance Metrics:** Query response times

### Integration Best Practices

#### Document Repository Integration

1. **Use Read-Only Access:** KAI only needs read access to documents
2. **API Credentials:** Use dedicated service accounts with minimal permissions
3. **Incremental Updates:** Enable change detection for efficient updates
4. **Error Handling:** Implement retry logic for transient failures

#### AI System Integration

1. **Query Forwarding:** Forward user queries to KAI Document Compagnon
2. **Async Processing:** Handle alerts and recommendations asynchronously
3. **Rate Limiting:** Respect API rate limits for optimal performance
4. **Error Handling:** Gracefully handle API errors without impacting user experience

### Next Steps

#### For Technical Teams

* **Review integration requirements** for your document repositories
* **Plan API integration** with your AI search system
* **Understand deployment model** that fits your needs (SaaS, on-prem, Snowflake)
* [**Contact us** to discuss specific architecture questions](https://k-ai.ai/contact/)

#### For Business Teams

* **Understand the value** of semantic understanding for your AI system
* **See how KAI Document Compagnon** can improve your knowledge base
* [**Schedule a demo** to see the architecture in action](https://k-ai.ai/contact/)

_KAI Architecture - Enterprise-grade security, performance, and scalability._
