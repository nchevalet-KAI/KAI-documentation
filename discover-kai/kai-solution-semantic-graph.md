---
icon: globe-pointer
---

# KAI Solution : Semantic graph

When KAI is deployed and connected on your knowledge base, a semantic graph is automatically produced from all of your KB's documents.

KAI Semantic Graph is produced automatically when we index all of your documents. Each documents is converted as a sub semantic graph and this one is merge with the global semantic graph attached to your KAI Instance.

KAI Semantic Graph is the core of our technology, our Search and Audit module use only the KAI Semantic Graph.

If you want to create application who use directly our semantic graph to have the ability to exploit knowledge from your databases, you are at the right place.

**Some examples of technical use cases**

#### Improve RAG accuracy

When a user ask a query, usually, you will vectorize his query and find the nearest document's chunks following his query. After that, you will ask to the LLM to generate an answer following the user query and retrieved chunks.

The problem is, at this stage, you will lose document's contexts which brings hallucination (when you retrieve document chunks who, contextually, don't have to be used to generate the answer) or uncomplete answer (when you don't retrieve good document's chunks who has to be used to generate the answer).&#x20;

With KAI, you can use our endpoint ([/api/semantic-graph/identify-nodes](https://documenter.getpostman.com/view/30765019/2s9YXcek45#7fcf3cee-611c-4429-ac3e-31c8fc29f100)) to retrieve the semantic context for the user query following your databases and use it jointly with your retrieved chunks. You will pass in your LLM the user query, retrieved semantic nodes from our API and your retrieved document's chunks. In this case, the answer generated will be improved by the semantic context from your knowledge base following the user query and you will obtain a better accuracy.

#### Have an conceptual overview of your knowledge base

For metrics, you want to know exactly all subjects covered by your knowledge base and you want to know for one subject, which documents is involved.

You can use this endpoint ([/api/semantic-graph/nodes](https://documenter.getpostman.com/view/30765019/2s9YXcek45#811547e7-b9b0-4299-b3f1-2d9eb5e17cf9)) to retrieve all semantic nodes of KAI Semantic graph and build on top a graph based representation of your knowledge.









