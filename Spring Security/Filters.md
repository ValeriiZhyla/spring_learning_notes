

A Filter is an object that is invoked at the preprocessing and postprocessing of a request. Filter can be used to log every request, or to check every request and look for some specific header or token. They can also handle the encryption, decryption, and input validation.

Each filter can be applied to some group of URLs, or to all URLs.

We create two filters:
1.  _TransactionFilter_ – to start and commit transactions
2.  _RequestResponseLoggingFilter_ – to log requests and responses

Moreover, to have the filters fire in the right order, we need to use the _@Order_ annotation. These filters are registered by default for all of the URLs in our application.

```java
@Component
@Order(1)
public class TransactionFilter implements Filter {

    @Override
    public void doFilter(
      ServletRequest request, 
      ServletResponse response, 
      FilterChain chain) throws IOException, ServletException {
 
        HttpServletRequest req = (HttpServletRequest) request;
        LOG.info(
          "Starting a transaction for req : {}", 
          req.getRequestURI());
 
        chain.doFilter(request, response);
        LOG.info(
          "Committing a transaction for req : {}", 
          req.getRequestURI());
    }
    // other methods 
}

```

```java
@Component
@Order(2)
public class RequestResponseLoggingFilter implements Filter {

    @Override
    public void doFilter(
      ServletRequest request, 
      ServletResponse response, 
      FilterChain chain) throws IOException, ServletException {
 
        HttpServletRequest req = (HttpServletRequest) request;
        HttpServletResponse res = (HttpServletResponse) response;
        LOG.info(
          "Logging Request  {} : {}", req.getMethod(), 
          req.getRequestURI());
        chain.doFilter(request, response);
        LOG.info(
          "Logging Response :{}", 
          res.getContentType());
    }

    // other methods
}
```




Only after the filters are passed, request will be handled with corresponding [[Servlets and Controllers]].

Link: https://www.baeldung.com/spring-boot-add-filter

![[FiltersServlets.png.png]]