![image](https://github.com/user-attachments/assets/63997abd-8e10-4c0a-b410-d8ec67ea6984)![image](https://github.com/user-attachments/assets/02f0e720-83fe-4357-95ba-ad276a67a9e8)## Instantiation Dependencies
![Creation Coupling!](/creation_coupling.png)

## Tactics
Tactics to make instantiation dependencies more loosely coupled.
### Factory Pattern
Current Scenario - insurance company is only offering home insurance policy. The home insurance policy creates multiple client classes to generate a home policy.
![Insurance!](/insurance1.png)

As the company grows, it wants to offer new type of insurance policy - car insurance.
![Insurance!](/insurance2.png)

But this will force us to change all client classes to handle this new policy type.
![Insurance!](/insurance3.png)
![Insurance!](/insurance4.png)

The complexity (tight coupling) will keep on growing as new policy types are introduced.
![Insurance!](/insurance5.png)
![Insurance!](/insurance6.png)

#### Solution
![Insurance!](/insurance7.png)

### Proxy Pattern
The StudentAccountManager class creates and uses multiple client classes. It also keeps a connection to a db open that may consume additional resources, espeically when we know that not all client classes need db right away, and some of them don't end up using db connection. Lot of memory and db connection resources are wasted.
![LMS!](/lms1.png)

#### Performance Optimization - Lazy Initialization
After creating the AccountManager class, we may / may not use it.
![LMS!](/lms2.png)

Deferred Creation
![LMS!](/lms3.png)

![LMS!](/lms4.png)

##### Lazy Initialization - Option 1
Change all the client components and conditionally create the StudentAccountManager object only if it needs it. Bad choice - it needs lot of code duplication and generally a lot of work
![LMS!](/lms5.png)

##### Lazy Initialization - Option 2
Significantly modify the StudentAccountManager clsss - better choice but may not be possible always if the source code of StudentAccountManager belongs to a third-party library
![LMS!](/lms6.png)

##### Lazy Initialization - Option 3 Proxy Pattern
![LMS!](/lms7.png)

Clients create an instance of ProxyAccountManager instead of StudentAccountManager
![LMS!](/lms8.png)

![LMS!](/lms9.png)

![LMS!](/lms10.png)

### Dependency Injection Pattern
Complex dependencies - real world scenario
![DI!](/ecomm1.png)

Poor code readability + tight coupling
![DI!](/ecomm2.png)

#### Solution
Use DI Framework
![DI!](/ecomm3.png)


