Spring Boot starts a servlet container and host the application in this container.
Important: @SpringBootApplication annotaion in main class. More here: [[SpringBootApplication]]

There are four main  startup internal stages:
- Set up default configuration
- Start Spring ApplicationContext
- Scan class path (find and process Annotations: Controllers, Components, Beans etc)
- Start Tomcat server (There are also alternative servers)

Videos:
- https://www.youtube.com/watch?v=E7_a-kB46LU&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=9
- https://www.youtube.com/watch?v=E7_a-kB46LU&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x&index=10