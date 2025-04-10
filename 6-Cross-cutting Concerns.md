## Introduction
Cross-cutting concerns are aspects of the system that affect multiple components of the system.

They impact the entire system and often lead to additional technical constraints. They are often a result of fulfilling quality requirements.

They cannot be easily separated into independent components and may violate DRY/SoC. They lead to code scattered across different components.

## Common Cross-Cutting Concerns
### Persistence
Problem statements;
1. How do we persist data from volatile memory to permanent storage
2. decouple business domain and (database) infra

Examples;
1. ORM Frameworks (Hibernate in Java, SQLAlchemy in Python)
   - abstracts the database interactions into highlevel operations on objects
   - provides a single & consistent persistence solution for entire application or multiple applications
   - decouples storage technology from business logic classes
  
### Error Handling
Requirements, more important for distributed sysytems;
1. Predictable and adequate responses
   - depending on category and severity
   - differentiate between logical and technical errors
2. Minimize effects of errors - reduce blast radius
3. Uniform and consistent error handling across possibly different technologies

Examples;
1. Mapping Java Exception to standard HTTP Error codes

### Security
Requirements;
1. Authentication - determine the sender's identity
2. Authorization - grant rights based on identity
3. Integrity - detect manipulation of data
4. Confidentiality - restrict unauthorized data access
5. Non-repudiation - authorship and validity of data
6. Availability - precautions against accidental or delibrate attempts to system failure

Examples;
1. Security Frameworks
   - Spring Security (Java), Django (Python)
2. Algorithms / libs
   - OpenSSL

### I18N
Requirements;
1. Formatting
2. labels
3. Date, Time, Time Zone
4. Currency
5. Documentation
6. Fonts
7. Cultural Differences
8. Error texts
9. App Logic
10. Page Layout
11. Shortcuts
12. Technical Units

Examples;
1. Resource Bundles

### Comms & Messaging
![Comms!](/comms.png)

Examples;
1. Message Queues and Message Brokers;
   - RabbitMQ, Kafka
2. Remote Procdure Calls standards;
   - gRPC, Apache Thrift, SOAP
3. API Styles;
   - REST, GraphQL
4. Networking Protocols
   - HTTP
   - RTP
   - UDP Multicast
   - WebSockets

### User Interface and Ergonomics
Requirements;
1. Adaptive and /or adaptable (e.g.; device, user, situation,...)
2. Optimize usability and user experience

Examples;
1. Responsive UIs
2. Adaptive Design - different version / layout for every platform
3. Consistent stylesheets
4. Reusable UI elements
5. Industry standard accessibility guidelines
   - WCAP - Web Content Accessibility Guidelines
