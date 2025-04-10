Following are some ways to reduce system complexity and apply the design principles.

## Generative Creation of Components
1. Reduce code we need to write / maintain
2. Delegate boilerplate code generation to automated tools
   
### Macros 
#### Preprocessor in C/C++
- Allows to apply DRY principle
- High performance runtime - because preprocessor applies macros before compilation
### Template-based Generators
- Java Emitter Templates (JET), JSP / JSF
- XSLT, FreeMaker, Thymeleaf
### Transpilers
- Wt (C++ Web Toolkit)
- JWt (Java Web-toolkit)
- Typescript
### Cross Platform Frameworks (Xamarin, React Native, Flutter, Phone Gap)
- DRY, Conceptual Integrity
### API based generators (gRPC, GraphQL)

## Programming Langauges & Paradigms
1. Functions and Procedures - SRP, SoC, Modularity, DRY
2. Type Systems
3. OOP
4. Memory Ownership Models - Avoids memory leaks, dangling pointers
5. Modules and Packages - Modularity, Loose Coupling, High Cohesion
6. Promises and Futures
7. Access Modifiers - Information Hiding
8. Optionals


## Additional Information
1. C/C++ macros are fragments of code that have been given a name. Whenever the name is used, it is replaced by the contents of the macro - https://gcc.gnu.org/onlinedocs/cpp/Macros.html
2. Java Emitter Templates - https://www.eclipse.org/articles/Article-JET/jet_tutorial1.html
3. Jakarta Server Pages (formerly JavaServer Pages) -https://en.wikipedia.org/wiki/Jakarta_Server_Pages
4. Thymeleaf is a modern server-side Java template engine for both web and standalone environments - https://www.thymeleaf.org/
5. Apache FreeMarker™ is a Java library to generate text output (HTML web pages, e-mails, configuration files, source code, etc.) based on templates and changing data - https://freemarker.apache.org/
6. C++ Web Toolkit is a web GUI library in modern C++ - https://www.webtoolkit.eu/wt
7. Java Web-toolkit is a web GUI library in pure Java - https://www.webtoolkit.eu/jwt
8. TypeScript is JavaScript with syntax for types - https://www.typescriptlang.org/
9. React Native is an open-source UI software framework used to develop applications for Android, Android TV, iOS, macOS, tvOS, Web, Windows, and UWP - https://reactnative.dev/
10. Flutter is an open-source UI software development kit used to develop cross-platform applications from a single codebase for the web, Fuchsia, Android, iOS, Linux, macOS, and Windows using Dart - https://flutter.dev/
11. gRPC is a cross-platform, open-source, high-performance remote procedure call framework - https://grpc.io/
12. GraphQL is a data query and manipulation language for APIs, allowing a client to specify the data it needs. A GraphQL server can fetch data from separate sources for a single client query and present the results in a unified graph - https://graphql.org/
