I'll use create a PostgreSQL instance on Heroku and use it for connection.

Guide: https://www.codejava.net/frameworks/spring-boot/connect-to-postgresql-database-examples

We have to specify following parameters in application.properties:

```properties
spring.datasource.url=
spring.datasource.username=
spring.datasource.password=
```

Note, that the dependency spring-boot-starter-data-jpa is required.

My credentials:

```properties
spring.datasource.url=postgres://rtqdhjzpirhsbt:64788246462fd0b789a67bf6e9f6b35031aeeaa89b63ca72f57c4f94f1000853@ec2-52-18-116-67.eu-west-1.compute.amazonaws.com:5432/dbmiq3db65kq18
spring.datasource.username=rtqdhjzpirhsbt
spring.datasource.password=***********************************************
```