---
description: This section describes the event definitions and event handler configurations.
---

# Events and event handlers

{% hint style="info" %}
All event definitions must be included in the input.json file.
{% endhint %}

### Events

{% code title="Wallet event" %}
```json
        "events": [
            {
                "id": "e-w-patient-nav-to-cd-next",
                "name": "w-patient-nav-to-cd.next",
                "description": "Event to navigate from start card to next card",
                "code": "w-patient-nav-to-cd.next",
                "status": "Active",
                "type": "WALLET_LOCAL",
                "event_definition_ref": "event/ew-patient-nav-to-cd-next.json",
                "submit_event_handler": "ehw-patient-nav-to-cd-next",
                "node_event_handlers": [],
                "card": "cd-start-rl-patient"
            },
```
{% endcode %}

### Event handler

{% code title="Wallet event handler" %}
```json
        "event_handlers": [
            {
                "id": "ehw-patient-nav-to-cd-next",
                "name": "w-patient-nav-to-cd.next",
                "description": "Wallet Event Handler to Navigate from Start to cd-next",
                "status": "Active",
                "event": "e-w-patient-nav-to-cd-next",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/ehw-patient-nav-to-cd-next.json"
            },
```
{% endcode %}
