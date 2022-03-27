When you start a Spring application, the framework firstly creates a special object called ApplicationContext. The ApplicationContext, also known as the Inversion of Control (IoC)  container, is the heart of the framework.

The ApplicationContext is a container in which your bean objects exist. 

The context is responsible for detecting and reading your Spring bean definitions. Once the ApplicationContext loads bean definitions, it can start creating bean objects for your application based on provided bean properties and their dependencies.

Text from http://dolszewski.com/spring/spring-bean/

ApplicationContext can be seen as main BeanFactory of the application.

Documentation: https://www.baeldung.com/spring-application-context

To use ApplicationContext as bean factory, we have to autowire it. To do it in main class, we can use the interface [[CommandLineRunner]] from SpringBoot.

```java
@SpringBootApplication
public class LearningApplication implements CommandLineRunner {
	@Autowired
	private ApplicationContext applicationContext;

	public static void main(String[] args) {
		SpringApplication.run(LearningApplication.class, args);
	}
	
	@Override
	public void run(String... args) {
		FooService service = applicationContext.getBean(FooService.class);
		System.out.println(service.getFooFormatter().format());
	}
}
```
