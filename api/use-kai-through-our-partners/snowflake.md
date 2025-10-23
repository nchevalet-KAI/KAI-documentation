---
icon: snowflake
---

# Snowflake

Our application is available on Snowflake Marketplace.

Here some technical and guide details to help you to use us through Snowflake.

### Technical requirements

#### Large language model

Currently we use these models :&#x20;

* Claude-3-7-sonnet
* openai-gpt-4.1
* snowflake-artic-embed-1-v2.0

You need to activate these models before installing KAI app.

#### Warehouse

We use [multi-cluster warehouses](https://docs.snowflake.com/en/user-guide/warehouses-multicluster) to optimize speed of our application. To activate it, you need to have an enterprise edition snowflake account.

#### External Access Integration

When you deploy KAI app, before activate it, you need to add a reference to an external access integration. On the references part of the app, accept the creation of an [external access integration.](https://docs.snowflake.com/en/developer-guide/external-network-access/creating-using-external-network-access)

This [external access integration](https://docs.snowflake.com/en/developer-guide/external-network-access/creating-using-external-network-access) will allow to the KAI app to call your knowledge base through API.

### Deploy KAI app

#### Grant all privileges and references

You should grant all privileges and references, here why we asking these privileges and references :

* BIND SERVICE ENDPOINT : Allow us to expose our API (Ingress)
* CREATE COMPUTE POOL : Allow us to create machines to host our application
* CREATE WAREHOUSE : Need to generate related datas (semantic graphs, audit, ...) for each KAI instances you create.
* CREATE DATABASE : All datas generated will be stored into a specific database on your Snowflake account.
* IMPORTED PRIVILEGES ON SNOWFLAKE DB: Allow us to use Cortex API (LLM call).
* (USAGE) EXTERNAL ACCESS INTEGRATION: Allow us to call your knowledge base once you configured it (egress).

#### Activate the application

When you click on activate the KAI application, the deployment script will :

* create a new database "KAI\_APP"
* create a warehouse&#x20;
* create 2 compute pools
* deploy the admin UI interface

Once the admin UI interface is deployed, you can go on it and deploy your first KAI Instance.

### Connect a knowledge base to KAI app

Generally, steps to connect a knowledge base to KAI app is :

* prepare credentials needed by KAI to connect the knowledge base. Take a look [here](https://k-ai.gitbook.io/knowledge-ai/api/knowledge-base) to know how to retrieve these credentials following the type of knowledge base you want to connect.
* Fill these credentials into KAI admin UI when you configure the knowledge base.
* (Optional) Fill the search goal, it will help to contextualize a bit more about your use case.
* Add mentioned hosts on the external access integration of the KAI app (you can have the name of the external access integration on the snowflake admin page of the KAI app on the tab "references").
  * method 1 : [SQL MODE](https://docs.snowflake.com/en/sql-reference/sql/alter-external-access-integration)
  * method 2 : [UI MODE](https://docs.snowflake.com/en/developer-guide/external-network-access/creating-using-external-network-access)
* Wait 10s and validate it on the KAI admin UI (waiting 10s is important to be sure the propagation of updated hosts on the EAI is effective).
