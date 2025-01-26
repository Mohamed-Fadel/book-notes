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

---

# Chapter 2: Organizing the Domain Logic (POEAA Notes)

In software design, organizing domain logic is crucial for building maintainable, scalable, and efficient applications. This chapter of *Patterns of Enterprise Application Architecture (POEAA)* by Martin Fowler outlines **three primary patterns** for domain logic organization:

1. **Transaction Script**  
2. **Domain Model**  
3. **Table Module**

## 1. Transaction Script

The **Transaction Script** pattern structures the application logic around procedures. Each procedure corresponds to a specific action or use case.

### How It Works:
- Accepts **data and inputs** from the presentation layer.
- Processes the inputs with **validations and calculations**.
- Stores or retrieves data in the database.
- Interacts with external systems, if necessary.
- Returns data or responses to the presentation layer (often with formatted results).

The **structure** is straightforward: one procedure per action.

### Advantages of Transaction Script:
- **Simplicity**: A clean, easy-to-understand procedural model.
- **Compatibility**: Works well with data source patterns like **Row Data Gateway** or **Table Data Gateway**.
- **Clear Transaction Boundaries**: Makes it easier for tools to manage transactions automatically.

### Disadvantages of Transaction Script:
- **Scalability Issues**: As domain logic grows, the script's complexity increases.
- **Code Duplication**: Repeated logic across different scripts can lead to maintenance challenges.

## 2. Domain Model

In the **Domain Model** pattern, logic is distributed across models. Each model encapsulates both **behavior** and **data**.

### Characteristics:
- Represents the real-world domain with rich, object-oriented abstractions.
- Models focus on solving the business problem, not just database interactions.

### Advantages of Domain Model:
- Leverages the **power of object-oriented programming** (inheritance, encapsulation, and polymorphism).
- Provides a more natural and reusable way to handle complex domains.

### Disadvantages of Domain Model:
- **Abstraction Challenges**: Designing effective abstractions and models can be difficult.
- **Data Source Complexity**: Adapting domain models to interact with complex database layers requires effort.

## 3. Table Module

The **Table Module** pattern organizes domain logic around database tables rather than objects. Unlike Domain Model, it works with **one instance for the entire table** and often utilizes **Record Sets**.

### Characteristics:
- Centralizes domain logic for each table into a single class or module.
- Avoids scattering logic across individual objects.

### Advantages of Table Module:
- **Integration**: Works seamlessly with architectures relying on **Record Sets**.

### Disadvantages of Table Module:
- Not explicitly detailed in this chapter. However, complexity and limited flexibility might be considerations.

## 4. Service Layer

The **Service Layer** provides a facade for business logic, isolating the presentation layer from the domain logic.

### How It Works:
- The **presentation logic** interacts with the domain layer exclusively through the Service Layer.
- Business logic is encapsulated in **transaction scripts** or **use-case controllers** inside the service.
- Domain models may become a direct representation of the database, without much behavior.

### Tips for Service Layer:
- **Keep It Thin**: Design the Service Layer as a facade that delegates to underlying domain objects.
- **Controller-Entity Style**: Maintain domain models as one-to-one representations of the database, and place business logic in controllers or services.

## Summary: Choosing the Right Pattern

- **Transaction Script**: Best for simple applications or where procedural logic is sufficient.
- **Domain Model**: Ideal for complex domains requiring rich behavior and abstraction.
- **Table Module**: Suits systems heavily reliant on Record Sets and centralized table-based logic.
- **Service Layer**: Acts as a glue between presentation and domain logic, providing a clear separation of concerns.

