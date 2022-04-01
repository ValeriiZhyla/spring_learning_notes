Servlet is a Java object, that implements the Servlet interface and handles the incoming HTTP requests. Methods init(), service() and destroy() have to be implemented.

```java
public class ServletLifeCycleExample extends HttpServlet {
    private Integer sharedCounter;

    @Override
    public void init(final ServletConfig config) throws ServletException {
        super.init(config);
        getServletContext().log("init() called");
        sharedCounter = 0;
    }

    @Override
    protected void service(final HttpServletRequest request, final HttpServletResponse response) throws ServletException, IOException {
        getServletContext().log("service() called");
        int localCounter;
        synchronized (sharedCounter) {
            sharedCounter++;
            localCounter = sharedCounter;
        }
        response.getWriter().write("Incrementing the count to " + localCounter);  // accessing a local variable
    }

    @Override
    public void destroy() {
        getServletContext().log("destroy() called");
    }
}
```

Each request is creates a new thread, that process this request. The mapping between URLs and Servlet classes is configured via web.xml

Servlets can be seen as low-level way to handle HTTP requests. They were used to implement web servers in the past, but nowadays they are implemented internally by different framework wrappers, like Controllers in Spring.

Spring Controllers are not the same as servlets, but Spring uses the custom extension of HttpServlet called DispacherServlet internally. 
