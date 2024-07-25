---
description: >-
  This section provides an overview of the steps to author the protocol for
  building decentralized applications (dApps).
---

# Build a dApp

{% hint style="warning" %}
**Note:** Ensure that each field and value follows the specified structure according to the protocol requirements.
{% endhint %}

## Understand the structure of the `input.json` file

* Open the `input.json` file in a text editor.
* View or modify the [network details](network-configuration.md#network-metadata).
* In the network settings, fill in the [author details](network-configuration.md#author-details-and-countries) and specify the [supported countries](network-configuration.md#author-details-and-countries).
* Configure the [join network settings](network-configuration.md#join-network-settings) and set up [solve token usage](network-configuration.md#solve-token-settings).
* Define the [roles](roles-and-journeys.md#roles) and [journeys](roles-and-journeys.md#journeys).
* Declare the included [cards](card-definitions/#cards), [events](events-and-event-handlers.md#events), and [event handlers](events-and-event-handlers.md#event-handlers).
* If necessary, include details about [care ledgers](../../care.wallet-user-manual/care.ledger.md).
* Save and validate the `input.json` file.

## Define the data structure

* Create a [data definition file](care-data-node.md#data-definition-file) based on how you want to organize data.
* Define the structure of the [transactional data](transactional-data.md).

## Create the definitions for cards&#x20;

* Define the [card structure](card-definitions/#card-definition-structure), including [tiles](card-definitions/tiles.md) and [functions](card-definitions/functions.md).

## Create events and event handler definitions

* Configure the [events](events-and-event-handlers.md#events) and [event handlers](events-and-event-handlers.md#event-handlers).
* Configure [node event handlers](node-event-handlers.md).

## Configure Python event handlers

* Understand the predefined functions in the [Python template](python-event-handlers.md#python-event-handler-template).
* Perform the steps to configure an event based on the [use case example](python-event-handlers.md#use-case-example).

