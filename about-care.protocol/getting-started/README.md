# Getting Started

**Care.Protocol** is a set of rules that govern how information is communicated in care networks. It is an event-driven architecture design that contains a predefined structure in JSON files. These structured files define the configurations for roles, relationships, journeys, events, and interactions in a network.

In this guide, you will learn how to author a network manually using the examples provided.

### Structure of files and folders

```
├── sample-network/
     ├── definitions/
     │    ├── card/
     │    ├── event/
     │    ├── event-handler/
     │    ├── python-event-handler/
     │    ├── resources/
     │    └── td/
     └── input.json 
```

### Prerequisites

Before you begin, make sure you have the following:

* An Integrated Development Environment (IDE) or a basic text editor for authoring files manually
* Python packages to configure and run Python Event Handlers in Care.Protocol
* Postman API platform and the network environment details for publishing
* BrowserStack, a cloud web and mobile testing platform for testing the application

