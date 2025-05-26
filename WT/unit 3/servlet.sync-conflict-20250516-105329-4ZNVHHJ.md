
---

# **Servlet Architecture**

Servlets are **Java programs** that run on a **Java-enabled server** (like Apache Tomcat) to handle **HTTP requests** and **generate dynamic web content** (usually HTML).

The **architecture** of a servlet follows this basic structure:

---

### **1. Servlet Life Cycle**

The servlet life cycle consists of three main methods defined by the `javax.servlet.Servlet` interface:

|Phase|Method|Description|
|---|---|---|
|Initialization|`init(ServletConfig)`|Called once when the servlet is created. Used for initialization (e.g., DB connection).|
|Request Handling|`service(ServletRequest, ServletResponse)`|Called every time a request comes in. Handles client requests and generates responses.|
|Destruction|`destroy()`|Called once when the servlet is taken out of service. Used for cleanup work.|
![[Pasted image 20250504151347.png]]

---

### **2. Servlet API Components**

- **Servlet Interface**: Defines the basic structure (`init`, `service`, `destroy` methods).
    
- **GenericServlet**: A simple implementation of the Servlet interface. Can be extended for non-HTTP protocols.
    
- **HttpServlet**: Extends GenericServlet and provides methods like `doGet()`, `doPost()`, `doPut()`, and `doDelete()` specifically for HTTP.
    

---

### **3. How Servlet Works (Flow)**

1. **Client Request**:
    
    - A client (browser) sends an HTTP request to the server.
        
2. **Web Server**:
    
    - The server receives the request and passes it to the **Servlet Container**.
        
3. **Servlet Container**:
    
    - Loads the servlet class (if not already loaded).
        
    - Instantiates the servlet object.
        
    - Calls the `init()` method once to initialize.
        
    - For each request:
        
        - Calls the `service()` method.
            
        - Based on the request type (GET, POST, etc.), it automatically calls the corresponding method (`doGet()`, `doPost()`, etc.).
            
4. **Response Generation**:
    
    - The servlet processes the request (maybe accessing databases, performing logic) and generates a response (usually HTML).
        
5. **Response to Client**:
    
    - The servlet sends the generated response back to the client through the server.
        
6. **Servlet Destruction**:
    
    - When the servlet is no longer needed (server shutdown or redeployment), the `destroy()` method is called to release resources.
        

---

### **4. Servlet Deployment (web.xml or Annotations)**

- **web.xml** (Deployment Descriptor):  
    Define servlet mappings manually in `WEB-INF/web.xml`.
    
- **Annotations** (`@WebServlet`):  
    Modern approach to declare servlets without `web.xml`.
    

Example:

```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        response.getWriter().println("Hello, World!");
    }
}
```

---

# **Diagram of Servlet Architecture**



```
Client (Browser)
        ↓
Web Server (Apache Tomcat)
        ↓
Servlet Container
        ↓
Servlet (init() → service() → destroy())
        ↓
Response
        ↓
Client (Browser)
```

---

Here’s a clear and complete answer for all your questions:

---

# **1. Compare `doGet()` and `doPost()` Methods in Servlet**

|Feature|`doGet()`|`doPost()`|
|---|---|---|
|Purpose|Handles HTTP GET requests (fetch data)|Handles HTTP POST requests (send data)|
|Data Visibility|Data is appended to URL and visible|Data is sent in request body, hidden|
|Data Size|Limited by URL length (~2 KB)|No size limitation (depends on server config)|
|Usage|Safe operations like viewing pages|Sensitive operations like form submissions|
|Example|Search queries|Login forms, File uploads|

---

# **2. URL Rewriting and Cookies in Servlet**

## **(i) URL Rewriting**

- URL rewriting is a technique to maintain session by appending session ID or data to the URL manually.
    
- Useful when cookies are disabled in the client browser.
    

**Example:**

```java
String encodedURL = response.encodeURL("welcome");
out.println("<a href='" + encodedURL + "'>Visit</a>");
```

The URL might look like:  
`http://localhost:8080/myApp/welcome;jsessionid=123ABC`

---

## **(ii) Cookies**

- Cookies are small pieces of data stored on the client’s machine.
    
- Used to maintain session tracking and user data.
    

**Example to create a cookie:**

```java
Cookie ck = new Cookie("username", "JohnDoe");
response.addCookie(ck);
```

**Example to read cookies:**

```java
Cookie[] cookies = request.getCookies();
for(Cookie c : cookies) {
    if(c.getName().equals("username")) {
        out.println("Username: " + c.getValue());
    }
}
```

---

# **3. What is a Session?**

- A **session** represents a series of interactions between a single client and the server over some period.
    
- HTTP is stateless by default; a **session** helps to maintain the state (such as login info) across multiple requests.
    

**In servlet:**

- You can get session object by:
    

```java
HttpSession session = request.getSession();
session.setAttribute("user", "JohnDoe");
```

- Retrieve data:
    

```java
String username = (String) session.getAttribute("user");
```

---

# **4. Servlet to Accept Two Numbers using POST and Display the Maximum**

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class MaxNumberServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        
        int num1 = Integer.parseInt(request.getParameter("num1"));
        int num2 = Integer.parseInt(request.getParameter("num2"));
        
        int max = (num1 > num2) ? num1 : num2;
        
        out.println("<html><body>");
        out.println("<h2>The Maximum Number is: " + max + "</h2>");
        out.println("</body></html>");
    }
}
```

**Example HTML form to send data to this servlet:**

```html
<form action="MaxNumberServlet" method="post">
    Number 1: <input type="text" name="num1"><br>
    Number 2: <input type="text" name="num2"><br>
    <input type="submit" value="Find Max">
</form>
```

---

Would you also like a **small flowchart** showing the servlet working (POST request flow)? 📘 It could help in your exams!