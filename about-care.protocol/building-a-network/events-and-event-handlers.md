---
description: This section describes the event definitions and event handler configurations.
---

# Events and event handlers

{% hint style="info" %}
All event and event handler definitions must be included in the `input.json` file.
{% endhint %}

### Events

An event represents the actions that occur based on user interactions. The user roles in the network produce or consume an event.

<table><thead><tr><th width="235">Field Name</th><th width="166">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the event used across the network.</td></tr><tr><td>name</td><td>string</td><td>The name of the event.</td></tr><tr><td>description</td><td>string</td><td>The description of the event.</td></tr><tr><td>code</td><td>string</td><td>The same as the event name.</td></tr><tr><td>status</td><td>string</td><td>The status for the event is set to Active.</td></tr><tr><td>type</td><td>string</td><td>The type of event. The possible values are WALLET_LOCAL, WALLET_FROM_NODE, WALLET_TO_NODE, NODE_TO_NODE and NODE_TO_ROLE.</td></tr><tr><td>event_definition_ref</td><td>string</td><td>The reference path and ID of the event definition.</td></tr><tr><td>submit_event_handler</td><td>string</td><td>The ID of the event handler used for submitting the event.</td></tr><tr><td>node_event_handlers</td><td>array</td><td>The list of outgoing event handlers for node events.</td></tr><tr><td>card</td><td>string</td><td>The reference ID of the card associated to the event.</td></tr></tbody></table>

The following example represents an event that lets a user navigate from one card to another defined in the `input.json` file.

{% code title="Example:" %}
```json
        "events": [
            {
                "id": "ew-patient-nav-to-cd-next1",
                "name": "W.PATIENT.NAV.CD-NEXT1",
                "description": "Event to navigate from start card to next card",
                "code": "W.PATIENT.NAV.CD-NEXT1",
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

The event handler defines the business rules associated with an event or message for each role in the network. It provides the business logic for a functionality.

<table><thead><tr><th width="230">Field Name</th><th width="200">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>number</td><td>The unique ID of the event handler used across the network.</td></tr><tr><td>name</td><td>string</td><td>The name of the event handler.</td></tr><tr><td>description</td><td>string</td><td>The description of the event handler.</td></tr><tr><td>type</td><td>string</td><td>The type of event handler. The possible values are: WALLET_EVENT_HANDLER and NODE_EVENT_HANDLER.</td></tr><tr><td>event_handler_definition_ref</td><td>string</td><td>The reference path and ID of the event handler definition.</td></tr></tbody></table>

{% code title="Example:" %}
```json
        "event_handlers": [
            {
                "id": "ehw-patient-nav-to-cd-next1",
                "name": "W.PATIENT.NAV.CD-NEXT1",
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

The following examples show a node to node event that sends a response from the doctor role to the patient role.

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
                  "eh-n-patient-save-doctor",
                  "eh-n-patient-save-answer"
                ]
              }
```
{% endcode %}

2. Create the event definition for `event/ev-doctor-response.json`.

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

3. Create the node event handler definition for `event-handler/eh-n-patient-save-response.json`.

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

```
{% endcode %}
