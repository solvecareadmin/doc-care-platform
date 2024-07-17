# Publishing the protocol

{% hint style="info" %}
Use Postman to perform the steps for publishing. To get the authorization and environment details, contact [care.support@solve.care](mailto:care.support@solve.care)_._
{% endhint %}

## Fetch MainNet authorization token

Initiate a request with the appropriate details for your environment.

<mark style="color:orange;">**POST**</mark>

{% code overflow="wrap" %}
```
https://{{abc-care-env}}/core-registry-service/oauth/token?grant_type=password&username=%2B{{networkAuthorPhone}}&password={{networkAuthorPassword}}&blockchainAddress={{networkAuthorWalletId}}
```
{% endcode %}

Pre-request script:

{% code title="Example:" %}
```javascript
pm.globals.set("abc-care-env", "dev.env.abc.net");
pm.globals.set("xxx-env", "site000.abc.net/sample-net");


pm.globals.set("networkAuthorPhone", "91888888888");
pm.globals.set("networkAuthorWalletId", "0xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx");
pm.globals.set("networkAuthorPassword", "999999");
pm.globals.set("networkId", "dev-network-xxx");
```
{% endcode %}

## Fetch network authorization token

<mark style="color:orange;">**POST**</mark>

{% code overflow="wrap" %}
```
https://{{eks-env}}/nom/oauth/token?grant_type=exchange_token&exchange_token={{networkAuthorMainNetToken}}
```
{% endcode %}

## Get sponsor address

<mark style="color:green;">**GET**</mark>

```url
https://{{eks-env}}/nom/v2/holders/me
```

Post-request script:

{% code title="Example:" overflow="wrap" %}
```javascript
const jsonData = pm.response.json().nodes;
const networkId = pm.globals.get("networkId");
const node = jsonData.filter(r => r.networkId === networkId && r.roleId === 'NETWORK_SPONSOR')[0];
pm.globals.set("sponsorWalletAddress", node.scAddress);
```
{% endcode %}

## Upload the protocol package

<mark style="color:orange;">**POST**</mark>

{% code overflow="wrap" %}
```url
https://{{eks-env}}/generic-protocol-service/v2/packaging/{{networkId}}/restore/zip
```
{% endcode %}

## Publish the protocol package

<mark style="color:orange;">**POST**</mark>

{% code overflow="wrap" %}
```url
https://{{eks-env}}/generic-protocol-service/v2/packaging/{{networkId}}/publish
```
{% endcode %}

{% code title="Example:" overflow="wrap" %}
```bash
curl --location --globoff 'https://{{eks-env}}/generic-protocol-service/v2/packaging/{{networkId}}/publish' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{networkAuthorCANToken}}' \
--data '{
    "certificates":"CERT-12345-2022",
    "effectiveDate": "20-05-2022",
    "sponsorWalletAddress": "{{sponsorWalletAddress}}"
    
    

}'
```
{% endcode %}

## Get publishing state

<mark style="color:green;">**GET**</mark>

```
https://{{eks-env}}/generic-protocol-service/v2/packaging/{{networkId}}/{{networkVersion}}
```

{% code title="Example:" overflow="wrap" %}
```bash
curl --location --globoff 'https://{{eks-env}}/generic-protocol-service/v2/packaging/{{networkId}}/{{networkVersion}}' \
--header 'Authorization: Bearer {{networkAuthorCANToken}}'
```
{% endcode %}

## Update CDN

Upload the CSV file with the same attributes as the uploaded DDF in the input folder of the Amazon S3 bucket. If necessary, delete existing data.

### Uploading data definition file (DDF)

The data definition file contains the model and structure for organizing data in CDN.

<mark style="color:orange;">**POST**</mark>

{% code overflow="wrap" %}
```url
https://{{eks-env}}/{{network-id}}/data-node/v1/ddf
```
{% endcode %}

{% code title="Example:" %}
```bash
curl --location 'https://data-node/v1/ddf?status=ACTIVE' \
--header 'Authorization: Basic Y2FyZS1iYWNrZW5kOnNlY3JldA==' \
--header 'Content-Type: application/json' \
--data '{
    "ddf_type": "us-doctors-sample",
    "meta_data": {
        "description": "Sample"
    },
    "messages": [
        {
            "message_category": "CSV",
            "message_type": "Doctors",
            "meta_data": {
                "description": "Sample",
                "indices": "us-doctors-sample"
            },
            "events": [
                {
                    "to_role": "rl-patient",
                    "event": "ev-cdn-broadcast"
                }
            ],
            "attributes": [
                {
                    "name": "Provider",
                    "description": "Provider",
                    "required": false,
                    "index_field": true,
                    "type": "integer",
                    "data_location": "Provider"
                },
                {
                    "name": "License",
                    "description": "License",
                    "required": false,
                    "index_field": true,
                    "type": "string",
                    "data_location": "License"
                },
                {
                    "name": "Specialization",
                    "description": "Specialization",
                    "required": false,
                    "index_field": true,
                    "type": "string",
                    "data_location": "Specialization"
                },
                {
                    "name": "Address",
                    "description": "Address",
                    "required": false,
                    "index_field": true,
                    "type": "string",
                    "data_location": "Address"
                }
            ]
        }
    ]
}'
```
{% endcode %}

### Searching data

<mark style="color:orange;">**POST**</mark>

```
https://{{eks-env}}/{{network-id}}/elasticsearch/us-doctors-sample/_search
```

{% code title="Example:" %}
```bash
curl --location 'https://elasticsearch/us-doctors-sample/_search' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ZWxhc3RpYzpweFkwMXNQTXMyZTRTdFp3M2U1MjU5N3U=' \
--data '{

"query": {

"match_all": {}

}

}'
```
{% endcode %}

### Deleting existing data from CDN

<mark style="color:orange;">**POST**</mark>

```
https://{{eks-env}}/{{network-id}}/elasticsearch/us-doctors-sample/_delete_by_query
```

{% code title="Example:" %}
```bash
curl --location 'https://{{eks-env}}/{{network-id}}/elasticsearch/us-doctors-sample/_delete_by_query' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ZWxhc3RpYzpweFkwMXNQTXMyZTRTdFp3M2U1MjU5N3U=' \
--data '{

"query": {

"match_all": {}

}

}'
```
{% endcode %}

### Checking the count

<mark style="color:orange;">**POST**</mark>

```
https://{{eks-env}}/{{network-id}}/elasticsearch/us-doctors-sample/_count
```

{% code title="Example:" %}
```bash
curl --location --globoff 'https://{{eks-env}}/{{network-id}}/elasticsearch/us-doctors-sample/_count' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ZWxhc3RpYzo5UlBJMTMzNFNydHBOMzI1NFNRcjd4clI=' \
--data '{

"query": {

"match_all": {}

}

}'
```
{% endcode %}

