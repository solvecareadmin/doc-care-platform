---
description: >-
  This section describes the definition, structure and attributes of
  transactional data
---

# Transactional data

The following example shows the transactional data definition for _td/td-default.json_.

{% code title="Example:" %}
```json
{
    "id": "td-default",
    "path": "td/td-default.json",
    "definition": {
        "collection": "DEFAULT",
        "description": "DEFAULT",
        "name": "DEFAULT",
        "resource": "DEFAULT",
        "status": "RELEASED",
        "type": "TRANSACTIONAL_DATA"
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
                "required": false,
                "system": false
            },
            {
                "code": "createdAt",
                "name": "createdAt",
                "type_definition": {
                    "type": "timestamp"
                },
                "order": 2,
                "required": false,
                "system": false
            },
            {
                "code": "answer",
                "name": "answer",
                "type_definition": {
                    "type": "string"
                },
                "order": 3,
                "required": false,
                "system": false
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
