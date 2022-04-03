We shouldn't save passwords as plain Strings in memory.
Instead, we have to encrypt them with some hash-function.

We can do it by defining a Spring Bean with type PasswordEncoder, and return some specific password encoder from it.

This NoOpPasswordEncoder uses **no hashing**. I'll use it at first, for learning purpose.

```java
@Bean  
public PasswordEncoder getPasswordEncoder() {  
    return NoOpPasswordEncoder.getInstance(); //no encryption  
}
```

Current **best practice** in Spring nowadays is the usage of BCryptPasswordEncoder

```java
@Bean  
public PasswordEncoder getPasswordEncoder() {  
    return new BCryptPasswordEncoder(); //proper encryption
}
```

BCrypt is besser than SHA, because we don't have to store the private key, it will be generated. More about [[Password Hashing Concepts]].