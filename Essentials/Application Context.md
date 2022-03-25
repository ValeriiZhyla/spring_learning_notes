When you start a Spring application, the framework firstly creates a special object called ApplicationContext. The ApplicationContext, also known as the Inversion of Control (IoC)  container, is the heart of the framework.

The ApplicationContext is a container in which your bean objects exist. 

The context is responsible for detecting and reading your Spring bean definitions. Once the ApplicationContext loads bean definitions, it can start creating bean objects for your application based on provided bean properties and their dependencies.

Text from http://dolszewski.com/spring/spring-bean/