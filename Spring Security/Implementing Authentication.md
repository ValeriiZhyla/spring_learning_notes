There are two ways to implement authentication.

At first, we can do it directly with some Database. In this case we can use only a plain JDBC: [[Configuring the Users with DataSource]]

Or we can add one more abstraction layer, for example, for the JPA usage: [[Configuring the Users with UserDetailsService]]