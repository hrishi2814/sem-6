# **Classes and Objects in Ruby (with Examples)**

## **1. Classes in Ruby**
A **class** is a blueprint for creating objects. It defines:
- **Attributes** (data/variables)
- **Methods** (functions/behaviors)

### **Syntax**
```ruby
class ClassName
  # Constructor (initialize method)
  def initialize(parameters)
    # Initialize attributes
  end

  # Methods
  def method_name
    # Method logic
  end
end
```

---

## **2. Objects in Ruby**
An **object** is an **instance of a class**. You create objects using the `new` method.

### **Syntax**
```ruby
object_name = ClassName.new(arguments)
```

---

## **3. Example: Defining a Class & Creating Objects**
### **`Person` Class Example**
```ruby
class Person
  # Constructor (called when Person.new is used)
  def initialize(name, age)
    @name = name  # @ denotes instance variables
    @age = age
  end

  # Method to display details
  def introduce
    puts "Hello, I'm #{@name} and I'm #{@age} years old."
  end

  # Method to update age
  def birthday
    @age += 1
    puts "Happy Birthday! Now I'm #{@age}."
  end
end
```

### **Creating Objects (Instances)**
```ruby
person1 = Person.new("Alice", 25)
person2 = Person.new("Bob", 30)

# Call methods
person1.introduce  # Output: "Hello, I'm Alice and I'm 25 years old."
person2.introduce  # Output: "Hello, I'm Bob and I'm 30 years old."

person1.birthday   # Output: "Happy Birthday! Now I'm 26."
```

---

## **4. Key Concepts**
### **Instance Variables (`@variable`)**
- Store object-specific data.
- Accessible only within the class methods.

### **Constructor (`initialize`)**
- Automatically called when `ClassName.new` is used.
- Used to set initial values.

### **Getter & Setter Methods**
By default, instance variables are **private**. To access them:
```ruby
class Person
  # Getter method for name
  def name
    @name
  end

  # Setter method for name
  def name=(new_name)
    @name = new_name
  end
end

person = Person.new("Charlie", 22)
puts person.name    # Output: "Charlie" (getter)
person.name = "Dave" # (setter)
```

### **Shortcut: `attr_accessor`**
Instead of writing getters/setters manually:
```ruby
class Person
  attr_accessor :name, :age  # Auto-creates getters & setters
end
```

---

## **5. Inheritance in Ruby**
A class can **inherit** from another class using `<`.

### **Example**
```ruby
class Animal
  def speak
    puts "Animal sound!"
  end
end

class Dog < Animal
  def speak
    puts "Woof!"
  end
end

dog = Dog.new
dog.speak  # Output: "Woof!" (overrides Animal#speak)
```

---

## **6. Summary**
| Concept | Example |
|---------|---------|
| **Class Definition** | `class Person; end` |
| **Constructor** | `def initialize(name); @name = name; end` |
| **Instance Variable** | `@name` |
| **Object Creation** | `person = Person.new("Alice")` |
| **Getter/Setter** | `attr_accessor :name` |
| **Inheritance** | `class Dog < Animal` |

---

## **7. When to Use Classes & Objects?**
✔ **Model real-world entities** (e.g., `User`, `Product`).  
✔ **Encapsulate data + behavior** (e.g., `BankAccount` with `deposit`/`withdraw`).  
✔ **Reuse code via inheritance** (e.g., `Animal` → `Dog`, `Cat`).  

---

# **Scalar Types and Their Operations in Ruby**

Scalar types in Ruby represent single values. The main scalar types are:

1. **Numbers** (Integers, Floats)
2. **Strings**
3. **Symbols**
4. **Booleans** (true, false, nil)

Let's explore each with examples of operations:

## **1. Numbers**
### **Integers**
```ruby
a = 10
b = 3

# Arithmetic operations
puts a + b   # 13 (Addition)
puts a - b   # 7  (Subtraction)
puts a * b   # 30 (Multiplication)
puts a / b   # 3  (Integer division)
puts a % b   # 1  (Modulo)
puts a ** b  # 1000 (Exponentiation)

# Comparison
puts a == b  # false
puts a > b   # true
```

### **Floats**
```ruby
x = 10.0
y = 3.0

puts x / y   # 3.3333333333333335 (Float division)
puts x.round(2) # 10.0 (Rounding)
```

## **2. Strings**
```ruby
str1 = "Hello"
str2 = "Ruby"

# Concatenation
puts str1 + " " + str2  # "Hello Ruby"
puts "#{str1} #{str2}"  # String interpolation (preferred)

# Common methods
puts str1.length        # 5
puts str1.upcase        # "HELLO"
puts str1.downcase      # "hello"
puts str1.reverse       # "olleH"
puts str1.include?("e") # true

# Access characters
puts str1[0]    # "H"
puts str1[0..2] # "Hel"
```

## **3. Symbols**
```ruby
# Symbols are immutable identifiers
status = :active

# Commonly used as hash keys
user = { name: "Alice", age: 25 }
puts user[:name]  # "Alice"
```

## **4. Booleans**
```ruby
# Boolean values
t = true
f = false
n = nil  # represents "nothing"

# Logical operations
puts t && f  # false (AND)
puts t || f  # true  (OR)
puts !t      # false (NOT)

# Truthiness
puts "Valid" if n  # Doesn't execute (nil is falsey)
puts "Valid" if 1  # Executes (any value except false/nil is truthy)
```

## **Type Conversion**
```ruby
# String to Number
puts "123".to_i  # 123 (Integer)
puts "12.3".to_f # 12.3 (Float)

# Number to String
puts 123.to_s    # "123"

# Other conversions
puts "a".ord     # 97 (ASCII value)
puts 97.chr      # "a" (Character from ASCII)
```

## **Summary Table**
| Type      | Example          | Key Operations                     |
|-----------|------------------|------------------------------------|
| Integer   | `42`            | `+`, `-`, `*`, `/`, `%`, `**`     |
| Float     | `3.14`          | Same as Integer + `round`, `ceil`  |
| String    | `"hello"`       | `+`, `length`, `upcase`, `reverse` |
| Symbol    | `:status`       | Used as immutable identifiers      |
| Boolean   | `true`, `false` | `&&`, `||`, `!`                    |

These scalar types and their operations form the foundation of Ruby programming.

---
