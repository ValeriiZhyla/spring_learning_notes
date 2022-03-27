There are two scope types for Beans in original Spring:
-   singleton – a single instance of this bean
-   prototype – multiple instances of this bean


We use @Scope annotation to define scope
```java
@Bean
@Scope("singleton")
public Person personSingleton() {
    return new Person();
}
```

Documentation: https://www.baeldung.com/spring-bean-scopes


There are other types of scopes in latest Spring (only for web):
-   request - instance for a single HTTP request
-   session - instance for an HTTP Session
-   application - instance for the lifecycle of a _ServletContext_
-   websocket - instance for a particular _WebSocket_ session