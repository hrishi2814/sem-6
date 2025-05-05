![[Pasted image 20250310151948.png]]

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sample Form</title>
</head>
<body>
    <h2>Sample Form</h2>
    <form action="#" method="POST">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required><br><br>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br><br>

        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br><br>

        <label>Gender:</label><br>
        <input type="radio" id="male" name="gender" value="male">
        <label for="male">Male</label>
        <input type="radio" id="female" name="gender" value="female">
        <label for="female">Female</label>
        <input type="radio" id="other" name="gender" value="other">
        <label for="other">Other</label><br><br>

        <label>Interests:</label><br>
        <input type="checkbox" id="sports" name="interests" value="sports">
        <label for="sports">Sports</label>
        <input type="checkbox" id="music" name="interests" value="music">
        <label for="music">Music</label>
        <input type="checkbox" id="reading" name="interests" value="reading">
        <label for="reading">Reading</label><br><br>

        <input type="submit" value="Submit">
    </form>
</body>
</html>

```


###  -------Table tags------------

### **HTML Table Tags with Explanation and Example**

HTML provides several tags to create and format tables. Below are five essential table-related tags:

---

### **1. `<table>` (Defines a Table)**

The `<table>` tag is the container for all table-related elements.

---

### **2. `<tr>` (Table Row)**

The `<tr>` tag is used to define a row in the table.

---

### **3. `<td>` (Table Data)**

The `<td>` tag represents individual table cells (data).

---

### **4. `<th>` (Table Header)**

The `<th>` tag is used to define header cells, typically displayed in **bold**.

---

### **5. `<caption>` (Table Caption)**

The `<caption>` tag is used to provide a title or description for the table.

---

### **Example Code:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML Table Example</title>
</head>
<body>

    <table border="1">
        <caption>Student Information</caption>
        <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Grade</th>
        </tr>
        <tr>
            <td>Alice</td>
            <td>20</td>
            <td>A</td>
        </tr>
        <tr>
            <td>Bob</td>
            <td>22</td>
            <td>B</td>
        </tr>
    </table>

</body>
</html>
```

---

### **Explanation:**

1. `<table>`: Starts the table.
2. `<caption>`: Adds a title to the table.
3. `<tr>`: Defines rows.
4. `<th>`: Represents header cells.
5. `<td>`: Represents data cells.

---

### **CSS Selectors with Explanation and Examples**

CSS selectors are used to target HTML elements and apply styles to them. Here are five important types of CSS selectors:

---

### **1. Universal Selector (`*`)**

- Selects all elements on the page.

#### **Example:**

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

✅ _This removes default margin and padding from all elements._

---

### **2. Element Selector (Tag Name)**

- Selects all occurrences of a specific HTML tag.

#### **Example:**

```css
p {
    color: blue;
    font-size: 18px;
}
```

✅ _This makes all `<p>` elements blue and increases the font size._

---

### **3. Class Selector (`.`)**

- Selects elements with a specific class attribute.

#### **Example:**

```css
.highlight {
    background-color: yellow;
    font-weight: bold;
}
```

```html
<p class="highlight">This text is highlighted.</p>
```

✅ _This applies a yellow background and bold text to elements with class `"highlight"`._

---

### **4. ID Selector (`#`)**

- Selects a unique element with a specific ID.

#### **Example:**

```css
#main-heading {
    text-align: center;
    color: red;
}
```

```html
<h1 id="main-heading">Welcome to My Website</h1>
```

✅ _This centers and colors the heading red._

---

### **5. Descendant Selector (`element1 element2`)**

- Selects an element inside another specific element.

#### **Example:**

```css
div p {
    color: green;
}
```

```html
<div>
    <p>This paragraph inside a div will be green.</p>
</div>
```

✅ _This applies green text to `<p>` elements that are inside a `<div>`._

---

### **Summary Table:**

