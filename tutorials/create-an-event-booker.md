# Create an Event Booker

## Overview

Welcome to the Event Booker example, a simple booking app for events or appointments. The underlying structure can be adapted for Web3 integration, allowing you to extend the app's functionality such as using tokens to pay booking fees for exclusive events.\
\
Here’s how the app works:

1. Launch the app to book an event or appointment.
2. Fill in the details of the event or appointment.
3. Confirm and submit your booking details.

## Steps

Ready to create your own booking app? Follow these steps:

### 1. Define the structure&#x20;

Open the `input.json` file in a text editor, then add the journey definition:

{% code title="input.json" overflow="wrap" %}
```json
            {
                "id": "jn-event-booker",
                "icon": "https://i.ibb.co/7N134gb/booking.png",
                "name": "Book an Event",
                "description": "Book an Event",
                "status": "Active",
                "start_card_ref_id": "cd-book-an-event",
                "roles": [
                    "rl-member"
                ],
                "journey_type": "STANDARD_JOURNEY"
            }
```
{% endcode %}

Define the included [cards](../protocol-guide/build-a-dapp/card-definitions/#cards):

{% code title="input.json" overflow="wrap" %}
```json
            {
                "id": "cd-book-an-event",
                "name": "Book an Event",
                "description": "Book an Event",
                "status": "Active",
                "card_definition_ref": "card/cd-book-an-event.json",
                "side": "PUBLIC",
                "role": "rl-member",
                "transaction_data_ref": "td/td-BOOKING-DETAILS.json",
                "private_card": "",
                "base_card": "base-card-1",
                "journey": "jn-event-booker",
                "outgoing_events": [
                    "e-w-navig-to-details"   
                ],
                "pre_rendering_events": [],
                "post_rendering_events": []
            },
            {
                "id": "cd-set-booking-details",
                "name": "Booking Details",
                "description": "Booking Details",
                "status": "Active",
                "card_definition_ref": "card/cd-set-booking-details.json",
                "side": "PUBLIC",
                "role": "rl-member",
                "transaction_data_ref": "td/td-BOOKING-DETAILS.json",
                "private_card": "",
                "base_card": "base-card-1",
                "journey": "jn-event-booker",
                "outgoing_events": [
                    "e-w-broad-shareAppt",
                    "e-w-navig-to-book-1"
                ],
                "pre_rendering_events": [],
                "post_rendering_events": []
            }
```
{% endcode %}

Define the included [events](../protocol-guide/build-a-dapp/events-and-event-handlers.md#events):

{% code title="input.json" %}
```json
            {
                "id": "e-w-navig-to-details",
                "name": "W-NAVIG-TO-SET",
                "description": "Event to Navigate from Book an Event to cd-set-booking-details",
                "code": "W-NAVIG-TO-SET",
                "status": "Active",
                "type": "WALLET_LOCAL",
                "event_definition_ref": "event/e-w-navig-to-details.json",
                "submit_event_handler": "eh-w-navig-to-details",
                "node_event_handlers": [],
                "card": "cd-book-an-event"                
            },            
			{
                "id": "e-w-navig-to-book-1",
                "name": "W-NAVIG-TO-BOOK-EVT",
                "description": "Event to Navigate from Set Booking to cd-book-an-event",
                "code": "W-NAVIG-TO-BOOK-EVT",
                "status": "Active",
                "type": "WALLET_LOCAL",
                "event_definition_ref": "event/e-w-navig-to-book-1.json",
                "submit_event_handler": "eh-w-navig-to-book-1",
                "node_event_handlers": [],
                "card": "cd-set-booking-details"
            },
            {
                "id": "e-w-broad-shareAppt",
                "name": "W-BROAD-SHAREAPPT",
                "description": "Submit UDETAILS",
                "code": "W-BROAD-SHAREAPPT",
                "status": "Active",
                "type": "WALLET_TO_NODE",
                "event_definition_ref": "event/e-w-broad-shareAppt.json",
                "submit_event_handler": "eh-w-e-w-broad-shareAppt",
                "node_event_handlers": [
                    "eh-h-e-w-broad-shareAppt"
                ],
                "card": "cd-set-booking-details"
            }
```
{% endcode %}

Define the included [event handlers](../protocol-guide/build-a-dapp/events-and-event-handlers.md#event-handlers):

{% code title="input.json" %}
```json
            {
                "id": "eh-w-navig-to-details",
                "name": "W-NAVIG-TO-SET",
                "description": "Wallet Event Handler to Navigate from Book an Event to cd-set-event-details",
                "status": "Active",
                "event": "e-w-navig-to-details",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-w-navig-to-details.json"
            },
            {
                "id": "eh-w-navig-to-book-1",
                "name": "W-NAVIG-TO-BOOK-EVT",
                "description": "Wallet Event Handler to Navigate from Set Booking Details to cd-book-an-event",
                "status": "Active",
                "event": "e-w-navig-to-book-1",
                "type": "WALLET_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-w-navig-to-book-1.json"
            },
            {
                "id": "eh-h-e-w-broad-shareAppt",
                "name": "eh-h-e-w-broad-shareAppt",
                "description": "Broadcast UDETAILS",
                "status": "Active",
                "event": "e-w-broad-shareAppt",
                "type": "NODE_EVENT_HANDLER",
                "event_handler_definition_ref": "event-handler/eh-h-e-w-broad-shareAppt.json"
            }     
```
{% endcode %}

### 2. Create the card definitions

Create the definitions for the start card: `cd-book-an-event.json` and the next card: `cd-set-booking-details.json`.

<pre class="language-json" data-title="cd-book-an-event.json"><code class="lang-json">{
    "id": "cd-book-an-event",
    "name": "Book an Event",
    "cardData": {
        "textforbookevent": "Book an event",
        "imageUrlzkk3n12": "https://d1fgr2dke6q42b.cloudfront.net/uat/media/1022dd5a-7203-4064-98fc-c95bde2fd7d0/arrow-right blue.png",
<strong>        "imageUrlzkk3n15": "https://d1fgr2dke6q42b.cloudfront.net/uat/media/1022dd5a-7203-4064-98fc-c95bde2fd7d0/arrow-right blue.png"
</strong>
    }, 
    "cardLayout": {
        "body": [
            {
                "id": "000t1",
                "tileComponent": [
                    {
                        "id": "Tile14",
                        "subView": [
                            {
                                "title": {
                                    "text": "textforbookevent",
                                    "fontSize": 16,
                                    "titleTextColor": "#000080",
                                    "style": "REGULAR"
                                },
                                "img": {
                                    "text": "imageUrlzkk3n12",
                                    "isUrl": true,
                                    "height": "25",
                                    "width": "25"
                                }
                            }
                        ],
                        "borderColor": "#C5C3C8",
                        "backgroundColor": "#ffffff",
                        "borderWidth": 3,
                        "type": "CONTAINER",
                        "uiAction": "${action502}",
                        "order": 3
                    }
                ],
                "tileType": "WRAP",
                "uiAction": "",
                "order": 1
            }
        ],
        "style": {
            "fontSize": 16,
            "bgColor": "#ffffff",
            "borderWidth": 1
        },
        "footer": {
            "menu": [
                {
                    "id": "EN01BottomButtonBack",
                    "subView": [
                        {
                            "title": {
                                "text": ""
                            }
                        }
                    ],
                    "align": "START",
                    "type": "BACK_BUTTON",
                    "uiAction": "${action478}",
                    "order": 1
                }
            ],
            "orientation": "HORIZONTAL"
        }
    },
    "cardUIAction": {
        "action478": {
            "action": ""
        },
        "action502": {
            "action": "e-w-navig-to-details" 
        }
    }
}   
</code></pre>

{% code title="cd-set-booking-details.json" %}
```json
{
    "id": "cd-set-booking-details",
    "name": "Booking Details",
    "cardData": {
        "0tile0iitextiiiw8": "Enter the details for your booking.",
        "2en01bottombutton1iitextiilor": "Send",
        "1tile1iitextiiixo1": "Location",
        "1tile1iihintii6km1": "e.g. London, UK",
        "1tile1iierrorii6se1": "",
        "1tile1iitextiiixo2": "Date",
        "1tile1iihintii6km2": "e.g. Day 1, Day 2",
        "1tile1iierrorii6se2": "",
        "1tile1iitextiiixo3": "Time",
        "1tile1iihintii6km3": "e.g. 2 p.m. EST",
        "1tile1iierrorii6se3": "",
        "tile1iitextiiixop": "Purpose",
        "1tile1iihintii6kmp": "e.g. Comic Convention",
        "1tile1iierrorii6sep": "" 
    }, 
    "cardLayout": {
        "body": [
            {
                "id": "000t1",
                "tileComponent": [
                    {
                        "id": "Tile0",
                        "subView": [
                            {
                                "title": {
                                    "text": "0tile0iitextiiiw8",
                                    "style": "BOLD",
                                    "titleTextColor": "#000080",
                                    "titleAlign": "START",
                                    "fontSize": 16
                                }
                            }
                        ],
                        "borderColor": "#C5C3C8",
                        "backgroundColor": "#ffffff",
                        "borderWidth": 1,
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 1
                    },
                    {
                        "id": "Tile1a",
                        "subView": [
                            {
                                "title": {
                                    "text": "1tile1iitextiiixo",
                                    "titleTextColor": "#000080",
                                    "titleAlign": "JUSTIFY"
                                },
                                "subTitle": {
                                    "text": "{$apptInfo}",
                                    "hint": "1tile1iihintii6km",
                                    "subTitleTextColor": "#000080",
                                    "subTitleAlign": "START",
                                    "keyboard": "text",
                                    "min": "1",
                                    "max": "1000",
                                    "validation": [
                                        {
                                            "name": "REQUIRED_FIELD",
                                            "error": "1tile1iierrorii6se"
                                        }
                                    ]
                                }
                            }
                        ],
                        "borderColor": "#C5C3C8",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 4
                    },
                    {
                        "id": "Tile1a",
                        "subView": [
                            {
                                "title": {
                                    "text": "tile1iitextiiixop",
                                    "titleTextColor": "#000080",
                                    "titleAlign": "JUSTIFY"
                                },
                                "subTitle": {
                                    "text": "{$apptPurpose}",
                                    "hint": "1tile1iihintii6kmp",
                                    "subTitleTextColor": "#000080",
                                    "subTitleAlign": "START",
                                    "keyboard": "text",
                                    "min": "1",
                                    "max": "1000",
                                    "validation": [
                                        {
                                            "name": "REQUIRED_FIELD",
                                            "error": "1tile1iierrorii6sep"
                                        }
                                    ]
                                }
                            }
                        ],
                        "borderColor": "#C5C3C8",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 4
                    },
                    {
                        "id": "Tile1a",
                        "subView": [
                            {
                                "title": {
                                    "text": "1tile1iitextiiixo1",
                                    "titleTextColor": "#000080",
                                    "titleAlign": "JUSTIFY"
                                },
                                "subTitle": {
                                    "text": "{$apptLocation}",
                                    "hint": "1tile1iihintii6km1",
                                    "subTitleTextColor": "#000080",
                                    "subTitleAlign": "START",
                                    "keyboard": "text",
                                    "min": "1",
                                    "max": "1000",
                                    "validation": [
                                        {
                                            "name": "REQUIRED_FIELD",
                                            "error": "1tile1iierrorii6se1"
                                        }
                                    ]
                                }
                            }
                        ],
                        "borderColor": "#C5C3C8",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 4
                    },
                    {
                        "id": "Tile1a",
                        "subView": [
                            {
                                "title": {
                                    "text": "1tile1iitextiiixo2",
                                    "titleTextColor": "#000080",
                                    "titleAlign": "JUSTIFY"
                                },
                                "subTitle": {
                                    "text": "{$apptDays}",
                                    "hint": "1tile1iihintii6km2",
                                    "subTitleTextColor": "#000080",
                                    "subTitleAlign": "START",
                                    "keyboard": "text",
                                    "min": "1",
                                    "max": "1000",
                                    "validation": [
                                        {
                                            "name": "REQUIRED_FIELD",
                                            "error": "1tile1iierrorii6se2"
                                        }
                                    ]
                                }
                            }
                        ],
                        "borderColor": "#C5C3C8",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 4
                    },
                    {
                        "id": "Tile1a",
                        "subView": [
                            {
                                "title": {
                                    "text": "1tile1iitextiiixo3",
                                    "titleTextColor": "#000080",
                                    "titleAlign": "JUSTIFY"
                                },
                                "subTitle": {
                                    "text": "{$apptTime}",
                                    "hint": "1tile1iihintii6km3",
                                    "subTitleTextColor": "#000080",
                                    "subTitleAlign": "START",
                                    "keyboard": "text",
                                    "min": "1",
                                    "max": "1000",
                                    "validation": [
                                        {
                                            "name": "REQUIRED_FIELD",
                                            "error": "1tile1iierrorii6se3"
                                        }
                                    ]
                                }
                            }
                        ],
                        "borderColor": "#C5C3C8",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 4
                    }
                ],
                "tileType": "WRAP",
                "uiAction": "",
                "order": 1
            }
        ],
        "style": {
            "fontSize": 16,
            "bgColor": "#ffffff",
            "borderWidth": 1
        },
        "footer": {
            "menu": [
                {
                    "id": "EN01BottomButtonBack",
                    "subView": [
                        {
                            "title": {
                                "text": ""
                            }
                        }
                    ],
                    "align": "START",
                    "type": "BACK_BUTTON",
                    "uiAction": "${action461}",
                    "order": 1
                },
                {
                    "id": "EN01BottomButton1",
                    "subView": [
                        {
                            "title": {
                                "text": "2en01bottombutton1iitextiilor"
                            }
                        }
                    ],
                    "align": "START",
                    "type": "BUTTON",
                    "uiAction": "${action420}",
                    "order": 2
                }
            ],
            "orientation": "HORIZONTAL"
        }
    },
    "cardUIAction": {
        "action461": {
            "action": "e-w-navig-to-book-1"
        },
        "action420": {
            "action": "e-w-broad-shareAppt" 
        }
    }
}   
```
{% endcode %}

### 3. Create the event definitions

Create the definition for the event to navigate from start card to the next card: `e-w-navig-to-details.json`.

{% code title="e-w-navig-to-details.json" %}
```json
{
    "definition": {
        "description": "Event to Navigate from Book an Event to cd-set-event-details",
        "name": "W-NAVIG-TO-SET",
        "resource": "W-NAVIG-TO-SET",
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

Create the definition for the submit event: `e-w-broad-shareAppt.json`.

{% code title="e-w-broad-shareAppt.json" %}
```json
{
    "definition": {
        "description": "Submit Booking Details",
        "name": "W-BROAD-SHAREAPPT",
        "resource": "W-BROAD-SHAREAPPT",
        "type": "EVENT_DATA"
    },
    "structure": {
        "attributes": [
            {
                "name": "apptInfo",
                "code": "apptInfo",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "order": 1
            },
            {
                "name": "apptPurpose",
                "code": "apptPurpose",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "order": 2
            },
            {
                "name": "apptLocation",
                "code": "apptLocation",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "order": 3
            }, 
            {
                "name": "apptDays",
                "code": "apptDays",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "order": 4
            },
            {
                "name": "apptTime",
                "code": "apptTime",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "order": 5
            },
            {
                "name": "senderNodeAddress",
                "code": "senderNodeAddress",
                "type_definition": {
                    "type": "string"
                },
                "required": true,
                "system": false,
                "order": 7
            }
        ]
    }
}
```
{% endcode %}

Create the definition for the navigation event after submitting details: `e-w-navig-to-book-1.json`.

{% code title="e-w-navig-to-book-1.json" %}
```json
{
  "definition": {
    "description": "Event to Navigate from Set Booking Details to cd-book-an-event",
    "name": "W-NAVIG-TO-BOOK-EVT",
    "resource": "W-NAVIG-TO-BOOK-EVT",
    "type": "EVENT_DATA"
  },
  "structure": {
    "attributes": [
      {
        "code": "transactionalGuid",
        "name": "transactionalGuid",
        "type_definition": { "type": "string" },
        "order": 1,
        "system": false,
        "required": false
      }
    ]
  }
}

```
{% endcode %}

### 4. Create the event handler definitions

Create the event handler definition for the navigation event to enter booking details: `eh-w-navig-to-details.json`.

```json
{
    "walletEventHandler": [
        {
            "refId": "e-w-navig-to-details",
            "walletEvents": [
                {
                    "actions": [
                        {
                            "name": "submit",
                            "order": 1,
                            "parameter": [
                                {
                                    "method": "DETAILS",
                                    "url": ""
                                }
                            ]
                        }
                    ],
                    "postAction": "cd-set-event-details",
                    "refId": "e-w-navig-to-details"
                }
            ]
        }
    ]
}
```

Create the event handler definition for the submit event that sends the booking details to the admin node: `eh-h-e-w-broad-shareAppt.json`.

```json
{
    "nodeEventHandlers": [
        {
            "type": "MAPPER",
            "name": "Append attributes",
            "order": 1,
            "dataSource": "EVENT_PAYLOAD",
            "additionalAttributes": {
                "transactionalGuid": {
                    "source": "GENERATED",
                    "value": "UUID" 
                },
                "leadNodeAddress": {
                    "source": "EVENT_PAYLOAD",
                    "value": "senderNodeAddress"
                },
                "apptInfo": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptInfo"
                },
                "apptPurpose": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptPurpose"
                },
                "apptLocation": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptLocation"
                },
                "apptWorkDays": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptDays"
                },
                "apptWorkHours": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptTime"
                },
                "createdAt": {
                    "source": "GENERATED",
                    "value": "CURRENT_TIMESTAMP"
                },
                "updatedAt": {
                    "source": "GENERATED",
                    "value": "CURRENT_TIMESTAMP"
                }
            },
            "excludedAttributes": [
                "senderNodeAddress"
            ]
        },
        {
            "type": "EXPRESSION_LANGUAGE",
            "name": "Append attributes",
            "order": 2,
            "dataSource": "HANDLER_ARGUMENTS",
            "computedAttributes": {
                "submittedAt": "\"Received on: \" + new java.text.SimpleDateFormat(\"dd/MM/yyyy\").format(new java.util.Date(arguments['createdAt']))"            }
        },
        {
            "type": "VAULT_INSERT",
            "name": "BOOKING_DETAILS",
            "order": 3,
            "collection": "BOOKING_DETAILS",
            "collectionVersion": 1,
            "dataSource": "HANDLER_ARGUMENTS",
            "handlerOutput": "PERSISTED_ENTITY"
        },
        {
            "type": "NEXT_EVENT_RECIPIENT",
            "name": "Fetch sender address",
            "order": 4,
            "recipientAddress": {
                "source": "EVENT_PAYLOAD",
                "value": "senderNodeAddress"
            },
            "handlerOutput": "HANDLER_ARGUMENTS"
        },
        {
            "type": "MAPPER",
            "name": "Append and Exclude attributes in the result",
            "order": 5,
            "dataSource": "EVENT_PAYLOAD",
            "additionalAttributes": {
                "transactionalGuid": {
                    "source": "HANDLER_ARGUMENTS",
                    "value": "transactionalGuid"
                },
                "submittedAt": {
                    "source": "HANDLER_ARGUMENTS",
                    "value": "submittedAt"
                },
                "apptInfo": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptInfo"
                },
                "apptPurpose": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptPurpose"
                },
                "apptLocation": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptLocation"
                },
                "apptWorkDays": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptDays"
                },
                "apptWorkHours": {
                    "source": "EVENT_PAYLOAD",
                    "value": "apptTime"
                }
            },
            "excludedAttributes": [
                "createdAt",
                "updatedAt",
                "leadNodeAddress",
                "senderNodeAddress"
            ]
        }
    ]
}
```

Create the event handler definition for the navigation event after submitting booking details: `eh-w-navig-to-book-1`. The booking details are stored in the data collection: `td/td-BOOKING_DETAILS`.

```json
{
    "walletEventHandler": [
        {
            "refId": "e-w-navig-to-book-1",
            "walletEvents": [
                {
                    "actions": [
                        {
                            "name": "submit",
                            "order": 1,
                            "parameter": [
                                {
                                    "method": "GET",
                                    "url": "/transactions/BOOKING_DETAILS"
                                }
                            ]
                        }
                    ],
                    "postAction": "cd-book-an-event",
                    "refId": "e-w-navig-to-book-1" 
                }
            ]
        }
    ]
}
```
