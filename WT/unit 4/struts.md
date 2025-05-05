# **Struts Framework: Overview, Components, and Interceptors**

## **1. Introduction to Struts**
**Apache Struts** is an open-source **MVC (Model-View-Controller) framework** for building Java web applications. It extends the **Java Servlet API** and provides a structured way to develop enterprise-level applications.

### **Key Features of Struts**
✔ **MVC Architecture** – Separates business logic, UI, and control flow.  
✔ **Convention over Configuration** – Reduces boilerplate code.  
✔ **Interceptors** – Reusable components for pre/post-processing requests.  
✔ **Tag Library** – Simplifies JSP development.  
✔ **Integration Support** – Works with Spring, Hibernate, etc.  

---

## **2. Core Components of Struts**
### **1. Model**
- Represents **business logic & data** (POJOs, JavaBeans, DAO, Services).
- Example:
  ```java
  public class User {
      private String name;
      // Getters & Setters
  }
  ```

### **2. View**
- **JSP, HTML, FreeMarker, or Velocity** templates.
- Uses **Struts Tags** to display dynamic data.
- Example (JSP with Struts tags):
  ```jsp
  <%@ taglib prefix="s" uri="/struts-tags" %>
  <s:property value="user.name" />
  ```

### **3. Controller**
- Managed by **Struts 2 Filters** (`StrutsPrepareAndExecuteFilter`).
- **Actions** (POJO classes) handle HTTP requests.
- Example:
  ```java
  public class LoginAction {
      private String username;
      // Execute method (called by default)
      public String execute() {
          if(username.equals("admin")) 
              return "success";
          else 
              return "error";
      }
      // Getters & Setters
  }
  ```

### **4. Configuration (`struts.xml`)**
- Defines **actions, results, interceptors**.
- Example:
  ```xml
  <struts>
      <package name="default" extends="struts-default">
          <action name="login" class="com.example.LoginAction">
              <result name="success">/welcome.jsp</result>
              <result name="error">/error.jsp</result>
          </action>
      </package>
  </struts>
  ```

---

## **3. Struts Interceptors**
Interceptors are **reusable components** that process requests **before & after** an Action executes.

### **Key Concepts**
- **Pre-processing** (Before Action executes)  
  - Example: Logging, Security checks.
- **Post-processing** (After Action executes)  
  - Example: Data validation, Transaction management.

### **Default Struts Interceptors**
| Interceptor         | Purpose |
|---------------------|---------|
| `params`            | Maps request parameters to Action properties. |
| `validation`        | Validates input data. |
| `fileUpload`        | Handles file uploads. |
| `exception`         | Manages exceptions globally. |
| `logger`            | Logs request details. |

### **Custom Interceptor Example**
1. **Create Interceptor**:
   ```java
   public class AuthInterceptor extends AbstractInterceptor {
       @Override
       public String intercept(ActionInvocation invocation) throws Exception {
           System.out.println("Before Action");
           String result = invocation.invoke(); // Execute Action
           System.out.println("After Action");
           return result;
       }
   }
   ```
2. **Configure in `struts.xml`**:
   ```xml
   <interceptors>
       <interceptor name="auth" class="com.example.AuthInterceptor"/>
   </interceptors>
   <action name="secureAction" class="com.example.SecureAction">
       <interceptor-ref name="auth"/>
       <interceptor-ref name="defaultStack"/>
   </action>
   ```

---

## **4. Struts Workflow**
1. **Client Request** → Received by `StrutsPrepareAndExecuteFilter`.  
2. **Interceptors** → Pre-process (e.g., validation).  
3. **Action Execution** → Calls business logic.  
4. **Result Rendering** → JSP/HTML response.  
5. **Interceptors** → Post-process (e.g., logging).  

---

## **5. Struts vs. Spring MVC**
| Feature          | Struts 2                          | Spring MVC                        |
|-----------------|----------------------------------|----------------------------------|
| **Architecture** | MVC with Interceptors            | MVC with HandlerMapping          |
| **Dependency Injection** | Limited (Plugins needed) | Built-in (Core feature) |
| **Flexibility** | Moderate                         | High (Modular)                  |
| **Learning Curve** | Moderate                        | Steeper                        |

---

