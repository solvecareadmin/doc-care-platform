---
description: This section provides examples on how to configure Python event handlers.
---

# Python event handlers

The Python event handler contains a set of base classes that provide an interface to the platform's core components, such as Vault, Wallet, Node, and Care Data Node (CDN). The following template includes base classes and functions that provide features to retrieve, search, update, and save data.

### Python template

{% code title="Example:" fullWidth="false" %}
```python
class CDN:
    def __init__(self, index: str):
        self.context = context
        self.index = index
    def find_all(self, parameters: SearchRequest) -> List:
        return self.context.getCareDataNodeProvider().findAll(self.index, parameters)
    def find_first(self, parameters: SearchRequest) -> SearchResponse:
        return self.context.getCareDataNodeProvider().findFirst(self.index, parameters)
    def raw_search(self, from_row, num_rows, search_request) -> List:
        return self.context.getCareDataNodeProvider().rawSearch(self.index, from_row, num_rows, search_request)

class Wallet:
    def __init__(self):
        self.context = context
    def get_wallet_profile(self) -> WalletProfile:
        return self.context.getMainNetNodeProvider().getMainNetProfile(ProfileType.WALLET)
    def get_phone_profile(self) -> PhoneProfile:
        return self.context.getMainNetNodeProvider().getMainNetProfile(ProfileType.PHONE)
    def get_contact_profile(self) -> ContactProfile:
        return self.context.getMainNetNodeProvider().getMainNetProfile(ProfileType.CONTACT)
    def update_wallet_profile(self, data: Map, attribute_mapping: Map) -> Map:
        self.context.getMainNetNodeProvider().updateWalletProfile(data, attribute_mapping)
        return data
    def update_phone_profile(self, data: Map, attribute_mapping: Map) -> Map:
        self.context.getMainNetNodeProvider().updatePhoneProfile(data, attribute_mapping)
        return data
    def update_contact_profile(self, data: Map, attribute_mapping: Map) -> Map:
        self.context.getMainNetNodeProvider().updateContactProfile(data, attribute_mapping)
        return data

class Vault:
    def __init__(self):
        self.context = context
    def save(self, collection: str, data: Map) -> Map:
        vault = self.context.getVaultStorage(collection)
        guid = vault.save(data)
        return vault.getByGuid(guid)
    def update(self, collection: str, criteria: List, data: Map, insert_if_absent: bool) -> Map:
        vault = self.context.getVaultStorage(collection)
        guid = vault.update(criteria, data, insert_if_absent)
        return vault.getByGuid(guid)
    def search(self, collection: str, filters: List) -> List:
        vault = self.context.getVaultStorage(collection)
        return vault.search(filters)

def execute(ctx: HandlerExecutionContext) -> Map:
    result = HashMap(arguments())
    # PUT YOUR CODE HERE
    return result
```
{% endcode %}

### Use case example

The following examples show how to send an event from CDN to Care.Wallet.

1. Define the event in the `input.json` file.

{% code title="Example:" %}
```json
{
    "id": "ev-cdn-broadcast",
    "name": "N.CDN.BROADCAST.MESSAGE",
    "code": "N.CDN.BROADCAST.MESSAGE",
    "description": "CDN broadcast message",
    "status": "Active",
    "type": "NODE_TO_ROLE",
    "from_role": "DATA_NODE",
    "to_role": "PATIENT",
    "event_definition_ref": "event/ev-cdn-broadcast.json",
    "node_event_handlers": [
      "eh-n-patient-process-py"
    ]
  }
```
{% endcode %}

2. Create the event definition for `event/ev-cdn-broadcast.json`_._

{% code title="Example:" %}
```json
{
  "definition": {
    "description": "Broadcast CDN message",
    "name": "N_CDN_BROADCAST_MESSAGE",
    "resource": "N_CDN_BROADCAST_MESSAGE",
    "type": "EVENT_DATA"
  },
  "structure": {
    "attributes": [
      {
        "code": "transactionId",
        "name": "transactionId",
        "type_definition": {
          "type": "string"
        },
        "order": 1,
        "system": false
      },
      {
        "code": "indexName",
        "name": "indexName",
        "type_definition": {
          "type": "string"
        },
        "order": 2,
        "system": false
      },
      {
        "code": "ddfType",
        "name": "ddfType",
        "type_definition": {
          "type": "string"
        },
        "order": 3,
        "system": false
      },
      {
        "code": "msgType",
        "name": "msgType",
        "type_definition": {
          "type": "string"
        },
        "order": 4,
        "system": false
      },
      {
        "code": "attributes",
        "name": "attributes",
        "type_definition": {
          "type": "collection",
          "item_type_definition": {
            "type": "string"
          }  
        },
        "order": 5,
        "system": false
      }
    ]
  }
}
```
{% endcode %}

3. Define the event handler in the `input.json` file.

{% code title="Example:" %}
```json
 {
    "id": "eh-n-patient-process-py",
    "name": "N.CDN.BROADCAST.MESSAGE",
    "description": "N.CDN.BROADCAST.MESSAGE",
    "status": "Active",
    "event": "ev-cdn-broadcast",
    "type": "NODE_EVENT_HANDLER",
    "python_event_handler_ref": "python-event-handler/eh-n-patient-process.py"
  }
```
{% endcode %}

4. Create a Python event handler definition that saves the data.

{% code title="Example:" %}
```python
def execute(ctx: HandlerExecutionContext) -> Map:
    result = HashMap(arguments())
    # PUT YOUR CODE HERE
    start_row = 0
    num_rows = 10
    query = {
      "match_all": {}
    }
    page = CDN('DOCTORS').search(start_row, num_rows, query)
    Vault('MY_DATA').save(page.getContent())
    return result
```
{% endcode %}
