# Python event handlers

### Python template

```python
import java
import polyglot
HandlerExecutionContext = java.type('care.solve.node.core.context.HandlerExecutionContext')
Map = java.type('java.util.Map')
HashMap = java.type('java.util.HashMap')
List = java.type('java.util.List')
SearchRequest = java.type('care.solve.node.core.model.cdn.SearchRequest')
SearchResponse = java.type('care.solve.node.core.model.cdn.SearchResponse')
QueryCondition = java.type('care.solve.node.core.model.cdn.QueryCondition')
QueryConditions = java.type('care.solve.node.core.model.cdn.QueryConditions')
SimpleQueryBuilder = java.type('care.solve.node.core.model.cdn.SimpleQueryBuilder')
WalletProfile = java.type('care.solve.node.core.model.mainnetnode.WalletProfile')
PhoneProfile = java.type('care.solve.node.core.model.mainnetnode.PhoneProfile')
ContactProfile = java.type('care.solve.node.core.model.mainnetnode.ContactProfile')
ProfileType = java.type('care.solve.node.core.model.mainnetnode.ProfileType')
NodeInfo = java.type("care.solve.node.core.model.NodeInfo")
ProfileAttribute = java.type('care.solve.node.core.model.mainnetnode.ProfileAttribute')
EqualitySearchFilter = java.type("care.solve.node.core.model.query.EqualitySearchFilter")
NumericBoundsSearchFilter = java.type("care.solve.node.core.model.query.NumericBoundsSearchFilter")
SearchQueryFilter = java.type("care.solve.node.core.model.query.SearchQueryFilter")
HandlerDefinition = java.type("care.solve.node.handler.generic.definition.ScriptHandlerDefinition")
ProtocolSpecification = java.type("com.care.solve.client.protocol.dto.spec.protocol.ProtocolSpecificationDto")
NodeProtocolSpecification = java.type("com.care.solve.client.protocol.dto.spec.event.NodeProtocolSpecificationDto")
context: HandlerExecutionContext = polyglot.import_value('context')
protocol: ProtocolSpecification = polyglot.import_value('protocol')
node_protocol: ProtocolSpecification = polyglot.import_value('node_protocol')
handler_definition: HandlerDefinition = polyglot.import_value('handler_definition')
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
class Mainnet:
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
def arguments() -> Map:
    return context.getArguments()
...
def cw_id():
    return polyglot.import_value('context').getCareWalletId()
def execute(ctx: HandlerExecutionContext) -> Map:
    result = HashMap(arguments())
    # PUT YOUR CODE HERE
    return result
```

### Use case example

The following example shows how to fetch list of doctors from CDN using the Python template.

1. Declare the card, event, wallet event handler, and node event handler in the _input.json_ file.

{% code title="Card" %}
```json
{
    "id": "cd-sample-fetch",
    "name": "Welcome to Fetch Data - Sample Card",
    "description": "Welcome",
    "status": "Active",
    "card_definition_ref": "card/cd-sample-fetch.json",
    "side": "PUBLIC",
    "role": "PATIENT",
    "journey": "jn-patient",
    "outgoing_events": [],
    "pre_rendering_events": ["e-sample-fetch"],
    "post_rendering_events": []
}
```
{% endcode %}

{% code title="Event" %}
```json
{
    "id": "e-sample",
    "description": "Sample Event",
    "code": "EV-SAMPLE",
    "status": "Active",
    "type": "WALLET_FROM_NODE",
    "submit_event_handler": "e-w-sample-fetch-py",
    "card": "cd-sample-fetch"
}
```
{% endcode %}

{% code title="Wallet event handler " %}
```json
{
  "id": "e-w-sample-fetch-py",
  "name": "Sample fetch wallet event handler",
  "description": "Some description",
  "status": "Active",
  "event": "e-sample",
  "type": "WALLET_EVENT_HANDLER",
  "event_handler_ref": "event-handler/eh-w-sample-fetch.json"
}
```
{% endcode %}

{% code title="Node event handler" %}
```json
{
  "id": "eh-n-sample-fetch-py",
  "name": "Sample fetch event handler",
  "description": "Some description",
  "status": "Active",
  "event": "e-sample",
  "type": "NODE_EVENT_HANDLER",
  "python_event_handler_ref": "event-handler/sample-fetch.py"
}
```
{% endcode %}

2. Create the wallet event handler definition.

{% code title="Wallet event handler" %}
```json
{
  "walletEventHandler": [
    {
      "refId": "e-w-sample-fetch-py",
      "walletEvents": [
        {
          "actions": [
            {
              "name": "getdata",
              "order": 1,
              "parameter": [
                {
                  "method": "GET",
                  "url": "/script?handlerId=eh-n-sample-fetch-py"
                }
              ]
            }
          ],
          "postAction": "cd-sample-fetch",
          "refId": "e-w-sample-fetch-py"
        }
      ]
    }
  ]
}
```
{% endcode %}

3. Use Python code template to create function to search data in CDN.

```python
def execute(ctx: HandlerExecutionContext) -> Map:
    result = HashMap(arguments())
    # PUT YOUR CODE HERE
    start_row = 0
    num_rows = 10
    query = {
      "match_all": {}
    }
    page = CDN('Doctors').search(start_row, num_rows, query)
    result.put('page', page)
    return result
```