## **6. Summary**
- **Struts Components**: Model (POJOs), View (JSP), Controller (Actions), `struts.xml`.  
- **Interceptors**: Reusable logic for pre/post-processing.  
- **Best For**: Medium-to-large Java web apps needing structured MVC.  

---
---
# **Struts Framework Architecture with Diagram**

Apache Struts is a **Model-View-Controller (MVC)** framework for building Java web applications. Below is a detailed explanation of its architecture, along with a workflow diagram.

---

## **1. Struts 2 Architecture Overview**
Struts 2 follows a **pull-MVC** architecture (where the view pulls data from the Action rather than the controller pushing it). The key components are:

| Component | Role |
|-----------|------|
| **Actions** | Handle business logic (like Controllers in MVC). |
| **Interceptors** | Pre- and post-process requests (e.g., validation, logging). |
| **Value Stack & OGNL** | Manages data flow between components. |
| **Results / Result Types** | Defines the response (e.g., JSP, JSON). |
| **View Technologies** | JSP, FreeMarker, etc.  |

---

## **2. Struts 2 Workflow Diagram**
Here’s a step-by-step breakdown of how Struts processes a request:

1. **User Request**  
   - A client sends an HTTP request (e.g., `/login.action`).  

2. **FilterDispatcher (Front Controller)**  
   - The request is intercepted by `StrutsPrepareAndExecuteFilter`.  
   - It checks `web.xml` and forwards the request to the appropriate **ActionMapper**.  

3. **Action Mapping**  
   - The **ActionProxy** consults `struts.xml` to find the correct **Action class**.  

4. **Interceptors Execution**  
   - Before the Action runs, **interceptors** (e.g., validation, file upload) are executed.  

5. **Action Execution**  
   - The **Action class** processes the request (e.g., validates user input).  

6. **Result Generation**  
   - The Action returns a **result code** (e.g., `"success"`, `"error"`).  
   - The **Result Type** (e.g., JSP, JSON) renders the response.  

7. **Interceptors (Post-Processing)**  
   - Interceptors run again in reverse order (e.g., cleanup, logging).  

8. **Response Sent to Client**  
   - The final HTML/JSON response is returned to the user.  

### **Diagram of Struts 2 Flow**
```
User Request  
    ↓  
[FilterDispatcher]  
    ↓  
[ActionMapper → ActionProxy]  
    ↓  
[Interceptors]  
    ↓  
[Action Class]  
    ↓  
[Result (JSP/JSON)]  
    ↓  
[Interceptors (Post-Processing)]  
    ↓  
Response to Client  
```

---

## **3. Key Components Explained**
### **1. Actions**
- Plain Java classes (POJOs) that handle business logic.  
- Example:
  ```java
  public class LoginAction {
      public String execute() {
          return "success"; // Determines the next view
      }
  }
  ```

### **2. Interceptors**
- Reusable modules for cross-cutting concerns (e.g., logging, security).  
- Example Interceptors:  
  - `params` (maps request parameters to Action properties).  
  - `validation` (input validation).  
  - `fileUpload` (handles file uploads).  

### **3. Value Stack & OGNL**
- **Value Stack**: Stores data accessible across the request lifecycle.  
- **OGNL (Object-Graph Navigation Language)**: Used to manipulate data in the stack.  

### **4. Results**
- Defines the response type (e.g., `JSP`, `redirect`, `JSON`).  
- Configured in `struts.xml`:
  ```xml
  <result name="success">/welcome.jsp</result>
  ```

### **5. View Technologies**
- **JSP** (with Struts tags).  
- **FreeMarker/Velocity** (for templating).  

---

## **4. Struts vs. Traditional MVC**
| Feature | Struts 2 | Traditional MVC |
|---------|---------|----------------|
| **Controller** | `FilterDispatcher` + Actions | Servlet |
| **Model** | POJOs + Value Stack | JavaBeans |
| **View** | JSP + Struts Tags | JSP/HTML |
| **Request Flow** | Interceptor-based | Direct Servlet-to-JSP |

---

## **5. Summary**
- Struts 2 uses **Actions** (instead of Servlets) for business logic.  
- **Interceptors** provide AOP-like functionality (e.g., logging, security).  
- The **Value Stack** allows seamless data sharing between layers.  
- Results determine the response (JSP, JSON, etc.).  

---


