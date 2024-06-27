# Architecture

## Presentation Layer

The **Presentation Layer** enables users to interact securely with cards, journeys, networks, and personal data.

* **Care.Wallet**: A mobile app that serves as a gateway for users to join a Care.Network and use personalized healthcare services.
* **Journeys**: A sequence of interconnected cards within a Care.Network, defining specific workflows for roles such as patients, doctors, and nurses.
* **Care.Cards**: Contain pieces of information, such as text and images, and buttons that users interact with on the app's user interface.

## Application Layer

The **Application Layer** manages configuration, administration, and communication within networks, including external sources.

* **Care.Network**: A digital network of various healthcare roles that operates based on a specific set of rules defined in a Care.Protocol.
* **Care.Protocol**: Provides the governing rules and definitions of events and event handlers to facilitate secure transactions of roles and nodes within a network.
* **Care Data Node**: A specialized node created for each network to manage the storage and processing of data files, as well as data exchanges with external systems.

## Services Layer

The **Services Layer** manages the core operations and management of nodes, ensuring secure transmission of data and events across the network.

* **Network Onboarding Manager (NOM)**: Facilitates the initial creation and assignments of Care.Nodes upon joining the network.
* **Node Lifecycle Manager (NLM)**: Manages the creation and lifecycle states of Care.Nodes, such as active, start, stop, and hibernate.
* **Base Node Services (BNS)**: Facilitates the secure transmission of events and data through the blockchain.

## Blockchain Layer

The **Blockchain Layer** provides secure, transparent, and decentralized data storage and recording of transactions.

* **Care.Node**: Facilitates data storage and event handling across the network. It is a small, secure, versatile object that can be deployed in any environment.
* **MainNet**: Holds the core registry service that maps Care.Wallet users to their respective Care.Networks, such as the country matrix for region-based services.
* **Node Vault**: Facilitates the secure storage and management of personal data for the Care.Node, with data backups stored in [Storj](https://www.storj.io/).
* **Event Ledger**: Records the event logs, including payload data such as sending information from a sender node address to a recipient node address.
