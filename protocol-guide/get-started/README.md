# Get Started

**TuumIO** **Protocol** defines the rules governing information communication and data exchange. It employs an event-driven architecture and utilizes JSON files to represent configurations for roles, relationships, journeys, events, and interactions. By using standard data structures, it reduces complexity and enables interoperability between systems.

In this guide, you'll learn how to manually author TuumIO Protocol using provided examples.

### Structure of files and folders

<pre><code>├── sample-network/
     ├── definitions/
     │    ├── card/
<strong>     │    ├── ddf/     
</strong>     │    ├── event/
     │    ├── event-handler/
     │    ├── python-event-handler/
     │    ├── resources/
     │    └── td/
     └── input.json 
</code></pre>

### Prerequisites

Before you begin, ensure you have the following:

* An Integrated Development Environment (IDE) or a text editor to manually author files.
* The required Python packages to configure and run Python event handlers.
* Postman API platform and the network environment details for publishing.
* BrowserStack, a cloud web and mobile testing platform, for testing the application.

