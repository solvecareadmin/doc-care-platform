---
description: >-
  This section describes the overall network specifications, including author
  details, countries, join network settings, and solve token settings.
---

# Network configuration

### Network metadata

<table><thead><tr><th width="213">Field Name</th><th width="174">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>network_id</td><td>string</td><td>The unique ID assigned to the network.</td></tr><tr><td>node_url</td><td>string</td><td>The unique node URL for the network.</td></tr><tr><td>version</td><td>number</td><td>The unique name of the network.</td></tr><tr><td>description</td><td>string</td><td>The short description about the network.</td></tr><tr><td>publish_date</td><td>string</td><td>The publish date of the network protocol.</td></tr><tr><td>effective_date</td><td>string</td><td>The effective date when the protocol is applied to the network.</td></tr></tbody></table>

{% code title="Example:" %}
```json
{
    "care_protocol": {
        "network_id": "dev-network-xxx",
        "node_url": "https://site000.abc.net",
        "name": "My Care Network",
        "version": 1,
        "description": "This is a sample care network.",
        "publish_date": "2024-03-27",
        "effective_date": "2024-03-27",
```
{% endcode %}

### Author details and countries

<table><thead><tr><th width="212">Field Name</th><th width="172">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>author_name</td><td>string</td><td>The name of the author (entity or person).</td></tr><tr><td>author_website</td><td>string</td><td>The website URL of the author.</td></tr><tr><td>author_address1</td><td>string</td><td>The address of the author (line1).</td></tr><tr><td>author_address2</td><td>string</td><td>The address of the author (line2).</td></tr><tr><td>geo_fence_countries</td><td>string</td><td>The list of countries that can join the network.</td></tr></tbody></table>

{% code title="Example:" %}
```json
        "network_settings": {
                    "author_details": {
                        "author_name": "John Carter",
                        "author_address1": "127 Goyette River, Lake Audreanne",
                        "author_website": "www.abc-company.net",
                        "author_address2": "Arizona"
                    },
                    "geo_fence_countries": [
                        "US",
                        "IN",
                        "UA"
                    ]
                },
```
{% endcode %}

### Join network settings

<table><thead><tr><th width="211">Field Name</th><th width="169">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>role</td><td>string</td><td>The ID of the role joining the network.</td></tr><tr><td>join_method</td><td>string</td><td>The method of joining the network.</td></tr><tr><td>required_consents</td><td>array</td><td>The cards which you allow other users in the network to access.</td></tr><tr><td>terms_and_conditions_checksum</td><td>string</td><td>The terms and conditions for joining the network.</td></tr></tbody></table>

{% code title="Example:" %}
```json
                    "join_network_settings": {
                      "join_roles": [
                        {
                          "role": "rl-patient",
                          "join_method": "DEFAULT",
                          "required_consents": ["WALLET", "PHONE"],
                          "terms_and_conditions_checksum": "d61c0c428b88a19c1d0b9e10dae816fe"
                        },
                        {
                          "role": "rl-doctor",
                          "join_method": "INVITE",
                          "required_consents": ["WALLET"],
                          "terms_and_conditions_checksum": "6dadacb7b61860d446c5ebdffcc2be54"
                        }
                      ]
                    },
```
{% endcode %}

### Solve token usage

<table><thead><tr><th width="205">Field Name</th><th width="150">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>deposit_value</td><td>string</td><td>The deposit value of SOLVE tokens.</td></tr><tr><td>redemption_value</td><td>string</td><td>The redemption value of SOLVE tokens.</td></tr><tr><td>solve_gas_setting</td><td>JSON</td><td>The SOLVE gas usage setting.</td></tr><tr><td>event_wise_cost</td><td>array</td><td>The event wise cost in SOLVE token.</td></tr><tr><td>event</td><td>string</td><td>The event used for transactions in the network.</td></tr><tr><td>cost</td><td>long</td><td>The cost in SOLVE gas for each event transaction.</td></tr></tbody></table>

{% code title="Example:" %}
```json
                    "solve_token_usage": {
                      "deposit_value": "Market",
                      "redemption_value": "Deposit",
                      "solve_gas_setting": {
                        "event_wise_cost": []
                      },
                      "custom_payments": {
                        "event_wise_cost": []
                      }
                    }
                  },
```
{% endcode %}
