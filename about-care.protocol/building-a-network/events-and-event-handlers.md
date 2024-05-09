---
description: This section describes the event definitions and event handler configurations.
---

# Events and event handlers

{% hint style="info" %}
All event and event handler definitions must be included in the `input.json` file.
{% endhint %}

### Events

<table><thead><tr><th width="235">Field Name</th><th width="166">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the event used across the network.</td></tr><tr><td>name</td><td>string</td><td>The name of the event.</td></tr><tr><td>description</td><td>string</td><td>The description of the event.</td></tr><tr><td>code</td><td>string</td><td>The same as event name.</td></tr><tr><td>status</td><td>string</td><td>The status for the event set to Active.</td></tr><tr><td>type</td><td>string</td><td>The type of event. The possible values are: WALLET_LOCAL, WALLET_FROM_NODE, WALLET_TO_NODE, NODE_TO_NODE and NODE_ROLE.</td></tr><tr><td>event_definition_ref</td><td>string</td><td>The reference path and ID of the event definition.</td></tr><tr><td>submit_event_handler</td><td>string</td><td>The event handler ID for submitting the event.</td></tr><tr><td>node_event_handlers</td><td>array</td><td>The list of outgoing event handlers for node events.</td></tr><tr><td>card</td><td>string</td><td>The reference ID of the card.</td></tr></tbody></table>

{% code title="Example:" %}
```json
        "events": [
            {
                "id": "ew-patient-nav-to-cd-next1",
                "name": "patient-nav-to-cd.next1",
                "description": "Event to navigate from start card to next card",
                "code": "patient-nav-to-cd.next1",
                "status": "Active",
                "type": "WALLET_LOCAL",
                "event_definition_ref": "event/ew-patient-nav-to-cd-next1.json",
                "submit_event_handler": "ehw-patient-nav-to-cd-next1",
                "node_event_handlers": [],
                "card": "cd-start-rl-patient"
            },
```
{% endcode %}

### Event handlers

<table><thead><tr><th width="230">Field Name</th><th width="200">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>number</td><td>The unique ID of the event handler used across the network.</td></tr><tr><td>name</td><td>string</td><td>The name of the event handler.</td></tr><tr><td>description</td><td>string</td><td>The description of the event handler.</td></tr><tr><td>type</td><td>string</td><td>The type of event handler. The possible values are: WALLET_EVENT_HANDLER and NODE_EVENT_HANDLER.</td></tr><tr><td>event_handler_definition_ref</td><td>string</td><td>The reference path and ID of the event handler definition.</td></tr></tbody></table>

{% code title="Example:" %}
```json
        "event_handlers": [
            {
                "id": "ehw-patient-nav-to-cd-next1",
                "name": "patient-nav-to-cd.next1",
                "description": "Wallet Event Handler to Navigate from Start to cd-next1",
                "status": "Active",
                "event": "ew-patient-nav-to-cd-next1",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/ehw-patient-nav-to-cd-next1.json"
            },
```
{% endcode %}

### Definitions

The following example is an event definition for `event/ew-patient-nav-to-cd-next1.json`.

{% code title="Example:" %}
```json
{
  "definition": {
    "description": "Get started",
    "name": "GET_STARTED",
    "resource": "GET_STARTED",
    "type": "EVENT_DATA"
  },
  "structure": {
    "attributes": [
      {
        "code": "answer",
        "name": "answer",
        "type_definition": {
          "type": "number"
        },
        "order": 3,
        "system": false,
        "required": false
      },

      {
        "code": "memberId",
        "name": "memberId",
        "type_definition": {
          "type": "string"
        },
        "order": 1,
        "system": false,
        "required": false
      }
    ]
  }
}
```
{% endcode %}

The following example is an event handler definition for `event-handler/ehw-patient-nav-to-cd-next1.json`.&#x20;

```json
{
    "walletEventHandler": [
        {
            "refId": "e-w-patient-nav-to-cd-next1",
            "walletEvents": [
                {
                    "actions": [
                        {
                            "name": "submit",
                            "order": 1,
                            "parameter": [
                                {
                                    "method": "POST",
                                    "url": "/events"
                                }
                            ]
                        }
                    ],
                    "postAction": "cd-next2",
                    "refId": "e-w-patient-nav-to-cd-next1"
                }
            ]
        }
    ]
}
```
