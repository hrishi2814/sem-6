# **Servlet and MySQL Database Connectivity**

## **Steps for Connectivity:**

1. **Load JDBC Driver**.
    
2. **Establish Connection** with MySQL database.
    
3. **Execute SQL Query** (Retrieve data).
    
4. **Display the Result** in the servlet response.
    

---

## **Example Table (employee)**

|emp_id|emp_name|emp_dept|
|---|---|---|
|101|John|HR|
|102|Alice|IT|

---

## **Example Servlet Code**

```java
import java.io.*;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class EmployeeServlet extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;

        try {
            // 1. Load the MySQL JDBC Driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 2. Establish Connection (replace database, username, password)
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/your_database", "root", "password");

            // 3. Create Statement
            stmt = conn.createStatement();
            String query = "SELECT emp_id, emp_name, emp_dept FROM employee";

            // 4. Execute Query
            rs = stmt.executeQuery(query);

            // 5. Display Results
            out.println("<html><body>");
            out.println("<h2>Employee Details</h2>");
            out.println("<table border='1'><tr><th>ID</th><th>Name</th><th>Department</th></tr>");

            while(rs.next()) {
                int id = rs.getInt("emp_id");
                String name = rs.getString("emp_name");
                String dept = rs.getString("emp_dept");
                out.println("<tr><td>" + id + "</td><td>" + name + "</td><td>" + dept + "</td></tr>");
            }

            out.println("</table>");
            out.println("</body></html>");
        }
        catch(Exception e) {
            out.println("Error: " + e.getMessage());
        }
        finally {
            try { if(rs != null) rs.close(); } catch(Exception e) {}
            try { if(stmt != null) stmt.close(); } catch(Exception e) {}
            try { if(conn != null) conn.close(); } catch(Exception e) {}
        }
    }
}
```

---

## **Important Notes:**

- **JAR File Needed**: Add MySQL Connector JAR (e.g., `mysql-connector-java-8.0.xx.jar`) to your project’s `lib` folder.
    
- **Database**: You must create the database and `employee` table before running.
    

```sql
CREATE DATABASE your_database;
USE your_database;

CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    emp_dept VARCHAR(50)
);

INSERT INTO employee VALUES (101, 'John', 'HR'), (102, 'Alice', 'IT');
```

---

✅ **Summary**:

- Load driver ➔ Connect to DB ➔ Run query ➔ Show results ➔ Close connection.
    

---

### Here’s a **simple flowchart** showing **Servlet-MySQL database interaction**:

---

```
[ User sends HTTP Request (e.g., via browser) ]
                          ↓
[ Servlet receives the request ]
                          ↓
[ Load JDBC Driver ]
                          ↓
[ Establish Connection to MySQL Database ]
                          ↓
[ Execute SQL Query (SELECT emp_id, emp_name, emp_dept FROM employee) ]
                          ↓
[ Get ResultSet (data from DB) ]
                          ↓
[ Format data in HTML (table, list, etc.) ]
                          ↓
[ Send back HTML Response to User ]
                          ↓
[ Display Employee Data on Browser ]
```

---

✅ **Key Points**:

- Servlet works like a **middleman** between the **browser** and **database**.
    
- The **ResultSet** is used to fetch database data inside Java code.
    
- Always **close** `Connection`, `Statement`, and `ResultSet` properly to avoid memory leaks.
    

---
