
# Software Application Architectural Patterns

A practical overview of modern software architecture styles, tradeoffs, and use cases.

---

layout: center
---

# What is Software Architecture?

Software architecture defines:

- System structure
- Component interactions
- Data flow
- Scalability model
- Deployment boundaries
- Maintainability strategy

---

# Architecture Categories

```mermaid
mindmap
  root((Software Architecture))
    Monolithic
      Layered
      Modular Monolith
    Distributed
      Microservices
      SOA
      Event-Driven
    Domain-Centric
      Hexagonal
      Clean
      Onion
    UI Patterns
      MVC
      MVVM
    Specialized
      CQRS
      Event Sourcing
      Serverless
      Pipe and Filter
      Microkernel
```

---

# 1. Layered Architecture (N-Tier)

## Structure

- Presentation Layer
- Business Logic Layer
- Data Access Layer
- Database Layer

### Advantages

- Easy to understand
- Clear separation
- Good for CRUD systems

### Disadvantages

- Tight coupling over time
- Performance overhead

---

# Layered Architecture Diagram

```mermaid
flowchart TD
    UI[Presentation Layer]
    BL[Business Logic Layer]
    DAL[Data Access Layer]
    DB[(Database)]

    UI --> BL
    BL --> DAL
    DAL --> DB
```

---

# 2. Monolithic Architecture

Entire application deployed as one unit.

### Characteristics

- Single codebase
- Single deployment artifact
- Shared database

### Best For

- MVPs
- Small teams
- Early-stage startups

---

# Monolithic Architecture Diagram

```mermaid
flowchart TD
    Client[Client]

    subgraph Monolith
      UI[UI]
      Auth[Auth Module]
      Billing[Billing Module]
      Orders[Orders Module]
      DB[(Shared Database)]
    end

    Client --> UI
    UI --> Auth
    UI --> Billing
    UI --> Orders
    Auth --> DB
    Billing --> DB
    Orders --> DB
```

---

# 3. Microservices Architecture

Application split into independently deployable services.

### Characteristics

- Independent scaling
- Independent deployments
- Service ownership

### Challenges

- Distributed complexity
- Observability
- Network latency

---

# Microservices Diagram

```mermaid
flowchart LR
    Client --> Gateway[API Gateway]

    Gateway --> Auth[Auth Service]
    Gateway --> Orders[Orders Service]
    Gateway --> Billing[Billing Service]
    Gateway --> Inventory[Inventory Service]

    Auth --> DB1[(Auth DB)]
    Orders --> DB2[(Orders DB)]
    Billing --> DB3[(Billing DB)]
    Inventory --> DB4[(Inventory DB)]
```

---

# 4. Service-Oriented Architecture (SOA)

Enterprise integration-focused architecture.

### Characteristics

- Enterprise Service Bus (ESB)
- Shared enterprise services
- Heavy governance

---

# SOA Diagram

```mermaid
flowchart TD
    App1[CRM]
    App2[ERP]
    App3[HR System]

    ESB[Enterprise Service Bus]

    Shared[Shared Services]

    App1 --> ESB
    App2 --> ESB
    App3 --> ESB

    ESB --> Shared
```

---

# 5. Event-Driven Architecture

Systems communicate through asynchronous events.

### Technologies

- Kafka
- RabbitMQ
- Pulsar

### Benefits

- Scalability
- Loose coupling
- Real-time responsiveness

---

# Event-Driven Diagram

```mermaid
flowchart LR
    Producer[Order Service]
    Broker[(Event Broker)]
    Consumer1[Billing Consumer]
    Consumer2[Inventory Consumer]
    Consumer3[Notification Consumer]

    Producer --> Broker
    Broker --> Consumer1
    Broker --> Consumer2
    Broker --> Consumer3
```

---

# 6. Hexagonal Architecture

Also called Ports and Adapters.

### Core Principle

Business logic isolated from infrastructure.

---

# Hexagonal Architecture Diagram

```mermaid
flowchart TD
    UI[Web UI]
    API[REST API]
    DB[(Database)]
    MQ[Message Queue]

    subgraph Core Domain
      Logic[Business Logic]
    end

    UI --> Logic
    API --> Logic
    Logic --> DB
    Logic --> MQ
```

---

# 7. Clean Architecture

Dependencies point inward.

### Layers

- Entities
- Use Cases
- Interface Adapters
- Frameworks

---

# Clean Architecture Diagram

```mermaid
flowchart TD
    Frameworks[Frameworks & Drivers]
    Adapters[Interface Adapters]
    UseCases[Use Cases]
    Entities[Entities]

    Frameworks --> Adapters
    Adapters --> UseCases
    UseCases --> Entities
```

---

# 8. MVC Pattern

Separates UI responsibilities.

### Components

- Model
- View
- Controller

---

# MVC Diagram

