# **PHP Fundamentals: Arrays, Functions, Control Statements, MySQL Connection & Sessions**

## **1. PHP Arrays**
Arrays store multiple values in a single variable.

### **Types of Arrays**
1. **Indexed Arrays** (Auto-numbered keys)
   ```php
   $colors = ["Red", "Green", "Blue"];
   echo $colors[1]; // Output: Green
   ```

2. **Associative Arrays** (Custom key-value pairs)
   ```php
   $user = ["name" => "John", "age" => 25];
   echo $user["name"]; // Output: John
   ```

3. **Multidimensional Arrays** (Arrays within arrays)
   ```php
   $users = [
       ["name" => "Alice", "age" => 30],
       ["name" => "Bob", "age" => 22]
   ];
   echo $users[1]["name"]; // Output: Bob
   ```

---

## **2. PHP Functions**
Functions are reusable blocks of code.

### **Basic Function**
```php
function greet($name) {
    return "Hello, $name!";
}
echo greet("Alice"); // Output: Hello, Alice!
```

### **Function with Default Argument**
```php
function sayHi($name = "Guest") {
    return "Hi, $name!";
}
echo sayHi(); // Output: Hi, Guest!
```

---

## **3. PHP Control Statements**
### **If-Else**
```php
$age = 20;
if ($age >= 18) {
    echo "Adult";
} else {
    echo "Minor";
}
```

### **Switch-Case**
```php
$day = "Mon";
switch ($day) {
    case "Mon": echo "Monday"; break;
    case "Tue": echo "Tuesday"; break;
    default: echo "Invalid day";
}
```

### **Loops**
1. **For Loop**
   ```php
   for ($i = 1; $i <= 5; $i++) {
       echo $i . " ";
   }
   // Output: 1 2 3 4 5
   ```

2. **Foreach (for Arrays)**
   ```php
   $colors = ["Red", "Green", "Blue"];
   foreach ($colors as $color) {
       echo $color . " ";
   }
   // Output: Red Green Blue
   ```

---

## **4. Connecting PHP to MySQL**
### **PHP Code to Fetch Records from MySQL**
```php
<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "test_db";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Fetch records
$sql = "SELECT id, name, email FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"] . " - Name: " . $row["name"] . " - Email: " . $row["email"] . "<br>";
    }
} else {
    echo "0 results";
}

$conn->close();
?>
```

---

## **5. PHP Session Management**
Sessions store user data across multiple pages.

### **Starting a Session**
```php
session_start();
$_SESSION["username"] = "Alice";
```

### **Accessing Session Data**
```php
session_start();
echo "Welcome, " . $_SESSION["username"]; // Output: Welcome, Alice
```

### **Destroying a Session (Logout)**
```php
session_start();
session_unset(); // Remove all session variables
session_destroy(); // Destroy the session
header("Location: login.php"); // Redirect
```

---

## **Summary**
✔ **Arrays** → Store multiple values (indexed, associative, multidimensional).  
✔ **Functions** → Reusable code blocks (`function greet()`).  
✔ **Control Statements** → `if-else`, `switch`, `for`, `foreach`.  
✔ **MySQL Connection** → `mysqli` to fetch/display records.  
✔ **Sessions** → `session_start()`, `$_SESSION`, `session_destroy()`.  

---
