---
description: >-
  This section describes the structure of event and event handler definitions,
  and some examples for the different types of events and event handlers.
---

# Events and Event Handlers

{% hint style="info" %}
All event and event handler definitions must be included in the `input.json` file.
{% endhint %}

## Events

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
                "id": "ev-patient-nav-to-cd-next",
                "name": "W.PATIENT.NAV.CD-NEXT",
                "description": "Event to navigate from start card to next card",
                "code": "W.PATIENT.NAV.CD-NEXT",
                "status": "Active",
                "type": "WALLET_LOCAL",
                "event_definition_ref": "event/ev-patient-nav-to-cd-next.json",
                "submit_event_handler": "eh-w-ev-patient-nav-to-cd-next",
                "node_event_handlers": [],
                "card": "cd-start-rl-patient"
            },
```
{% endcode %}

The following example defines an event containing user details: `event/ev-patient-nav-to-cd-next.json`.

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

## Event handlers

The event handler defines the instructions that execute tasks based on specific events, such as navigation and data manipulation.

### Types of event handlers

* `WALLET_EVENT_HANDLER` — This event handler is defined in JSON and can be used to navigate between cards, submit data, or retrieve data.
* `NODE_EVENT_HANDLER` — This event handler is defined in either JSON or Python and can be used to search, retrieve, update, or save data. To learn more about the different types of node event handlers, see [Node Event Handlers](node-event-handlers.md) and [Python Event Handlers](python-event-handlers.md).

| Field Name                      | Value Type | Description                                                                                         |
| ------------------------------- | ---------- | --------------------------------------------------------------------------------------------------- |
| id                              | string     | The unique ID of the event handler.                                                                 |
| name                            | string     | The name of the event handler.                                                                      |
| description                     | string     | The description of the event handler.                                                               |
| status                          | string     | The status of the event handler is set to Active.                                                   |
| event                           | string     | The event which the event handler executes.                                                         |
| type                            | string     | The type of event handler. The possible values are: WALLET\_EVENT\_HANDLER and NODE\_EVENT\_HANDLER |
| event\_handler\_definition\_ref | string     | The reference path and ID of the event handler definition.                                          |

The following example is the wallet event handler for navigating to the next card, as defined in the `input.json` file.

{% code title="Example:" %}
```json
        "event_handlers": [
            {
                "id": "eh-w-patient-nav-to-cd-next",
                "name": "W.PATIENT.NAV.CD-NEXT",
                "description": "Wallet Event Handler to Navigate from Start to cd-next",
                "status": "Active",
                "event": "ev-patient-nav-to-cd-next",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-w-ev-patient-nav-to-cd-next.json"
            },
```
{% endcode %}

The following example is an event handler definition in a JSON file that sends the details to the next card in the sequence: `event-handler/eh-w-ev-patient-nav-to-cd-next1.json`.&#x20;

{% code title="Example:" %}
```json
{
    "walletEventHandler": [
        {
            "refId": "ev-patient-nav-to-cd-next",
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
                    "postAction": "cd-next",
                    "refId": "ev-patient-nav-to-cd-next"
                }
            ]
        }
    ]
}
```
{% endcode %}

## Use case examples

### Submitting health questions

In this example, a patient submits answers from the health questions card and the data is saved in a collection.

1. Define the events in the `input.json` file. Here, we have two events:

{% code title="Example:" %}
```json
            {
                "id": "ev-w-broad-health-questions",
                "name": "W.BROAD.H.QUESTIONS",
                "description": "Submit health questions",
                "code": "W.BROAD.H.QUESTIONS",
                "status": "Active",
                "type": "WALLET_TO_NODE",
                "event_definition_ref": "event/ev-w-broad-health-questions.json",
                "submit_event_handler": "eh-ev-w-broad-health-questions",
                "next_event": "ev-w-broad-health-questions-na",
                "node_event_handlers": [
                    "eh-n-ev-w-broad-health-questions", "eh-n-patient-process-py"
                ],
                "card": "cd-health-questions"
            },
            {
                "id": "ev-w-broad-health-questions-na",
                "name": "W.BROAD.H.QUESTIONS.NA",
                "description": "Broadcast health questions from Patients to rl-netadmin",
                "code": "W.BROAD.H.QUESTIONS.NA",
                "status": "Active",
                "type": "NODE_TO_ROLE",
                "event_definition_ref": "event/ev-w-broad-health-questions-na.json",
                "from_role": "rl-patient",
                "to_role": "rl-netadmin",
                "node_event_handlers": [
                    "eh-n-ev-w-broad-health-questions-na"
                ],
                "card": "cd-health-questions"
            },
