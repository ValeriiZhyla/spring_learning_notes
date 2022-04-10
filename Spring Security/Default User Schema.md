## Initialize Schema

Spring will use the default user schema configuration, if no further configuration was done. The syntax of the schema depends on database dialect.

We can set up the schema for the in-memory databases by adding the file  **schema.sql** in ressources folder.

Here is the abstract structure:

```sql
create table users(
	username varchar_ignorecase(50) not null primary key,
	password varchar_ignorecase(500) not null,
	enabled boolean not null
);

create table authorities (
	username varchar_ignorecase(50) not null,
	authority varchar_ignorecase(50) not null,
	constraint fk_authorities_users foreign key(username) references users(username)
);
create unique index ix_auth_username on authorities (username,authority);
```

Oracle schema:

```sql
CREATE TABLE USERS (
    USERNAME NVARCHAR2(128) PRIMARY KEY,
    PASSWORD NVARCHAR2(128) NOT NULL,
    ENABLED CHAR(1) CHECK (ENABLED IN ('Y','N') ) NOT NULL
);


CREATE TABLE AUTHORITIES (
    USERNAME NVARCHAR2(128) NOT NULL,
    AUTHORITY NVARCHAR2(128) NOT NULL
);
ALTER TABLE AUTHORITIES ADD CONSTRAINT AUTHORITIES_UNIQUE UNIQUE (USERNAME, AUTHORITY);
ALTER TABLE AUTHORITIES ADD CONSTRAINT AUTHORITIES_FK1 FOREIGN KEY (USERNAME) REFERENCES USERS (USERNAME) ENABLE;
```

Default Schema documentation: https://docs.spring.io/spring-security/reference/servlet/authentication/passwords/jdbc.html#servlet-authentication-jdbc-schema

We can use different table and column structure, but then we have to use explicit SQL statements. More here: [[Configuring the Users with DataSource#Custom Schema]].

## Initialize Users
We can initialize the database object by creating the **data.sql** file in ressource directory. The SQL Statements will be executed on startup.
```sql
INSERT INTO users (username, password, enabled) VALUES ('user', 'password', true);  
INSERT INTO users (username, password, enabled) VALUES ('admin', 'admin', true);  
  
INSERT INTO authorities (username, authority) VALUES ('user', 'ROLE_USER');  
INSERT INTO authorities (username, authority) VALUES ('admin', 'ROLE_ADMIN');
```
