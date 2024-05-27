---
description: >-
  This section describes the different types of node event handlers, their
  definitions, parameters, and examples.
---

# Node event handlers

### Types of event handlers

* `VAULT_INSERT` – This event handler is used for inserting a record to a specific collection in the vault.
* `VAULT_UPDATE` – This event handler is used for updating a record in a specific collection in the vault based on the dynamic search criteria.
* `MAPPER` – This event handler is used for data transformation, such as excluding, appending, or generating data in the execution chain.
* `NEXT_EVENT_RECIPIENT` – This event handler is used to identify the recipient for the next event.
* `EXPRESSION_LANGUAGE` – This event handler is used to allow writing data manipulation expressions to easily access, filter, and calculate values.
* `CUSTOM` – This event handler is used to specify a specific class that implements a legacy JAR handler.

### Handler definition constants

#### Handler data source (`GenericHandlerDataSource`)

* `EMPTY`- An empty source or collection.
* `EVENT_PAYLOAD` - The payload source of events processed in the handlers chain.
* `HANDLER_ARGUMENTS` - The reponse value from the previous handler in the chain.
* `PERSISTED_IDENTITY` - For vault-related handlers, it is the state of inserted or updated document in a collection.

#### Dynamic handler value (`DynamicHandlerValue`)

It uses "source" and "value" fields to link data. The actual value can be determined dynamically based on the information in the "source" field. Here are the possible values:

| Source              | Possible values                                                 | Description                                                                                    |
| ------------------- | --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `CONSTANT`          | Any value                                                       | The constant propagates the value field as a result.                                           |
| `GENERATED`         | \[UUID, CURRENT\_TIMESTAMP]                                     | It generates a UUID or timestamp.                                                              |
| `EVENT`             | \[`SENDER`, `RECIPIENT`, `CODE`, `TIMESTAMP`, `CORRELATION_ID`] | It gets the value of the original event sender, recipient, code, timestamp, or correlation ID. |
| `EVENT_PAYLOAD`     | Attribute name                                                  | It gets the value of the attribute in the event payload.                                       |
| `HANDLER_ARGUMENTS` | Attribute name                                                  | It gets the value of the attribute in the handler arguments.                                   |

### Handler definition examples

#### Vault Insert handler

| Parameters        | Data type                                                                                     | Description                                                                |
| ----------------- | --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| type              | GenericHandlerType \[VAULT\_INSERT]                                                           | The handler type.                                                          |
| order             | Integer                                                                                       | The order of the handler in the execution chain.                           |
| name              | String                                                                                        | The name of the handler which is used for logging.                         |
| collection        | String                                                                                        | The name of the vault collection.                                          |
| collectionVersion | Integer                                                                                       | The version of the vault collection.                                       |
| dataSource        | `GenericHandlerDataSource` \[`EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`]                   | The data source that provides the document to be into the collection.      |
| handlerOutput     | `GenericHandlerDataSource` \[`EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS, PERSISTED_ENTITY`] | The handler output that will be passed as an argument to the next handler. |

{% code title="Example:" %}
```json
    {
      "type": "VAULT_INSERT",
      "name": "Insert SAMPLE record",
      "order": 2,
      "collection": "SAMPLE",
      "collectionVersion": 1,
      "dataSource": "HANDLER_ARGUMENTS",
      "handlerOutput": "PERSISTED_ENTITY"
    }
```
{% endcode %}

#### Vault Update handler

| Parameters        | Data type                                                                                         | Description                                                                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type              | GenericHandlerType \[VAULT\_UPDATE]                                                               | The handler type.                                                                                                                                       |
| order             | Integer                                                                                           | The order of the handler in the execution chain.                                                                                                        |
| name              | String                                                                                            | The name of the handler which is used for logging.                                                                                                      |
| collection        | String                                                                                            | The name of the vault collection.                                                                                                                       |
| collectionVersion | Integer                                                                                           | The version of the vault collection.                                                                                                                    |
| dataSource        | `GenericHandlerDataSource` \[ `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS` ]                     | The data source that provides the document to be into the collection.                                                                                   |
| handlerOutput     | `GenericHandlerDataSource` \[ `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`, `PERSISTED_ENTITY` ] | The handler output will be passed as an argument to the next handler.                                                                                   |
| insertIfAbsent    | Boolean                                                                                           | It defines a flag that inserts the document if it does not exist in the collection, based on the search criteria. The value is set to false by default. |
| searchCriteria    | Array of `SearchQueryFilter`                                                                      | The search criteria to find the document to be updated.                                                                                                 |

{% code title="Example:" %}
```json
    {
      "type": "VAULT_UPDATE",
      "name": "Answer SAMPLE question",
      "order": 1,
      "collection": "SAMPLE",
      "collectionVersion": 1,
      "dataSource": "EVENT_PAYLOAD",
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
    }
```
{% endcode %}

#### Data Transformation handler

| Parameters           | Data type                                                                                                                                                                      | Description                                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- |
| type                 | GenericHandlerType \[VAULT\_UPDATE]                                                                                                                                            | The handler type.                                                     |
| order                | Integer                                                                                                                                                                        | The order of the handler in the execution chain.                      |
| name                 | String                                                                                                                                                                         | The name of the handler which is used for logging.                    |
| dataSource           | `GenericHandlerDataSource` \[ `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS` ]                                                                                                  | The data source that provides the document to be into the collection. |
| handlerOutput        | `GenericHandlerDataSource` \[ `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`, `PERSISTED_ENTITY` ]                                                                              | The handler output will be passed as an argument to the next handler. |
| excludedAttributes   | Array of strings                                                                                                                                                               | A set of attributes to be excluded from the input data.               |
| additionalAttributes | <p>Map of &#x3C;String, <code>DynamicHandlerValue></code></p><p>(see <a href="node-event-handlers.md#dynamic-handler-value-dynamichandlervalue">Dynamic handler value</a>)</p> | A map of attributes with dynamic values calculated in the runtime.    |

{% code title="Example:" %}
```json
    {
      "type": "MAPPER",
      "name": "Append SAMPLE payload",
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
        "doctorNodeAddress": {
          "source": "EVENT",
          "value": "SENDER"
        }
      },
      "excludedAttributes": [
        "correlationId"
      ]
    }
```
{% endcode %}

#### Next Event Recipient handler

| Parameters       | Data type                                                                                                                                                | Description                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| type             | GenericHandlerType \[VAULT\_UPDATE]                                                                                                                      | The handler type.                                                     |
| order            | Integer                                                                                                                                                  | The order of the handler in the execution chain.                      |
| name             | String                                                                                                                                                   | The name of the handler which is used for logging.                    |
| handlerOutput    | `GenericHandlerDataSource` \[ `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`]                                                                             | The handler output will be passed as an argument to the next handler. |
| recipientAddress | <p><code>DynamicHandlerValue</code></p><p>(see <a href="node-event-handlers.md#dynamic-handler-value-dynamichandlervalue">Dynamic handler value</a>)</p> | The dynamic value represents the recipient of the next event.         |

{% code title="Example:" %}
```json
    {
      "type": "NEXT_EVENT_RECIPIENT",
      "name": "Fetch SAMPLE target doctor",
      "order": 2,
      "recipientAddress": {
        "source": "HANDLER_ARGUMENTS",
        "value": "doctorNodeAddress"
      },
      "handlerOutput": "HANDLER_ARGUMENTS"
    }
```
{% endcode %}
