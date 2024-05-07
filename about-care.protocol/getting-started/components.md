---
description: >-
  This section describes the structured files and modules that can be configured
  in Care.Protocol.
---

# Components

### input.json

The _input.json_ file is a hierarchical structure of objects defined within a network. It contains information about the network, roles, journeys, cards, events, event handlers, and care ledgers.

### Care Data Node (CDN)

Care Data Node is the database of the network. It retrieves external data and converts them into events in a network. It is used to interface a network with external client systems, such as electronic medical records, member management systems, and payment systems.

### Care.Card definitions

Care.Card is a decentralized application within a network that contains data types, user interface elements, and interactive functions that are triggered by events. The Care.Card definition structure contains card data, card layout, card footer, and card UI actions.

### Event definitions

The events define the actions of each role in a network, such as sending and receiving information. An event is chained in time series on a blockchain that creates a secure and transparent record of transactions within a network.

### Event handlers

An event handler is a set of business rules associated with an event or message for each role. It is configured to execute a set of predefined actions in response to a specific event. Depending on the requirements, event handlers can also be set up to handle errors or exceptions.

### Python event handlers

Python event handlers are designed to execute complex events and transactions that require data processing, analysis, import and export. A Python event handler can fetch external data in various formats such as HL7, X12 EDI, XML, JSON, or CSV.

### Resources

The resources contain a collection of predefined data that are inserted or updated automatically during initialization.&#x20;

### Transactional data

Transactional data contains a collection of configurable data that can be referenced from roles, cards, or events within the network.
