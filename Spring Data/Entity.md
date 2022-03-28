@Entity Annotation shows to Spring, that this class will be used as model object. Each entity requires the primary key, that is defined with @Id annotation.

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Wine {

    @Id
    private String id;
    private String name;
    private String producer;

    public Wine() {
    }

    public Wine(String id, String name, String producer) {
        this.id = id;
        this.name = name;
        this.producer = producer;
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getProducer() {
        return producer;
    }
}
```