---
description: >-
  This section describes the structured files and modules that can be configured
  in TuumIO Protocol.
---

# Components

### `input.json`

The `input.json` file is a hierarchical structure of objects defined within a network. It contains information about the network, roles, journeys, cards, events, event handlers, and TuumIO ledgers.

### TuumIO Data Node

The TuumIO Data Node (TDN) serves as the network's central database for storing and processing data files. It facilitates data exchange with external client systems, including electronic medical records, claims systems, member systems, and payment systems.

### TuumIO Card definitions

A TuumIO Card is an interactive module encapsulating multiple data types, user interface elements, and interoperable functions. The TuumIO Card definition structure includes card data, layout, card footer, and UI actions.

### Event definitions

Events define the interactions and communication between roles or nodes in the network, such as sending and receiving information. Events are chained together in a time series on a blockchain, creating a secure, transparent, and immutable record of transactions within the network.

### Event handlers

An event handler is a set of instructions that execute tasks based on specific events. These tasks include updating records, transforming data, and identifying recipients for the next event.

### Python event handlers

Python event handlers are designed to execute complex events and transactions that require data processing, analysis, import, and export. They can fetch external data in HL7, X12 EDI, XML, JSON, or CSV formats.

### Resources

Resources contain predefined data that is inserted or updated automatically during initialization.

### Transactional data

Transactional data consists of configurable data that can be referenced from roles, cards, or events within the network.
