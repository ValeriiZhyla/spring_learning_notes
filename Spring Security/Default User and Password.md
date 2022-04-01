Dafault username: user
Default password: generated during startup

```log
2022-04-01 18:44:49.059  WARN 18744 --- [           main] .s.s.UserDetailsServiceAutoConfiguration : 

Using generated security password: ac09a4e5-cd44-4bbb-aa88-a9ded882873e

This generated password is for development use only. Your security configuration must be updated before running your application in production.

```

Spring generates the new password on each startup. 
Default username and password can be set in application.properties file:

```properties
spring.security.user.name=hello
spring.security.user.password=world
```

Video: https://www.youtube.com/watch?v=PhG5p_yv0zs&list=PLqq-6Pq4lTTYTEooakHchTGglSvkZAjnE&index=3