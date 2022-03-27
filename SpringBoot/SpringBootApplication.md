This annotation @SpringBootApplication is equivalent to using _@Configuration_, _@EnableAutoConfiguration_, and _@ComponentScan_.

```java
@SpringBootApplication
class VehicleFactoryApplication {
    public static void main(String[] args) {
        SpringApplication.run(VehicleFactoryApplication.class, args);
    }
}
```
As a result, when we run this Spring Boot application, **it will automatically scan the components in the current package and its sub-packages**. Thus it will register them in Spring's Application Context, and allow us to inject beans using _@Autowired_.
See [[Autowiring]].

Links:
- https://www.baeldung.com/spring-boot-annotations#spring-boot-application
- https://www.baeldung.com/spring-autowire