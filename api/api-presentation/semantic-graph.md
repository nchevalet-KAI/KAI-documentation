# SEMANTIC GRAPH

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

