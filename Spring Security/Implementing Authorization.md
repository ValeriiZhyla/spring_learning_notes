Let's create a simple controller with three endpoints:

```java
@RestController
public class HomeResource {

    @GetMapping("/")
    public String home() {
        return "Welcome";
    }

    @GetMapping("/user")
    public String homeUser() {
        return "Welcome User";
    }

    @GetMapping("/admin")
    public String homeAdmin() {
        return "Welcome Admin";
    }
}
```

Then we have to create the configuration, that extends the WebSecurityConfigurerAdapter class and is registered as Spring Security Configuration Bean with _@EnableWebSecurity_ annotation.

To configure the authorization rules for different roles, we ahve to override configure(HttpSecurity http) method.

This configuration will allow the usage of all endpoints only for the user with ADMIN role.

```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests().
            .antMatchers("/**").hasRole("ADMIN")
            .and().formLogin();
    }
}

```

You can chain the rules, and go from most restricted rules to least restricted endpoints.

```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/admin").hasRole("ADMIN")
            .antMatchers("/user").hasAnyRole("USER", "ADMIN")
            .antMatchers("/", "static/css", "static/js").permitAll()
            .and().formLogin();
    }
```


Video: https://www.youtube.com/watch?v=payxWrmF_0k&list=PLqq-6Pq4lTTYTEooakHchTGglSvkZAjnE&index=5