We have to put the Java objects in containers, that are managed by Spring. Then Spring can perform all the necessary internal handling.
If we use normal Java objects, without putting them into Spring container, Spring will know nothing about these objects. 

Bean concept: https://www.youtube.com/watch?v=xlWwMSu5I70&list=PLC97BDEFDCDD169D7&index=3

Code tutorial for Bean Factories: https://www.youtube.com/watch?v=7c6ZTF6cF88&list=PLC97BDEFDCDD169D7&index=4

There are three ways to create Beans:
- XML old and deprecated way
- @Component - for classes of application
- @Bean - for classes from libs

The usage of XmlBeanFactory (and XML beans) is deprecated, this is an example of "oldest" way to create a bean.

```java
public class LearningApplication {  
	public static void main(String[] args) {  
		SpringApplication.run(LearningApplication.class, args);  
		BeanFactory factory = new XmlBeanFactory(new FileSystemResource("src/main/resources/beans.xml"));  
		Triangle triangle = (Triangle) factory.getBean("triangle");  
		triangle.draw();  
	}  
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
 xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
 <bean id="triangle" class="com.orator.learning.Triangle"/>  
</beans>
```

Descriptions of beans:
- https://stackoverflow.com/questions/17193365/what-in-the-world-are-spring-beans
- http://dolszewski.com/spring/spring-bean/

Today beans are configured via @Component class anotation, or its derivatives @Service,  @Repository, @Controller. Simply add one of these annotations to your class.
```java
@Component  
class BeanWithDependency {  
	private final MyBeanClass beanClass;  
	
	BeanWithDependency(MyBeanClass beanClass) {  
        this.beanClass = beanClass;  
	}  
}
```


We can also use @Bean and @Configuration annotations to wrap classes from libraries. 
```java
@Configuration  
class MyConfigurationClass {  
	@Bean  
	public NotMyClass notMyClass() {  
	    return new NotMyClass();  
	}  
}
```

The scope of a Spring bean defines how many instances of a particular class the framework creates at runtime. The scope also describes on what condition a new object is created. [[Bean Scopes]]