```
{% endcode %}

2. Create the event definition for the submit event that contains the data used in the patient health questions: `event/ev-w-broad-health-questions.json`.

{% code title="Example:" %}
```json
{
    "definition": {
        "description": "Save H_QUESTIONS at Patients",
        "name": "W-BROAD-H-QUESTIONS",
        "resource": "W-BROAD-H-QUESTIONS",
        "type": "EVENT_DATA"
    },
    "structure": {
        "attributes": [
            {
                "name": "Symptoms",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "code": "Symptoms",
                "order": 1
            },
            {
                "name": "History",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "code": "History",
                "order": 2
            },
            {
                "name": "Gender",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "code": "Gender",
                "order": 3
            },
            {
                "name": "Age",
                "type_definition": {
                    "type": "number"
                },
                "required": true,
                "system": false,
                "times": 1,
                "code": "Age",
                "order": 4
            },
            {
                "code": "transactionalGuid",
                "name": "transactionalGuid",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "times": 1,
                "order": 5
            },
            {
                "code": "createdAt",
                "name": "createdAt",
                "type_definition": {
                    "type": "timestamp"
                },
                "required": false,
                "system": false,
                "times": 1,
                "order": 6
            },
            {
                "name": "senderNodeAddress",
                "code": "senderNodeAddress",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "order": 7
            }
        ],
        "primary_key": "false"
    }
}
```
{% endcode %}

3. Define the event handlers for the submit event in the `input.json` file. Here, the submit event has two event handlers: `eh-ev-w-broad-health-questions.json` and `eh-n-ev-w-broad-health-questions.json`.&#x20;

{% code title="Example:" %}
```json
            {
                "id": "eh-ev-w-broad-health-questions",
                "name": "eh-ev-w-broad-health-questions",
                "description": "Submit H_Questions",
                "status": "Active",
                "event": "ev-w-broad-health-questions",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-ev-w-broad-health-questions.json"
            },
            {
                "id": "eh-n-ev-w-broad-health-questions",
                "name": "eh-n-ev-w-broad-health-questions",
                "description": "Broadcast H_QUESTIONS from Patients to rl-netadmin",
                "status": "Active",
                "event": "ev-w-broad-health-questions",
                "type": "NODE_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-n-ev-w-broad-health-questions.json"
            },
```
{% endcode %}

4. Create the wallet event handler definition for submitting the event data: `event-handler/eh-ev-w-broad-health-questions.json`.

{% code title="Example:" %}
```json
{
    "walletEventHandler": [
        {
            "refId": "ev-w-broad-health-questions",
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
                    "postAction": "cd-health-questions-done",
                    "refId": "ev-w-broad-health-questions"
                } 
            ]
        }
    ]
}
```
{% endcode %}

5. Create the node event handler definition for saving the event payload: `eh-n-ev-w-broad-health-questions.json`.

{% code title="Example:" %}
```json
{
    "nodeEventHandlers": [
        {
            "type": "MAPPER",
            "name": "Append or Exclude attributes to H_QUESTIONS payload",
            "order": 1,
            "dataSource": "EVENT_PAYLOAD",
            "additionalAttributes": {
                "createdAt": {
                    "source": "GENERATED",
                    "value": "CURRENT_TIMESTAMP"
                },
                "transactionalGuid": {
                    "source": "GENERATED",
                    "value": "UUID"
                },
                "senderNodeAddress": {
                    "source": "EVENT",
                    "value": "SENDER"
                }
            },
            "excludedAttributes": []
        },
        {
            "type": "VAULT_INSERT",
            "name": "H_QUESTIONS",
            "order": 2,
            "collection": "H_QUESTIONS",
            "collectionVersion": 1,
            "dataSource": "HANDLER_ARGUMENTS",
            "handlerOutput": "PERSISTED_ENTITY"
        },
        {
            "type": "MAPPER",
            "name": "Append or Exclude attributes in the result",
            "order": 3,
            "dataSource": "EVENT_PAYLOAD",
            "additionalAttributes": {
                "createdAt": {
                    "source": "HANDLER_ARGUMENTS",
                    "value": "createdAt"
                },
                "transactionalGuid": {
                    "source": "HANDLER_ARGUMENTS",
                    "value": "transactionalGuid"
                },
                "senderNodeAddress": {
                    "source": "EVENT",
                    "value": "SENDER"
                }
            },
            "excludedAttributes": []
        }
    ]
}
```
{% endcode %}

6. Create the event definition for the next event: `ev-w-broad-health-questions-na.json`.

```json
{
    "definition": {
        "description": "Save H_QUESTIONS at PATIENT_ANSWERS",
        "name": "W-BROAD-H-QUESTIONS",
        "resource": "W-BROAD-H-QUESTIONS",
        "type": "EVENT_DATA"
    },
    "structure": {
        "attributes": [
            {
                "name": "Symptoms",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "code": "Symptoms",
                "order": 1
            },
            {
                "name": "History",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "code": "History",
                "order": 2
            },
            {
                "name": "Gender",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "code": "Gender",
                "order": 3
            },
            {
                "name": "Age",
                "type_definition": {
                    "type": "number"
                },
                "required": true,
                "system": false,
                "times": 1,
                "code": "Age",
                "order": 4
            },
            {
                "code": "transactionalGuid",
                "name": "transactionalGuid",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "times": 1,
                "order": 5
            },
            {
                "code": "createdAt",
                "name": "createdAt",
                "type_definition": {
                    "type": "timestamp"
                },
                "required": false,
                "system": false,
                "times": 1,
                "order": 6
            },
            {
                "name": "senderNodeAddress",
                "code": "senderNodeAddress",
                "type_definition": {
                    "type": "string"
                },
                "required": false,
                "system": false,
                "order": 7
            }
        ],
        "primary_key": "false"
    }
}
```

7. Define the event handler for the next event in the `input.json` file. The next event has one event handler: `eh-n-ev-w-broad-health-questions-na.json`.

```json
            {
                "id": "eh-n-ev-w-broad-health-questions-na",
                "name": "eh-n-ev-w-broad-health-questions-na",
                "description": "Broadcast H_QUESTIONS from Patients to rl-netadmin",
                "status": "Active",
                "event": "ev-w-broad-health-questions-na",
                "type": "NODE_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-n-ev-w-broad-health-questions-na.json"
            }
