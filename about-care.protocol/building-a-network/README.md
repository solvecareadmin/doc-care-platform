---
description: This section describes the overview of steps in authoring a network.
---

# Building a Network

### Define the structure of the `input.json` file

{% hint style="warning" %}
**Note:** Based on the protocol requirements, make sure that each value follows the specified format.&#x20;
{% endhint %}

* Open the `input.json` file in a text editor, and then enter the [network details](network-configuration.md#network-metadata).
* In the network settings, fill in the [author details and included countries](network-configuration.md#author-details-and-countries).
* Configure the [join network settings](network-configuration.md#join-network-settings) and [solve token usage](network-configuration.md#solve-token-settings).
* Add the [roles](roles-and-journeys.md#roles) and [journeys](roles-and-journeys.md#journeys).
* Declare the included [cards](card-definitions/#cards), [events](events-and-event-handlers.md#events), and [event handlers](events-and-event-handlers.md#event-handlers).
* Save and validate the `input.json` file.

### Define the data structure

* Create a [data definition file](care-data-node.md#data-definition-file).
* Define the [transactional data](transactional-data.md) structure.

### Create the definitions for cards, events, and event handlers

* Define the [card structure](card-definitions/#card-definition-structure).
* Create the event and event handler [definitions](events-and-event-handlers.md#definitions).

### Configure Python event handlers

* Understand the predefined functions in the [Python template](python-event-handlers.md#python-event-handler-template).
* Perform the steps to configure an event based on the [use case example](python-event-handlers.md#use-case-example).

