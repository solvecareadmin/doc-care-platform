---
description: >-
  This section describes the different types of node event handlers, their
  definitions, parameters, and examples.
---

# Node Event Handlers

### Types of node event handlers

* `VAULT_INSERT` – This event handler is used to insert a record into a specific collection in the vault.
* `VAULT_UPDATE` – This event handler is used to update a record in a specific collection in the vault based on the dynamic search criteria.
* `MAPPER` – This event handler is used for data transformation, such as excluding, appending, or generating data in the execution chain.
* `NEXT_EVENT_RECIPIENT` – This event handler is used to identify the recipient for the next event.
* `EXPRESSION_LANGUAGE` – This event handler allows writing data manipulation expressions to easily access, filter, and calculate values.
* `CUSTOM` – This event handler is used to specify a specific Java class that implements a legacy JAR (Java Archive) handler.

### Handler definition constants

#### Handler data source (`GenericHandlerDataSource`)

* `EMPTY`– An empty source or collection.
* `EVENT_PAYLOAD` – The payload source of events processed in the handlers chain.
* `HANDLER_ARGUMENTS` – The response value from the previous handler in the chain.
* `PERSISTED_IDENTITY` – For vault-related handlers, it is the state of inserted or updated documents in a collection.

#### Dynamic handler value (`DynamicHandlerValue`)

It uses "source" and "value" fields to link data. The actual value can be determined dynamically based on the information in the "source" field. Here are the possible values:

| Source              | Possible values                                              | Description                                                                                    |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| `CONSTANT`          | Any value                                                    | The constant propagates the value field as a result.                                           |
| `GENERATED`         | `UUID`, `CURRENT_TIMESTAMP`                                  | It generates a UUID or timestamp.                                                              |
| `EVENT`             | `SENDER`, `RECIPIENT`, `CODE`, `TIMESTAMP`, `CORRELATION_ID` | It gets the value of the original event sender, recipient, code, timestamp, or correlation ID. |
| `EVENT_PAYLOAD`     | Attribute name                                               | It gets the value of the attribute in the event payload.                                       |
| `HANDLER_ARGUMENTS` | Attribute name                                               | It gets the value of the attribute in the handler arguments.                                   |

### Handler definition examples

#### Vault Insert handler

| Parameters        | Data type / Values                                              | Description                                                                |
| ----------------- | --------------------------------------------------------------- | -------------------------------------------------------------------------- |
| type              | `VAULT_INSERT`                                                  | The handler type.                                                          |
| order             | Integer                                                         | The order of the handler in the execution chain.                           |
| name              | String                                                          | The name of the handler which is used for logging.                         |
| collection        | String                                                          | The name of the vault collection.                                          |
| collectionVersion | Integer                                                         | The version of the vault collection.                                       |
| dataSource        | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`                   | The data source of the record which will be inserted into the collection.  |
| handlerOutput     | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS, PERSISTED_ENTITY` | The handler output that will be passed as an argument to the next handler. |

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

| Parameters        | Data type / Values                                                 | Description                                                                                                                                            |
| ----------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type              | `VAULT_UPDATE`                                                     | The handler type.                                                                                                                                      |
| order             | Integer                                                            | The order of the handler in the execution chain.                                                                                                       |
| name              | String                                                             | The name of the handler which is used for logging.                                                                                                     |
| collection        | String                                                             | The name of the vault collection.                                                                                                                      |
| collectionVersion | Integer                                                            | The version of the vault collection.                                                                                                                   |
| dataSource        | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`                      | The data source from which the record changes (diffs) will be retrieved.                                                                               |
| handlerOutput     | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`, `PERSISTED_ENTITY`  | The handler output that will be passed as an argument to the next handler.                                                                             |
| insertIfAbsent    | Boolean                                                            | It defines a flag that inserts the document if it does not exist in the collection based on the search criteria. The value is set to false by default. |
| searchCriteria    | Array of `SearchQueryFilter`                                       | The search criteria to find the document to be updated.                                                                                                |

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

| Parameters           | Data type / Values                                                                                                                                              | Description                                                                |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| type                 | `MAPPER`                                                                                                                                                        | The handler type.                                                          |
| order                | Integer                                                                                                                                                         | The order of the handler in the execution chain.                           |
| name                 | String                                                                                                                                                          | The name of the handler which is used for logging.                         |
| dataSource           | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`                                                                                                                   | The data source for the unmapped data.                                     |
| handlerOutput        | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`, `PERSISTED_ENTITY`                                                                                               | The handler output that will be passed as an argument to the next handler. |
| excludedAttributes   | Array of strings                                                                                                                                                | A set of attributes to be excluded from the input data.                    |
| additionalAttributes | <p>Map of <code>DynamicHandlerValue</code></p><p>(see <a href="node-event-handlers.md#dynamic-handler-value-dynamichandlervalue">Dynamic handler value</a>)</p> | A map of attributes with dynamic values calculated at runtime.             |

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

