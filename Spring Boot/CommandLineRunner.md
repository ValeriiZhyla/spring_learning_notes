You can implement the CommandLineRunner interface, if you want to use the Spring application as "normal" Java application, that can be started via command line with some arguments .

```java
@SpringBootApplication
public class CmdApplication implements CommandLineRunner {

	public static void main(String[] args) {
		SpringApplication.run(CmdApplication.class, args);
	}
	
	@Override
	public void run(String... args) {
		//your code
	}
}
```