---
description: This section describes the overview of steps in authoring a network.
---

# Building a Network

### Define the structure of the input.json file

1. Open the file in a text editor, and then enter the [network details](network-configuration.md#network-metadata).
2. In the network settings, fill in the [author details and included countries](network-configuration.md#author-details-and-countries).
3. Configure the [join network settings](network-configuration.md#join-network-settings) and [solve token usage](network-configuration.md#solve-token-settings).
4. Add the [roles](roles-and-journeys.md#roles) and [journeys](roles-and-journeys.md#journey).
5. Declare the included [cards](card-definitions/#cards), [events](events-and-event-handlers.md), and [event handlers.](events-and-event-handlers.md)
6. Save and validate the input.json file.

{% hint style="warning" %}
**Note:** Based on the protocol requirements, make sure that each value follows the specified format.&#x20;
{% endhint %}

### Create the card definitions, events, and event handlers&#x20;

* Define the [card structure](card-definitions/#card-definition-structure).
* Configure wallet events and event handlers.
* Configure node events and event handlers.
* Define the transactional data structure.

### Configure Python node event handlers

* Understand the predefined functions in the [Python template](python-event-handlers.md#python-event-handler-template).
* Perform the steps to configure the network based on the [use case example](python-event-handlers.md#use-case-example).

