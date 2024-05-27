---
description: >-
  This section describes the event definitions, event types, event handlers, and
  some practical examples.
---

# Events and event handlers

{% hint style="info" %}
All event and event handler definitions must be included in the `input.json` file.
{% endhint %}

### Events

An event represents the actions that occur based on user interactions within a network. It defines the data used to communicate between roles or nodes in the network, such as sending and receiving information.&#x20;

#### Types of events

* `WALLET_LOCAL` - A local event within Care.Wallet, such as sending data from one card to another.
* `WALLET_FROM_NODE` - An event that gets data from a specific node, such as retrieving a list of records in Care.Wallet.
* `WALLET_TO_NODE` - An event that sends data from Care.Wallet to a specific node, such as submitting records.
* `NODE_TO_NODE` - An event that sends data from one node to another node. For example, a patient booking an appointment with a doctor.
* `NODE_TO_ROLE` - An event that sends data to all nodes with a designated role in a network. For example, a patient searching for a pediatrician among all doctors in the network.

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

The event handler defines the instructions that execute tasks based on specific events.

The following example is an event handler defined in the `input.json` file.

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

The following example defines an event handler that sends the details to the next card in the sequence: `event-handler/eh-w-patient-nav-to-cd-next1.json`.&#x20;

{% code title="Example:" %}
```json
{
    "walletEventHandler": [
        {
            "refId": "ew-patient-nav-to-cd-next1",
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
                    "refId": "ew-patient-nav-to-cd-next1"
                }
            ]
        }
    ]
}
```
{% endcode %}

### Use case example

The following examples demonstrate a node-to-node event that sends a response from the doctor to the patient. For information on the different types of node event handlers, see [Node event handlers](node-event-handlers.md).

1. Define the event in the `input.json` file.

{% code title="Example" %}
```json
            {
                "id": "ev-doctor-response-to-patient",
                "name": "N.DR.RESPONSE.PT",
                "code": "N.DR.RESPONSE.PT",
                "description": "Response to patient",
                "status": "Active",
                "type": "NODE_TO_NODE",
                "from_role": "rl-doctor",
                "to_role": "rl-patient",
                "event_definition_ref": "event/ev-doctor-response.json",
                "node_event_handlers": [
                  "eh-n-patient-save-response",
                  "eh-n-patient-save-doctor"
                ]
              }
```
{% endcode %}

2. Create the event definition with the data used in the doctor's response: `event/ev-doctor-response.json`.

{% code title="Example:" %}
```json
{
    "definition": {
      "description": "Broadcast SAMPLE to doctors",
      "name": "N_DR_RESPONSE",
      "resource": "N_DR_RESPONSE",
      "type": "EVENT_DATA"
    },
    "structure": {
      "attributes": [
        {
          "code": "transactionalGuid",
          "name": "transactionalGuid",
          "system": false,
          "order": 1,
          "type_definition": {
            "type": "string"
          }
        },
        {
          "code": "answer",
          "name": "answer",
          "system": false,
          "order": 2,
          "type_definition": {
            "type": "string"
          }
        },
        {
          "code": "answerTitle",
          "name": "answerTitle",
          "system": false,
          "order": 3,
          "type_definition": {
            "type": "string"
          }
        },
        {
          "code": "doctorName",
          "name": "doctorName",
          "system": false,
          "order": 4,
          "type_definition": {
            "type": "string"
          }
        },
        {
          "code": "status",
          "name": "status",
          "system": false,
          "order": 5,
          "type_definition": {
            "type": "string"
          }
        },
        {
          "code": "answeredAt",
          "name": "answeredAt",
          "system": false,
          "order": 6,
          "type_definition": {
            "type": "timestamp"
          }
        }
      ]
    }
  }

```
{% endcode %}

3. Define the event handlers in the `input.json` file.

```json
            {
                "id": "eh-n-patient-save-response",
                "name": "N.PT.SAVE.RESPONSE",
                "description": "empty",
                "status": "Active",
                "event": "ev-doctor-response-to-patient",
                "type": "NODE_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-n-patient-save-response.json"
            },
            {
                "id": "eh-n-patient-save-doctor",
                "name": "N.PT.SAVE.DR",
                "description": "empty",
                "status": "Active",
                "event": "ev-doctor-response-to-patient",
                "type": "NODE_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-n-patient-save-doctor.json"
            }
```

4. Create the node event handler definition that saves the record to the patient node: `event-handler/eh-n-patient-save-response.json`.

{% code title="Example:" %}
```json
{
    "nodeEventHandlers": [
      {
        "type": "MAPPER",
        "name": "Append SAMPLE payload",
        "order": 1,
        "dataSource": "EVENT_PAYLOAD",
        "additionalAttributes": {
          "doctorNodeAddress": {
            "source": "EVENT",
            "value": "SENDER"
          }
        }
      },
      {
        "type": "VAULT_UPDATE",
        "name": "Patients",
        "order": 2,
        "collection": "SAMPLE",
        "collectionVersion": 1,
        "dataSource": "HANDLER_ARGUMENTS",
        "insertIfAbsent": true,
        "searchCriteria": [
          {
            "queryMatcher": "EQUAL",
            "fieldName": "transactionalGuid",
            "dynamicValue": {
              "source": "EVENT_PAYLOAD",
              "value": "transactionalGuid"
            }
          }
        ],
        "handlerOutput": "PERSISTED_ENTITY"
      },
      {
        "type": "MAPPER",
        "name": "Append SAMPLE payload",
        "order": 3,
        "dataSource": "EVENT_PAYLOAD"
      }
    ]
  }
```
{% endcode %}

5. Create the node event handler that saves the doctor details to the patient node: `event-handler/eh-n-patient-save-doctor.json`

```json
{
  "nodeEventHandlers": [
    {
      "type": "MAPPER",
      "name": "Append SAMPLE payload",
      "order": 1,
      "dataSource": "EVENT_PAYLOAD",
      "additionalAttributes": {
        "nodeAddress": {
          "source": "EVENT",
          "value": "SENDER"
        },
        "name": {
          "source": "EVENT_PAYLOAD",
          "value": "doctorName"
        },
        "lastActivityAt": {
          "source": "EVENT_PAYLOAD",
          "value": "answeredAt"
        }
      },
      "excludedAttributes": [
        "doctorName",
        "answer",
        "answerTitle",
        "answeredAt",
        "status"
      ]
    },
    {
      "type": "VAULT_UPDATE",
      "name": "Patients",
      "order": 1,
      "collection": "USERS",
      "collectionVersion": 1,
      "dataSource": "HANDLER_ARGUMENTS",
      "insertIfAbsent": true,
      "searchCriteria": [
        {
          "queryMatcher": "EQUAL",
          "fieldName": "nodeAddress",
          "dynamicValue": {
            "source": "EVENT",
            "value": "SENDER"
          }
        }
      ],
      "handlerOutput": "EVENT_PAYLOAD"
    }
  ]
}
```