|Selector|Description|Example|
|---|---|---|
|`*`|Universal Selector|`* { margin: 0; }`|
|`p`|Element Selector|`p { color: blue; }`|
|`.class`|Class Selector|`.highlight { font-weight: bold; }`|
|`#id`|ID Selector|`#main-heading { color: red; }`|
|`element1 element2`|Descendant Selector|`div p { color: green; }`|

---
## Document Object Model

- 

Here's a simple **HTML + JavaScript** program that demonstrates the **Document Object Model (DOM)**. This example allows a user to change the text and background color of a paragraph using buttons.:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM Manipulation Example</title>
    <style>
        #text {
            font-size: 20px;
            padding: 10px;
            background-color: lightgray;
        }
    </style>
</head>
<body>
    <h2>DOM Manipulation Example</h2>
    <p id="text">This is a sample paragraph.</p>
    <button onclick="changeText()">Change Text</button>
    <button onclick="changeColor()">Change Background Color</button>

    <script>
        function changeText() {
            document.getElementById("text").innerText = "Text has been changed!";
        }

        function changeColor() {
            document.getElementById("text").style.backgroundColor = "yellow";
        }
    </script>
</body>
</html>

```

### **Explanation:**

1. **HTML Structure**:
    
    - A `<p>` element with `id="text"` displays the initial text.
    - Two buttons trigger JavaScript functions.
2. **CSS Styling**:
    
    - The paragraph has default styles (font size and background color).
3. **JavaScript Functions (DOM Manipulation)**:
    
    - `changeText()`: Modifies the paragraph's text using `innerText`.
    - `changeColor()`: Changes the paragraph’s background color using `style.backgroundColor`.

This demonstrates basic **DOM manipulation** by updating elements dynamically.

---
### **Explanation of Alert, Confirmation, and Prompt Box in JavaScript:**

1. **Alert Box (`alert()`)**
    
    - Used to display a simple message to the user.
    - The user can only click "OK" to proceed.
    
    **Example:**
    
    ```javascript
    alert("This is an alert box!");
    ```
    
2. **Confirmation Box (`confirm()`)**
    
    - Displays a message with "OK" and "Cancel" buttons.
    - Returns `true` if the user clicks "OK" and `false` if they click "Cancel".
    
    **Example:**
    
    ```javascript
    let result = confirm("Are you sure?");
    if (result) {
        alert("You clicked OK!");
    } else {
        alert("You clicked Cancel!");
    }
    ```
    
3. **Prompt Box (`prompt()`)**
    
    - Allows user input with a text box.
    - Returns the entered value or `null` if the user cancels.
    
    **Example:**
    
    ```javascript
    let name = prompt("Enter your name:");
    alert("Hello, " + name + "!");
    ```
    

---

### **HTML + JavaScript Code to Calculate Factorial**

This code takes a number from the user using `prompt()`, calculates the factorial, and displays the result in an `alert()` box.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Factorial Calculator</title>
</head>
<body>
    <h2>Factorial Calculator</h2>
    <button onclick="calculateFactorial()">Find Factorial</button>

    <script>
        function calculateFactorial() {
            let num = prompt("Enter a number:");
            if (num === null || num === "" || isNaN(num) || num < 0) {
                alert("Please enter a valid positive number.");
                return;
            }

            num = parseInt(num);
            let factorial = 1;
            for (let i = 1; i <= num; i++) {
                factorial *= i;
            }

            alert("Factorial of " + num + " is: " + factorial);
        }
    </script>
</body>
</html>
```

---

### **Explanation of the Code:**

1. **Button**: Clicking the button triggers the `calculateFactorial()` function.
2. **Prompt Box**: Asks the user for a number.
3. **Validation**: Checks if the input is a valid positive number.
4. **Factorial Calculation**: Uses a `for` loop to compute the factorial.
5. **Alert Box**: Displays the result.

---
If you want a simpler way to validate a form **without using regex**, you can use **basic string functions and number checks**. Here’s an easier approach:

---

### **📌 Simplified HTML + JavaScript Form Validation (No Regex)**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Form Validation</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .error { color: red; font-size: 14px; }
    </style>
