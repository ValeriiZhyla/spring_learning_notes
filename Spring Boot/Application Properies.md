Most convenient way to specify some properties for application (like URL of database server) is a file application.properties, located in ressources folder. 

```properties
server.port=8081

spring.data.mongodb.uri=mongodb://localhost/test
```

We can also use enivonment arguments here:
```properties
spring.datasource.username=${OPENSHIFT_MYSQL_DB_USERNAME}
spring.datasource.password=${OPENSHIFT_MYSQL_DB_PASSWORD}
```

And command line arguments:

```properties
server.port=${port}
```

Guide: https://docs.spring.io/spring-boot/docs/1.2.0.M1/reference/html/howto-properties-and-configuration.html

Commonly used properies: https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html