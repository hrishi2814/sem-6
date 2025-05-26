# **Multiple Selection Constructs in Ruby**

Ruby provides several ways to implement multiple selection (conditional branching) logic. Below are the primary methods:

---

## **1. `if-elsif-else` (Basic Conditional)**
The most common way to handle multiple conditions.

### **Syntax:**
```ruby
if condition1
  # Code if condition1 is true
elsif condition2
  # Code if condition2 is true
else
  # Default case
end
```

### **Example:**
```ruby
grade = 85

if grade >= 90
  puts "A"
elsif grade >= 80
  puts "B"
elsif grade >= 70
  puts "C"
else
  puts "F"
end
# Output: "B"
```

---

## **2. `case-when` (Switch-Case Alternative)**
Best for comparing a single variable against multiple values.

### **Syntax:**
```ruby
case variable
when value1
  # Code for value1
when value2
  # Code for value2
else
  # Default case
end
```

### **Example:**
```ruby
day = "Monday"

case day
when "Monday"
  puts "Start of the week"
when "Friday"
  puts "Weekend is near!"
else
  puts "Midweek day"
end
# Output: "Start of the week"
```

### **Advanced `case` (With Ranges & Conditions)**
```ruby
score = 75

case score
when 90..100 then "A"
when 80..89 then "B"
when 70..79 then "C"
else "F"
end
# Returns "C"
```

---

## **3. Ternary Operator (`? :`)**
A shorthand for simple `if-else` conditions.

### **Syntax:**
```ruby
condition ? true_action : false_action
```

### **Example:**
```ruby
age = 20
status = age >= 18 ? "Adult" : "Minor"
puts status # Output: "Adult"
```

---

## **4. `unless` (Inverted `if`)**
Used when you want to execute code **unless** a condition is true.

### **Syntax:**
```ruby
unless condition
  # Runs if condition is false
else
  # Runs if condition is true (rarely used)
end
```

### **Example:**
```ruby
logged_in = false

unless logged_in
  puts "Please log in"
end
# Output: "Please log in"
```

---

## **5. Short-Circuit Evaluation (`&&`, `||`)**
Useful for simple conditional assignments.

### **Examples:**
```ruby
# Assign a default value if nil
name = username || "Guest"

# Execute only if condition is true
user.admin? && delete_all_users!
```

---

## **6. Using `then` for One-Liners**
Ruby allows compact conditions with `then`.

### **Example:**
```ruby
if x > 10 then puts "Big" else puts "Small" end
```

---

## **Comparison Table**
| **Construct**       | **Best Use Case**                     |
|---------------------|--------------------------------------|
| `if-elsif-else`     | Multiple complex conditions          |
| `case-when`         | Matching a variable against many values |
| `ternary` (`? :`)   | Simple true/false assignments        |
| `unless`            | Inverted logic (if-not)              |
| Short-circuit (`&&`, `||`) | Default values or conditional execution |

---

## **Conclusion**
- **Use `if-elsif-else`** for complex branching.
- **Use `case-when`** for multiple value checks (like a switch-case).
- **Use `ternary`** for compact true/false assignments.
- **Use `unless`** when the condition is better expressed negatively.
- **Short-circuiting (`&&`, `||`)** is great for defaults and conditional execution.

---
