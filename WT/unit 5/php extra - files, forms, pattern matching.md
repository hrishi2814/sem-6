## 🧩 Pattern Matching in PHP (Regex)

PHP supports pattern matching using **Perl-compatible regular expressions (PCRE)** via `preg_match()`.

### 🧪 Syntax:

```php
preg_match($pattern, $subject, $matches)
```

- `$pattern`: The regex (in `"/pattern/"` format).
    
- `$subject`: The string to search in.
    
- `$matches` _(optional)_: Array to store matched parts.
    

### ✅ Example: Email validation

```php
<?php
$email = "user@example.com";
if (preg_match("/^[\w.-]+@[\w.-]+\.[a-z]{2,}$/i", $email)) {
    echo "Valid email";
} else {
    echo "Invalid email";
}
?>
```

---

## 🧾 Form Handling in PHP

PHP uses superglobals like `$_POST` and `$_GET` to collect form data.

### 📄 HTML Form (form.html):

```html
<form action="process.php" method="POST">
  Name: <input type="text" name="username">
  <input type="submit" value="Submit">
</form>
```

### 🧠 PHP Backend (process.php):

```php
<?php
// Safely access form data
$name = $_POST['username'] ?? 'Guest';

// Prevent XSS using htmlspecialchars
echo "Welcome, " . htmlspecialchars($name);
?>
```

### 🔐 Tips:

- Always use `htmlspecialchars()` when displaying user input.
    
- Use `isset()` or null coalescing (`??`) to avoid undefined index warnings.
    

---

## 📁 File Operations in PHP

PHP provides both **simple** and **manual** methods to read/write files.

---

### ✍️ Writing to a File

**Quick method:**

```php
file_put_contents("notes.txt", "Hello\n", FILE_APPEND);
```

- `FILE_APPEND`: Adds to the file without erasing it.
    

**Manual method:**

```php
$fp = fopen("notes.txt", "a");
fwrite($fp, "Another line\n");
fclose($fp);
```

---

### 📖 Reading from a File

```php
$content = file_get_contents("notes.txt");
echo $content;
```

**Manual read line-by-line:**

```php
$fp = fopen("notes.txt", "r");
while ($line = fgets($fp)) {
    echo $line . "<br>";
}
fclose($fp);
```

---

## 🧵 Summary Table

|Feature|Function(s)|Notes|
|---|---|---|
|Pattern Matching|`preg_match()`|For validating formats (email, etc.)|
|Form Handling|`$_POST`, `$_GET`, `htmlspecialchars()`|Secure input/output|
|File Writing|`file_put_contents()`, `fwrite()`|Use `FILE_APPEND` to avoid overwriting|
|File Reading|`file_get_contents()`, `fgets()`|Use loops for line-by-line reading|

---

Let me know if you want an all-in-one practical demo that covers form + regex validation + saving to a file!