---
description: This section describes the overview of steps in authoring a network.
---

# Building a Network

### Define the structure of the _input.json_ file

{% hint style="warning" %}
**Note:** Based on the protocol requirements, make sure that each value follows the specified format.&#x20;
{% endhint %}

* Open the _input.json_ file in a text editor, and then enter the [network details](network-configuration.md#network-metadata).
* In the network settings, fill in the [author details and included countries](network-configuration.md#author-details-and-countries).
* Configure the [join network settings](network-configuration.md#join-network-settings) and [solve token usage](network-configuration.md#solve-token-settings).
* Create a Data Definition File (DDF) structure.
* Add the [roles](roles-and-journeys.md#roles) and [journeys](roles-and-journeys.md#journey).
* Declare the included [cards](card-definitions/#cards), [events](events-and-event-handlers.md#events), and [event handlers](events-and-event-handlers.md#event-handlers).
* Save and validate the _input.json_ file.

### Create the card definitions, events, and event handlers&#x20;

* Define the [card structure](card-definitions/#card-definition-structure).
* Create the event and event handler [definitions](events-and-event-handlers.md#definitions).
* Define the transactional data structure.

### Configure Python event handlers

* Understand the predefined functions in the [Python template](python-event-handlers.md#python-event-handler-template).
* Perform the steps to configure an event based on the [use case example](python-event-handlers.md#use-case-example).

