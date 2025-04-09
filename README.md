# Motivation for Software Architecture
1. Low quality product -> Customers will leave
2. Poorly Structured software that is hard to maintain -> Constant rework + low profit margin
3. Daunting for existing developers -> Developers get demoralized and leave
4. Difficult to for new developers to learn -> Will be reluctant to join, low productivity

# What is "Good" Architecture?
Good Architeture is contextual depending upon many factors;
1. Envrionment
2. Scale
3. Customers
4. Budget

# Software
Computer programs, procedures and possibly associated documenetation and data pertaining to the operation of a computer system.

1. Programs - Multiple applications
2. Proceducres - Version Control, Review Process, Release Process
3. Documentation - Developer / User Guide
4. Data - Files / Databases

Software architecture is essential for a long-term success of "Software intensive systems".

# Software Intensive System
A system for which software is a major technical challenge and is perhaps the major factor that affects system schedule, cost, and risk.

<b>System</b> is combination of interacting elements organized to achieve one or more stated purposes.

# Software Architecture
## What does it provide?
1. The structure / organization of a software system. 
2. It impacts the system's qualities; modifiability, performance, security, etc. Often, it is orthogonal to the system's functionality
3. Software architecture is result of numerous design decisions;
<li>Make design decisions explicit - why is more important than the what.</li>
<li>Explain requirements and rationale behind design decisions</li>

## Goals & Benefits
```mermaid
  flowchart TB
    A[Good Software Architecture] --> B[Creates a meaningful division of components using <br/> well-known design principles, patterns & best practices <br/>- Abstraction from complex details<br/>- Isolate cross-cutting concerns]
  A[Good Software Architecture] --> C[Specifies necessary implementation measures]
A[Good Software Architecture] --> D[Defines design guidelines to ensure conceptual integrity]
A[Good Software Architecture] --> E[Documents and provides rationale for design decisions]
```

```mermaid
  flowchart TB
    A[Benefits of Good Software Architecture] --> B[Shows that functional and quality requirements will or can be fulfilled]
  A[Benefits of Good Software Architecture] --> C[Helps stakeholders to understand the system]
A[Benefits of Good Software Architecture] --> D[Helps reuse components]
A[Benefits of Good Software Architecture] --> E[Ensures system longetivity<br/>- Facilitates system maintenance]
```
## Software Complexity
Amount of human efforts required to understand something in order to change or extend it. <b><font color="red">Complexity kills software systems!</font></b>

> <i>"The goal of a software architecture is to minimize the human resources required to build and maintain the required system."</i><br/>Robert  C. Martin

## Project Goals vs. Software Architecture Goals
(Short term vs. Long term Goals)

1. Common Goals- Functional requirements, Quality Product
2. Project Goals (Short-term Goals)- Delivery on Time, and within budget
3. Software Architecture Goals (Long-term Goals)- Maintainability, Understandibility, Extensibility, Reduction of complexity, Long term investments (infra, technologies, knowledge)

Software architect has to <b>make right trade-offs</b> to meet long-term strategic goals and short-term operational goals of the current project.

## Essential Key Concepts
### Building Blocks (components, packages)
1. Unit of hierrachical (de)composition and encapsulation
2. Provides static structure
3. Different sizes depending on context. SMALL - function, class, data structure, module; MEDIUM - package, library, framework, program, script, container, pod); LARGE - Application Cluster / Container Cluster
### Relationship between Building Blocks
1. Components interact with each other -> Dynamic system behaviour. To interact with each other, components need interfaces.
2. Interface is a well-defined access point to a component (or system)
3. Software architecture defines interfaces in-terms of;<br/>- Systax, data structures, functional behaviour <br/>- Error behaviour, Quality characteristics, technologies, protocols, constraints, semantics, etc
### Relationship between Building Blocks and their environment
### Principles, Rules and Guidelines
1. Guide design of the building blocks and their relationships
2. Development process
3. System lifecycle
4. Cross-cutting concerns, etc

#### Interfaces
1. Interface imply connections, relationships and dependencies between components
2. Interface Examples; <br/> - Java - Java interfaces <br/>- Web apps/ services - REST, gRPC, graphQL <br/> Unix - File Interface

##### Types of Interfaces
###### Provided Interface (API)
Provider implements functionality and provides interface. Provider is the owner of the interface. Consumers depend on the interface.
```mermaid
  sequenceDiagram
    Consumer ->> Provider: Please do stuff for me
    Provider -->> Consumer: Sure, I will do it THIS way
```
###### Required Interface (SPI)
Service Provider Interface. Consumer provides interface. Functionality Provider implements the interface. Dependency is reversed compared to API. Provider has to implement as per the consumer interface. Used in 
1. IDE plugins; IDE defines interface, plugin providers implement the interface
2. Device Driver Interface; OS provides interfaces & Device drivers are implemented by device manufacturers as per the interfaces
```mermaid
  sequenceDiagram
    Consumer ->> Provider: Please do stuff for me and do it THIS way
    Provider -->> Consumer: OK
```
###### Standard Interface
3rd party defines the interface. Consumer and provider follows the rules defined by the standard interface. Example; OAuthx.0, EMVCo standards
