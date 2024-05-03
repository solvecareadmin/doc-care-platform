---
description: >-
  This section describes the overall network information and settings in the
  input.json file.
---

# Network configuration

### Network metadata

<table><thead><tr><th width="213">Field Name</th><th width="174">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>network_id</td><td>string</td><td>The unique ID assigned to the network.</td></tr><tr><td>node_url</td><td>string</td><td>The unique node URL for the network.</td></tr><tr><td>version</td><td>string</td><td>The unique name of the network.</td></tr><tr><td>description</td><td>number</td><td>The short description about the network.</td></tr><tr><td>publish_date</td><td>string</td><td>The publish date of the network protocol.</td></tr><tr><td>effective_date</td><td>string</td><td>The effective date when the protocol is applied to the network.</td></tr></tbody></table>

### Network settings

<table><thead><tr><th width="212">Field Name</th><th width="172">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>author_name</td><td>string</td><td>The name of the author (entity or person).</td></tr><tr><td>author_website</td><td>string</td><td>The website URL of the author.</td></tr><tr><td>author_address1</td><td>string</td><td>The address of the author (line1).</td></tr><tr><td>author_address2</td><td>string</td><td>The address of the author (line2).</td></tr><tr><td>geo_fence_countries</td><td>string</td><td>The list of countries that can join the network.</td></tr></tbody></table>

#### Code example

```json
{
    "care_protocol": {
        "network_id": "dev-network-xxx",
        "node_url": "https://site000.abc.net",
        "name": "My Network",
        "version": 1,
        "description": "This is a sample network.",
        "publish_date": "2024-03-27",
        "effective_date": "2024-03-27",
        "network_settings": {
            "author_details": {
                "author_name": "",
                "author_address1": "",
                "author_website": "",
                "author_address2": ""
            },
            "geo_fence_countries": [
                "US",
                "IN",
                "UA"
            ]
        },
        
```

### Join network settings

<table><thead><tr><th width="211">Field Name</th><th width="169">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>role</td><td></td><td></td></tr><tr><td>join_method</td><td></td><td></td></tr><tr><td>required_consents</td><td></td><td></td></tr><tr><td>terms_and_conditions_checksum</td><td></td><td></td></tr></tbody></table>

#### Code example

```json
            "join_network_settings": {
                "join_roles": [
                    {
                        "role": "rl-aom7t1oc6laj7k353ysvldm0gbk",
                        "join_method": "DEFAULT",
                        "required_consents": [
                            "WALLET",
                            "PHONE"
                        ],
                        "terms_and_conditions_checksum": "ca641043260d33f8df25d480e1b5932d"
                    },
```

### Solve token settings

| Field Name | Value Type | Description |
| ---------- | ---------- | ----------- |
|            |            |             |
|            |            |             |
|            |            |             |

#### Code example

```
// Some code
```
