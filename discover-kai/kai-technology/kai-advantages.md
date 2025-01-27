---
icon: microchip
---

# KAI Technology advantages

### Why KAI solution compared to other RAG based solutions ?

KAI's Neural Semantic Graph provides a sophisticated, context-preserving method for document processing compared to RAG. It excels in semantic slicing, content vectorization, and document indexing, ensuring that semantic connections are maintained throughout. Unlike basic vectorization in RAG, KAI offers enhanced search capabilities and document cleansing, minimizing errors and providing a more reliable foundation for knowledge mining and retrieval.

<table data-full-width="true"><thead><tr><th width="160"></th><th width="354">KAI's Neural Semantic Graph</th><th>RAG</th></tr></thead><tbody><tr><td>Document Slicing</td><td>Semantic slicing - slicing based on document creation logic. <br><strong>=> Semantic meaning intact.</strong></td><td>Basic, arbitrary chunking. <br>=> Loss of meaning.</td></tr><tr><td>Document Analysis</td><td>Automatic detection of concepts and themes. Content vectorization. Generated meta. <br><strong>⇒ Keeps semantic context.</strong></td><td>Basic vectorization. Embedding <br>=> Loss of context.</td></tr><tr><td>Document Indexing</td><td>Creation of the semantic graph, following concepts and themes. <br><strong>=> Creation of global semantic context.</strong></td><td>Pooling of raw vectors. <br>=> No semantic links between documents.</td></tr><tr><td>User Search</td><td>Analysis of search via semantic graph. Retrieval of the right documents. <br><strong>=> Generation of contextualized response.</strong></td><td>Retrieval of the chunks that are closest to the user's query. <br>=> Generation of answers with chunks, possibility of increased hallucinations.</td></tr><tr><td>Document Cleansing</td><td>Use of semantic graph to detect contradictory documents with respect to themes and concepts.</td><td>Not Applicable</td></tr><tr><td>Knowledge Mining</td><td>Via prompt factory + Semantic graph</td><td>Not Applicable</td></tr></tbody></table>

> For more details, have a check on the Semantic Graph page [kai-solution-semantic-graph.md](../kai-solution-semantic-graph.md "mention")
