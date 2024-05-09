---
description: >-
  This section describes the card definitions used within the network, including
  card data, card layout, card footer, and card UI actions.
---

# Card definitions

{% hint style="info" %}
All card definitions must be included in the _input.json_ file.
{% endhint %}

### Cards

A card contains data types, user interface elements, and interactive functions triggered by events.

<table><thead><tr><th width="230">Field Name</th><th width="158">Value Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>The unique ID of the card.</td></tr><tr><td>name</td><td>string</td><td>The name of the card.</td></tr><tr><td>description</td><td>string</td><td>The description of the card.</td></tr><tr><td>status</td><td>string</td><td>The status for the card set to Active.</td></tr><tr><td>card_definition_ref</td><td>string</td><td>The reference to the UI component of the card.</td></tr><tr><td>side</td><td>string</td><td>The default value is generated in the platform.</td></tr><tr><td>role</td><td>string</td><td>The role ID referenced in the card.</td></tr><tr><td>transaction_data_ref</td><td>string</td><td>The reference to the transaction data used upon initialization.</td></tr><tr><td>journey</td><td>string</td><td>The journey in which the card belongs to.</td></tr><tr><td>outgoing_events</td><td>array</td><td>The events or actions triggered by the card.</td></tr><tr><td>pre_rendering_events</td><td>array</td><td>The events or actions used to initialize the card.</td></tr></tbody></table>

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

### Card definition structure

{% hint style="info" %}
Each card definition is located in the **/definitions/card/** folder.
{% endhint %}

* **Card data** - The information or data displayed within the card, such as texts, images, and links.
* **Card layout** - The arrangement and organization of elements within the card, including body content style, and footer menus.
* **Card footer** - Additional options, navigation buttons, or menus are located at the bottom of the card for user interaction and navigation.
* **Card UI actions** - Interactive actions triggered by user interactions within the card, such as navigation, form submissions, or data updates.&#x20;

#### Card data

The card data can include different types of information relevant to a healthcare journey. The data is presented in a structured manner within the UI view of the card.

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

#### Card layout

The card body presents the main content of the card which includes tiles, texts, images, and functions. For information on supported tile definitions, see [Tile definitions](tile-definitions.md).

<pre class="language-json" data-title="Example:"><code class="lang-json">    "cardLayout": {
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
<strong>                    {
</strong>                        "id": "Tile16",
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
</code></pre>

#### Card footer

The card footer contains the navigation options, actions, or buttons for interacting with the card or navigating to other cards. The interactive elements can trigger specific actions, such as submitting data, saving changes, or returning to previous views.

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

#### Card UI actions

The card UI actions enable various functionalities such as retrieving data, interacting with external systems or APIs, and validating user inputs.

{% code title="Example:" %}
```json
    "cardUIAction": {
        "action1": {
            "action": "HOME"
        },
        "action2": {
            "action": [
                {
                    "name": "Function.CallEventHandler",
                    "method": "DETAILS",
                    "NAVIGATION": "cd-consent-rl-doctor"
                }
            ]
        }
    },
```
{% endcode %}

