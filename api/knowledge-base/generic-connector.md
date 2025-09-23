---
description: Connect KAI to any kind of Knowledge Base through our generic connector
---

# Generic connector

If you have build an internal knowledge base system, you can easely connect this to KAI following or generic connector.

The generic connector work like a proxy to serve your documents.

<figure><img src="../../.gitbook/assets/Capture d’écran 2025-09-23 à 14.26.30.png" alt=""><figcaption></figcaption></figure>

The Generic Connector Proxy App is a tiny application you have to develop following this requirements.

### Authentification requirements

The Generic Connector is created to be with a machine to machine flow. To secure the Generic Connector, we will use an apikey.

Each request made by KAI will have an apikey in the header. Your application have to check and validate the request only if the header "api-key" is present and valid following your system security.

### Technical implementation

#### Concept

The backend system of KAI is a pipeline who take as input documents. Idea of the Generic Connector is to transform each element as a document. You can ingest textual elements (pure text or html) but also documents (pdf, docx, pptx, xlsx, ...).

A document in output have to be formalized like that :&#x20;

* id
  * **format**: string
  * **description**: unique id of the document following your knowledge base
* title
  * **format**: string&#x20;
  * **description**: name of the document
* url
  * **format**: string
  * **description**: url to redirect the user on the document (on your knowledge base) if he want to consult the document
* type\_content
  * **format**: "text" | [MimeType](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types)
  * **description**: the content type of the document. If text it means the content of the document will be in the "content" attribute as text; If [MimeType](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types), it means the attribute "content" will contain the content of the document in base64.
* content
  * **format**: text or base64
  * **description**: if the "type\_content" is set to "text", the "content" attribute will contain the content of the document in pure text as a string. If the "type\_content" is a [MimeType](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types), the "content" attribute will contain the document in base64 format.
* updated\_on
  * **format**: string
  * **description**: An attribute to know when is the last update of the document. This field will help to know if the document have to be reindexed because he has changed. Can be a date in string or a tag.
* attachments
  * **format**: List of Attachment&#x20;
  * **description**: A list of attachments linked to the document

An attachment have to be formalized like that :&#x20;

* base64
  * **format**: base64/string
  * **description**: the base64 of the content of the attachment file
* mime\_type
  * **format**: [MimeType](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types)
  * **description**: the mime type of the attachment file

#### Endpoints to implement

You have 3 endpoints to implement to make it work&#x20;

## List all documents

<mark style="color:green;">`POST`</mark> `/documents`

List all documents with a pagination system. Don't add attachments and content attributes here.

**Headers**

| Name         | Value              |
| ------------ | ------------------ |
| Content-Type | `application/json` |
| api-key      | `your_apikey`      |

**Body**

| Name     | Type   | Description                                                     |
| -------- | ------ | --------------------------------------------------------------- |
| `limit`  | number | the number of documents retrieved                               |
| `offset` | number | how many documents to skipp before starting to return documents |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "response": [
    {
      "id": "doc_1",
      "title": "first document",
      "url": "https://my-knowledgebase.co/xxx",
      "type_content": "text",
      "updated_on": "2023-01-01 00:00:00"
    },
    {
      "id": "doc_2",
      "title": "second document.pdf",
      "url": "https://my-knowledgebase.co/yyy",
      "type_content": "application/pdf",
      "updated_on": "2024-04-03 00:00:00"
    }
  ]
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

## Retrieve one specific document

<mark style="color:green;">`POST`</mark> `/document/:id`

Retrieve a specific document by his ID with his content (will be used to retrieve the document and index it)

**Headers**

| Name         | Value              |
| ------------ | ------------------ |
| Content-Type | `application/json` |
| api-key      | `your_apikey`      |

**Endpoint parameters**

| Name | Type   | Description            |
| ---- | ------ | ---------------------- |
| `id` | string | The id of the document |

**Response**

{% tabs %}
{% tab title="200 (for a document with text content)" %}
```json
{
  "response": {
    "id": "doc_1",
    "title": "first document",
    "url": "https://my-knowledgebase.co/xxx",
    "type_content": "text",
    "content":"Lorem ipsum...",
    "updated_on": "2023-01-01 00:00:00",
    "attachments": [
      {
        "base64": "JZakfdi0xLjQKJcTl8uXrp/Og0MTGCjEgMCBvYmoKPDwg...",
        "mime_type": "image/png"
      }
    ]
  }
}
```
{% endtab %}

{% tab title="200 (for a document based on a real document)" %}
```json
{
    "response": {
      "id": "doc_2",
      "title": "second document.pdf",
      "url": "https://my-knowledgebase.co/yyy",
      "type_content": "application/pdf",
      "content": "JVBERi0xLjQKJcTl8uXrp/Og0MTGCjEgMCBvYmoKPDwg...",
      "updated_on": "2024-04-03 00:00:00",
      "attachments": []
    }
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

## Count total number of documents available

<mark style="color:green;">`POST`</mark> `/count`

Retrieve the number of available documents to index on KAI.

**Headers**

| Name         | Value              |
| ------------ | ------------------ |
| Content-Type | `application/json` |
| api-key      | `your_apikey`      |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "response": 20000
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

Informations to fill on KAI studio to connect your knowledge base with your KAI instance :&#x20;

* name : The name you want to give to this connection between KAI and your Generic Connector
* host : the host of your Generic Connector. ex : https://my\_connector\_url&#x20;
* passkey : the api-key you want to KAI use when it call the Generic Connector