```

8. Create the node event handler definition that saves the event data to the collection: `event-handler/eh-ev-n-broad-health-questions-na.json`. Here, the data is saved to the `PATIENT_ANSWERS` collection based on the defined search criteria.

```json
{
    "nodeEventHandlers": [
        {
            "type": "MAPPER",
            "name": "Append or Exclude attributes to H_QUESTIONS payload",
            "order": 1,
            "dataSource": "EVENT_PAYLOAD",
            "additionalAttributes": {},
            "excludedAttributes": []
        },
        {
            "type": "VAULT_UPDATE",
            "name": "PATIENT_ANSWERS",
            "order": 2,
            "collection": "PATIENT_ANSWERS",
            "collectionVersion": 1,
            "dataSource": "HANDLER_ARGUMENTS",
            "insertIfAbsent": true,
            "searchCriteria": [
                {
                    "queryMatcher": "EQUAL",
                    "fieldName": "senderNodeAddress",
                    "dynamicValue": {
                        "source": "EVENT_PAYLOAD",
                        "value": "senderNodeAddress"
                    }
                }
            ],
            "handlerOutput": "PERSISTED_ENTITY"
        }
    ]
}
```

### Viewing records history

In this example, the wallet retrieves the history of records from a data collection and displays it on the card.

1. Define the event in the `input.json` file.

{% code title="Example:" %}
```json
            {
                "id": "ev-get-records-history",
                "name": "W.GET.RECORDS.HIST",
                "code": "W.GET.RECORDS.HIST",
                "description": "Get Records History",
                "status": "Active",
                "type": "WALLET_FROM_NODE",
                "event_definition_ref": "event/ev-get-records-history.json",
                "submit_event_handler": "eh-ev-get-records-history",
                "node_event_handlers": [],
                "card": "cd-view-records"
            }
```
{% endcode %}

2. Create the event definition with the source of data: `event/ev-get-records-history.json`. To retrieve data, this event uses the unique ID of the `transactionalGuid` generated from a submit event.

{% code title="Example:" %}
```json
{
    "definition": {
        "description": "Get Records History",
        "name": "Get Records History",
        "resource": "Get Records History",
        "type": "EVENT_DATA"
    },
    "structure": {
        "attributes": [
            {
                "code": "transactionalGuid",
                "name": "transactionalGuid",
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

3. Define the event handler in the `input.json` file.

{% code title="Example:" %}
```json
            {
                "id": "eh-ev-get-records-history",
                "name": "eh-ev-get-records-history",
                "description": "eh-ev-get-records-history",
                "status": "Active",
                "event": "ev-get-records-history",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-ev-get-records-history.json"
            }   
```
{% endcode %}

4. Create the wallet event handler definition that gets the records history data from the collection: `event-handler/eh-ev-get-records-history.json`. This event handler uses the GET method to retrieve record data based on the filter query.

{% code title="Example:" %}
```json
{
    "walletEventHandler": [
        {
            "refId": "ev-get-records-history",
            "walletEvents": [
                {
                    "actions": [
                        {
                            "name": "",
                            "order": 1,
                            "parameter": [
                                {
                                    "method": "GET",
                                    "url": "/transactions/RECORD_DATA?filter=[{\"queryMatcher\":\"EQUAL\",\"fieldName\":\"senderNodeAddress\",\"value\":\"${senderNodeAddress}\"}]"
                                }
                            ]
                        }
                    ],
                    "postAction": "",
                    "refId": "ev-get-records-history"
                }
            ]
        }
    ]
}
```
{% endcode %}