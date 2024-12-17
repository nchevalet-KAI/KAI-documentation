---
icon: square-exclamation
---

# FAQs

### Basic questions

<details>

<summary>How do we install the tool ? </summary>

* It's a middleware, we plug to your architecture and knowledge bases and you connect to our AI through APIs.
* We have an API with the documentation of the endpoints availables, several SDKs on Github to install it easily ( Python, Typescript, PHP ) and templates examples (React, Vue)&#x20;

</details>



### Audit Module

<details>

<summary>What is detected / managed ?  </summary>

It's like a taskboard, in "detected" state, it lists all detected conflicts to check, you edit documents on your side, and the "managed" status will regenerate the indexation of the documents mentioned.&#x20;

</details>

* Which knowledge bases are compatible with your solution ? &#x20;
  * We can plug on multiple knowledge bases :  SharePoint, Drive, Confluence, Notion, …&#x20;
* What is the duration of the indexation ? &#x20;
  * It depends on your documents, the types, the size, .. it can takes few minutes to few days for biggest bases.&#x20;
* How do we manage the tables, charts, complex presentations or data.&#x20;
  * Our algorithm is based on 2 bricks : &#x20;
    * Our file parsers, which read and translate all your data into readable texts. &#x20;
    * Our homemade semantic graph generator. &#x20;
* Is your algorithms are open / public or proprietary ? &#x20;
  * We have developed our proprietary solution, escpecially adapted to business contexts. &#x20;
* How is the solution deployed?&#x20;
  * We deploy on SAAS or On-premise. In a POC case, we favor the SAAS solution.&#x20;
* Can you provide more details on your architecture ? &#x20;
  * For the AI part, except our homemade personalized algorithm, we also use various LLM ( GPT 4-o, Sonnet 3.5,..). We are agnostic and can use other LLM on-demand according to your specific context.&#x20;
  * We use Kubernetes to orchestrate and manage the scalable and automated deployment of our containerized solution.&#x20;
  * We can provide more explanation on demand.&#x20;
