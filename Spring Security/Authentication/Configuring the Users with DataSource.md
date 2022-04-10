In practice the users are stored in some database. If we want to work with this database with JDBC, we have to use an instance of _DataSource_.

We have to add the _DataSource_, and Spring will inject it. If we add the [[H2 Database]] to dependencies, Spring will start automatically.


## Hardcoding the Users and Schema

The default schema will be created, and then some hardcoded users inserted.

```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    private final DataSource dataSource;

    @Autowired
    public SecurityConfiguration(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.jdbcAuthentication()
            .dataSource(dataSource)
            .withDefaultSchema()
            .withUser(
                User.withUsername("user")
                    .password("password")
                    .roles("USER")
            )
            .withUser(
                User.withUsername("admin")
                    .password("admin")
                    .roles("ADMIN")
        );
    }
    
    @Bean
    public PasswordEncoder getPasswordEncoder() {
        return NoOpPasswordEncoder.getInstance();
    }
}
```

## Getting the Users from Database
### Default Schema
If the database with users and authorities is configured and filled, we can just tell spring to use it.

```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    private final DataSource dataSource;

    @Autowired
    public SecurityConfiguration(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.jdbcAuthentication()
            .dataSource(dataSource);
    }

    @Bean
    public PasswordEncoder getPasswordEncoder() {
        return NoOpPasswordEncoder.getInstance();
    }
}
```

Required schema is described here: [[Default User Schema]].

### Custom Schema
If we don't want to use default schema, we have to pass the SQL Queries in corresponding authentication methods: _usersByUsernameQuery(String query)_ and _authoritiesByUsernameQuery(String query)_.

```java
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    private final DataSource dataSource;

    @Autowired
    public SecurityConfiguration(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.jdbcAuthentication()
            .dataSource(dataSource)
            .usersByUsernameQuery(
                "SELECT username, password, enabled " + 
                    "FROM users " + 
                    "WHERE username = ?"
            )
            .authoritiesByUsernameQuery(
                "SELECT username, authority " +
                    "FROM authorities " +
                    "WHERE username = ?"
            );
    }

    @Bean
    public PasswordEncoder getPasswordEncoder() {
        return NoOpPasswordEncoder.getInstance();
    }
}
```


## Links

Video: https://www.youtube.com/watch?v=LKvrFltAgCQ&list=PLqq-6Pq4lTTYTEooakHchTGglSvkZAjnE&index=7


