---
description: >-
  This section describes the structure of card definitions, including card data,
  card layout, card footer, and card UI actions.
---

# Card Definitions

{% hint style="info" %}
All card definitions must be included in the `input.json` file.
{% endhint %}

## Cards

A card contains multiple data types, user interface elements, and interactive functions triggered by events.

<table><thead><tr><th width="230">Field Name</th><th width="158">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the card.</td></tr><tr><td>name</td><td>string</td><td>The name of the card.</td></tr><tr><td>description</td><td>string</td><td>The description of the card.</td></tr><tr><td>status</td><td>string</td><td>The status of the card is set to Active.</td></tr><tr><td>card_definition_ref</td><td>string</td><td>The reference to the UI component of the card.</td></tr><tr><td>side</td><td>string</td><td>The side on which data is presented.</td></tr><tr><td>role</td><td>string</td><td>The role ID is referenced in the card.</td></tr><tr><td>transaction_data_ref</td><td>string</td><td>The reference to the transaction data used upon initialization.</td></tr><tr><td>journey</td><td>string</td><td>The journey to which the card belongs.</td></tr><tr><td>outgoing_events</td><td>array</td><td>The events or actions triggered by the card.</td></tr><tr><td>pre_rendering_events</td><td>array</td><td>The events or actions used to initialize the card.</td></tr></tbody></table>

{% code title="Example:" %}
```json
    "cards": [
      {
        "id": "cd-start-rl-patient",
        "name": "Patient start card",
        "description": "Start card for patient",
        "status": "Active",
        "card_definition_ref": "card/cd-start-rl-patient.json",
        "side": "PUBLIC",
        "role": "rl-patient",
        "transaction_data_ref": "td/td-default.json",
        "private_card": "",
        "base_card": "",
        "journey": "jn-start-journey",
        "outgoing_events": ["ew-patient-nav-to-cd-next1"],
        "pre_rendering_events": [],
        "post_rendering_events": []
      }
    ],
```
{% endcode %}

## Card definition structure

{% hint style="info" %}
Each card definition is located in the `/definitions/card/` folder.
{% endhint %}

* **Card data** - The information or data displayed within the card, such as texts, images, and links.
* **Card layout** - The arrangement and organization of elements within the card, including body content style, and footer menus.
* **Card footer** - The additional options, navigation buttons, or menus at the bottom of the card for user interaction and navigation.
* **Card UI actions** - The actions triggered by user interactions within the card, such as navigation, form submissions, or data updates.&#x20;

### Card data

Card data can include text, images, links or different types of information relevant to a healthcare journey.

{% code title="Example:" %}
```json
{
    "id": "cd-start-rl-patient",
    "name": "Get started",
    "cardData": {
        "Tile11000vtext": "Welcome to my care network!",
        "Tile11000vsubText": "This is an example.",
        "Tile11000vsubText1": "This is another example.",
        "imgUrlpjbx": "https://123.abc.net/media/Intro.png",
        "EN01BottomButton1002vtext": "Get Started"
    },
```
{% endcode %}

### Card layout

The card body displays the card's content, which includes tiles, texts, images, and interactive functions. For information on supported tile definitions, see [Tile definitions](tile-definitions.md). For details on supported functions, see [Functions](functions.md).

{% code title="Example:" %}
```json
    "cardLayout": {
        "body": [
            {
                "id": "00tc01",
                "tileComponent": [
                    {
                        "id": "Tile0",
                        "subView": [
                            {
                                "title": {
                                    "text": "Tile11000vtext",
                                    "style": "bold"
                                }
                            }
                        ],
                        "align": "START",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 1
                    },
                    {
                        "id": "Tile11",
                        "subView": [
                            {
                                "title": {
                                    "text": "Tile11000vsubText"
                                },
                                "subTitle": {
                                    "text": "Tile11000vsubText1"
                                }
                            }
                        ],
                        "align": "START",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 1
                    },
                    {
                        "id": "Tile16",
                        "subView": [
                            {
                                "img": {
                                    "text": "imgUrlpjbx",
                                    "isUrl": true,
                                    "height": "250",
                                    "width": "250"
                                }
                            }
                        ],
                        "align": "START",
                        "textColor": "#212121",
                        "borderColor": "#1a1a1a",
                        "type": "CONTAINER",
                        "uiAction": "",
                        "order": 1
                    }
                ],
                "tileType": "WRAP",
                "uiAction": "",
                "order": 1
            }
        ],
```
{% endcode %}

### Card footer

The card footer includes buttons or actions used to interact with the card itself or navigate to other related cards. These buttons or actions can perform specific tasks like submitting information, saving changes, or going back to previous screens.

{% code title="Example:" %}
```json
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
                    "uiAction": "${action1}",
                    "order": 1
                },
                {
                    "id": "EN01BottomButton1",
                    "subView": [
                        {
                            "title": {
                                "text": "EN01BottomButton1002vtext"
                            }
                        }
                    ],
                    "align": "END",
                    "type": "BUTTON",
                    "uiAction": "${action2}",
                    "order": 2
                }
            ],
            "orientation": "HORIZONTAL"
        }
    },
```
{% endcode %}

### Card UI actions

The card UI actions define user interactions within the card's content. These actions trigger functionalities like navigation, data updates, input validation, or external function calls.

{% code title="Example:" %}
```json
    "cardUIAction": {
        "action1": {
            "action": ""
        }, "action2": {
            "action": "cd-next2"
        }
    }
}
```
{% endcode %}