</head>
<body>
    <h2>Registration Form</h2>
    <form id="registrationForm" onsubmit="return validateForm()">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name">
        <span class="error" id="nameError"></span><br><br>

        <label for="email">Email:</label>
        <input type="text" id="email" name="email">
        <span class="error" id="emailError"></span><br><br>

        <label for="mobile">Mobile Number:</label>
        <input type="text" id="mobile" name="mobile">
        <span class="error" id="mobileError"></span><br><br>

        <input type="submit" value="Register">
    </form>

    <script>
        function validateForm() {
            let isValid = true;

            // Get form values
            let name = document.getElementById("name").value.trim();
            let email = document.getElementById("email").value.trim();
            let mobile = document.getElementById("mobile").value.trim();

            // Name Validation: Minimum 3 characters, only letters allowed
            if (name.length < 3 || !isNaN(name)) {
                document.getElementById("nameError").innerText = "Enter a valid name (Min 3 letters).";
                isValid = false;
            } else {
                document.getElementById("nameError").innerText = "";
            }

            // Email Validation: Must include "@" and "."
            if (email.indexOf("@") === -1 || email.indexOf(".") === -1) {
                document.getElementById("emailError").innerText = "Enter a valid email.";
                isValid = false;
            } else {
                document.getElementById("emailError").innerText = "";
            }

            // Mobile Number Validation: Must be 10 digits
            if (mobile.length !== 10 || isNaN(mobile)) {
                document.getElementById("mobileError").innerText = "Enter a valid 10-digit mobile number.";
                isValid = false;
            } else {
                document.getElementById("mobileError").innerText = "";
            }

            return isValid; // Return false prevents form submission if invalid
        }
    </script>
</body>
</html>
```

---

### **🔹 Explanation (No Regex Used):**

✅ **Name Validation**:

- Checks if the name has at least 3 characters.
- Ensures the input is not purely numbers (`isNaN(name)`).  
    ✅ **Email Validation**:
- Checks if the email **contains** `"@"` and `"."` (basic check).  
    ✅ **Mobile Number Validation**:
- Ensures it's exactly **10 characters long**.
- Uses `isNaN(mobile)` to make sure it's a number.

---

### **✨ Why This Approach?**

✔️ **Easier to understand** (No regex needed).  
✔️ **Basic string methods** (`length`, `indexOf()`, `isNaN()`).  
✔️ **Good for simple validation** without extra complexity.

Would you like to add more fields (e.g., password, address)? 😊

---
### **Advantages of jQuery**

jQuery is a popular JavaScript library that simplifies **HTML document traversal, event handling, animations, and AJAX interactions**. Here are some key advantages:

1. **Easy to Use and Learn**
    
    - jQuery simplifies JavaScript code, making it shorter and easier to read.
    - Example: Selecting an element in vanilla JavaScript:
        
        ```javascript
        document.getElementById("myElement").style.color = "red";
        ```
        
        **With jQuery:**
        
        ```javascript
        $("#myElement").css("color", "red");
        ```
        
2. **Cross-Browser Compatibility**
    
    - jQuery automatically handles differences between browsers, ensuring smooth performance.
3. **Less Code, More Functionality**
    
    - Complex JavaScript operations can be done in just a few lines using jQuery.
4. **Built-in Animations and Effects**
    
    - jQuery provides pre-built animations like `fadeIn()`, `fadeOut()`, and `slideToggle()`.
5. **AJAX Support**
    
    - jQuery simplifies AJAX calls, making it easy to fetch data from a server.

---

### **jQuery Syntax with Example**

jQuery syntax is simple:

```javascript
$(selector).action();
```

- **`$`** → Represents jQuery.
- **`selector`** → Selects HTML elements (`id`, `class`, `tag`).
- **`action()`** → Performs an operation (e.g., hiding, showing, animating).

#### **Example: jQuery to Hide a Paragraph on Button Click**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery Example</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <p id="myParagraph">This is a paragraph.</p>
    <button id="hideBtn">Hide</button>

    <script>
        $(document).ready(function(){
            $("#hideBtn").click(function(){
                $("#myParagraph").hide(); // Hides the paragraph when button is clicked
            });
        });
    </script>
</body>
</html>
```

