## Overview
### Importance of Interfaces
One of the most important aspects of an architecture are interfaces and the relationships between components.

Interfaces are the backbones of the overall system
- define the structure and behaviour of the system
- provide a link between specialized components
- cooridate and orchestrate a complex network of subsystems
- connection to the outside world

## Basic Properties of Interfaces
### Interface Style
#### Resource Oriented
1. Focuses on defining and manipulating resources of the system (images / books / users / products / etc)
2. Number of resources are arbitary
3. Number of operations are limited
4. Example; REST (REpresentational State Transfer)
   - Business objects are referred ast web resources and represented via URIs using http
   - a resource can have various representations / format (content types). JSON / XML
   - standardized interface definitions using HTTP methods (verbs)
#### Service Oriented
1. Focuses on defining and accessing services that encapsulates business logic
2. Can define wide range of operations - not restricted by http methods as in case of REST
3. Allows for more complex interactions
4. Method calls are encapsulated in messages
   - SOAP - XML via http
   - gPRC - Protocol Buffers via http 2.0
5. Interface definitions are less generic and tailored to perform a distinct business operation

### Call Behaviour
#### Synchronous
1. Caller waits for the response from Callee
2. Easy to understand - Linear flow
3. Ideal for operations where
   - result is immediately required to proceed
   - simple CRUD ops

#### Asynchronous
1. Ideal when the caller
   - can continue excuting other tasks without waiting for a response
   - the result cannot be available immediately
  
### Interface Data Format
![Content Type!](/contenttype.png)

### Internal vs External Interface
External interfaces (consumed by customers or external systems) may have unknown consumers - opportunities for misuse. Needs strict security and stability requirements.

## Best Practices
### Requirements of a good interface
1. Fulfill user requirements
   - suitable functionality (fit client needs) - difficult for public APIs
2. Easy to learn and use
   - provide IDL (e.g.; using Swagger)
   - unit tests as documentation
3. Easy to extend
   - consider API versioning from beginning
4. Hard to misuse (intentionally or unintentionally)
5. Consistent with other interfaces in the system - conceptual integrity
6. Consider Quality requirements - security, performance, robustness, etc...

### Best Practices
1. Use it yourself, implement tests, and use the tests as a reference example
   - you get a feel of how the interface is going to be used from the perspective of consumers or extended service providers
   - test for correctness
2. Clarify requirements with the consumer and provider
3. Hide implementation details from consumers - Information Hiding principle
4. Use meaningful and self-descriptive names that are consistent with domain model
   ![Interfaces!](/names_to_avoid.png)
   ![Naming Fields!](/field_names.png)
5. Minimise surprises and side effects (principle of least surprise)
6. Provide atomic information units
   - easy to evaluate, no parsing of strings
7. Documentation (especially for boundary conditions, threadhold examples and errors)
