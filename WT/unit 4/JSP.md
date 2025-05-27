## What is JSP?

JSP (Java Server Pages) is a server-side technology that allows developers to create dynamic web content by embedding Java code directly into HTML pages. It's part of the Java EE (Enterprise Edition) platform and provides a simpler way to create web applications compared to pure servlets.

---
Here’s a comparison of **JSP vs. Servlets** in a tabular form:  

| Feature               | JSP (JavaServer Pages) | Servlets |
|-----------------------|------------------------|----------|
| **Type**             | HTML with embedded Java (Java inside HTML) | Java with embedded HTML (HTML inside Java) |
| **Ease of Coding**    | Easier for web designers (HTML-centric) | More complex (requires Java coding for HTML output) |
| **Separation of Concerns** | Better (UI and logic can be separated) | Poor (mixes Java logic with HTML in `out.println()`) |
| **Compilation**       | Automatically compiled into a servlet by the container | Must be manually written and compiled |
| **Syntax**           | Uses JSP tags (`<% ... %>`, `<%= ... %>`), EL, JSTL | Pure Java code with `doGet()`, `doPost()` methods |
| **Implicit Objects**  | Predefined (`request`, `response`, `session`, etc.) | Must be obtained from `HttpServletRequest`/`Response` |
| **Maintainability**   | Easier to update UI (no recompilation needed for HTML changes) | Harder (changes require recompilation) |
| **Use Case**         | Best for **presentation layer** (dynamic content rendering) | Best for **controller logic** (request handling, business logic) |
| **Performance**      | Slightly slower (converted to servlet first) | Slightly faster (directly executes Java code) |
| **Tag Libraries**    | Supports **JSTL**, custom tags for reusable components | No built-in tag support (requires manual Java coding) |

### Summary:
- **JSP** is better for **presentation** (UI-focused development).  
- **Servlets** are better for **business logic** (request handling, processing).  
- Modern Java web apps use **both** (Servlets as controllers, JSPs as views).  

---


# **JSP Syntax in Short**

JSP provides different elements to embed Java code inside HTML:

1. **Directives (`<%@ %>`)** – Used for page configuration (imports, sessions, error handling).
2. **Scriptlets (`<% %>`)** – Embeds Java code inside JSP.
3. **Expressions (`<%= %>`)** – Outputs Java expressions directly in HTML.
4. **Declarations (`<%! %>`)** – Declares variables/methods (like class-level in servlet).
5. **Comments (`<%-- --%>`)** – JSP-specific comments (not visible in HTML source).
6. **EL (Expression Language `${ }`)** – Simplifies data access from models.
7. **JSTL Tags (`<c:if>`, `<c:forEach>`)** – Standard tags for logic/loops.

---

# **JSP Program Example**
### **Demonstrates:**
✔ `page` directive  
✔ Scriptlet (`<% %>`)  
✔ Expression (`<%= %>`)  
✔ JSP Comment (`<%-- --%>`)  

### **Code (demo.jsp)**
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<%@ page import="java.util.Date" %> <!-- Page Directive (import) -->

<html>
<head>
    <title>JSP Syntax Demo</title>
</head>
<body>
    <h1>JSP Syntax Example</h1>
    
    <%-- JSP Comment (Not visible in HTML source) --%>
    
    <!-- Scriptlet (Java Code) -->
    <% 
        String name = "John Doe";
        int age = 30;
    %>
    
    <!-- Expression (Outputs Java variable) -->
    <p>Welcome, <%= name %>!</p>  
    <p>Your age is: <%= age %></p>
    
    <!-- Using page directive import (Date) -->
    <p>Current time: <%= new Date() %></p>
    
    <!-- Scriptlet with loop -->
    <ul>
    <% for(int i=1; i<=3; i++) { %>
        <li>Item <%= i %></li>
    <% } %>
    </ul>
</body>
</html>
```

---

### **Output in Browser:**
```
JSP Syntax Example

Welcome, John Doe!
Your age is: 30
Current time: Thu May 02 15:30:45 IST 2024

• Item 1
• Item 2
• Item 3
```

---

### **Key Takeaways:**
1. **`<%@ page %>`** → Configures JSP (imports, content type).  
2. **`<% %>`** → Executes Java code (e.g., loops, variables).  
3. **`<%= %>`** → Prints variables/expressions (shorthand for `out.print()`).  
4. **`<%-- --%>`** → Comments (not sent to browser).  

This example avoids **declarations (`<%! %>`)** and **JSTL** for simplicity but covers core JSP syntax.  

---