---

### **🔹 Explanation of Example:**

1. **`$(document).ready()`** → Ensures the script runs only after the document is fully loaded.
2. **`$("#hideBtn").click()`** → Triggers when the button is clicked.
3. **`$("#myParagraph").hide();`** → Hides the paragraph.

---

### **Common jQuery Selectors & Methods**

|Selector|Description|Example|
|---|---|---|
|`$("p")`|Selects all `<p>` elements|`$("p").hide();`|
|`$("#id")`|Selects an element by ID|`$("#myDiv").fadeOut();`|
|`$(".class")`|Selects elements by class|`$(".box").css("background", "blue");`|
|`$("div:first")`|Selects the first `<div>`|`$("div:first").slideUp();`|

---

### **Conclusion**

jQuery is a powerful, easy-to-use JavaScript library that simplifies **DOM manipulation, animations, event handling, and AJAX calls**. It requires **less code** while maintaining **cross-browser compatibility**.

---
### **Operators, Functions, and Arrays in JavaScript**

JavaScript provides several core features that help in performing calculations, executing reusable blocks of code, and handling collections of data. Let's break these down with examples.

---

## **1. Operators in JavaScript**

Operators are symbols that perform operations on values. They can be arithmetic, logical, comparison, or assignment operators.

### **Types of Operators:**

1. **Arithmetic Operators** (`+`, `-`, `*`, `/`, `%`, `**`)
    
    ```js
    let a = 10, b = 3;
    console.log(a + b);  // 13 (Addition)
    console.log(a - b);  // 7  (Subtraction)
    console.log(a * b);  // 30 (Multiplication)
    console.log(a / b);  // 3.33 (Division)
    console.log(a % b);  // 1  (Modulus)
    console.log(a ** b); // 1000 (Exponentiation)
    ```
    
2. **Comparison Operators** (`==`, `===`, `!=`, `>`, `<`, `>=`, `<=`)
    
    ```js
    console.log(5 == '5');  // true (only checks value)
    console.log(5 === '5'); // false (checks value and type)
    console.log(10 > 5);    // true
    console.log(10 <= 5);   // false
    ```
    
3. **Logical Operators** (`&&`, `||`, `!`)
    
    ```js
    let x = true, y = false;
    console.log(x && y);  // false (AND - both should be true)
    console.log(x || y);  // true (OR - at least one should be true)
    console.log(!x);      // false (NOT - negates the value)
    ```
    
4. **Assignment Operators** (`=`, `+=`, `-=`, `*=`, `/=`)
    
    ```js
    let num = 10;
    num += 5;  // num = num + 5 (15)
    num *= 2;  // num = num * 2 (30)
    console.log(num);
    ```
    

---

## **2. Functions in JavaScript**

A function is a reusable block of code that can be called to perform a specific task.

### **Function Syntax**

```js
function functionName(parameters) {
   // function body
   return value; // (optional)
}
```

### **Example 1: Function with Parameters**

```js
function add(a, b) {
   return a + b;
}
console.log(add(10, 5)); // Output: 15
```

### **Example 2: Function Without Parameters**

```js
function greet() {
   console.log("Hello, JavaScript!");
}
greet(); // Output: Hello, JavaScript!
```

### **Example 3: Arrow Function**

Arrow functions provide a concise way to write functions.

```js
const multiply = (a, b) => a * b;
console.log(multiply(4, 5)); // Output: 20
```

---

## **3. Arrays in JavaScript**

An array is a collection of values stored in a single variable.

### **Creating an Array**

```js
let fruits = ["Apple", "Banana", "Mango"];
console.log(fruits[0]); // Output: Apple
```

### **Common Array Methods**

1. **Push & Pop (Add/Remove from End)**
    
    ```js
    let numbers = [1, 2, 3];
    numbers.push(4); // Adds 4 to the end
    console.log(numbers); // [1, 2, 3, 4]
    
    numbers.pop(); // Removes last element
    console.log(numbers); // [1, 2, 3]
    ```
    
