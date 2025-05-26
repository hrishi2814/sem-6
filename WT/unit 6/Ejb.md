# **Enterprise JavaBeans (EJB)**

## **What is EJB?**
**Enterprise JavaBeans (EJB)** is a server-side component architecture used in Java EE (now Jakarta EE) for building scalable, distributed, and transactional business applications. EJBs encapsulate business logic and can be deployed in an application server (like WildFly, IBM WebSphere, or Oracle WebLogic).

---

## **Architecture of EJB**
The EJB architecture consists of three main components:

1. **EJB Container**  
   - Manages EJBs (lifecycle, transactions, security, concurrency).
   - Provides services like persistence, messaging, and remote access.

2. **EJB Components**  
   - **Session Beans** (Stateless, Stateful, Singleton)
   - **Message-Driven Beans (MDBs)**
   - **Entity Beans** (Deprecated, replaced by JPA/Hibernate)

3. **Client Applications**  
   - Can be web apps (Servlets, JSP), standalone Java apps, or other EJBs.

---

## **Types of EJB**
| Type | Description | Use Case |
|------|------------|----------|
| **Stateless Session Bean** | Does not maintain client state between calls. | Business logic (e.g., calculations, database operations). |
| **Stateful Session Bean** | Maintains client state across multiple requests. | Shopping carts, user sessions. |
| **Singleton Session Bean** | One instance per application, shared across clients. | Caching, application-wide configuration. |
| **Message-Driven Bean (MDB)** | Processes JMS (Java Message Service) messages asynchronously. | Event-driven systems (e.g., order processing). |

*(Note: Entity Beans were replaced by **JPA (Java Persistence API)** for database operations.)*

---

## **Example: Stateless EJB**
### **1. Define a Business Interface**
```java
import javax.ejb.Remote;

@Remote
public interface Calculator {
    int add(int a, int b);
}
```

### **2. Implement the EJB**
```java
import javax.ejb.Stateless;

@Stateless
public class CalculatorBean implements Calculator {
    @Override
    public int add(int a, int b) {
        return a + b;
    }
}
```

### **3. Client Code (e.g., Servlet)**
```java
import javax.ejb.EJB;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;

@WebServlet("/calculate")
public class CalculatorClient extends HttpServlet {
    @EJB
    private Calculator calculator;

    protected void doGet(HttpServletRequest req, HttpServletResponse res) {
        int result = calculator.add(5, 10);
        res.getWriter().println("Result: " + result); // Output: 15
    }
}
```

---

## **Key Features of EJB**
✔ **Transaction Management** (`@TransactionAttribute`)  
✔ **Security** (`@RolesAllowed`, `@PermitAll`)  
✔ **Concurrency Control** (`@Lock` for Singleton beans)  
✔ **Remote Access** (using `@Remote` interface)  
✔ **Asynchronous Processing** (`@Asynchronous`)  

---

## **Conclusion**
- **EJB** is used for enterprise-level applications requiring scalability and transactions.  
- **Session Beans** handle business logic, while **MDBs** process messages.  
- **JPA** is preferred over Entity Beans for database operations.  

---
