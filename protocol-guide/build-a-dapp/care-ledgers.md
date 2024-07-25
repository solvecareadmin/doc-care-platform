# Care Ledgers

## Care Ledger specifications

A care ledger is used to store and manage data related to events or transactions within the network. If necessary, include details about `care_ledgers` and `care_ledger_tags` in your protocol.

Use tags to categorize data within care ledgers, such as Appointments, Prescriptions, Results, and others.

| Field Name | Value  | Description                           |
| ---------- | ------ | ------------------------------------- |
| id         | string | The unique ID of the care ledger tag. |
| name       | string | The name of the care ledger tag.      |

{% code title="Example:" %}
```json
        "care_ledger_tags": [            
            {
                "id": "clt-Answer-QA",
                "name": "Answer QA"
            },
            {
                "id": "clt-Request-Appointment",
                "name": "Request Appointment"
            }
        ],
```
{% endcode %}

Declare the attributes and values for the care ledgers.

| Field Name         | Value  | Description                                                                       |
| ------------------ | ------ | --------------------------------------------------------------------------------- |
| id                 | string | The unique ID of the care ledger.                                                 |
| name               | string | The name of the care ledger.                                                      |
| description        | string | The description of the care ledger.                                               |
| event\_id          | string | The reference ID of the event to be recorded in the care ledger.                  |
| private\_cards     | array  | The cards with consent to view.                                                   |
| public\_cards      | array  | The cards associated to the event record, which can be shared across the network. |
| care\_ledger\_tags | array  | The reference IDs of the care ledger tags.                                        |

{% code title="Example:" %}
```json
        "care_ledgers": [
            {
                "id": "cl-e-PSbUgucq4Z8zCSemaBiuSyc2uijm8",
                "name": "Answer QA",
                "description": "Answer QA",
                "event_id": "e-w-broad-sendqa-next",
                "private_cards": [],
                "public_cards": [
                    "cd-wv129h6n1lr1ognzepj2abp1iqvp"
                ],
                "care_ledger_tags": [
                    "clt-Answer-QA"
                ]
            },
            {
                "id": "cl-e-PSbUgucq4Z8zCSemaBiuSyc2jXg4",
                "name": "Request Appointment from Patient to Doctor",
                "description": "Request Appointment from Patient to Doctor",
                "event_id": "e-w-broad-shareAppt-next",
                "private_cards": [],
                "public_cards": [
                    "cd-mwlyle6o9ko65ojdorbrg259g761"
                ],
                "care_ledger_tags": [
                    "clt-Request-Appointment"
                ]
            }
        ]    
```
{% endcode %}