| Parameters       | Data type / Values                                                                                                                                       | Description                                                                |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| type             | `NEXT_EVENT_RECIPIENT`                                                                                                                                   | The handler type.                                                          |
| order            | Integer                                                                                                                                                  | The order of the handler in the execution chain.                           |
| name             | String                                                                                                                                                   | The name of the handler which is used for logging.                         |
| handlerOutput    | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`                                                                                                            | The handler output that will be passed as an argument to the next handler. |
| recipientAddress | <p><code>DynamicHandlerValue</code></p><p>(see <a href="node-event-handlers.md#dynamic-handler-value-dynamichandlervalue">Dynamic handler value</a>)</p> | The dynamic value represents the recipient of the next event.              |

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

#### Expression Language handler

The expression language used for this handler type is based on Spring Expression Language (SpEL). For more information, see the documentation for [Spring Expression Language (SpEL)](https://docs.spring.io/spring-framework/docs/3.0.x/reference/expressions.html).&#x20;

Here are the operators supported in the language:

| Type        | Operators                                    |
| ----------- | -------------------------------------------- |
| Arithmetic  | +, -, \*, /, %, ^, div, mod                  |
| Relational  | <, >, ==, !=, <=, >=, lt, gt, eq, ne, le, ge |
| Logical     | and, or, not, &&, \|\|, !                    |
| Conditional | ?:                                           |
| Regex       | matches                                      |

Here are the parameters in the event handler definition:

| Parameter          | Data type / Values                                                                            | Description                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| type               | `EXPRESSION_LANGUAGE`                                                                         | The handler type.                                                                     |
| order              | Integer                                                                                       | The order of the handler in the execution chain.                                      |
| name               | String                                                                                        | The name of the handler which is used for logging.                                    |
| dataSource         | `EMPTY`, `EVENT_PAYLOAD`, `HANDLER_ARGUMENTS`                                                 | The data source of the record which will be inserted into the collection.             |
| computedAttributes | Map of expressions, where the key is a variable name, and the value is the expression itself. | The handler executes the expression and puts the value inside the specified variable. |

{% code title="Example 1:" %}
```json
    {
      "type": "EXPRESSION_LANGUAGE",
      "name": "Calc",
      "order": 2,
      "dataSource": "EMPTY",
      "computedAttributes": {
        "c": "arguments['a']+arguments['b']"
      }
    }
```
{% endcode %}

In Example 1, let's assume that the `HANDLER_ARGUMENTS` has variables `a` and `b`. If the variables represent numeric values, such as `a=1` and `b=2`, then the result will be `1+2=3`.  If the variables represent string values, such as `a='1'` and `b='2`', then the result will be `'1'+'2'='12'`.

{% code title="Example 2:" %}
```json
    {
      "type": "EXPRESSION_LANGUAGE",
      "name": "Calc",
      "order": 2,
      "dataSource": "EMPTY",
      "computedAttributes": {
        "res": "arguments[users].?[country=='USA'].size()"
      }
    }
```
{% endcode %}

In Example 2, let's assume that the `HANDLER_ARGUMENTS` has a variable `user`, which represent a list with the following value:

```json
    [
      {
        "name": "John",
        "country": "USA"
      },
      {
        "name": "Sam",
        "country": "Canada"
      },
    ]
```

The expression `arguments[users].?[country=='USA'].size()` will filter the items which has the country value set to `"USA"`.  Then it calculates the size, which returns the count. In this case, the result will be `1`.

{% code title="Example 3:" %}
```json
    {
      "type": "EXPRESSION_LANGUAGE",
      "name": "Calc",
      "order": 2,
      "dataSource": "EMPTY",
      "computedAttributes": {
        "res": "arguments[users].?[country=='USA'].size() > 0 ? 'USA_PRESENT' : 'USA_NOT_PRESENT'"
      }
    }
```
{% endcode %}

In Example 3, let's assume that the `HANDLER_ARGUMENTS` has a variable `user`, which represent a list with the following value:

```json
    [
      {
        "name": "John",
        "country": "USA"
      },
      {
        "name": "Sam",
        "country": "Canada"
      },
    ]
```

The expression `arguments[users].?[country=='USA'].size() > 0 ? 'USA_PRESENT' : 'USA_NOT_PRESENT'` will filter the items which has the country value set to `"USA"`. Then it calculates the size, which returns the count. In this case, the count is `1`. If the count is greater than 0, then the result will be  `'USA_PRESENT'`.

#### Custom (JAR) handler

| Parameter | Data type / Values | Description                                                           |
| --------- | ------------------ | --------------------------------------------------------------------- |
| type      | CUSTOM             | The handler type.                                                     |
| order     | Integer            | The order of the handler in the execution chain.                      |
| jarUrl    | String             | The URL where the JAR file with the handler implementation is stored. |
| className | String             | The full Java class name that implements the corresponding interface. |

{% code title="Example:" %}
```json
  {
    "type": "CUSTOM",
    "order": 2,
    "jarUrl": "https://a.solvecare.net/artifactory/libs-snapshot-local/care/solve/generic/node/hello-world-handler/1.0.4-SNAPSHOT/hello-world-handler-1.0.4-20220406.133327-6.jar",
    "className": "care.solve.node.handler.demo.patient.PatientComputeBmiHandler"
  }
```
{% endcode %}