```mermaid
flowchart LR
    User --> Controller
    Controller --> Model
    Model --> View
    View --> User
```

---

# 9. MVVM Pattern

Popular in frontend and mobile apps.

### Used In

- Angular
- SwiftUI
- WPF
- Android

---

# MVVM Diagram

```mermaid
flowchart LR
    View --> ViewModel
    ViewModel --> Model
    Model --> ViewModel
    ViewModel --> View
```

---

# 10. CQRS

Separate read and write models.

### Benefits

- Optimized scaling
- Flexible queries

### Drawbacks

- Complexity
- Synchronization overhead

---

# CQRS Diagram

```mermaid
flowchart TD
    Client[Client]

    Command[Command API]
    Query[Query API]

    WriteDB[(Write DB)]
    ReadDB[(Read DB)]

    Client --> Command
    Client --> Query

    Command --> WriteDB
    WriteDB --> ReadDB
    Query --> ReadDB
```

---

# 11. Event Sourcing

Store changes as immutable events.

### Example Events

- OrderCreated
- PaymentReceived
- ShipmentSent

---

# Event Sourcing Diagram

```mermaid
flowchart LR
    Commands[Commands]
    Events[(Event Store)]
    Projections[Read Models]

    Commands --> Events
    Events --> Projections
```

---

# 12. Serverless Architecture

Functions executed on demand.

### Platforms

- AWS Lambda
- Azure Functions
- Google Cloud Functions

---

# Serverless Diagram

```mermaid
flowchart TD
    Client --> API[API Gateway]
    API --> F1[Lambda Function A]
    API --> F2[Lambda Function B]
    API --> F3[Lambda Function C]

    F1 --> DB[(Cloud DB)]
    F2 --> DB
    F3 --> DB
```

---

# 13. Modular Monolith

Structured monolith with strong module boundaries.

### Advantages

- Simpler than microservices
- Better maintainability
- Easier migration path

---

# Modular Monolith Diagram

```mermaid
flowchart TD
    subgraph Application
      Auth[Auth Module]
      Orders[Orders Module]
      Billing[Billing Module]
      Inventory[Inventory Module]
    end

    DB[(Shared Database)]

    Auth --> DB
    Orders --> DB
    Billing --> DB
    Inventory --> DB
```

---

# 14. Microkernel / Plugin Architecture

Core system extended via plugins.

### Examples

- VS Code
- WordPress
- Eclipse

---

# Plugin Architecture Diagram

```mermaid
flowchart TD
    Core[Core System]

    Plugin1[Plugin A]
    Plugin2[Plugin B]
    Plugin3[Plugin C]

    Plugin1 --> Core
    Plugin2 --> Core
    Plugin3 --> Core
```

---

# 15. Pipe-and-Filter Architecture

Data processed through sequential stages.

### Common Uses

- ETL pipelines
- Media processing
- Compilers

---

# Pipe-and-Filter Diagram

```mermaid
flowchart LR
    Input[Input]
    Filter1[Transform]
    Filter2[Validate]
    Filter3[Enrich]
    Output[Output]

    Input --> Filter1 --> Filter2 --> Filter3 --> Output
```

---

# Modern Architecture Evolution

```mermaid
flowchart LR
    Monolith --> ModularMonolith[Modular Monolith]
    ModularMonolith --> Microservices
    Microservices --> EventDriven[Event-Driven System]
```

---

# Architecture Comparison Matrix

| Pattern | Complexity | Scalability | Team Size | Best For |
|---|---|---|---|---|
| Monolith | Low | Medium | Small | MVPs |
| Layered | Low | Medium | Small-Medium | CRUD apps |
| Modular Monolith | Medium | High | Medium | Growing products |
| Microservices | High | Very High | Large | Enterprise scale |
| Event-Driven | High | Very High | Large | Real-time systems |
| Clean/Hexagonal | Medium | High | Medium | Complex domains |
| Serverless | Medium | Auto | Small-Medium | Event workloads |

---

# Recommended Architecture Journey

```mermaid
journey
    title Typical System Evolution
    section Startup
      Monolith: 5: Team
      Layered App: 4: Team
    section Growth
      Modular Monolith: 5: Engineering
      Domain Separation: 4: Engineering
    section Scale
      Microservices: 3: Platform
      Event-Driven: 4: Platform
```

---

# Choosing the Right Architecture

Consider:

- Team size
- Deployment frequency
- Scalability requirements
- Operational maturity
- Business complexity
- Domain boundaries
- Budget and infrastructure

---

# Key Takeaways

- No architecture is universally best
- Simplicity wins early
- Complexity should be earned
- Modular monoliths are often underrated
- Microservices solve organizational scaling more than technical scaling
- Event-driven systems require operational maturity

---

# Final Thought

> "Architecture is the set of decisions you wish you could get right early."

---

# Thank You

Questions?
