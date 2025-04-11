We cannot completely eliminate coupling / dependencies from our system. Otherwise, our system would not be meaningful but will be just a collection of isolated components.

## Structural Dependencies
One component of the system is directly reliant on the structure or design of another component. Changes in one component leads to changes in dependent component.

### Types
#### Inheritance - Not much we can do to reduce the coupling between components
#### Type Usage
![Type Usage!](/type_usage1.png)
![Type Usage!](/type_usage2.png)

##### Solutions
1. Use polymorphism
![Polymorphism!](/poly1.png)
![Polymorphism!](/poly2.png)

2. Facade Pattern
![Facade!](/facade1.png)
![Facade!](/facade2.png)

3. Delegation through the Decorator Pattern
Base Request Handler
![Decorator!](/decorator1.png)

Now, After we created above class, we may want to introduce additional functionality to http request handling - Say Authentication, Caching of Http responses, Compression of Http responses, etc. But not all the clients of CoreRequestHandler class will need all those functionalities. So we don't want to bake these additional functionalities into the CoreRequestHandler class.

One way to address is to create an inheritance chain of all the functionality that we need. But this inheritance tighly couples all those classes together.
![Decorator!](/decorator2.png)
For example, any changes to AuthenticationRequestHandler impacts it's subclasses.
![Decorator!](/decorator3.png)

Better approach is to use a Decorator pattern;
![Decorator!](/decorator4.png)

AuthenticationDecorator.java
```
    public class AuthenticationDecorator extends RequestHandlerDecorator {
        public AuthenticationHandler(HttpRequestHandler handler) {
          super(handler);
        }

        public HttpResponse handle(HttpRequest request) {
          // Pre-processing for authentication
          if (!authenticate(request)) {
              return new HttpResponse(401, "Authentication Failed");
          }
          //Forward the request to the wrapped handler if authenticated
          return wrappedHandler.handle(request);
        }

        private boolean authenticate(HttpRequest request) {
          ...
        }
    }
```
CachingDecorator.java
```
    public class CachingDecorator extends RequestHandlerDecorator {
        public CachingDecorator(HttpRequestHandler handler) {
          super(handler);
        }

        public HttpResponse handle(HttpRequest request) {
          HttpResponse response = getCachedResponse(request);
          if (response != null)
            return response;
          response = wrappedHandler.handle(request);
          cacheResponse(request, response);
          return response;
        }
        ...
    }
```
CompressionDecorator.java
```
    public class CompressionDecorator extends RequestHandlerDecorator {
        public CompressionDecorator(HttpRequestHandler handler) {
          super(handler);
        }

        public HttpResponse handle(HttpRequest request) {
          HttpResponse response = wrappedHandler.handle(request);
          return compressResponse(response);
        }

        private HttpResponse compressResponse(HttpResponse response) {
            // Compress the response data
            return response;
        }
    }
```
Benefits of the Decorator Pattern
- Different components can create different combinations of decorators that wrap an instance of CoreHttpRequestHandler
  For example, a component where we don't need any additional functionalities, we can use CoreHttpRequestHandler
  ```
      public class ComponentA {
          private HttpRequestHandler handler;
          public ComponentA() {
            handler = new CoreHttpRequestHandler();
          }
          public void handleHttpRequest(HttpRequest request){
            handler.handle(request);
          }
      }
  ```
  A component needing Authentication and Compression;
  ```
        public class ComponentB {
          private HttpRequestHandler handler;
          public ComponentB() {
            handler = new AuthenticationDecorator(new CompressionDecorator(new CoreHttpRequestHandler()));
          }
          public void handleHttpRequest(HttpRequest request){
            handler.handle(request);
          }
      }
  ```
