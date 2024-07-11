# Getting Started

**Care.Protocol** defines the rules governing information communication within Care.Networks. It uses an event-driven architecture with a predefined structure in JSON files. These files define configurations for roles, relationships, journeys, events, and interactions within the network.

In this guide, you'll learn how to manually author Care.Protocol using provided examples.

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

Before you begin, ensure you have the following:

* An Integrated Development Environment (IDE) or a text editor to manually author files.
* The required Python packages to configure and run Python event handlers in Care.Protocol.
* Postman API platform and the network environment details for publishing.
* BrowserStack, a cloud web and mobile testing platform, for testing the application.

