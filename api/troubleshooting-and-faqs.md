---
icon: square-exclamation
---

# FAQs

### Basic questions

<details>

<summary>How do we install the tool ?</summary>

It's a middleware, we plug to your architecture and knowledge bases and you connect to our AI through APIs.&#x20;

We have an **API** with the [documentation](api-presentation.md) of the endpoints available, several **SDKs** on [Github](sdks.md) to install it easily ( Python, Typescript, PHP, Ruby ) and templates examples (React, Vue, Streamlit).

</details>

<details>

<summary>Which knowledge bases are compatible with your solution ?</summary>

We can plug on multiple knowledge bases : SharePoint, Drive, Confluence, Notion, Service Now,…

We can use the common connectors of the market, but also can connect on your in-house Knowledge base. In this case, we can check together the technical requirements.

</details>

<details>

<summary>What is the duration of the indexation ?</summary>

It depends on your documents, types, sizes, .. it can takes few minutes to few days for biggest bases.

</details>

<details>

<summary>How do we manage the tables, charts, complex presentations or data.</summary>

Our algorithm is based on 2 special bricks :&#x20;

* Our file parsers, which read and translate all your data into readable texts.  We will be able to read texts, tables and most of charts, graphs, diagrams,.. we can find in presentations.&#x20;

- Our homemade semantic graph generator. We translate non-text information into textual and linear information, human readable.

</details>

<details>

<summary>Which kind of document can you read ?</summary>

* We cover most current written formats: pdf, ppt, doc, text, excel, ..
* However, we do not cover the audio and video formats for the moment.

</details>

<details>

<summary>Is your algorithms are open / public or proprietary ?</summary>

We have developed our proprietary solution, especially adapted to business contexts.

</details>

<details>

<summary>How is the solution deployed?</summary>

We deploy on SAAS or On-premise. \
**In a POC case, we favor the SAAS solution.**

</details>

<details>

<summary>Can you provide more details on your architecture ?</summary>

* For the AI part, except our [homemade personalized algorithm](troubleshooting-and-faqs.md#how-do-we-manage-the-tables-charts-complex-presentations-or-data), we also use various LLM (GPT 4-o, Sonnet 3.5,..). We are agnostic and can use other LLM on-demand according to your specific context.
* We use Kubernetes to orchestrate and manage the scalable and automated deployment of our containerized solution.&#x20;
* We can provide more explanation on demand.

</details>

### Audit Module

<details>

<summary>What is detected / managed ?</summary>

It's like a taskboard, in "detected" state, it lists all detected conflicts to check, you edit documents on your side, and the "managed" status will regenerate the indexation of the documents mentioned.

</details>

<details>

<summary>What is missing subjects ?</summary>

We collect the queries from the search and chatbot modules, made by your users, and aggregate all the missing answers of our system due to a lack of information in your knowledge base.&#x20;

</details>

<details>

<summary>Can I check all anomalies, conflicts and duplicates in a given document ?</summary>

Yes, with the API endpoint : /documents-to-manage,  you will be able to get all the documents with a issue about a conflict or a duplication. Then, use the&#x20;

</details>



### Search Module

<details>

<summary>Can I get an answer including several sourced documents ?</summary>

Absolutely, in your parameters, with the API call, you just have to active the "multidocument" option to true. And the answer provided will be able to mention and mix several sources.

</details>

<details>

<summary>If I have many similar but potentially wrong informations in my knowledge base, what kind of answer we will get?</summary>

If the multidocument parameter is on true, the /query endpoint will retrieve all documents mentioning the information, without selecting one answer. It's up to you, to choose the correct one. It's also why, we advise to do an Audit before.&#x20;

If the multidocument parameter is on false, we will provide the most possible correct answer according to our algorithm, but it's possible to retrieve a bad/outdated answer.

</details>
