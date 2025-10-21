---
icon: snowflake
---

# Snowflake

Our application is available on Snowflake Marketplace.

Here some technical and guide details to help you to use us through Snowflake.

### Technical requirements

#### Large language model

Currently we use 2 models :&#x20;

* Claude 3.5 sonnet
* snowflake-artic-embed-1-v2.0

You need to activate these models before installing KAI app.

#### Warehouse

We use [multi-cluster warehouses](https://docs.snowflake.com/en/user-guide/warehouses-multicluster) to optimize speed of our application. To activate it, you need to have an enterprise edition snowflake account.

### Connect a knowledge base to KAI app

An [external access integration](https://docs.snowflake.com/en/developer-guide/external-network-access/creating-using-external-network-access) is automatically (after you grant it) created when you deploy KAI App. It will be used to call your [knowledge base](https://k-ai.gitbook.io/knowledge-ai/api/knowledge-base) through their respective API.&#x20;

Generally, steps to connect a knowledge base to KAI app is :

* prepare credentials needed by KAI to connect the knowledge base. Take a look [here](https://k-ai.gitbook.io/knowledge-ai/api/knowledge-base) to know how to retrieve these credentials following the type of knowledge base you want to connect.
* Fill these credentials into KAI admin UI when you configure the knowledge base.
* Fill the search goal, it will help to contextualize a bit more about your use case.
* Add mentioned hosts on the external access integration of the KAI app.
* Wait 10s and validate it on the KAI admin UI.
