# **Enterprise JavaBeans (EJB) Architecture and Types**

## **1. EJB Architecture Overview**
Enterprise JavaBeans (EJB) is a server-side component architecture for building scalable, distributed, and transactional business applications in Java EE (now Jakarta EE). The EJB architecture consists of three main components:

### **A. EJB Container**
- Manages the lifecycle of EJBs.
- Provides services such as **transactions, security, concurrency, and persistence**.
- Handles **dependency injection (DI)** and **interceptors**.
- Acts as an intermediary between clients and EJBs.

### **B. EJB Components**
- **Session Beans** (Stateless, Stateful, Singleton)
- **Message-Driven Beans (MDBs)**
- **Entity Beans (Deprecated in EJB 3.x, replaced by JPA Entities)**

### **C. EJB Client**
- Can be a **Java EE application (Servlet, JSF, JAX-RS)**, a **standalone Java client**, or a **remote system** (via RMI-IIOP).
- Accesses EJBs through **dependency injection (`@EJB`)** or **JNDI lookup**.

---

## **2. Types of EJBs**
### **A. Session Beans**
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

## **3. Key EJB Services**
| **Service**       | **Description** |
|------------------|----------------|
| **Transactions** | Automatic transaction management (`@TransactionAttribute`) |
| **Security**     | Role-based access control (`@RolesAllowed`) |
| **Concurrency**  | Singleton beans support `@Lock(READ/WRITE)` |
| **Timers**       | Scheduled tasks (`@Schedule`) |
| **Interceptors** | AOP-style method interceptors (`@AroundInvoke`) |

---

## **4. When to Use Which EJB Type?**
| **Use Case**               | **Recommended EJB** |
|---------------------------|--------------------|
| **Stateless operations**   | Stateless Session Bean |
| **Client-specific state**  | Stateful Session Bean |
| **Shared global state**    | Singleton Session Bean |
| **Asynchronous messaging** | Message-Driven Bean (MDB) |
| **Database persistence**  | JPA Entity (not EJB Entity Bean) |

---

## **5. Conclusion**
- **EJB provides a robust server-side architecture** for enterprise applications.
- **Session Beans** (Stateless, Stateful, Singleton) handle business logic.
- **Message-Driven Beans (MDBs)** process asynchronous messages.
- **Entity Beans are deprecated** (use JPA instead).
- **EJB Container** manages lifecycle, transactions, security, and scalability.

This architecture is widely used in **banking, e-commerce, and large-scale distributed systems** where **transactions, security, and scalability** are critical.