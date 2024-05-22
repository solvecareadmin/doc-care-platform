---
description: >-
  This section describes the structured files and modules that can be configured
  in Care.Protocol.
---

# Components

### `input.json`

The `input.json` file is a hierarchical structure of objects defined within a network. It contains information about the network, roles, journeys, cards, events, event handlers, and care ledgers.

### Care Data Node

The Care Data Node (CDN) serves as the network's central database for storing and processing data files. It additionally facilitates data exchange with external client systems, including electronic medical records, claims systems, member systems, and payment systems.

### Care.Card definitions

A Care.Card is a decentralized application within a network. It comprises data types, user interface elements, and interactive functions that respond to events. The Care.Card definition structure contains card data, layout, card footer, and UI actions.

### Event definitions

The events define the actions of each role in the network, such as sending and receiving information. An event is chained together in a time series on a blockchain, creating a secure and transparent record of transactions within a network.

### Event handlers

An event handler is a set of business rules associated with a specific event or message for each role or node within the network. It is configured to execute predefined actions in response to the event.

### Python event handlers

Python event handlers are designed to execute complex events and transactions that require data processing, analysis, import, and export. A Python event handler can fetch external data in HL7, X12 EDI, XML, JSON, or CSV formats.

### Resources

The resources contain predefined data that are inserted or updated automatically during initialization.&#x20;

### Transactional data

Transactional data contains configurable data that can be referenced from roles, cards, or events within the network.
