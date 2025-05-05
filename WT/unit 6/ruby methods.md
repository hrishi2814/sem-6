# **Methods in Ruby: How to Write and Call Them**

Methods in Ruby (similar to functions in other languages) are reusable blocks of code that perform specific tasks. Here's a complete guide to writing and calling methods in Ruby.

## **1. Defining Methods**

### **Basic Syntax**
```ruby
def method_name(parameter1, parameter2)
  # Method body
  return value  # optional
end
```

### **Simple Example**
```ruby
def greet
  puts "Hello, Ruby!"
end
```

### **Method with Parameters**
```ruby
def greet(name)
  puts "Hello, #{name}!"
end
```

### **Method with Default Parameters**
```ruby
def greet(name = "Ruby")
  puts "Hello, #{name}!"
end
```

### **Method with Return Value**
```ruby
def add(a, b)
  return a + b  # 'return' is optional (last expression is returned by default)
end
```

## **2. Calling Methods**

### **Basic Call**
```ruby
greet  #=> "Hello, Ruby!"
```

### **Call with Arguments**
```ruby
greet("Alice")  #=> "Hello, Alice!"
```

### **Call with Parentheses (Optional)**
```ruby
greet "Alice"   # Works without parentheses
greet("Alice")  # Also works
```

### **Using Return Value**
```ruby
result = add(3, 5)
puts result  #=> 8
```

## **3. Special Method Types**

### **Predicate Methods (End with ?)**
```ruby
def even?(number)
  number % 2 == 0
end

puts even?(4)  #=> true
```

### **Bang Methods (End with !)**
```ruby
def capitalize!(string)
  string.upcase!
end

name = "ruby"
capitalize!(name)
puts name  #=> "RUBY" (mutates the original)
```

### **Splat Operator (Variable Arguments)**
```ruby
def sum(*numbers)
  numbers.sum
end

puts sum(1, 2, 3)  #=> 6
```

## **4. Method Scope & Visibility**

### **Instance Methods**
```ruby
class Calculator
  def add(a, b)
    a + b
  end
end

calc = Calculator.new
puts calc.add(2, 3)  #=> 5
```

### **Class Methods**
```ruby
class MathUtils
  def self.square(x)
    x * x
  end
end

puts MathUtils.square(4)  #=> 16
```

## **5. Best Practices**
1. Use **snake_case** for method names (`calculate_total`)
2. Keep methods **short and focused** (single responsibility)
3. Use **?** for methods that return booleans
4. Use **!** for methods that modify their receiver
5. **Avoid** too many parameters (consider using hashes for options)

## **6. Complete Example**
```ruby
def calculate_total(price, quantity, discount = 0)
  subtotal = price * quantity
  total = subtotal - (subtotal * discount / 100.0)
  total.round(2)
end

puts calculate_total(10, 5)       #=> 50.0
puts calculate_total(10, 5, 20)   #=> 40.0 (with 20% discount)
```

