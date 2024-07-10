---
description: >-
  This section provides information about the functions that are supported
  within card definitions.
---

# Functions

Use the functions to link cards to event handlers, execute operations to fetch data, validate data input, navigate between cards, and manage other interactions.

## Fetching data

### Function.SOLVE.getTokenBalance&#x20;

Fetches the available SOLVE token balance after joining a network.

#### Parameter

| Field      | Value  | Description                                                                |
| ---------- | ------ | -------------------------------------------------------------------------- |
| name       | string | The name of the function: `Function.SOLVE.getTokenBalance`                 |
| sourceKeys | array  | Not required                                                               |
| totalKey   | string | Not required                                                               |
| resultKey  | string | The key name in which you want to store the final outcome of the function. |

{% code title="Example:" %}
```json
    "prerenderingFunctions": [
        {
            "name": "Function.SOLVE.getTokenBalance",
            "sourceKeys": [],
            "totalKey": "",
            "resultKey": "solveBalance"
        }
    ]
```
{% endcode %}



### Function.SOLVE.getExchangeRate

Fetches the exchange value of SOLVE from USD.

#### Parameter

| Field      | Value  | Description                                                                       |
| ---------- | ------ | --------------------------------------------------------------------------------- |
| name       | string | The name of the function: `Function.SOLVE.getExchangeRate`                        |
| sourceKeys | array  | The key name, which has a value in USD and is passed as an input to the function. |
| resultKey  | string | The key name in which you want to store the final outcome of the function.        |

{% code title="Example:" %}
```json
"prerenderingFunctions": [
    {
        "name": "Function.SOLVE.getExchangeRate",
        "sourceKeys": [ "totalUsdCost" ],
        "resultKey": "totalSolveCost"
    }
]
```
{% endcode %}

### Function.Profile.key

Shows user profile data inside the network.

#### Parameter

