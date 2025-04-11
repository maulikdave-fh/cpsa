## Call Dependencies
![Call Dependency!](/calld1.png)

The call can be;
1. Method call inside a process
2. Network  call between 2 apps, running on;
   - the same computer
   - separate computers
  
## Tactics
### Using Abstractions (Interfaces)
![Call Dependency!](/calld2.png)
Below OrderService is decoupled from specific implementations. It may not be even aware what PaymentProcessor it is using. An actual decision on what processor will be called can be deferred to DI framework or other configuration which can be resolved at the runtime.
![Call Dependency!](/calld3.png)

Consider a situation where different components that we have to call don't have the same interface;
![Call Dependency!](/calld4.png)
What it means that we cannot use the same abstraction. To solve this, we can use Adapter Pattern.

### Adapter Pattern
In this pattern, we introduce an intermediatory class, called an adaptor.
![Call Dependency!](/calld5.png)

### Avoid Cyclical (Cirular) Relationships
### Asynchronous Messaging
![Call Dependency!](/calld6.png)
#### Why Messaging Reduces Coupling?
1. Sender doesn't expect to receive any data back. 
2. Asynchronous comms
   - Receiver may not be even available when sender puts a message into queue
3. Sender is using the message broker /queue interface, not receiver's. Any changes to receiver are unknown and decoupled from sender
### Restrict Comms
Example; Close layered architecture

