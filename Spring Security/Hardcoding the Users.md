We can extend the class WebSecurityConfigurerAdapter and override the method configure(AuthenticationManagerBuilder auth) to hardcode the user with some password.

This class should be marked for Spring with _@EnableWebSecurity_ annotation.

```java
@EnableWebSecurity  
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {  
  
    @Override  
 protected void configure(AuthenticationManagerBuilder auth) throws Exception {  
        auth.inMemoryAuthentication()  
            .withUser("user").password("password").roles("USER");  
 }
```

If we want to add multiple users, we can chain the call with chaining method and().

```java
@EnableWebSecurity  
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {  
  
    @Override  
 protected void configure(AuthenticationManagerBuilder auth) throws Exception {  
        auth.inMemoryAuthentication()  
            .withUser("user").password("password").roles("USER")  
            .and()  
            .withUser("user2").password("password2").roles("USER");  
 }
```

Spring will use this configuration, to build the instance of AuthenticationManager using the AuthenticationManagerBuilder.

In general, we don't want to store the passwords as plain text. More about [[Password Encryprion]].

Hardcoding the users is good for beginning, but in practice the users are stored in some database and accessed via JDBC: [[Configuring the Users with DataSource]]

Video: https://www.youtube.com/watch?v=iyXne7dIn7U