| Field | Value  | Description                                                                                                                                                                                                                                                                                              |
| ----- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| text  | string | <p>The name of the function: <code>Function.Profile.key</code></p><p>The following keys can be used as input:</p><ul><li>name (nickname)</li><li>cw_id</li><li>phone</li><li>country (get user's country code, such as "US")</li><li>first_name</li><li>last_name</li><li>ssn</li><li>language</li></ul> |

{% code title="Example 1:" %}
```json
{
    "id": "Tile0",
    "subView": [
        {
        "title": {
        "text": "Function.Profile.first_name"
        }
    }
]
}
```
{% endcode %}

{% code title="Example 2:" %}
```json
{
    "id": "Tile14a",
    "subView": [
     {
       "title": {
       "text": "2tile14aiitextiihsb",
       "titleTextColor": "#000080",
       "style": "BOLD"
      },
       "subTitle": {
       "text": "Function.Profile.cw_id",
       "subTitleTextColor": "#000080",
       "style": "REGULAR"
      },
   }
]
}
```
{% endcode %}

### Function.PROTOCOL.preLoadData

Executes a GET request to the user node.

#### Parameter

| Field | Value  | Description                                               |
| ----- | ------ | --------------------------------------------------------- |
| name  | string | The name of the function: `Function.PROTOCOL.preLoadData` |
| url   | string | The URL path where the data is stored.                    |

{% code title="Example:" %}
```json
    "prerenderingFunctions": [
            {
                "name": "Function.PROTOCOL.preLoadData",
                "url": "/transactions/H_QUESTIONS"
            }
```
{% endcode %}

### Function.getGPSLocation

Fetches user's current location latitude and longitude.

#### Parameter

| Field      | Value  | Description                                                                                |
| ---------- | ------ | ------------------------------------------------------------------------------------------ |
| name       | string | The name of the function: `Function.getGPSLocation`                                        |
| sourceKeys | array  | The key names that correspond to the user's location coordinates (latitude and longitude). |

{% code title="Example:" %}
```json
    "prerenderingFunctions": [
        {
            "name": "Function.getGPSLocation",
            "sourceKeys": [ "userLocationLatitude", "userLocationLongitude" ]
        }
```
{% endcode %}

### Function.Preference.language

Shows user preference data such as language preference.

#### Parameter

<table><thead><tr><th width="218">Field</th><th>Value</th><th>Description</th></tr></thead><tbody><tr><td>text</td><td>string</td><td>The name of the function: <code>Function.Preference.language</code><br>This function is used only inside Tiles.</td></tr></tbody></table>

{% code title="Example:" %}
```json
{
    "id": "Tile0",
    "subView": [
        {
            "title": {
                "text": "Function.Preference.language"
            }
        }
    ],
}
```
{% endcode %}

## Performing calculations

### Function.data.totalCount

Shows the total count of fetched data.

#### Parameter

| Field | Value  | Description                                          |
| ----- | ------ | ---------------------------------------------------- |
| text  | string | The name of the function: `Function.data.totalCount` |

{% code title="Example:" %}
```json
{
    "id": "Tile0a",
    "subView": [
        {
            "title": {
                "text": "0tile0aiitextiizsx",
                "style": "BOLD",
                "titleTextColor": "#000080",
                "titleAlign": "START"
            },
            "subTitle": {
                "text": "Function.data.totalCount",
                "style": "REGULAR",
                "subTitleTextColor": "#000080",
                "subTitleAlign": "END"
            }
        }
    ],
    "borderColor": "#87ceeb",
    "type": "CONTAINER",
    "uiAction": "",
    "order": 2
}
```
{% endcode %}

### Function.calculateSum

Calculates the total sum of all input value.

#### Parameter

| Field      | Value  | Description                                                                                                                                                              |
| ---------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name       | string | The name of the function: `Function.calculateSum`                                                                                                                        |
| sourceKeys | array  | The names of the keys on which you want to calculate the sum.                                                                                                            |
| resultKey  | string | The key name in which you want to store the final outcome of the function.                                                                                               |
| NAVIGATE   | string | The value of the card ID where you want to navigate after getting the result from the function. If you want to show results on the same card, then use the same card ID. |

{% code title="Example:" %}
```json
"cardUIAction": {
     "action1": {
        "action": [
        {
          "name": "Function.calculateSum",
          "url": "",
          "sourceKeys":["keyName1","keyName2","keyName3"],
          "sourceKey":"",
          "resultKey" : "KeyName3",
          "NAVIGATE":"cd-cost-preview"
         }
       ]
     }
   }
```
{% endcode %}

### Function.calculateSubtract

Calculates the subtraction of the input value.

#### Parameter

| Field     | Value  | Description                                                                                                                                                              |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name      | string | The name of the function: `Function.calculateSubtract`                                                                                                                   |
| sourceKey | string | The key name that you want to subtract from the totalKey.                                                                                                                |
| totalKey  | string | The key name from which the source key value gets subtracted.                                                                                                            |
| resultKey | string | The key name in which you want to store the final outcome of the function.                                                                                               |
| NAVIGATE  | string | The value of the card ID where you want to navigate after getting the result from the function. If you want to show results on the same card, then use the same card ID. |

{% code title="Example:" %}
```json
"cardUIAction": {
     "action1": {
        "action": [
        {
          "name": "Function.calculateSubtract",
          "url": "",
          "sourceKeys":[],
          "sourceKey":"keyName1",
          "totalKey":"keyName2"
          "resultKey" : "KeyName3",
          "NAVIGATE":"cd-cost-preview"
         }
       ]
     }
   }
```
{% endcode %}

### Function.calculateMultiply

Calculates the multiplication of all input values.

#### Parameter

| Field      | Value  | Description                                                                                                                                                              |
| ---------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name       | string | The name of the function: `Function.calculateMultiply`                                                                                                                   |
| sourceKeys | array  | The key names on which you want to calculate multiplication.                                                                                                             |
| resultKey  | string | The key name in which you want to store the final outcome of the function.                                                                                               |
| NAVIGATE   | string | The value of the card ID where you want to navigate after getting the result from the function. If you want to show results on the same card, then use the same card ID. |

{% code title="Example:" %}
```json
"cardUIAction": {
     "action1": {
        "action": [
        {
          "name": "Function.calculateMultiply",
          "url": "",
          "sourceKeys":["keyName1","keyName2","keyName3"],
          "sourceKey":"",
          "resultKey" : "KeyName3",
          "NAVIGATE":"cd-cost-preview"
         }
       ]
     }
   }
```
{% endcode %}

### Function.calculateDivide

Calculates the division of the input value.

#### Parameter

| Field     | Value  | Description                                                                |
| --------- | ------ | -------------------------------------------------------------------------- |
| name      | string | The name of the function: `Function.calculateDivision`                     |
| sourceKey | string | The key name that you want to get divided from the totalKey.               |
| totalKey  | string | The key name from which the source key value gets divided.                 |
| resultKey | string | The key name in which you want to store the final outcome of the function. |

{% code title="Example:" %}
```json
"cardUIAction": {
     "action1": {
        "action": [
        {
           "name": "Function.calculateDivide",
           "url": "",
           "sourceKeys":[],
           "sourceKey":"keyName1",
           "totalKey":"keyName2"
           "resultKey" : "KeyName3",
           "NAVIGATE":"cd-cost-preview"  
         }
       ]
     }
   }
```
{% endcode %}

### Function.calculatePercentage

Calculates the percentage of the input value.

#### Parameter

| Field     | Value  | Description                                                                                                                                                                                                   |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name      | string | The name of the function: `Function.calculatePercentage`                                                                                                                                                      |
| sourceKey | string | The key name that has the percentage value, like 10% should be used as 10, 20% should be used as 20.                                                                                                          |
| totalKey  | string | The key name on which sourceKey will be applied. For example, if sourceKey has a key name with a value of 10 and totalKey has a key name with a total value of 200, the outcome will be 10 \* 200 / 100 = 20. |
| resultKey | string | The key name on which the final outcome of the function is stored.                                                                                                                                            |
| NAVIGATE  | string | The value of the card ID where you want to navigate after getting the result from the function. If you want to show results on the same card, then use the same card ID.                                      |

{% code title="Example:" %}
```json
"cardUIAction": {
     "action1": {
        "action": [
        {
           "name": "Function.calculatePercentage",
           "url": "",
           "sourceKeys":[],
           "sourceKey":"keyName1",
           "totalKey":"keyName2"
           "resultKey" : "KeyName3",
           "NAVIGATE":"cd-cost-preview"
          }
        ]
      }
    }
```
{% endcode %}

## Validating data input

### Function.validateReferralCode

Validates if the referral code entered is a valid Care.Wallet ID.

#### Parameter

| Field     | Value  | Description                                                     |
| --------- | ------ | --------------------------------------------------------------- |
| name      | string | The name of the function: `Function.validateReferralCode`       |
| resultKey | string | The input key for referral code. For example: `{$ReferralCode}` |

{% code title="Example:" %}
```json
        "action2":{
            "action": [
                {
                    "name": "Function.validateReferralCode",
                    "resultKey": "{recipientPublicKey}"
                },
                {
                    "name": "e-w-parti-refer-trial"
                }
            ]
        } 
```
{% endcode %}

### Check field format and field value

Validates field format and value. This function is used in [SmartTile1](tiles.md#smarttile1-input-validation-tile).

#### Parameter

| Field       | Value  | Description                                                                                                                                                                                                                                                          |
| ----------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fieldFormat | string | <p>The name of the field value to be validated. The supported fieldFormat values are:</p><ul><li>age</li><li>email</li><li>pin</li><li>year</li><li>date</li><li>phone</li><li>country</li><li>ssn</li><li>otp</li><li>text</li><li>number</li><li>trialId</li></ul> |
| min         | string | The minimum length of the field value.                                                                                                                                                                                                                               |
| max         | string | The maximum length of the field value.                                                                                                                                                                                                                               |
| validation  | string | The validation whether field is required and the error message.                                                                                                                                                                                                      |
| name        | string | The validation whether field is required.                                                                                                                                                                                                                            |
| error       | string | The error message that shows when the value entered in invalid.                                                                                                                                                                                                      |

{% code title="Example:" %}
```json
{
    "id": "SmartTile1",
    "subView": [
        {
            "title": {
                "text": "5tile2iitextii7g0",
                "titleTextColor": "#000000",
                "titleAlign": "START"
            },
            "subTitle": {
                "text": "{$phoneValue}",
                "hint": "5tile2iihintiij3r",
                "subTitleTextColor": "#000000",
                "subTitleAlign": "START",
                "tip": "5tile2iitipiivqw",
                "fieldFormat": "phone",
                "min": "1",
                "max": "30",
                "validation": [
                    {
                        "name": "REQUIRED_FIELD",
                        "error": "5tile2iierroriinaz"
                    }
                ]
            },
            "img": {
                "text": "imageUrlktoxk",
                "isUrl": true,
                "height": "24",
                "width": "24"
            }
        }
    ],
    "borderColor": "#afafaf",
    "type": "CONTAINER",
    "uiAction": "",
    "order": 5
}
```
{% endcode %}

## Linking and navigation

### Function.Navigate

Moves to the destination card without calling events or event-handlers.

#### Parameter

| Field  | Value  | Description                                    |
| ------ | ------ | ---------------------------------------------- |
| name   | string | The name of the function: `Function.Navigate`  |
| cardId | string | The card ID reference of the destination card. |

{% code title="Example:" %}
```json
    "cardUIAction": {
        "action1": {
            "action": "HOME"
        },
        "action17d1": {
            "action": [
                {
                    "name": "Function.Navigate",
                    "cardId": "cd-bpmho1x359gohn1rw6xdppzkzu11"
                }
            ]
        },
        "action17d2": {
            "action": [
                {
                    "name": "Function.Navigate",
                    "cardId": ""
                }
            ]
        },
        "action17d3": {
            "action": [
                {
                    "name": "Function.Navigate",
                    "cardId": ""
                }
            ]
        }
    }
```
{% endcode %}

### Function.ChangeCard

Pushes to a new view after comparing the compareKey values.

#### Parameter

| Field                 | Value   | Description                                                                                               |
| --------------------- | ------- | --------------------------------------------------------------------------------------------------------- |
| name                  | string  | The name of the function: `Function.ChangeCard`                                                           |
| compareKey            | string  | The dynamic value based on results from another function.                                                 |
| compareValue          | integer | The fixed value to which the compareKey value is compared to.                                             |
| cardIdForGreaterValue | string  | The card ID that is viewed when the compareKey value is greater than the fixed value set in compareValue. |
| cardIdForLessValue    | string  | The card ID that is viewed when the compareKey value is less than the fixed value set in compareValue.    |
| cardId                | string  | The card ID of the current view.                                                                          |

{% code title="Example:" %}
```json
{
    "name": "Function.ChangeCard",
    "compareKey": "resultSum1",
    "compareValue": 60,
    "cardIdForGreaterValue": "cd-40yoxo205nu4sippxzmzj22mnn0",
    "cardIdForLessValue": "cd-34fdshqildm8ojse2tzu7jd85qj",
    "cardId": "cd-40yoxo205nu4sippxzmzj22mnn0"
}
```
{% endcode %}

### Function.deposit.SOLVE

Navigates from any card to the "SOLVE" tab view.

#### Parameter

| Field    | Value  | Description                                        |
| -------- | ------ | -------------------------------------------------- |
| uiAction | string | The name of the function: `Function.deposit.SOLVE` |

{% code title="Example:" %}
```json
{
    "id": "Tile14",
    "subView": [
        {
            "title": {
                "text": "2tile14iitextii8ek"
            },
            "img": {
                "text": "imageUrl8i1kh",
                "isUrl": true,
                "height": "25",
                "width": "25"
            }
        }
    ],
    "borderColor": "#afafaf",
    "type": "CONTAINER",
    "uiAction": "Function.deposit.SOLVE",
    "order": 2
}
```
{% endcode %}

### Multiple selection

Allows multiple item selection for [Tile12: Dropdown Option Selector](tiles.md#tile12-dropdown-option-selector).

#### Parameter

| Field       | Value  | Description                                                        |
| ----------- | ------ | ------------------------------------------------------------------ |
| fieldFormat | string | The value that allows selecting multiple items in a dropdown list. |

{% code title="Example:" %}
```json
{
    "id": "Tile12",
    "subView": [
        {
            "title": {
                "text": "4tile12iitextii0xr",
                "style": "REGULAR",
                "titleTextColor": "#000000",
                "titleAlign": "START",
                "fontSize": 16
            },
            "subTitle": {
                "text": "4tile12iitextii1w4",
                "fontSize": 16,
                "data": "4tile12iidataii9pw",
                "hint": "4tile12iihintiigmm",
                "keyboard": "text",
                "subTitleTextColor": "#000000",
                "subTitleAlign": "START",
                "fieldFormat": "multiple"
            },
            "img": {
                "text": "imageUrlltc9e",
                "isUrl": true,
                "height": "25",
                "width": "25"
            }
        }
    ],
    "borderColor": "#afafaf",
    "backgroundColor": "#ffffff",
    "borderWidth": 1,
    "type": "CONTAINER",
    "uiAction": "",
    "order": 4
}
```
{% endcode %}

### isLink or isUrl

Adds links inside the text of a tile, such as [Tile0: Text Label](tiles.md#tile0-text-label).

#### Parameter

| Field           | Value  | Description                                                                                       |
| --------------- | ------ | ------------------------------------------------------------------------------------------------- |
| isLink or isURL | string | To enable the link features in a tile, the value is set to `"true"`.                              |
| urls            | array  | The list of labels and URLs. If isLink or isURL is set to "true", then this property is required. |
| label           | string | The title or subtitle text that will be clickable from the tile.                                  |
| url             | string | The URL that opens when the label text is clicked.                                                |

{% code title="Example:" %}
```json
{
  "id": "Tile0",
  "subView": [
      {
          "title": {
              "text": "6tile0aiitextiicqd",
              "style": "REGULAR",
              "titleTextColor": "#000000",
              "titleAlign": "START",
              "isUrl": true,
              "urls": [
                  { 
                    "label":"Terms",
                    "url":"https://solve.care/carewallet-terms-and-conditions/" 
                  },
                  {
                    "label":"Privacy",
                    "url":"https://solve.care/carewallet-privacy-policy/" 
                  }
              ]
          }
      }
  ],
  "borderColor": "#afafaf",
  "type": "CONTAINER",
  "uiAction": "",
  "order": 7
},
```
{% endcode %}

### Function.CallEventHandler

Executes other functions to pass user input to the next card.

#### Parameter

| Field  | Value  | Description                                           |
| ------ | ------ | ----------------------------------------------------- |
| name   | string | The name of the function: `Function.CallEventHandler` |
| method | string | The user input data to pass to the next card.         |

{% code title="Example:" %}
```json
        "action3": {
            "action": {
                "name": "Function.CallEventHandler",
                "method": "DETAILS",
                "NAVIGATION": "cd-participants-terms"
            }
        }
```
{% endcode %}

### Function.COPY.TEXT

Copies the subtitle or title text from specific tiles.

#### Parameter

| Field    | Value  | Description                                    |
| -------- | ------ | ---------------------------------------------- |
| uiAction | string | The name of the function: `Function.COPY.TEXT` |

{% code title="Example:" %}
```json
{
    "id": "Tile0a",
    "subView": [
        {
            "title": {
                "text": "0tile0aiitextiictl",
                "style": "BOLD",
                "titleTextColor": "#000000",
                "titleAlign": "START"
            },
            "subTitle": {
                "text": "0tile0aiitextiiocy",
                "style": "REGULAR",
                "subTitleTextColor": "#000000",
                "subTitleAlign": "END"
            }
        }
    ],
    "borderColor": "#afafaf",
    "type": "CONTAINER",
    "uiAction": "Function.COPY.TEXT",
    "order": 1
}
```
{% endcode %}

### Function.camera\_selfie

Captures a selfie or selects from the gallery.

#### Parameter

| Field     | Value  | Description                                                                                                      |
| --------- | ------ | ---------------------------------------------------------------------------------------------------------------- |
| name      | string | The name of the function: `Function.camera_selfie`                                                               |
| resultKey | string | The key name which will save the image in base64 format and will be added to the payload to be sent to the node. |

{% code title="Example:" %}
```json
"cardUIAction": {
     "action1": {
        "action":[
        {
          "name": "Function.camera_selfie",
          "resultKey" : "KeyName",
          "NAVIGATE":"cd-cost-preview"
         }
       ]
     }
   }
```
{% endcode %}

### Function.uploadFiles

Uploads multiple files in `AttachmentUploadTile`.

#### Parameter

| Field        | Value  | Description                                                                                                                             |
| ------------ | ------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| name         | string | The name of the function: `Function.uploadFiles`                                                                                        |
| sourceKeys   | array  | The input key of the AttachmentUploadTile. For example, for input key `{$attachingFiles}`, the value for sourceKey is "attachingFiles". |
| resultKey    | string | The final submit key for storing data.                                                                                                  |
| timestampKey | string | The time in milliseconds when the file is successfully uploaded.                                                                        |

{% code title="Example:" %}
```json
{
  "id": "AttachmentUploadTile",
  "subView": [
      {
          "title": {
              "text": "1tile13iitextiiacf",
              "style": "REGULAR",
              "titleTextColor": "#000000",
              "titleAlign": "START",
              "fontSize": 16
          },
          "subTitle": {
              "text": "{$attachingFiles}",
              "fontSize": 16,
              "fileType": "PDF,PNG,JPG",
              "hint": "1tile13iihintii9rf",
              "subTitleTextColor": "#000000",
              "subTitleAlign": "START"
          }
      }
  ],
  "borderColor": "#afafaf",
  "backgroundColor": "#ffffff",
  "borderWidth": 1,
  "type": "CONTAINER",
  "uiAction": "",
  "order": 2
}
```
{% endcode %}

{% code title="Example:" %}
```json
"cardUIAction": {
    "action394": {
        "action": [
            {
                "name": "Function.uploadFiles",
                "sourceKeys": ["attachingFiles"],
                "resultKey": "record_folder_ref",
                "timestampKey": "createdAt"
            },
            {
                "name": "e-w-pt-save-pt_da-ms3o"
            }
        ]
    }
}
```
{% endcode %}
