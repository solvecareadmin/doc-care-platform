---
description: This section shows the structure and attributes of transactional data.
---

# Transactional data

Transactional data contains configurable data that can be referenced from roles, cards, or events within the network. The following example shows the definition of transactional data in `td/td-default.json`.

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
