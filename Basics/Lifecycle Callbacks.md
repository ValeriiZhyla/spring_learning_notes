There are two important stages in the Bean Lifecycle: directly after initialization and directly before destruction. We can handle these moments with two interfaces: InitializingBean, DisposableBean.

These interfaces require the implementation of corresponding methods: 
```java
@Component
public class LifecycleExample implements InitializingBean, DisposableBean {

    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("Im alive!");
    }

    @Override
    public void destroy() throws Exception {
        System.out.println("Chao");
    }
}
```
These methods will be automatically called when object is initialized/disposed.