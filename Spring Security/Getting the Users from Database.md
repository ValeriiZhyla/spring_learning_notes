In practice the users are stored in some database and accessed via JDBC.


We have to add the data source, and Spring will inject it. If we add the [[H2 Database]] to dependencies, spring will start automatically.

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
}
```

## Getting the Users from Database
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
}
```

Required schema is described here: [[Default User Schema]].

I will use the simple [[Reference Controller]] for testing.

Video: https://www.youtube.com/watch?v=LKvrFltAgCQ&list=PLqq-6Pq4lTTYTEooakHchTGglSvkZAjnE&index=7


