# KAI

## Project: KAI

## 📁 Collection: Introduction

## 📁 Collection: Endpoints

### End-point: /api/semantic-graph/nodes

This endpoint retrieves information about semantic relationships between different concepts (nodes) in a graph. The response is an array of objects, where each object represents a relationship between two nodes. Each object contains the following fields:

* id: The unique identifier for the relationship.
* node\_1: The first concept or entity in the relationship.
* node\_2: The second concept or entity in the relationship.
* edge: A textual description that explains the relationship between node\_1 and node\_2.

#### Method: POST

> ```
> {{host}}/api/semantic-graph/nodes
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "limit": 20,
    "offset": 0
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 1,
            "node_1": "Plantes",
            "node_2": "Boite",
            "edge": "Les plantes doivent être expédiées dans une boite\nUn dessin de fleur doit être réalisé sur le dessus du colis"
        },
        {
            "id": 2,
            "node_1": "Dessin de fleur",
            "node_2": "Livreur",
            "edge": "Le dessin de fleur permet au livreur de connaître le sens du colis lors de la livraison"
        },
        {
            "id": 3,
            "node_1": "Colis",
            "node_2": "Supplément",
            "edge": "\nThe key terms \"Colis\" and \"Supplément\" are closely related in the provided text. The text discusses various aspects of packaging and shipping colis (packages/parcels), including:\n\n- Packaging requirements for different types of items (e.g. plants, seeds, luxury watches)\n- Size and weight limitations for colis\n- Labeling and addressing requirements for colis\n- Availability of shipping labels and how to obtain them\n- Pickup and delivery options for colis\n- Insurance coverage and options for declaring higher value for colis\n\nThe text also mentions that a \"supplément\" (additional fee) of 10 euros will be charged for each colis containing flowers.\n"
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/semantic-graph/linked-nodes

Retrieve all relations and edges linked to the nodes of a given relationship. You can check details in 2 request examples.

#### Method: POST

> ```
> {{host}}/api/semantic-graph/linked-nodes
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "id": 3
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 39,
            "node_1": "Colis",
            "node_2": "Restrictions de poids",
            "edge": "Packages must not weigh more than 70 kg\nPackage length must not exceed 274 cm; .........",
            "count": 4,
            "documents": [
                "Sharepoint::01Y3GAAY7QA3xxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAY2RQWxxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAY6MYUxxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAYZAWOxxxxxxxxxxxxxxxxxxx"
            ]
        },
        {
            "id": 55,
            "node_1": "Colis",
            "node_2": "Perdu",
            "edge": "Un colis est considéré comme perdu s'il n'a pas été livré 24 heures après .......",
            "count": 1,
            "documents": [
                "Sharepoint::01Y3GAAY2RQWLxxxxxxxxxxxxxxxxxxx"
            ]
        },
        {
            "id": 81,
            "node_1": "Conducteur UPS",
            "node_2": "Colis",
            "edge": "The UPS driver picks up or delivers the package\nUPS Access Point ..........",
            "count": 1,
            "documents": [
                "Sharepoint::01Y3GAAY6CJWZLJxxxxxxxxxxxxxxxxxxx"
            ]
        },
        {
            "id": 93,
            "node_1": "Client",
            "node_2": "Colis",
            "edge": "The client is the recipient of the package\nLes documents .......",
            "count": 2,
            "documents": [
                "Sharepoint::01Y3GAAY6CJWZxxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAY2RQWLxxxxxxxxxxxxxxxxxxx"
            ]
        }
    ]
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 175,
            "node_1": "Contact",
            "node_2": "Service client",
            "edge": "Le contact principal mentionné est le service client",
            "count": 1,
            "documents": [
                "Sharepoint::01Y3GAAYZXCSOZME2JVJF2E74MTJONYKLG"
            ]
        },
        {
            "id": 22,
            "node_1": "Horaires",
            "node_2": "Jours de semaine",
            "edge": "Service hours are different for weekdays (Monday to Friday)\nService hours are different for Saturday",
            "count": 1,
            "documents": [
                "Sharepoint::01Y3GAAYYWAQDJ6IXGB5F3N424OFPFCCOE"
            ]
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/semantic-graph/nodes-by-label

List all Nodes where the mentioned Node is present. The input « label » must be the exact name of the node\_1 or node\_2.

#### Method: POST

> ```
> {{host}}/api/semantic-graph/nodes-by-label
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "label": "UPS"
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 26,
            "node_1": "UPS",
            "node_2": "United Parcel Service Belgium SA",
            "edge": "UPS is represented by United Parcel Service Belgium SA in Belgium\nUPS is represented by United Parcel Service SARL in Luxembourg\nUPS a ........",
            "count": 3,
            "documents": [
                "Sharepoint::01Y3GAAY7QA3HMMxxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAY2WJJSYHxxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAYZAWOE2Lxxxxxxxxxxxxxxxxxxx"
            ]
        },
        {
            "id": 46,
            "node_1": "UPS",
            "node_2": "Articles interdits",
            "edge": "UPS interdit l'envoi de certains ........",
            "count": 3,
            "documents": [
                "Sharepoint::01Y3GAAY5OMOxxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAY7QA3xxxxxxxxxxxxxxxxxxx",
                "Sharepoint::01Y3GAAYZU6Jxxxxxxxxxxxxxxxxxxx"
            ]
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/semantic-graph/identify-nodes

Identify nodes who can be used to defined the semantic context of the query. It will return all nodes that are semantically similar to the search query.

#### Method: POST

> ```
> {{host}}/api/semantic-graph/identify-nodes
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "query": "United Parcel Service"
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 31,
            "node_1": "UPS",
            "node_2": "Sous-traitants",
            "edge": "\nThe key information found in the extracted texts is:\n\n1. UPS is a logistics and delivery company that provides transportation services for packages, documents, and palletized goods. UPS operates through various subsidiaries in different countries, such as United Parcel Service Belgium SA, United Parcel Service France SAS, and United Parcel Service SARL in Luxembourg.\n\n2. UPS utilizes subcontractors to provide its services and can contract in its own name as well as on behalf of its employees, agents, and subcontractors, all of whom benefit from the terms and conditions.\n\n3. The transportation services provided by UPS may be subject to international conventions such as the Warsaw Convention or the CMR Convention, which can govern and limit the liability of transportation companies for loss, damage, or delay of goods.\n\n4. UPS has the right to charge late payment fees, interest, and administrative costs if the shipper, recipient, or any other party responsible for the transportation costs fails to pay the amounts due. UPS can also retain or sell the shipment to recover the unpaid debt.\n\n5. UPS is not liable for its inability to commence or continue the transport of a shipment due to events beyond its control, such as transportation disruptions, government actions, or other force majeure events.\n",
            "count": 2,
            "documents": [
                "Sharepoint::01Y3GAAY7QA3HMMIUEIVGLWNL276LLQWMX",
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5"
            ]
        },
        {
            "id": 26,
            "node_1": "UPS",
            "node_2": "United Parcel Service Belgium SA",
            "edge": "UPS is represented by United Parcel Service Belgium SA in Belgium\nUPS is represented by United Parcel Service SARL in Luxembourg\nUPS a établi des limites de poids et de taille spécifiques pour les colis\nUPS is represented by United Parcel Service Belgium SA in Belgium\nUPS is represented by United Parcel Service SARL in Luxembourg",
            "count": 3,
            "documents": [
                "Sharepoint::01Y3GAAY7QA3HMMIUEIVGLWNL276LLQWMX",
                "Sharepoint::01Y3GAAY2WJJSYHJAYTFBLXEQTPSCDGJUO",
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5"
            ]
        },
        {
            "id": 209,
            "node_1": "UPS",
            "node_2": "Refund Guarantee",
            "edge": "UPS offers a refund guarantee on shipping costs for certain services and destinations\nDetails of the refund guarantee are available on the UPS website\nUPS Customer Service can confirm details about the refund guarantee",
            "count": 1,
            "documents": [
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5"
            ]
        },
        {
            "id": 210,
            "node_1": "UPS",
            "node_2": "COD Service",
            "edge": "UPS offers a Cash on Delivery (COD) service\nUPS offers Cash on Delivery (COD) service, collecting payment from the recipient and transferring it to the sender\nUPS's liability for collecting COD amounts is limited to the lowest of three amounts: the COD amount, the maximum authorized amount, or the actual value of the goods",
            "count": 1,
            "documents": [
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5"
            ]
        },
        {
            "id": 7,
            "node_1": "UPS",
            "node_2": "France",
            "edge": "\nThe key information found in the given text is:\n\n1. UPS is a shipping and logistics company that provides transportation services in France.\n2. The text outlines the general terms and conditions for UPS transportation services, including:\n   - Restrictions on package size, weight, and value\n   - Prohibited items that cannot be shipped\n   - Applicability of international transportation conventions like the Warsaw Convention and CMR Convention\n   - UPS's use of subcontractors and ability to route shipments through transit points\n   - Grouping of shipments from different senders\n3. The text also covers UPS's cash on delivery (COD) service, including:\n   - Maximum COD amount per recipient per day\n   - Acceptance of checks in the destination country's currency\n   - UPS's process for paying the COD amount to the shipper\n   - Shipper's responsibility for losses or claims related to undelivered COD shipments\n   - Limitation of UPS's liability for COD collections\n\nUPS is used for shipping within France, with a delivery time of 24 hours.\nFor shipping within France using UPS Access Point, the cost is 10 euros for orders below 250 euros and free for orders above 250 euros. The delivery time is 24 hours.\nFor shipping within France using UPS, the cost is 25 euros for orders below 250 euros. The delivery time is 24 hours.",
            "count": 3,
            "documents": [
                "Sharepoint::01Y3GAAY7QA3HMMIUEIVGLWNL276LLQWMX",
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5",
                "Sharepoint::01Y3GAAYZFEMBZ5L3H25BIHL7EOG737VES"
            ]
        },
        {
            "id": 23,
            "node_1": "UPS",
            "node_2": "Conditions Générales de Transport",
            "edge": "UPS establishes Conditions Générales de Transport for shipping packages, documents, and envelopes\nThe Conditions Générales de Transport are complemented by the Guide des Services et Tarifs UPS 2024\nUPS forms a contract with the Expéditeur for shipping services\nA single shipping note or waybill issued by UPS\nLe conducteur UPS indique généralement l'endroit où le colis a été déposé\nUPS establishes Conditions Générales de Transport for shipping packages, documents, and envelopes\nThe Guide des Services UPS 2024 complements the Conditions Générales de Transport\nUPS se réserve le droit de refuser le transport de certains articles\nUPS pourrait ne pas contrôler les entrées et sorties des envois individuels de tous les centres de manutention.\nUPS peut refuser de transporter un envoi qui ne respecte pas les restrictions ou conditions spécifiées.\nUPS peut suspendre le transport d'un envoi qui ne respecte pas les conditions ou en cas de problèmes de livraison.\nUPS peut suspendre le transport s'il ne parvient pas à effectuer la livraison pour diverses raisons.\nUPS n'est pas tenu de suspendre le transport d'un colis sauf exceptions prévues\nUPS n'est pas tenu de rediriger la livraison vers un autre destinataire ou une autre adresse\nUPS n'est pas tenu de renvoyer un colis à son expéditeur",
            "count": 4,
            "documents": [
                "Sharepoint::01Y3GAAY7QA3HMMIUEIVGLWNL276LLQWMX",
                "Sharepoint::01Y3GAAY2RQWLGIFAHAZE3VWMZ6PWAQDXU",
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5",
                "Sharepoint::01Y3GAAYZU6J7BO2XJCFA2P27T6XSK63BO"
            ]
        },
        {
            "id": 76,
            "node_1": "UPS",
            "node_2": "Droit de rétention",
            "edge": "UPS peut garder tout envoi qu'il transporte jusqu'à la réception du paiement intégral si une somme n'est pas payée\nUPS peut vendre un envoi et utiliser le produit de la vente pour se rembourser de la dette correspondante\nUPS n'offre pas de manutention spéciale pour certains types d'envois.\nUPS peut facturer des frais de stockage en cas de problèmes avec l'envoi.\nUPS peut encourir des taxes et droits de douane que l'expéditeur devra rembourser en cas de problèmes avec l'envoi.\nUPS peut être tenu de payer des taxes, droits ou impôts pour le compte de l'expéditeur, du destinataire ou d'un tiers\nUPS demandera d'abord le paiement des montants concernés au destinataire et/ou au tiers avant de se tourner vers l'expéditeur\nUPS a une responsabilité limitée pour les envois, régie par les conditions énoncées dans le document\nUPS a le droit de traiter les données personnelles fournies par l'expéditeur ou le destinataire dans le cadre du transport\nLa responsabilité d'UPS pour violation des règles de traitement des données est limitée conformément au paragraphe 9-5\nLes réclamations contre UPS doivent être signifiées par écrit dans des délais spécifiques",
            "count": 2,
            "documents": [
                "Sharepoint::01Y3GAAY7QA3HMMIUEIVGLWNL276LLQWMX",
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5"
            ]
        },
        {
            "id": 51,
            "node_1": "UPS",
            "node_2": "Options de paiement",
            "edge": "UPS offre plusieurs options de paiement pour les envois\nPayPal est l'une des options de paiement disponibles pour les envois UPS\nUPS a le droit d'imputer des frais de retard de paiement avec un maximum de 40 EUR (43 CHF en Suisse) par facture\nUPS a le droit d'imputer des frais de retard de paiement jusqu'à 40 EUR (43 CHF en Suisse)\nUPS peut garder l'envoi jusqu'à la réception du paiement intégral ou le vendre pour se rembourser\nUPS may accept checks for COD, which can be in euros or the destination country's currency",
            "count": 3,
            "documents": [
                "Sharepoint::01Y3GAAY44O44H3BHWHVE2W55I4PJ4IA5R",
                "Sharepoint::01Y3GAAY7QA3HMMIUEIVGLWNL276LLQWMX",
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5"
            ]
        },
        {
            "id": 241,
            "node_1": "UPS",
            "node_2": "Guide",
            "edge": "Le Guide et ce document constituent l'intégralité du contrat entre UPS et l'expéditeur",
            "count": 1,
            "documents": [
                "Sharepoint::01Y3GAAYZAWOE2LVGZCFFKFGGHUKYFVLC5"
            ]
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/orchestrator/stats/count-detected-documents

get number of detected documents

#### Method: POST

> ```
> {{host}}/api/orchestrator/stats/count-detected-documents
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": 20
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/orchestrator/stats/count-documents

get number of documents analyzed

#### Method: POST

> ```
> {{host}}/api/orchestrator/stats/count-documents
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": 6
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/orchestrator/stats/count-indexable-documents

get number of indexable document

#### Method: POST

> ```
> {{host}}/api/orchestrator/stats/count-indexable-documents
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": 0
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/orchestrator/stats/count-indexed-documents

get number of indexed documents

#### Method: POST

> ```
> {{host}}/api/orchestrator/stats/count-indexed-documents
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": 20
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/orchestrator/list-docs

list indexed documents

#### Method: POST

> ```
> {{host}}/api/orchestrator/list-docs
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": [
        {
            "id": "Sharepoint::01Y3GAAYxxxxxxxxxx",
            "name": "Note pour XXXXXXXXX.docx"
        },
        {
            "id": "Sharepoint::01Y3GAAYxxxxxxxxxx",
            "name": "DOC 8 APRES XXXXXXXX.docx"
        },
        {
            "id": "Sharepoint::01Y3GAAYxxxxxxxxxx",
            "name": "DOC 1 Emballage XXXXXXX.docx"
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: api/orchestrator/files/download

download file from your knowledge base.

#### Method: POST

> ```
> {{host}}/api/orchestrator/files/download
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "id": "{{documentId}}"
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/orchestrator/differential-indexation

Index only new/updated/removed documents. It ensures that the documents are updated and their indexing reflects the latest modifications. (in progress, not finish)

#### Method: POST

> ```
> {{host}}/api/orchestrator/differential-indexation
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /global-health

It returns global server running stats.

#### Method: POST

> ```
> {{host}}/global-health
> ```

#### Headers

| Content-Type | Value                                                                                                                        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Accept       | text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,_/_;q=0.8,application/signed-exchange;v=b3;q=0.7 |

#### Headers

| Content-Type    | Value                                                                |
| --------------- | -------------------------------------------------------------------- |
| Accept-Language | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,fr-FR;q=0.6,fr;q=0.5,en-GB;q=0.4 |

#### Headers

| Content-Type  | Value    |
| ------------- | -------- |
| Cache-Control | no-cache |

#### Headers

| Content-Type | Value      |
| ------------ | ---------- |
| Connection   | keep-alive |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| DNT          | 1     |

#### Headers

| Content-Type | Value    |
| ------------ | -------- |
| Pragma       | no-cache |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Dest | document |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Mode | navigate |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-Site | none  |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-User | ?1    |

#### Headers

| Content-Type              | Value |
| ------------------------- | ----- |
| Upgrade-Insecure-Requests | 1     |

#### Headers

| Content-Type | Value                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| User-Agent   | Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.69 |

#### Headers

| Content-Type | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| sec-ch-ua    | "Chromium";v="118", "Microsoft Edge";v="118", "Not=A?Brand";v="99" |

#### Headers

| Content-Type     | Value |
| ---------------- | ----- |
| sec-ch-ua-mobile | ?0    |

#### Headers

| Content-Type       | Value   |
| ------------------ | ------- |
| sec-ch-ua-platform | "macOS" |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| sec-gpc      | 1     |

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
```

#### Response: 200

```json
{
    "response": "OK"
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /health

It returns the running status of the instance and api.

#### Method: POST

> ```
> {{host}}/health
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": "OK"
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /version

get version of service kai-api

#### Method: POST

> ```
> {{host}}/version
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": "20240529"
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/audit/conflict-information

Obtain conflict information in your knowledge base when two documents contain similar information with differences that may cause interpretation issues.

#### Method: POST

> ```
> {{host}}/api/audit/conflict-information
> ```

#### Headers

| Content-Type    | Value                                                                |
| --------------- | -------------------------------------------------------------------- |
| Accept-Language | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,fr-FR;q=0.6,fr;q=0.5,en-GB;q=0.4 |

#### Headers

| Content-Type  | Value    |
| ------------- | -------- |
| Cache-Control | no-cache |

#### Headers

| Content-Type | Value      |
| ------------ | ---------- |
| Connection   | keep-alive |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| DNT          | 1     |

#### Headers

| Content-Type | Value    |
| ------------ | -------- |
| Pragma       | no-cache |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Dest | document |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Mode | navigate |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-Site | none  |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-User | ?1    |

#### Headers

| Content-Type              | Value |
| ------------------------- | ----- |
| Upgrade-Insecure-Requests | 1     |

#### Headers

| Content-Type | Value                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| User-Agent   | Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.69 |

#### Headers

| Content-Type | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| sec-ch-ua    | "Chromium";v="118", "Microsoft Edge";v="118", "Not=A?Brand";v="99" |

#### Headers

| Content-Type     | Value |
| ---------------- | ----- |
| sec-ch-ua-mobile | ?0    |

#### Headers

| Content-Type       | Value   |
| ------------------ | ------- |
| sec-ch-ua-platform | "macOS" |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| sec-gpc      | 1     |

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "limit": 20,
    "offset": 0
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 2,
            "subject": "Valeur maximale xxxxxxxxx",
            "state": "DETECTED",
            "creation_date": "2024-09-16T13:48:15.651Z",
            "documents": [
                {
                    "docId": "Sharepoint::01Y3xxxxxxxxxxx",
                    "information_involved": "la valeur xxxxxxxxxxx"
                },
                {
                    "docId": "Sharepoint::01Y3GAxxxxxxxxxx",
                    "information_involved": "Il n'est pas nécessaire de nous xxxxxxxxxxxx"
                }
            ],
            "docsRef": [
                {
                    "id": "Sharepoint::01Y3xxxxxxxxxxx",
                    "name": "Complément produit rares.docx",
                    "url": "https://xxxxxxxxxxxxxxxxxxxxxxx.xxxxxxxxxxxxxx.xxxxxxxxxxxxxxxx"
                },
                {
                    "id": "Sharepoint::01Y3GAxxxxxxxxxx",
                    "name": "DOC 4 Assurances.docx",
                    "url": "https://xxxxxxxxxxxxxxxxxxxxxxx.xxxxxxxxxxxxxx.xxxxxxxxxxxxxxxx"
                }
            ]
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/audit/duplicated-information

Get similar information in your knowledge base.

#### Method: POST

> ```
> {{host}}/api/audit/duplicated-information
> ```

#### Headers

| Content-Type | Value                                                                                                                        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Accept       | text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,_/_;q=0.8,application/signed-exchange;v=b3;q=0.7 |

#### Headers

| Content-Type    | Value                                                                |
| --------------- | -------------------------------------------------------------------- |
| Accept-Language | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,fr-FR;q=0.6,fr;q=0.5,en-GB;q=0.4 |

#### Headers

| Content-Type  | Value    |
| ------------- | -------- |
| Cache-Control | no-cache |

#### Headers

| Content-Type | Value      |
| ------------ | ---------- |
| Connection   | keep-alive |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| DNT          | 1     |

#### Headers

| Content-Type | Value    |
| ------------ | -------- |
| Pragma       | no-cache |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Dest | document |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Mode | navigate |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-Site | none  |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-User | ?1    |

#### Headers

| Content-Type              | Value |
| ------------------------- | ----- |
| Upgrade-Insecure-Requests | 1     |

#### Headers

| Content-Type | Value                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| User-Agent   | Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.69 |

#### Headers

| Content-Type | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| sec-ch-ua    | "Chromium";v="118", "Microsoft Edge";v="118", "Not=A?Brand";v="99" |

#### Headers

| Content-Type     | Value |
| ---------------- | ----- |
| sec-ch-ua-mobile | ?0    |

#### Headers

| Content-Type       | Value   |
| ------------------ | ------- |
| sec-ch-ua-platform | "macOS" |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| sec-gpc      | 1     |

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "limit": 20,
    "offset": 0
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 2,
            "subject": "Payment options",
            "state": "DETECTED",
            "creation_date": "2024-09-16T13:48:07.222Z",
            "documents": [
                {
                    "docId": "Sharepoint::01Y3GAAY44O44Hxxxxxxxxxxx",
                    "information_involved": "Plusieurs options de xxxxxxxxxxxx"
                },
                {
                    "docId": "Sharepoint::01Y3GAAY7QA3Hxxxxxxxxxxxxxx",
                    "information_involved": "Si le destinataire xxxxxxxxxxxxxxxxx"
                }
            ],
            "docsRef": [
                {
                    "id": "Sharepoint::01Y3GAAY44O44Hxxxxxxxxxxx",
                    "name": "DIVERS.docx",
                    "url": "xxxxxxxxxxxxxxxxxxxxxxxxx"
                },
                {
                    "id": "Sharepoint::01Y3GAAY7QA3Hxxxxxxxxxxxxxx",
                    "name": "DOC 5 PAIEMENT.docx",
                    "url": "xxxxxxxxxxxxxxxxxxxxxxxxx"
                }
            ]
        },
        {
            "id": 7,
            "subject": "Couverture de base pour les pertes ou dommages jusqu'à 85€",
            "state": "DETECTED",
            "creation_date": "2024-09-16T13:48:23.736Z",
            "documents": [
                {
                    "docId": "Sharepoint::01Y3GAAYZQ3xxxxxxxxxx",
                    "information_involved": "Votre envoi bénéficie xxxxxxxxxxxx"
                },
                {
                    "docId": "Sharepoint::01Y3GAAYxxxxxxxxxxxx",
                    "information_involved": "En tout état de cause, xxxxxxxxxxxxxx"
                }
            ],
            "docsRef": [
                {
                    "id": "Sharepoint::01Y3GAAYZQ3xxxxxxxxxx",
                    "name": "DIVERS.docx",
                    "url": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
                },
                {
                    "id": "Sharepoint::01Y3GAAYxxxxxxxxxxxx",
                    "name": "DOC 4 Assurances.docx",
                    "url": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
                }
            ]
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/audit/conflict-information/set-managed

set the state to managed for a conflict information.

#### Method: POST

> ```
> {{host}}/api/audit/conflict-information/set-managed
> ```

#### Headers

| Content-Type | Value                                                                                                                        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Accept       | text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,_/_;q=0.8,application/signed-exchange;v=b3;q=0.7 |

#### Headers

| Content-Type    | Value                                                                |
| --------------- | -------------------------------------------------------------------- |
| Accept-Language | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,fr-FR;q=0.6,fr;q=0.5,en-GB;q=0.4 |

#### Headers

| Content-Type  | Value    |
| ------------- | -------- |
| Cache-Control | no-cache |

#### Headers

| Content-Type | Value      |
| ------------ | ---------- |
| Connection   | keep-alive |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| DNT          | 1     |

#### Headers

| Content-Type | Value    |
| ------------ | -------- |
| Pragma       | no-cache |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Dest | document |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Mode | navigate |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-Site | none  |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-User | ?1    |

#### Headers

| Content-Type              | Value |
| ------------------------- | ----- |
| Upgrade-Insecure-Requests | 1     |

#### Headers

| Content-Type | Value                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| User-Agent   | Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.69 |

#### Headers

| Content-Type | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| sec-ch-ua    | "Chromium";v="118", "Microsoft Edge";v="118", "Not=A?Brand";v="99" |

#### Headers

| Content-Type     | Value |
| ---------------- | ----- |
| sec-ch-ua-mobile | ?0    |

#### Headers

| Content-Type       | Value   |
| ------------------ | ------- |
| sec-ch-ua-platform | "macOS" |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| sec-gpc      | 1     |

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "id": 2
}
```

#### Response: 200

```json
{
    "response": {
        "id": 2,
        "subject": "Valeur maximale des montres dans un colis",
        "documents": [
            {
                "docId": "Sharepoint::01Y3GAAYZQ3Oxxxxxxxxxxx",
                "information_involved": "la valeur xxxxxxxxxxxxxx"
            },
            {
                "docId": "Sharepoint::01Y3GAAYZxxxxxxxxxxxxxxx",
                "information_involved": "Il n'est pas xxxxxxxxxxxxxxxxx"
            }
        ],
        "state": "MANAGED",
        "creation_date": "2024-09-16T13:48:15.651Z"
    }
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/audit/duplicated-information/set-managed

set the state to managed for a duplicated information

#### Method: POST

> ```
> {{host}}/api/audit/duplicated-information/set-managed
> ```

#### Headers

| Content-Type | Value                                                                                                                        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Accept       | text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,_/_;q=0.8,application/signed-exchange;v=b3;q=0.7 |

#### Headers

| Content-Type    | Value                                                                |
| --------------- | -------------------------------------------------------------------- |
| Accept-Language | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,fr-FR;q=0.6,fr;q=0.5,en-GB;q=0.4 |

#### Headers

| Content-Type  | Value    |
| ------------- | -------- |
| Cache-Control | no-cache |

#### Headers

| Content-Type | Value      |
| ------------ | ---------- |
| Connection   | keep-alive |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| DNT          | 1     |

#### Headers

| Content-Type | Value    |
| ------------ | -------- |
| Pragma       | no-cache |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Dest | document |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Mode | navigate |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-Site | none  |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-User | ?1    |

#### Headers

| Content-Type              | Value |
| ------------------------- | ----- |
| Upgrade-Insecure-Requests | 1     |

#### Headers

| Content-Type | Value                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| User-Agent   | Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.69 |

#### Headers

| Content-Type | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| sec-ch-ua    | "Chromium";v="118", "Microsoft Edge";v="118", "Not=A?Brand";v="99" |

#### Headers

| Content-Type     | Value |
| ---------------- | ----- |
| sec-ch-ua-mobile | ?0    |

#### Headers

| Content-Type       | Value   |
| ------------------ | ------- |
| sec-ch-ua-platform | "macOS" |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| sec-gpc      | 1     |

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "id": 2
}
```

#### Response: 200

```json
{
    "response": {
        "id": 2,
        "subject": "Payment options",
        "documents": [
            {
                "docId": "Sharepoint::01Y3GAAY44xxxxxxxxxR",
                "information_involved": "Plusieurs options xxxxxxxxxxxxxx"
            },
            {
                "docId": "Sharepoint::01Y3GAAY7QA3HMMIUExxxxxxxxxxx",
                "information_involved": "Si le destinataire xxxxxxxxxxxxxxxxxxx"
            }
        ],
        "state": "MANAGED",
        "creation_date": "2024-09-16T13:48:07.222Z"
    }
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/audit/documents-to-manage

list of all documents who contain conflict or duplicated information.

Conflict or duplicated information have 2 state: 'DETECTED' or 'MANAGED'

#### Method: POST

> ```
> {{host}}/api/audit/documents-to-manage
> ```

#### Headers

| Content-Type | Value                                                                                                                        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Accept       | text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,_/_;q=0.8,application/signed-exchange;v=b3;q=0.7 |

#### Headers

| Content-Type    | Value                                                                |
| --------------- | -------------------------------------------------------------------- |
| Accept-Language | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,fr-FR;q=0.6,fr;q=0.5,en-GB;q=0.4 |

#### Headers

| Content-Type  | Value    |
| ------------- | -------- |
| Cache-Control | no-cache |

#### Headers

| Content-Type | Value      |
| ------------ | ---------- |
| Connection   | keep-alive |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| DNT          | 1     |

#### Headers

| Content-Type | Value    |
| ------------ | -------- |
| Pragma       | no-cache |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Dest | document |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Mode | navigate |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-Site | none  |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-User | ?1    |

#### Headers

| Content-Type              | Value |
| ------------------------- | ----- |
| Upgrade-Insecure-Requests | 1     |

#### Headers

| Content-Type | Value                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| User-Agent   | Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.69 |

#### Headers

| Content-Type | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| sec-ch-ua    | "Chromium";v="118", "Microsoft Edge";v="118", "Not=A?Brand";v="99" |

#### Headers

| Content-Type     | Value |
| ---------------- | ----- |
| sec-ch-ua-mobile | ?0    |

#### Headers

| Content-Type       | Value   |
| ------------------ | ------- |
| sec-ch-ua-platform | "macOS" |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| sec-gpc      | 1     |

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "limit": 20,
    "offset": 0
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": "Azure Blob Storage::xxxx::e-Alerte Generalisation Facturation Electronique.pdf",
            "name": "e-Alerte Generalisation Facturation Electronique.pdf",
            "url": "/api/orchestrator/files/download?id=Azure%20Blob%20Storage%3A%3Axxxx%3A%3Ae-Alerte%20Generalisation%20Facturation%20Electronique.pdf"
        },
        {
            "id": "Azure Blob Storage::xxxx::Facturation lectronique entre entreprises pour les TPE-PME - francenum.gouv.pdf",
            "name": "Facturation lectronique entre entreprises pour les TPE-PME - francenum.gouv.pdf",
            "url": "/api/orchestrator/files/download?id=Azure%20Blob%20Storage%3A%3Axxxx%3A%3AFacturation%20lectronique%20entre%20entreprises%20pour%20les%20TPE-PME%20-%20francenum.gouv.pdf"
        },
        {
            "id": "Azure Blob Storage::xxxx::faq_fe_v30122021.pdf",
            "name": "faq_fe_v30122021.pdf",
            "url": "/api/orchestrator/files/download?id=Azure%20Blob%20Storage%3A%3Axxxx%3A%3Afaq_fe_v30122021.pdf"
        },
        {
            "id": "Azure Blob Storage::d4930e91-44fd-435a-bb33-d621af415f35::github-git-cheat-sheet_copy.pdf",
            "name": "github-git-cheat-sheet_copy.pdf",
            "url": "/api/orchestrator/files/download?id=Azure%20Blob%20Storage%3A%3Ad4930e91-44fd-435a-bb33-d621af415f35%3A%3Agithub-git-cheat-sheet_copy.pdf"
        },
        {
            "id": "Azure Blob Storage::d4930e91-44fd-435a-bb33-d621af415f35::github-git-cheat-sheet.pdf",
            "name": "github-git-cheat-sheet.pdf",
            "url": "/api/orchestrator/files/download?id=Azure%20Blob%20Storage%3A%3Ad4930e91-44fd-435a-bb33-d621af415f35%3A%3Agithub-git-cheat-sheet.pdf"
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/audit/missing-subjects

List all missing subjects following user queries

#### Method: POST

> ```
> {{host}}/api/audit/missing-subjects
> ```

#### Headers

| Content-Type | Value                                                                                                                        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Accept       | text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,_/_;q=0.8,application/signed-exchange;v=b3;q=0.7 |

#### Headers

| Content-Type    | Value                                                                |
| --------------- | -------------------------------------------------------------------- |
| Accept-Language | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,fr-FR;q=0.6,fr;q=0.5,en-GB;q=0.4 |

#### Headers

| Content-Type  | Value    |
| ------------- | -------- |
| Cache-Control | no-cache |

#### Headers

| Content-Type | Value      |
| ------------ | ---------- |
| Connection   | keep-alive |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| DNT          | 1     |

#### Headers

| Content-Type | Value    |
| ------------ | -------- |
| Pragma       | no-cache |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Dest | document |

#### Headers

| Content-Type   | Value    |
| -------------- | -------- |
| Sec-Fetch-Mode | navigate |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-Site | none  |

#### Headers

| Content-Type   | Value |
| -------------- | ----- |
| Sec-Fetch-User | ?1    |

#### Headers

| Content-Type              | Value |
| ------------------------- | ----- |
| Upgrade-Insecure-Requests | 1     |

#### Headers

| Content-Type | Value                                                                                                                                     |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| User-Agent   | Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_15\_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.69 |

#### Headers

| Content-Type | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| sec-ch-ua    | "Chromium";v="118", "Microsoft Edge";v="118", "Not=A?Brand";v="99" |

#### Headers

| Content-Type     | Value |
| ---------------- | ----- |
| sec-ch-ua-mobile | ?0    |

#### Headers

| Content-Type       | Value   |
| ------------------ | ------- |
| sec-ch-ua-platform | "macOS" |

#### Headers

| Content-Type | Value |
| ------------ | ----- |
| sec-gpc      | 1     |

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "limit": 20,
    "offset": 0
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 1,
            "subject": "Shipping Costs",
            "questions": [
                "combien me coûte l'envoie d'un colis de 45 m3 en angleterre ?"
            ],
            "information_needed": "- Inquiry about the cost of sending a large volume package (45 m3) to England."
        },
        {
            "id": 2,
            "subject": "Logistics",
            "questions": [
                "combien me coûte l'envoie d'un colis de 45 000 m3 en angleterre ?"
            ],
            "information_needed": "Concern related to the logistics of transporting a large volume of goods."
        },
        {
            "id": 34,
            "subject": "Envoi de colis",
            "questions": [
                "quel est le prix pour envoyer un colis de 45000 cm3 en angleterre ?"
            ],
            "information_needed": "- Inquiry about the cost of shipping a 45000 cm3 package to England.\n- Procedure for sending a 45000 cm3 package to England."
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/search/query

search question and get an answer with different paramters,

\>query: query to search on the semantic index\
\>user: (optional) user identifier to log for this query\
\>impersonate: name a profile to imitate the style of answer. eg: Knowledge manager\
\>multiDocuments: true if you want to search across multiple documents, false if you want to retrieve an answer following only one document

\>needFollowingQuestions: true if you want to the API purpose multiple next questions, else false

You can check details in 2 request examples.

#### Method: POST

> ```
> {{host}}/api/search/query
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "query": "what is UPS delivery time in France ?",
    "user": "userid",
    "impersonate": "",
    "multiDocuments": false,
    "needFollowingQuestions": false
}
```

#### Response: 200

```json
{
    "response": {
        "query": "what is UPS delivery time in France ?",
        "answer": "Le délai de livraison UPS en France est de 24 heures pour les envois nationaux, que ce soit avec le service standard UPS ou UPS Access Point.",
        "reason": "Le document fournit des informations explicites sur les délais de livraison UPS en France. Il indique de manière cohérente que pour le service UPS standard et le service UPS Access Point, le délai de livraison pour les envois en France est de 24 heures.",
        "confidentRate": 0.95,
        "gotAnswer": true,
        "documents": [
            {
                "id": "Sharepoint::01Y3GAAYZFEMxxxxxxxxxxxx",
                "name": "COMPARAISON.docx",
                "url": "xxxxxxxxxxxxxxxxxxxxxxxxxx"
            }
        ],
        "followingQuestions": []
    }
}
```

#### Response: 200

```json
{
    "response": {
        "query": "what is the price to send a 45m3 package in China?",
        "answer": "",
        "reason": "The provided documents only contain shipping prices for France, EU countries, UK and US destinations. There is no information about shipping prices for packages in China.",
        "confidentRate": 0,
        "gotAnswer": false,
        "documents": [],
        "followingQuestions": []
    }
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/search/identify-specific-document

Identify a concise question following the user needs and documents from knowledge base. If in the return 'isFinal' is true, the correct question is found and you can get correct question in 'question' field. If 'isFinal' is false, you can get AI proposed question in 'question' field.

#### Method: POST

> ```
> {{host}}/api/search/identify-specific-document
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "conversation": [
        {
            "from": "user",
            "message": "Tell me somme information about UPS"
        }
    ]
}
```

#### Response: 200

```json
{
    "response": {
        "isFinal": true,
        "question": "What information does the UPS 2024 Service Guide for France provide?"
    }
}
```

#### Response: 200

```json
{
    "response": {
        "isFinal": false,
        "question": "Pouvez-vous préciser ce que vous cherchez à savoir sur la commande SSH ?"
    }
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/search/stats/list-search

History of searches performed since the beginning in ascending order. A pagination system can be created with the offset value, limit per query value.

#### Method: POST

> ```
> {{host}}/api/search/stats/list-search
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "limit": 20,
    "offset": 0
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": 1,
            "query": "Note pour l’ivoire",
            "answer_text": "La note pour l'ivoire est un message d'avertissement sur un colis. Le message, écrit en français, indique que le colis peut contenir de l'ivoire et doit être manipulé avec précaution. Cette information est représentée visuellement par une icône de colis.",
            "user_id": ""
        },
        {
            "id": 2,
            "query": "quelles sont les heures d'ouverture du service client ?",
            "answer_text": "Selon nos documents, il y a deux informations différentes concernant les heures d'ouverture du service client :\n\n1. Une source indique que le service client est disponible de 8h à 21h du lundi au vendredi, et fermé le samedi.\n\n2. Une autre source mentionne des horaires différents : du lundi au vendredi de 8h00 à 19h00, et le samedi de 8h00 à 13h00.\n\nEn raison de cette discordance, il serait préférable de contacter directement le service client pour obtenir les horaires les plus à jour.",
            "user_id": ""
        },
        {
            "id": 3,
            "query": "quelles sont les heures d'ouverture du service client ?",
            "answer_text": "Selon nos documents, il y a deux informations différentes concernant les heures d'ouverture du service client :\n\n1. Une source indique que le service client est disponible de 8h à 21h du lundi au vendredi, et fermé le samedi.\n\n2. Une autre source mentionne des horaires différents : du lundi au vendredi de 8h00 à 19h00, et le samedi de 8h00 à 13h00.\n\nEn raison de cette discordance, il serait préférable de contacter directement le service client pour obtenir les horaires les plus à jour.",
            "user_id": ""
        },
        {
            "id": 4,
            "query": "quelles sont les heures d'ouverture du service client ?",
            "answer_text": "Selon nos documents, il y a deux informations différentes concernant les heures d'ouverture du service client :\n\n1. Une source indique que le service client est disponible de 8h à 21h du lundi au vendredi, et fermé le samedi.\n\n2. Une autre source mentionne des horaires différents : du lundi au vendredi de 8h00 à 19h00, et le samedi de 8h00 à 13h00.\n\nEn raison de cette discordance, il serait préférable de contacter directement le service client pour obtenir les horaires les plus à jour.",
            "user_id": ""
        },
        {
            "id": 5,
            "query": "quelles sont les heures d'ouverture du service client ?",
            "answer_text": "Selon nos documents, il y a deux informations différentes concernant les heures d'ouverture du service client :\n\n1. Une source indique que le service client est disponible de 8h à 21h du lundi au vendredi, et fermé le samedi.\n\n2. Une autre source mentionne des horaires différents : du lundi au vendredi de 8h00 à 19h00, et le samedi de 8h00 à 13h00.\n\nEn raison de cette discordance, il serait préférable de contacter directement le service client pour obtenir les horaires les plus à jour.",
            "user_id": ""
        },
        {
            "id": 6,
            "query": "quelles sont les heures d'ouverture du service client ?",
            "answer_text": "Selon nos documents, il y a deux informations différentes concernant les heures d'ouverture du service client :\n\n1. Une source indique que le service client est disponible de 8h à 21h du lundi au vendredi, et fermé le samedi.\n\n2. Une autre source mentionne des horaires différents : du lundi au vendredi de 8h00 à 19h00, et le samedi de 8h00 à 13h00.\n\nEn raison de cette discordance, il serait préférable de contacter directement le service client pour obtenir les horaires les plus à jour.",
            "user_id": ""
        },
        {
            "id": 7,
            "query": "Comment faire pour envoyer un colis de 45000 cm3 en angleterre ?",
            "answer_text": "Pour envoyer un colis de 45000 cm3 en Angleterre, suivez ces étapes :\n\n1. Assurez-vous que votre colis respecte les limites de taille et de poids :\n\n - Poids maximal : 70kg\n\n - Longueur maximale : 274 cm\n\n - Longueur + circonférence combinées : ne dépassant pas 400 cm\n\n2. Préparez une facture commerciale en trois exemplaires :\n\n - Un pour les douanes\n\n - Un pour le client\n\n - Un pour vous-même\n\n3. Emballez soigneusement votre colis et étiquetez-le correctement.\n\n4. Choisissez un service d'expédition approprié (UPS ou autre transporteur).\n\n5. Soyez prêt à payer les frais de dédouanement, car depuis le 1er janvier 2021, les envois entre l'UE et le Royaume-Uni sont soumis à un dédouanement.",
            "user_id": ""
        },
        {
            "id": 8,
            "query": "quelles sont les heures d'ouverture du service client ?",
            "answer_text": "Selon nos documents, il y a deux informations différentes concernant les heures d'ouverture du service client :\n\n1. Une source indique que le service client est disponible de 8h à 21h du lundi au vendredi, et fermé le samedi.\n\n2. Une autre source mentionne des horaires différents : du lundi au vendredi de 8h00 à 19h00, et le samedi de 8h00 à 13h00.\n\nEn raison de cette discordance, il serait préférable de contacter directement le service client pour obtenir les horaires les plus à jour.",
            "user_id": ""
        },
        {
            "id": 9,
            "query": "quelles sont les heures d'ouverture du service client ?",
            "answer_text": "Il y a des informations contradictoires concernant les heures d'ouverture du service client :\n\n1. Selon une source :\n\n - Du lundi au vendredi : de 8h à 21h\n\n - Fermé le samedi\n\n2. Selon une autre source :\n\n - Du lundi au vendredi : de 8h à 19h\n\n - Le samedi : de 8h à 13h\n\nEn raison de cette incohérence, il serait préférable de contacter directement le service client pour obtenir les horaires exacts et à jour.",
            "user_id": ""
        },
        {
            "id": 10,
            "query": "à quelle h le service client est ouvert ?",
            "answer_text": "Selon les informations disponibles, les horaires du service client sont les suivants :\n\n1. Une source indique :\n\n - Du lundi au vendredi : de 8h à 21h\n\n - Fermé le samedi\n\n2. Une autre source indique :\n\n - Du lundi au vendredi : de 8h00 à 19h00\n\n - Le samedi : de 8h00 à 13h00\n\nEn raison de cette différence, il est recommandé de vérifier les horaires les plus récents auprès du service client directement.",
            "user_id": ""
        },
        {
            "id": 11,
            "query": "Comment faire pour envoyer un colis de 45000 cm3 en angleterre ?",
            "answer_text": "Pour envoyer un colis de 45000 cm3 en Angleterre, voici les étapes à suivre :\n\n1. Vérifiez que votre colis respecte les limites de taille :\n\n - Le poids ne doit pas dépasser 70 kg\n\n - La longueur ne doit pas dépasser 274 cm\n\n - La longueur et la circonférence combinées ne doivent pas dépasser 400 cm\n\n2. Préparez une facture commerciale, car depuis le 1er janvier 2021, les envois vers le Royaume-Uni nécessitent un dédouanement. Vous aurez besoin de trois exemplaires imprimés de cette facture :\n\n - Un pour les douanes\n\n - Un pour le client\n\n - Un pour vous-même\n\n3. Emballez soigneusement votre colis et attachez-y l'étiquette d'expédition ainsi qu'un exemplaire de la facture commerciale.\n\n4. Placez un autre exemplaire de la facture commerciale à l'intérieur du colis pour votre client.\n\n5. Gardez le troisième exemplaire de la facture commerciale pour vos archives.\n\n6. Déposez votre colis dans un point de collecte UPS ou programmez un enlèvement.\n\nN'oubliez pas que des frais de douane et des taxes peuvent s'appliquer, qui seront généralement à la charge du destinataire.",
            "user_id": ""
        },
        {
            "id": 12,
            "query": "ca me coûte combien d'envoyer un colis de 45000 cm3 en angleterre ?",
            "answer_text": "D'après les informations fournies, l'envoi d'un colis de 45000 cm3 en Angleterre (Royaume-Uni) coûterait 26,9 €.\n\nCe prix correspond à la catégorie \"Moyen\" dans le tableau des tarifs, qui s'applique aux colis d'un volume maximal de 50 000 cm3.",
            "user_id": ""
        },
        {
            "id": 13,
            "query": "combien me coûte l'envoie d'un colis en angleterre ?",
            "answer_text": "Le coût d'envoi d'un colis en Angleterre (Royaume-Uni) varie en fonction de la taille du colis :\n\n- Très petit colis : 16€\n- Petit colis : 19€\n- Colis moyen : 26,9€\n- Grand colis : 32,6€\n- Très grand colis : 37,9€\n\nLe prix dépend donc de la taille de votre colis, allant de 16€ pour un très petit colis à 37,9€ pour un très grand colis.",
            "user_id": ""
        },
        {
            "id": 14,
            "query": "combien me coûte l'envoie d'un colis de 45 000 m3 en angleterre ?",
            "answer_text": null,
            "user_id": ""
        },
        {
            "id": 15,
            "query": "combien me coûte l'envoie d'un colis de 45 m3 en angleterre ?",
            "answer_text": null,
            "user_id": ""
        },
        {
            "id": 16,
            "query": "combien me coûte l'envoie d'un colis de 45 000 cm3 en angleterre ?",
            "answer_text": "Le coût d'envoi d'un colis de 45 000 cm3 en Angleterre est de 26,9 €. \n\nCependant, il est important de noter que depuis le 1er janvier 2021, les expéditions vers le Royaume-Uni nécessitent un dédouanement. Ce tarif pourrait donc ne pas inclure les frais de dédouanement potentiels.",
            "user_id": ""
        },
        {
            "id": 17,
            "query": "Comment faire pour envoyer un colis de 45000 cm3 en angleterre ?",
            "answer_text": "Pour envoyer un colis de 45000 cm3 en Angleterre, voici les étapes à suivre :\n\n1. Vérifiez que votre colis respecte les limites de taille :\n\n - Le poids ne doit pas dépasser 70 kg\n\n - La longueur ne doit pas dépasser 274 cm\n\n - La longueur et la circonférence combinées ne doivent pas dépasser 400 cm\n\n2. Préparez une facture commerciale, car depuis le 1er janvier 2021, les envois vers le Royaume-Uni nécessitent un dédouanement. Vous aurez besoin de trois exemplaires imprimés de cette facture :\n\n - Un pour les douanes\n\n - Un pour le client\n\n - Un pour vous-même\n\n3. Emballez soigneusement votre colis et attachez-y l'étiquette d'expédition ainsi qu'un exemplaire de la facture commerciale.\n\n4. Placez un autre exemplaire de la facture commerciale à l'intérieur du colis pour votre client.\n\n5. Gardez le troisième exemplaire de la facture commerciale pour vos archives.\n\n6. Déposez votre colis dans un point de collecte UPS ou programmez un enlèvement.\n\nN'oubliez pas que des frais de douane et des taxes peuvent s'appliquer, qui seront généralement à la charge du destinataire.",
            "user_id": ""
        },
        {
            "id": 18,
            "query": "combien coûte l'envoie un colis de 45000 cm3 en angleterre ?",
            "answer_text": "Le coût d'envoi d'un colis de 45000 cm3 en Angleterre est de 26,9 €.",
            "user_id": ""
        },
        {
            "id": 19,
            "query": "combien coûte l'envoie d'un colis de 45000 cm3 en angleterre ?",
            "answer_text": "Le coût d'envoi d'un colis de 45000 cm3 en Angleterre est de 26,9 €.",
            "user_id": ""
        },
        {
            "id": 20,
            "query": "coût pour envoyer un colis de 45 000 cm3 en angleterre",
            "answer_text": "Le coût pour envoyer un colis de 45 000 cm3 en Angleterre (Royaume-Uni) est de 26,9 €.\n\nCette taille de colis correspond à la catégorie \"Moyen\" dans le tableau des tarifs, qui comprend les colis jusqu'à 50 000 cm3.",
            "user_id": ""
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/search/stats/count-search

count number of call on search (/query) endpoint

#### Method: POST

> ```
> {{host}}/api/search/stats/count-search
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": 83
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/search/stats/count-answered-search

count number of call on search (/query) endpoint where KAI find an answer

#### Method: POST

> ```
> {{host}}/api/search/stats/count-answered-search
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Response: 200

```json
{
    "response": 80
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/search/docs

Retrieve the documents names and url locations of the documents based on the provided document IDs.

#### Method: POST

> ```
> {{host}}/api/search/docs
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "docsIds":
    [
        "{{documentId}}",
        "{{documentId2}}"
    ]
}
```

#### Response: 200

```json
{
    "response": [
        {
            "id": "Sharepoint::01Y3GAAYZ2L5MNAxxxxxxx",
            "name": "Complément produit rares.docx",
            "url": "https://xxxxxxxxxxx.xxxxxxxxx.xxxxxxxxxxx"
        },
        {
            "id": "Sharepoint::01Y3GAAYYWAQDJ6xxxxxxx",
            "name": "contact en image.pdf",
            "url": "https://xxxxxxxxxxx.xxxxxxxxx.xxxxxxxxxxx"
        }
    ]
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

### End-point: /api/search/doc

get back a document signature

#### Method: POST

> ```
> {{host}}/api/search/doc
> ```

#### Headers

| Content-Type | Value         |
| ------------ | ------------- |
| api-key      | \{{api-key\}} |

#### Headers

| Content-Type | Value             |
| ------------ | ----------------- |
| instance-id  | \{{instance-id\}} |

#### Body (**raw**)

```json
{
    "id": "{{documentId}}"
}
```

#### Response: 200

```json
{
    "response": {
        "name": "DOC 4 Assurances.docx",
        "url": "https://skillsolutionsoftware.sharepoint.com/sites/Skillbase-KAI/_layouts/15/Doc.aspx?sourcedoc=%7B6CA0DB30-C3F8-404D-82DF-C396F747176A%7D&file=DOC%204%20Assurances.docx&action=default&mobileredirect=true",
        "document": {
            "id": "Sharepoint::01Y3GAAYZQ3OQGZ6GDJVAIFX6DS33UOF3K",
            "name": "DOC 4 Assurances.docx",
            "extraproperties": {
                "id": "01Y3GAAYZQ3OQGZ6GDJVAIFX6DS33UOF3K",
                "cTag": "\"c:{6CA0DB30-C3F8-404D-82DF-C396F747176A},2\"",
                "eTag": "\"{6CA0DB30-C3F8-404D-82DF-C396F747176A},1\"",
                "file": {
                    "hashes": {
                        "quickXorHash": "S3IkNDfzFTntRKk90ttbIB2/PJw="
                    },
                    "mimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
                },
                "name": "DOC 4 Assurances.docx",
                "size": 21772,
                "shared": {
                    "scope": "users"
                },
                "webUrl": "https://skillsolutionsoftware.sharepoint.com/sites/Skillbase-KAI/_layouts/15/Doc.aspx?sourcedoc=%7B6CA0DB30-C3F8-404D-82DF-C396F747176A%7D&file=DOC%204%20Assurances.docx&action=default&mobileredirect=true",
                "createdBy": {
                    "user": {
                        "id": "7b51bc72-3609-4f5a-90dc-dc092bef6ef9",
                        "email": "sngo@wats.ai",
                        "displayName": "Stephane NGO"
                    }
                },
                "kb_signature": {
                    "name": "Skillbase-KAI::KAI/KAI DEMO V2 - Instances/LVMH DEMO",
                    "type": "SharepointKnowledgeBase"
                },
                "fileSystemInfo": {
                    "createdDateTime": "2024-06-07T15:08:17Z",
                    "lastModifiedDateTime": "2024-06-07T15:08:17Z"
                },
                "lastModifiedBy": {
                    "user": {
                        "id": "7b51bc72-3609-4f5a-90dc-dc092bef6ef9",
                        "email": "sngo@wats.ai",
                        "displayName": "Stephane NGO"
                    }
                },
                "createdDateTime": "2024-06-07T15:08:17Z",
                "parentReference": {
                    "id": "01Y3GAAYZ6BZX3D5FZRJEJXM454S3M6UEN",
                    "name": "LVMH DEMO",
                    "path": "/drives/b!GizPr4fHx0-m8l-A_iIpSRdsr1PHDJBBvgIFWrKoORA1hRhJ_-lnR7uaI0AYJTJp/root:/KAI/KAI DEMO V2 - Instances/LVMH DEMO",
                    "siteId": "afcf2c1a-c787-4fc7-a6f2-5f80fe222949",
                    "driveId": "b!GizPr4fHx0-m8l-A_iIpSRdsr1PHDJBBvgIFWrKoORA1hRhJ_-lnR7uaI0AYJTJp",
                    "driveType": "documentLibrary"
                },
                "lastModifiedDateTime": "2024-06-07T15:08:17Z",
                "@microsoft.graph.downloadUrl": "https://skillsolutionsoftware.sharepoint.com/sites/Skillbase-KAI/_layouts/15/download.aspx?UniqueId=6ca0db30-c3f8-404d-82df-c396f747176a&Translate=false&tempauth=v1.eyJzaXRlaWQiOiJhZmNmMmMxYS1jNzg3LTRmYzctYTZmMi01ZjgwZmUyMjI5NDkiLCJhcHBfZGlzcGxheW5hbWUiOiJhdWRpdC1rbSIsImF1ZCI6IjAwMDAwMDAzLTAwMDAtMGZmMS1jZTAwLTAwMDAwMDAwMDAwMC9za2lsbHNvbHV0aW9uc29mdHdhcmUuc2hhcmVwb2ludC5jb21AZmZiNzRlMzYtNTRjZC00YmJmLThhNDQtMDg3ZjU4YjJjMGQzIiwiZXhwIjoiMTcyNjQ5Nzc5OCJ9.CgoKBHNuaWQSAjY0EgsIuKK55fGXqz0QBRoNMjAuMTkwLjE3Ny4yNSosdjlRZTRZSW45TDNvcVpUM0Zlb0srbjN0dXc0ZnJaQTdpUXU3MWkyYUpEcz0wmAE4AUIQoVDT-kJQAJDhsAHFsZ2f4koQaGFzaGVkcHJvb2Z0b2tlbnoBMboBJmdyb3VwLnJlYWQgYWxsc2l0ZXMucmVhZCBhbGxmaWxlcy5yZWFkwgFJODQ4ZTVjNTEtZGExYS00NmU1LWJiM2ItNTQxN2JjYWYxYzc1QGZmYjc0ZTM2LTU0Y2QtNGJiZi04YTQ0LTA4N2Y1OGIyYzBkM8gBAQ.m2aA0M-ZcqhvH5GCROaZlDh6ypteCPmHxcHlaoWYo3k&ApiVersion=2.0"
            }
        }
    }
}
```

⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃ ⁃

## 📁 Collection: SDK

***

Powered By: [postman-to-markdown](https://github.com/bautistaj/postman-to-markdown/)
