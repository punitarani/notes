# Distributed Computing Basics

## 2-Tiered Architecture

- This is a classic client-server system.
- It is modelled as a set of services provided by the servers and a set of clients.
- Clients know Servers but Servers may not know Clients.
- Clients and Servers are logical processes: they could reside on different or same processors.

## 3-Tiered Architecture

1. Presentation Layer (GUI)
    - Handles the user interface and the interaction with the user.
2. Application Processing Layer
    - Handles the business logic and the interaction with the database.
3. Data Management Layer
    - Handles the storage and retrieval of data.

- This is a more balanced approach allowing for better performance.
- It is also simpler to maintain and scale.

## Four-Tiered Architecture

4. Service Repository Layer
    - Handles the communication between the Application Processing Layer and the Data Management Layer.
