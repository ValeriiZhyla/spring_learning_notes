
The annotation @Autowire allows Spring to resolve and inject collaborating beans into our bean.

Documentation: https://www.baeldung.com/spring-autowire

Component scan should be enabled to use the autowiring. The annotation _@SpringBootApplication_ includes _@ComponentScan_. More here: [[SpringBootApplication]]

```java
@Component
public class FooFormatter {
    public String format() {
        return "foo";
    }
}
```

```java
@Component
public class FooService {  
    @Autowired
    private FooFormatter fooFormatter;
}
```

If we create the instance of FooService in classic java way, then we will ignore all Spring functionality, and Autowiring will not work. We have to call [[Application Context]] and get the Bean for our component.

**Dont**:
```java
FooService service = new FooService() // DONT DO IT - IT WILL PRODUCE GARBAGE
```

**Do**:
```java
FooService service = applicationContext.getBean(FooService.class); // CORRECT WAY
```

Spring says, that this way (called field injection) is not recommended. The better way is constructor injection.

You can do this for constructor injection:

```java
@Component
public class FooService {
    private final FooFormatter fooFormatter;

    @Autowired
    public FooService(FooFormatter fooFormatter) {
        this.fooFormatter = fooFormatter;
    }
}
```

Advantages: at first, we can use final modifier with constructor injection (we cant do it with  field injection). Field Injection violates the responsibility principle, it is not good for architecture and testing.
