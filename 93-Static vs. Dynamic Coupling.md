## Static Coupling
Explicit, fixed or hard-coded dependencies between components
- Typically, determined at compile time without running the application
- Decribes how our components are "wired" to each other

## Dynamic Coupling
- Dependencies are resolved at runtime
- Decribes how components "call each other"

## Examples
### Creation Dependency
#### Static Coupling
Looking at the code, we can tell what payment service is used by the order service without running it or inspecting its execution.
![Coupling!](/coupling1.png)
#### Dynamic Coupling
Here DI framework creates different instance of the payment service at runtime based on an external configuration / the version of the payment lib present in the classpath / env variable that was set on the server where app is running / etc. 
![Coupling!](/coupling2.png)
![Coupling!](/coupling3.png)
Just by looking at the code, we won't know which instance of the payment service will be created & used at runtime. The only way to find out is to inspect the app during its execution. This can be done looking at the logs, using a remote debugger or profiler, etc.

## Static Coupling - Advantages
1. Efficiency and performance
   - type safety checks are done, linking is done - compile time dependency has less overhead
2. Better tooling support
   - IDE - autocompletion, search for usage, refactoring, etc
   - Compile time error detection - fail fast, no surprises at runtime. These errors are much easier and faster to fix
   - Static Analysis tools (SonarQube, Checkstyle, etc)
3. Code is easier to read, maintain and reason about - Very important

## Static Coupling - Disadvantages
1. Rigid structure (less flexbility)
2. Hard to extend
   - Modifying dependencies / extending functionality requires rebuild and redeploy
  
## Dynamic Coupling - Advantages
1. Greater potential for;
   - Flexibility
   - Extensibility
2. No need to rebuild / redeploy our system to modify a dependency
   - move faster with new features / fixes

## Dynamic Coupling - Disadvantages
1. Performance overhead
   - Late binding of dependencies through Reflection
   - Dynamic lookups
   - DNS resolutions of address
   - Parsing config files
   - Network comms
2. Difficult debugging and troubleshooting
   - hard to analyze dependencies and issues
   - No support from IDE, complier, static analysis tool, etc.
3. Higher risk of runtime failures
