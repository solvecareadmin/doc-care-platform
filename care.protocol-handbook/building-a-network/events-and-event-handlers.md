---
description: >-
  This section describes the structure of event and event handler definitions,
  and some examples for the different types of events and event handlers.
---

# Events and Event Handlers

{% hint style="info" %}
All event and event handler definitions must be included in the `input.json` file.
{% endhint %}

### Events

An event represents the actions that occur based on user interactions within a network. It defines the data used to communicate between roles or nodes in the network, such as sending and receiving information.&#x20;

### Types of events

* `WALLET_LOCAL` — A local event within Care.Wallet, such as sending data from one card to another.
* `WALLET_FROM_NODE` — An event that gets data from a specific node, such as retrieving a list of records in Care.Wallet.
* `WALLET_TO_NODE` — An event that sends data from Care.Wallet to a specific node, such as submitting records.
* `NODE_TO_NODE` — An event that sends data from one node to another node, such as a patient booking an appointment with a doctor.
* `NODE_TO_ROLE` — An event that sends data to all nodes with a designated role in a network, such as a patient searching for the nearest pediatrician among all doctors in the network.

<table><thead><tr><th width="235">Field Name</th><th width="166">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the event.</td></tr><tr><td>name</td><td>string</td><td>The name of the event.</td></tr><tr><td>description</td><td>string</td><td>The description of the event.</td></tr><tr><td>code</td><td>string</td><td>The same as the event name.</td></tr><tr><td>status</td><td>string</td><td>The status of the event is set to Active.</td></tr><tr><td>type</td><td>string</td><td>The type of event. The possible values are WALLET_LOCAL, WALLET_FROM_NODE, WALLET_TO_NODE, NODE_TO_NODE and NODE_TO_ROLE.</td></tr><tr><td>event_definition_ref</td><td>string</td><td>The reference path and ID of the event definition.</td></tr><tr><td>submit_event_handler</td><td>string</td><td>The ID of the event handler used for submitting the event.</td></tr><tr><td>node_event_handlers</td><td>array</td><td>The list of outgoing event handlers for node events.</td></tr><tr><td>card</td><td>string</td><td>The reference ID of the card associated to the event.</td></tr></tbody></table>

The following example represents an event that lets users navigate from one card to another, as defined in the `input.json` file.

{% code title="Example:" %}
```json
        "events": [
            {
                "id": "ev-patient-nav-to-cd-next1",
                "name": "W.PATIENT.NAV.CD-NEXT1",
                "description": "Event to navigate from start card to next card",
                "code": "W.PATIENT.NAV.CD-NEXT1",
                "status": "Active",
                "type": "WALLET_LOCAL",
                "event_definition_ref": "event/ev-patient-nav-to-cd-next1.json",
                "submit_event_handler": "eh-w-patient-nav-to-cd-next1",
                "node_event_handlers": [],
                "card": "cd-start-rl-patient"
            },
```
{% endcode %}

The following example defines an event containing user details: `event/ev-patient-nav-to-cd-next1.json`.

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

### Event handlers

The event handler defines the instructions that execute tasks based on specific events, such as navigation and data manipulation.

| Field Name                      | Value Type | Description                                                                                         |
| ------------------------------- | ---------- | --------------------------------------------------------------------------------------------------- |
| id                              | string     | The unique ID of the event handler.                                                                 |
| name                            | string     | The name of the event handler.                                                                      |
| description                     | string     | The description of the event handler.                                                               |
| status                          | string     | The status of the event handler is set to Active.                                                   |
| event                           | string     | The event which the event handler executes.                                                         |
| type                            | string     | The type of event handler. The possible values are: WALLET\_EVENT\_HANDLER and NODE\_EVENT\_HANDLER |
| event\_handler\_definition\_ref | string     | The reference path and ID of the event handler definition.                                          |

### Types of event handlers

* `WALLET_EVENT_HANDLER` — This event handler is defined in JSON, which can be used to navigate between cards, and to submit or retrieve data.
* `NODE_EVENT_HANDLER` — This event handler is defined in either JSON or Python, which can be used to search, retrieve, update, or save data. To learn more about the different types of node event handlers, see [Node event handlers](node-event-handlers.md) and [Python event handlers](python-event-handlers.md).

The following example is a wallet event handler defined in the `input.json` file.

{% code title="Example:" %}
```json
        "event_handlers": [
            {
                "id": "eh-w-patient-nav-to-cd-next1",
                "name": "W.PATIENT.NAV.CD-NEXT1",
                "description": "Wallet Event Handler to Navigate from Start to cd-next1",
                "status": "Active",
                "event": "ev-patient-nav-to-cd-next1",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-w-patient-nav-to-cd-next1.json"
            },
```
{% endcode %}

The following example is an event handler definition in a JSON file that sends the details to the next card in the sequence: `event-handler/eh-w-patient-nav-to-cd-next1.json`.&#x20;

{% code title="Example:" %}
```json
{
    "walletEventHandler": [
        {
            "refId": "ev-patient-nav-to-cd-next1",
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
                    "refId": "ev-patient-nav-to-cd-next1"
                }
            ]
        }
    ]
}
```
{% endcode %}
