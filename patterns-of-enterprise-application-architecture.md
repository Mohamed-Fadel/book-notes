# Patterns of Enterprise Application Architecture

## Chapter 1: Layering

### Overview
Layering is a fundamental concept in designing enterprise applications. It organizes code into different levels or layers, where each layer provides services to the layer above it and uses services from the layer below.

### Basic Example
A simple example of layering in networking:

```
FTP < TCP < IP < Ethernet
```

In this model:
- Higher-level protocols depend on lower-level services.

### Key Points

- **Client-Server Systems**: The rise of client-server architecture emphasizes the importance of layering.
- **Enterprise Layers**: Typical layers in an enterprise application include:
  - **Presentation Layer**: Handles user interaction.
  - **Domain Layer**: Manages business logic.
  - **Data Layer**: Handles data storage and access.

### Layering Relationships
- The **presentation layer** can access the data store directly or through the domain layer.
- The **domain layer** abstracts the data sources from the presentation layer.
- For large or complex applications, each layer can be implemented in separate packages or modules.

### Hexagonal Architecture
- Both the **presentation** and **data source** layers connect to the external world.
- Hexagonal architecture visualizes the system as a core module surrounded by interfaces to external systems.
- **Key Principle**: Data and domain layers should not depend on the presentation layer.

### Client-Side Logic
- Moving logic to the client side reduces server calls, ensuring responsiveness and disconnected operation.
- However, this requires **synchronization logic** to manage state consistency.

### Code Splitting Across Machines
To split code across different machines, consider using these design patterns:
- **Remote Facade**: Simplifies remote communication.
- **Data Transfer Objects (DTOs)**: Efficiently pass data between systems.

### Complexity Boosters
Managing complexity in enterprise applications requires careful handling of various factors:

1. **Distribution**: Components deployed across different machines.
2. **Multi-threading**: Multiple operations happening simultaneously.
4. **Paradigm Chasms**: Bridging differences between object-oriented and relational systems.
5. **Multiplatform Development**: Supporting diverse platforms and environments.
6. **Extreme Performance Requirements**: Handling high transaction rates (e.g., 1,000 transactions per second).

### Conclusion
Understanding and applying layering principles help create scalable, maintainable, and robust enterprise applications. Techniques like hexagonal architecture and proper design patterns mitigate complexity and improve system efficiency.
