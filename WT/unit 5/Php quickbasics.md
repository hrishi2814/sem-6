# PHP Quick Rundown

## What is PHP?
PHP (Hypertext Preprocessor) is a server-side scripting language designed for web development. It's:
- Embedded in HTML
- Executed on the server
- Open-source and cross-platform
- Commonly used with databases like MySQL

## Basic PHP Syntax

```php
<?php
// This is a single-line comment

/*
This is a
multi-line comment
*/

// Variables start with $
$variable = "Hello World";
$number = 42;
$float = 3.14;
$bool = true;

// Outputting data
echo "This will be output to the browser";
print "This also outputs to the browser";

// Conditional statements
if ($number > 50) {
    echo "Number is greater than 50";
} elseif ($number < 50) {
    echo "Number is less than 50";
} else {
    echo "Number is 50";
}

// Loops
for ($i = 0; $i < 5; $i++) {
    echo "Iteration: $i";
}

while ($number > 0) {
    echo $number;
    $number--;
}

// Arrays
$array = array("apple", "banana", "cherry");
// or shorthand:
$array = ["apple", "banana", "cherry"];

// Associative arrays (key-value pairs)
$assoc = ["name" => "John", "age" => 30];

// Functions
function greet($name) {
    return "Hello, $name!";
}
echo greet("Alice");
?>
```

## Connecting PHP to MySQL

### Using MySQLi (procedural style):
```php
<?php
$servername = "localhost";
$username = "your_username";
$password = "your_password";
$dbname = "your_database";

// Create connection
$conn = mysqli_connect($servername, $username, $password, $dbname);

// Check connection
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}
echo "Connected successfully";

// Perform query
$sql = "SELECT id, name FROM users";
$result = mysqli_query($conn, $sql);

// Fetch data
if (mysqli_num_rows($result) > 0) {
    while($row = mysqli_fetch_assoc($result)) {
        echo "ID: " . $row["id"]. " - Name: " . $row["name"]. "<br>";
    }
} else {
    echo "0 results";
}

// Close connection
mysqli_close($conn);
?>
```

### Using PDO (more secure and supports multiple databases):
```php
<?php
$servername = "localhost";
$username = "your_username";
$password = "your_password";
$dbname = "your_database";

try {
    $conn = new PDO("mysql:host=$servername;dbname=$dbname", $username, $password);
    // Set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully"; 
    
    // Prepare and execute query
    $stmt = $conn->prepare("SELECT id, name FROM users");
    $stmt->execute();
    
    // Set the resulting array to associative
    $result = $stmt->setFetchMode(PDO::FETCH_ASSOC);
    
    foreach($stmt->fetchAll() as $row) {
        echo "ID: " . $row["id"]. " - Name: " . $row["name"]. "<br>";
    }
} catch(PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}

// Connection is closed automatically when script ends
?>
```

### Important Security Note:
Always use prepared statements to prevent SQL injection when inserting user input into queries. Here's an example with PDO:

```php
$stmt = $conn->prepare("INSERT INTO users (name, email) VALUES (:name, :email)");
$stmt->bindParam(':name', $name);
$stmt->bindParam(':email', $email);
$name = "John";
$email = "john@example.com";
$stmt->execute();
```