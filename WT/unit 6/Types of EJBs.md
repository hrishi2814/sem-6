### **A) Session Beans**

Used for **business logic** and **transaction management**. They are further classified into:

#### **(i) Stateless Session Beans (SLSB)**
- **No client-specific state** between method calls.
- **Pooled by the container** for scalability.
- Used for **stateless operations** (e.g., calculations, database updates).
- **Thread-safe** (container manages concurrency).

**Example:**
```java
@Stateless
public class PaymentService {
    public boolean processPayment(double amount) {
        // Business logic
        return true;
    }
}
```

#### **(ii) Stateful Session Beans (SFSB)**
- **Maintains client-specific state** across multiple requests.
- Used for **multi-step workflows** (e.g., shopping cart, user session).
- **Not thread-safe** (each client gets its own instance).
- **Destroyed when client session ends**.

**Example:**
```java
@Stateful
public class ShoppingCart {
    private List<String> items = new ArrayList<>();

    public void addItem(String item) {
        items.add(item);
    }

    public List<String> getItems() {
        return items;
    }
}
```

#### **(iii) Singleton Session Beans**
- **Only one instance per application** (shared across all clients).
- Used for **caching, configuration, or shared resources**.
- **Thread-safe** (requires explicit concurrency control via `@Lock`).

**Example:**
```java
@Singleton
@Startup // Eager initialization
public class AppConfig {
    private String appName;

    @PostConstruct
    public void init() {
        appName = "E-Commerce App";
    }

    public String getAppName() {
        return appName;
    }
}
```

---

### **B. Message-Driven Beans (MDBs)**
- Used for **asynchronous message processing** (JMS, Kafka, etc.).
- **No direct client interaction** (listens to a queue/topic).
- **Stateless** (container manages pooling).
- Supports **transactional messaging**.

**Example:**
```java
@MessageDriven(activationConfig = {
    @ActivationConfigProperty(propertyName = "destinationType", propertyValue = "javax.jms.Queue"),
    @ActivationConfigProperty(propertyName = "destination", propertyValue = "java:/jms/queue/OrderQueue")
})
public class OrderProcessor implements MessageListener {
    @Override
    public void onMessage(Message message) {
        // Process JMS message
        TextMessage txtMsg = (TextMessage) message;
        System.out.println("Received order: " + txtMsg.getText());
    }
}
```

---

### **C. Entity Beans (Deprecated in EJB 3.x)**
- Replaced by **JPA (Java Persistence API) Entities** (`@Entity`).
- Previously used for **database persistence**.
- Now, **JPA + Session Beans** is the recommended approach.

**Example (JPA Entity instead of EJB 2.x Entity Bean):**
```java
@Entity
public class Product {
    @Id
    private Long id;
    private String name;
    private double price;

    // Getters & Setters
}
```

---
