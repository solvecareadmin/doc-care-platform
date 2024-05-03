---
description: >-
  This section defines the user roles and journeys that link to cards and events
  in your network.
---

# Roles and journeys

### Roles

<table><thead><tr><th width="185">Field Name</th><th width="148">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td></td><td></td></tr><tr><td>name</td><td></td><td></td></tr><tr><td>description</td><td></td><td></td></tr><tr><td>type</td><td></td><td></td></tr><tr><td>status</td><td></td><td></td></tr><tr><td>version</td><td></td><td></td></tr></tbody></table>

```json
        "roles": [
            {
                "id": "rl-vhz4fm7811nkee2k79olbqes4f4",
                "name": "CW User",
                "description": "CW User Desc",
                "type": "Wallet",
                "status": "Active",
                "version": 1,
                "allow_events_with_role": [],
                "home_card_ref_id": "cd-h-CWUser-wow"
            },
            {
                "id": "rl-9xvtcyoamg2wvmaegorkzbdfpsq",
                "name": "Doctor",
                "description": "Doctor Desc",
                "type": "Wallet",
                "status": "Active",
                "version": 1,
                "allow_events_with_role": [],
                "home_card_ref_id": "cd-h-doctor-o8z"
            }
            
        ],
```

### Journey

| Field Name           | Description |
| -------------------- | ----------- |
| id                   |             |
| name                 |             |
| description          |             |
| status               |             |
| start\_card\_ref\_id |             |
| roles                |             |
| journey\_type        |             |

```json
        "journeys": [
            {
                "id": "jn-joining-journey-l0sa4",
                "icon": "",
                "name": "Welcome Journey for the Care.Network",
                "description": "Welcome Journey for the Care.Network",
                "status": "Active",
                "start_card_ref_id": "cd-welcome-card-7phrv",
                "roles": [],
                "journey_type": "JOIN_NETWORK_JOURNEY"
            },
            {
                "id": "jn-rl-vhz4fm7811nkee2k79olbqes4f4",
                "icon": "",
                "name": "Join as Patient",
                "description": "Join as Patient",
                "status": "Active",
                "start_card_ref_id": "cd-invite-rl-vhz4fm7811nkee2k79olbqes4f4",
                "roles": [
                    "rl-vhz4fm7811nkee2k79olbqes4f4"
                ],
                "journey_type": "JOIN_NETWORK_JOURNEY"
            },
```
