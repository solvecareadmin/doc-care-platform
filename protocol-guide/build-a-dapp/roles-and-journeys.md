---
description: >-
  This section describes the definition structure of user roles and journeys in
  a network.
---

# Roles and Journeys

## Roles

A role is a fundamental element of TuumIO Protocol that represents a specific participant type, such as patients or doctors. Each role is defined with the corresponding cards and events.

<table><thead><tr><th width="185">Field Name</th><th width="148">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the role.</td></tr><tr><td>name</td><td>string</td><td>The name of the role.</td></tr><tr><td>description</td><td>string</td><td>The description of the role.</td></tr><tr><td>type</td><td>string</td><td>The role type is defined in the platform.</td></tr><tr><td>status</td><td>string</td><td>The status of the role is set to Active.</td></tr><tr><td>version</td><td>number</td><td>The role's version number is updated when the role metadata value changes.</td></tr><tr><td>td_collections</td><td>array</td><td>The transactional data records are linked to the role.</td></tr><tr><td>allow_events_with_role</td><td>array</td><td>The events allowed for the role.</td></tr><tr><td>home_card_ref_id</td><td>string</td><td>The reference ID to the home card for the role.</td></tr></tbody></table>

{% code title="Example:" %}
```json
        "roles": [
            {
                "id": "rl-patient",
                "name": "PATIENT",
                "description": "The patient user role.",
                "type": "Wallet",
                "status": "Active",
                "version": 1,
                "allow_events_with_role": [],
                "home_card_ref_id": "cd-h-patient"
            },
            {
                "id": "rl-doctor",
                "name": "DOCTOR",
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

## Journeys

A journey is a sequence of interconnected cards, defining a specific workflow for a role or network.

<table><thead><tr><th width="189">Field Name</th><th width="165">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the journey.</td></tr><tr><td>icon</td><td>string</td><td>The path to the icon image file.</td></tr><tr><td>name</td><td>string</td><td>The name of the journey.</td></tr><tr><td>description</td><td>string</td><td>The description of the journey.</td></tr><tr><td>status</td><td>string</td><td>The status of the journey is set to Active.</td></tr><tr><td>start_card_ref_id</td><td>string</td><td>The reference ID of the journey starting card.</td></tr><tr><td>roles</td><td>string</td><td>The roles involved in the journey.</td></tr><tr><td>journey_data</td><td>array</td><td>The data model for synchronizing across multiple roles or nodes, triggered by events. See <a href="roles-and-journeys.md#journey-data-model">Journey data model</a>.</td></tr><tr><td>journey_type</td><td>string</td><td>The journey type is defined in the platform.</td></tr></tbody></table>

### Journey definitions

The following example shows the "Get Started" and the "Join as Doctor" journeys.

{% code title="Example:" %}
```json
        "journeys": [
            {
                "id": "jn-start-journey",
                "icon": "",
                "name": "Get Started",
                "description": "Start journey for Patient",
                "status": "Active",
                "start_card_ref_id": "cd-start-rl-patient",
                "roles": ["rl-patient"],
                "journey_data": [],
                "journey_type": "STANDARD_JOURNEY"
            },
            {
                "id": "jn-rl-doctor",
                "icon": "",
                "name": "Join as Doctor",
                "description": "Join as Doctor",
                "status": "Active",
                "start_card_ref_id": "cd-invite-rl-doctor",
                "roles": ["rl-doctor"],
                "journey_data": [],
                "journey_type": "JOIN_NETWORK_JOURNEY"
            },
```
{% endcode %}

### Journey data model

Here is another example of a "Book Appointment" journey that defines the events, roles, and permissions for synchronizing data across multiple nodes.

<table><thead><tr><th>Field Name</th><th width="170">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>name</td><td>string</td><td>The unique name of the journey data model.</td></tr><tr><td>start_event_ids</td><td>array</td><td>The IDs of start events that trigger data sharing and synchronization. <br><strong>Note:</strong> Only the user role with OWNER access can submit the start (init) event.</td></tr><tr><td>stop_event_ids</td><td>array</td><td>The IDs of stop events with shared data in the payload, completing the synchronization to all nodes.</td></tr><tr><td>affected_collections</td><td>array</td><td>The data collections where payload data is saved.</td></tr><tr><td>expire_in</td><td>string</td><td>The number of days (d), weeks (w), or years (y) from initialization until synchronization is stopped.</td></tr><tr><td>permissions</td><td>array</td><td>The list of roles and corresponding access permissions.</td></tr><tr><td>role</td><td>string</td><td>The reference ID of each role defined in the journey.</td></tr><tr><td>access</td><td>string</td><td>The access level permission set for each role.</td></tr></tbody></table>

{% code title="Example:" %}
```json
{
        "id": "book-appointment-journey",
        "name": "Book Appointment",
        "description": "Book Appointment",
        "status": "Active",
        "start_card_ref_id": "get-records-list-card",
        "roles": ["patient", "doctor", "nurse"],
        "journey_data": [
          {
            "name": "jdm-001-data-01",
            "start_event_ids": [
              "e-w-broad-patient-to-rl-xxx",
              "e-w-pt-confirm-appt"
            ],
            "stop_event_ids": [
              "e-w-pt-confirm-appt-fee"
            ],
            "affected_collections": [
              "td/td-BOOKING.json"
            ],
            "expire_in": "1d",
            "permissions": [
              {
                "role": "rl-PATIENT",
                "access": "OWNER"
              },
              {
                "role": "rl-DOCTOR",
                "access": "READ"
              },
              {
                "role": "rl-NURSE",
                "access": "DELEGATION"
              }
            ]
          }
        ],
        "journey_type": "STANDARD_JOURNEY"
      }
```
{% endcode %}