2. **Shift & Unshift (Add/Remove from Start)**
    
    ```js
    numbers.unshift(0); // Adds 0 at start
    console.log(numbers); // [0, 1, 2, 3]
    
    numbers.shift(); // Removes first element
    console.log(numbers); // [1, 2, 3]
    ```
    
3. **Looping Through an Array**
    
    ```js
    let colors = ["Red", "Green", "Blue"];
    for (let color of colors) {
       console.log(color);
    }
    ```
    
4. **Map Function (Transform Each Element)**
    
    ```js
    let nums = [1, 2, 3];
    let squared = nums.map(n => n * n);
    console.log(squared); // [1, 4, 9]
    ```
    

---

### **Summary**

- **Operators** help in performing calculations and logical operations.
- **Functions** allow us to write reusable code.
- **Arrays** help store and manipulate collections of data.
---


### **Document Tree in DOM (Document Object Model)**

The **Document Object Model (DOM)** represents the structure of an HTML document as a tree-like structure where each element (tags, attributes, text, etc.) is a **node**. This hierarchical structure is called the **document tree**.

---

## **1. Understanding the Document Tree**

When a browser loads an HTML page, it creates a **DOM tree** based on the document's elements.

For example, consider the following HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Document Tree</title>
  </head>
  <body>
    <h1>Hello, DOM!</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

### **DOM Tree Representation:**

```
Document
│
├── <html>
│   ├── <head>
│   │   └── <title> → "Document Tree"
│   ├── <body>
│   │   ├── <h1> → "Hello, DOM!"
│   │   └── <p> → "This is a paragraph."
```

Each node in this structure represents an HTML element or content.

---

## **2. Types of Nodes in the DOM**

1. **Document Node**: Represents the entire HTML document (`document` object in JavaScript).
2. **Element Nodes**: Represent HTML tags (`<html>`, `<head>`, `<body>`, `<h1>`, etc.).
3. **Text Nodes**: Contain text inside elements (`"Hello, DOM!"` inside `<h1>`).
4. **Attribute Nodes**: Represent attributes inside elements (`class="example"` inside an element).
5. **Comment Nodes**: Represent HTML comments (`<!-- This is a comment -->`).

---

## **3. Accessing and Modifying the DOM Tree Using JavaScript**

JavaScript allows us to interact with the DOM tree using various methods.

### **Accessing Elements**

```js
console.log(document.title); // Output: Document Tree
console.log(document.body);  // Outputs the <body> element
console.log(document.getElementById("myElement")); // Get element by ID
console.log(document.querySelector("p")); // Get first <p> element
```

### **Modifying Elements**

```js
document.querySelector("h1").textContent = "Modified Heading!";
document.body.style.backgroundColor = "lightgray";
```

### **Creating and Appending New Elements**

```js
let newParagraph = document.createElement("p");
newParagraph.textContent = "New paragraph added!";
document.body.appendChild(newParagraph);
```

---

## **4. Traversing the DOM Tree**

JavaScript provides ways to navigate the document tree:

- `parentNode` → Get parent of an element
- `childNodes` → Get children (including text and comment nodes)
- `firstChild`, `lastChild` → Get first and last child
- `nextSibling`, `previousSibling` → Navigate between siblings
- `children` → Get only element children (ignores text and comments)

Example:

```js
let body = document.body;
console.log(body.parentNode); // <html>
console.log(body.children);   // List of child elements
console.log(body.firstChild); // First node inside <body>
console.log(body.lastChild);  // Last node inside <body>
```

---

## **5. Summary**

- The **document tree** represents an HTML page as a hierarchical structure.
- The **DOM consists of nodes**: document, element, text, attribute, and comment nodes.
- JavaScript can be used to **access, modify, and traverse the DOM tree**.
- DOM methods like `getElementById`, `querySelector`, `appendChild`, and `parentNode` help in interacting with elements.

---
