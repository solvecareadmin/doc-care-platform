---
description: >-
  This section describes the details for user roles and journeys or user flows
  within the network.
---

# Roles and journeys

### Roles

<table><thead><tr><th width="185">Field Name</th><th width="148">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the role.</td></tr><tr><td>name</td><td>string</td><td>The name of the role.</td></tr><tr><td>description</td><td>string</td><td>The description of the role.</td></tr><tr><td>type</td><td>string</td><td>The role type defined in the system.</td></tr><tr><td>status</td><td>string</td><td>The status for the role set to Active.</td></tr><tr><td>version</td><td>number</td><td>The version number of the role, which is updated when the role metadata value changes.</td></tr><tr><td>td_collections</td><td>array</td><td>The transactional data records linked to the role.</td></tr><tr><td>allow_events_with_role</td><td>array</td><td>The events allowed for the role.</td></tr><tr><td>home_card_ref_id</td><td>string</td><td>The reference ID to the home card for the role.</td></tr></tbody></table>

{% code title="Example:" %}
```json
        "roles": [
            {
                "id": "rl-member",
                "name": "Member",
                "description": "The member user role.",
                "type": "Wallet",
                "status": "Active",
                "version": 1,
                "allow_events_with_role": [],
                "home_card_ref_id": "cd-h-member"
            },
            {
                "id": "rl-doctor",
                "name": "Admin",
                "description": "The Doctor user role.",
                "type": "Wallet",
                "status": "Active",
                "version": 1,
                "allow_events_with_role": [],
                "home_card_ref_id": "cd-h-doctor"
            }
            
        ],
```
{% endcode %}

### Journeys

<table><thead><tr><th width="189">Field Name</th><th width="165">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the journey.</td></tr><tr><td>name</td><td>string</td><td>The name of the journey.</td></tr><tr><td>description</td><td>string</td><td>The description of the journey.</td></tr><tr><td>status</td><td>string</td><td>The status for the journey set to Active.</td></tr><tr><td>start_card_ref_id</td><td>string</td><td>The reference ID of the journey starting card.</td></tr><tr><td>roles</td><td>string</td><td>The roles involved in the journey.</td></tr><tr><td>journey_type</td><td>string</td><td>The journey type defined in the system.</td></tr></tbody></table>

{% code title="Example:" %}
```json
        "journeys": [
            {
                "id": "jn-intro-journey",
                "icon": "",
                "name": "Intro journey for My Network",
                "description": "Intro journey for My Network",
                "status": "Active",
                "start_card_ref_id": "cd-intro-card",
                "roles": [],
                "journey_type": "JOIN_NETWORK_JOURNEY"
            },
            {
                "id": "jn-rl-doctor",
                "icon": "",
                "name": "Join as Doctor",
                "description": "Join as Doctor",
                "status": "Active",
                "start_card_ref_id": "cd-invite-rl-doctor",
                "roles": ["rl-doctor"],
                "journey_type": "JOIN_NETWORK_JOURNEY"
            },
```
{% endcode %}
