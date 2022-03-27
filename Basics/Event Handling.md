We need three things, to implement event system:
- Event class (extend _ApplicationEvent_)
- Event Listener class (implement _ApplicationListener_ as Component)
- Event Publisher instance (autowire ApplicationEventPublisher and use it)

At first, we need an event class, that extends _ApplicationEvent_ class. I'll create a simple event, that stores some message. Instances of this class will represent the events.

```java
public class ExampleEvent extends ApplicationEvent {
    private final String message;

    public ExampleEvent(Object source, String message) {
        super(source);
        this.message = message;
    }

    public String getMessage() {
        return message;
    }
}
```

Then we have to create the listener class, that implements _ApplicationListener_ interface for our target event type. It is required to react on the events, that will be published somewhere in code.
**Important: do not forget to register it as Spring object with @Component**

```java
@Component
public class ExampleEventListener implements ApplicationListener<ExampleEvent> {
    @Override
    public void onApplicationEvent(ExampleEvent event) {
        System.out.println("Event received: " + event.getMessage());
    }
}
```

Then we have to add ApplicationEventPublisher to our class, that can "fire" the event:

```java
	@Autowired  
	private ApplicationEventPublisher applicationEventPublisher;
```

And use it on the some place in code:
```java
	public void run(String... args) {
		String now = new SimpleDateFormat("yyyyMMdd_HHmmss")
			.format(Calendar.getInstance().getTime());
			
		ExampleEvent testEvent = new ExampleEvent(this,
			"Custom event created on " + now);
			
		applicationEventPublisher.publishEvent(testEvent);
	}
```

Documentation: https://www.baeldung.com/spring-events