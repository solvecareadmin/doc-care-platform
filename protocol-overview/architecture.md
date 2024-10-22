# Architecture

<figure><img src="../.gitbook/assets/platform-tuumIO-architecture (1).png" alt=""><figcaption><p>Figure 4: High-level Platform Architecture</p></figcaption></figure>

## Application Layer

The **Application Layer** handles configuration, administration, and communication within networks, allowing users to interact with decentralized applications (dApps).

* **TuumIO Wallet**: A mobile app that allows users to store and manage digital assets and serves as a gateway to various industry services and dApps.
* **Journeys**: A sequence of interconnected cards outlining specific workflows for roles such as participants, administrators, managers and employees.
* **TuumIO Card**: An interactive module that combines text, images, buttons, and interoperable functions on the app's user interface.
* **TuumIO Network**: A digital network of various healthcare roles, operating based on the rules defined in the TuumIO Protocol.
* **TuumIO Protocol**: A governance framework that defines the rules for data exchange and communication, facilitating secure transactions and interactions within the network.

## Data Layer

The **Data Layer** provides secure, transparent, decentralized data storage and records management.

* **MainNet**: Holds the core registry service that maps TuumIO Wallet users to their respective TuumIO Networks, such as the country matrix for region-based services.
* **Node Vault**: A secure and decentralized storage of data for TuumIO Nodes, with backups stored in [Storj](https://www.storj.io/).
* **Event Ledger**: A decentralized, immutable record of event logs from sender and recipient node addresses, including payload data.
* **TuumIO Data Node (CDN)**: A specialized node created for each network. It manages data storage, processing, and exchanges with external systems.

## Compute Layer

The **Compute Layer** manages core operations and node management, ensuring secure data and event transmission across the network.

* **TuumIO Node**: An entity that manages data storage and event handling across the network. It is a secure, versatile object deployable in any environment.
* **Network Onboarding Manager (NOM)**: Facilitates the initial creation and assignments of TuumIO Nodes upon joining the network.
* **Node Lifecycle Manager (NLM)**: Manages the creation and lifecycle states of TuumIO Nodes, including active, start, stop, and hibernate states.
* **Base Node Services (BNS)**: Ensures secure transmission of events and data through the blockchain.

