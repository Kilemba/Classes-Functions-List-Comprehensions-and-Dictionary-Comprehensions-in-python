# Classes-Functions-List-Comprehensions-and-Dictionary-Comprehensions-in-python
A comprehensive guide to essential Python concepts for aspiring data analysts. This guide covers list comprehensions, dictionary comprehensions, functions, and object-oriented programming with practical examples.

## Table of Contents
1. [List Comprehensions](#list-comprehensions)
2. [Dictionary Comprehensions](#dictionary-comprehensions)
3. [Functions](#functions)
4. [Classes and Objects](#classes-and-objects)

---

## List Comprehensions

List comprehensions provide a concise way to create lists based on existing lists or other iterable objects. They're essential in data analytics for transforming and filtering data efficiently.

### Basic Syntax
```python
new_list = [expression for item in iterable if condition]
```

### Example 1: Basic List Comprehension
```python
# Traditional approach
numbers = [1, 2, 3, 4, 5]
squares = []
for num in numbers:
    squares.append(num ** 2)

# List comprehension approach
squares = [num ** 2 for num in numbers]
print(squares)  # Output: [1, 4, 9, 16, 25]
```

### Example 2: With Conditional Logic
```python
# Filter even numbers and square them
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_squares = [num ** 2 for num in numbers if num % 2 == 0]
print(even_squares)  # Output: [4, 16, 36, 64, 100]
```

### Example 3: Data Analytics Application
```python
# Calculate percentage change in sales
sales = [100, 120, 115, 140, 135]
percentage_changes = [
    ((sales[i] - sales[i-1]) / sales[i-1]) * 100 
    for i in range(1, len(sales))
]
print(percentage_changes)  # Output: [20.0, -4.17, 21.74, -3.57]
```

### Example 4: Nested List Comprehension
```python
# Flatten a 2D list (common in data preprocessing)
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [num for row in matrix for num in row]
print(flattened)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Example 5: String Manipulation
```python
# Clean and normalize customer names
customer_names = ["  John Doe  ", "JANE SMITH", "  bob Jones"]
cleaned_names = [name.strip().title() for name in customer_names]
print(cleaned_names)  # Output: ['John Doe', 'Jane Smith', 'Bob Jones']
```

---

## Dictionary Comprehensions

Dictionary comprehensions allow you to create dictionaries in a concise and readable way. They're particularly useful for data transformation and aggregation tasks.

### Basic Syntax
```python
new_dict = {key_expression: value_expression for item in iterable if condition}
```

### Example 1: Basic Dictionary Comprehension
```python
# Create a dictionary mapping numbers to their squares
numbers = [1, 2, 3, 4, 5]
squares_dict = {num: num ** 2 for num in numbers}
print(squares_dict)  # Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

### Example 2: From Two Lists
```python
# Create a product catalog
products = ["Laptop", "Mouse", "Keyboard", "Monitor"]
prices = [999.99, 25.50, 79.99, 349.99]
catalog = {product: price for product, price in zip(products, prices)}
print(catalog)
# Output: {'Laptop': 999.99, 'Mouse': 25.5, 'Keyboard': 79.99, 'Monitor': 349.99}
```

### Example 3: Conditional Dictionary Comprehension
```python
# Filter products above a certain price
catalog = {"Laptop": 999.99, "Mouse": 25.50, "Keyboard": 79.99, "Monitor": 349.99}
expensive_items = {product: price for product, price in catalog.items() if price > 100}
print(expensive_items)  # Output: {'Laptop': 999.99, 'Monitor': 349.99}
```

### Example 4: Data Analytics - Aggregation
```python
# Count occurrences of each category
transactions = ["Food", "Transport", "Food", "Entertainment", "Food", "Transport"]
category_counts = {category: transactions.count(category) for category in set(transactions)}
print(category_counts)  # Output: {'Food': 3, 'Transport': 2, 'Entertainment': 1}
```

### Example 5: Transform Values
```python
# Convert temperatures from Celsius to Fahrenheit
temps_celsius = {"Morning": 20, "Afternoon": 28, "Evening": 22, "Night": 18}
temps_fahrenheit = {time: (temp * 9/5) + 32 for time, temp in temps_celsius.items()}
print(temps_fahrenheit)
# Output: {'Morning': 68.0, 'Afternoon': 82.4, 'Evening': 71.6, 'Night': 64.4}
```

---

## Functions

Functions are reusable blocks of code that perform specific tasks. In data analytics, functions help organize analysis workflows and promote code reusability.

### Basic Syntax
```python
def function_name(parameters):
    """Docstring describing the function"""
    # Function body
    return result
```

### Example 1: Simple Function
```python
def greet(name):
    """Return a personalized greeting"""
    return f"Hello, {name}!"

message = greet("Alice")
print(message)  # Output: Hello, Alice!
```

### Example 2: Function with Default Parameters
```python
def calculate_discount(price, discount_percent=10):
    """Calculate discounted price with default 10% discount"""
    discount_amount = price * (discount_percent / 100)
    return price - discount_amount

print(calculate_discount(100))      # Output: 90.0
print(calculate_discount(100, 25))  # Output: 75.0
```

### Example 3: Multiple Return Values
```python
def calculate_statistics(numbers):
    """Calculate mean, median, and range of a list"""
    sorted_nums = sorted(numbers)
    mean = sum(numbers) / len(numbers)
    median = sorted_nums[len(sorted_nums) // 2]
    data_range = max(numbers) - min(numbers)
    return mean, median, data_range

data = [10, 20, 30, 40, 50]
avg, med, rng = calculate_statistics(data)
print(f"Mean: {avg}, Median: {med}, Range: {rng}")
# Output: Mean: 30.0, Median: 30, Range: 40
```

### Example 4: Data Cleaning Function
```python
def clean_data(values):
    """Remove None values and convert to float"""
    cleaned = []
    for value in values:
        if value is not None:
            try:
                cleaned.append(float(value))
            except (ValueError, TypeError):
                continue
    return cleaned

raw_data = [10, "20", None, "30.5", "invalid", 40]
cleaned_data = clean_data(raw_data)
print(cleaned_data)  # Output: [10.0, 20.0, 30.5, 40.0]
```

### Example 5: Lambda Functions
```python
# Short anonymous functions for simple operations
sales = [100, 250, 175, 300, 425]

# Apply a 10% tax using lambda
with_tax = list(map(lambda x: x * 1.10, sales))
print(with_tax)  # Output: [110.0, 275.0, 192.5, 330.0, 467.5]

# Filter sales above threshold
high_sales = list(filter(lambda x: x > 200, sales))
print(high_sales)  # Output: [250, 300, 425]
```

### Example 6: Function with Variable Arguments
```python
def calculate_total(*amounts, tax_rate=0.08):
    """Calculate total with variable number of amounts and tax"""
    subtotal = sum(amounts)
    tax = subtotal * tax_rate
    total = subtotal + tax
    return {"subtotal": subtotal, "tax": tax, "total": total}

result = calculate_total(10.99, 25.50, 15.75)
print(result)  # Output: {'subtotal': 52.24, 'tax': 4.1792, 'total': 56.4192}
```

---

## Classes and Objects

Classes allow you to create custom data structures and bundle data with functionality. In data analytics, classes are useful for organizing complex analysis workflows and creating reusable data models.

### Basic Syntax
```python
class ClassName:
    def __init__(self, parameters):
        """Constructor method"""
        self.attribute = parameters
    
    def method(self):
        """Instance method"""
        return result
```

### Example 1: Basic Class
```python
class Customer:
    """Represent a customer with basic information"""
    
    def __init__(self, name, email, customer_id):
        self.name = name
        self.email = email
        self.customer_id = customer_id
    
    def display_info(self):
        return f"Customer: {self.name} (ID: {self.customer_id})"

# Create instances
customer1 = Customer("John Doe", "john@example.com", "C001")
customer2 = Customer("Jane Smith", "jane@example.com", "C002")

print(customer1.display_info())  # Output: Customer: John Doe (ID: C001)
print(customer2.name)             # Output: Jane Smith
```

### Example 2: Class with Data Processing
```python
class SalesAnalyzer:
    """Analyze sales data for a product"""
    
    def __init__(self, product_name, sales_data):
        self.product_name = product_name
        self.sales_data = sales_data
    
    def total_sales(self):
        return sum(self.sales_data)
    
    def average_sales(self):
        return self.total_sales() / len(self.sales_data)
    
    def max_sales(self):
        return max(self.sales_data)
    
    def generate_report(self):
        return {
            "product": self.product_name,
            "total": self.total_sales(),
            "average": self.average_sales(),
            "maximum": self.max_sales()
        }

# Usage
laptop_sales = SalesAnalyzer("Laptop Pro", [10, 15, 12, 20, 18])
report = laptop_sales.generate_report()
print(report)
# Output: {'product': 'Laptop Pro', 'total': 75, 'average': 15.0, 'maximum': 20}
```

### Example 3: Class with Class Variables
```python
class Product:
    """Represent a product with inventory tracking"""
    
    tax_rate = 0.08  # Class variable shared by all instances
    
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
    
    def total_value(self):
        return self.price * self.quantity
    
    def price_with_tax(self):
        return self.price * (1 + Product.tax_rate)
    
    @classmethod
    def update_tax_rate(cls, new_rate):
        cls.tax_rate = new_rate

# Create products
product1 = Product("Mouse", 25.00, 50)
product2 = Product("Keyboard", 75.00, 30)

print(f"Total inventory value: ${product1.total_value()}")  # Output: $1250.0
print(f"Price with tax: ${product1.price_with_tax():.2f}") # Output: $27.00

# Change tax rate for all products
Product.update_tax_rate(0.10)
print(f"New price with tax: ${product1.price_with_tax():.2f}") # Output: $27.50
```

### Example 4: Data Container Class
```python
class DataRecord:
    """Store and validate a single data record"""
    
    def __init__(self, date, revenue, expenses):
        self.date = date
        self.revenue = revenue
        self.expenses = expenses
    
    @property
    def profit(self):
        """Calculate profit (revenue - expenses)"""
        return self.revenue - self.expenses
    
    @property
    def profit_margin(self):
        """Calculate profit margin percentage"""
        if self.revenue == 0:
            return 0
        return (self.profit / self.revenue) * 100
    
    def __str__(self):
        return f"Date: {self.date}, Revenue: ${self.revenue}, Profit: ${self.profit}"

# Create records
record1 = DataRecord("2024-01-01", 10000, 7000)
record2 = DataRecord("2024-01-02", 12000, 8500)

print(record1)  # Output: Date: 2024-01-01, Revenue: $10000, Profit: $3000
print(f"Profit Margin: {record1.profit_margin:.2f}%")  # Output: Profit Margin: 30.00%
```

### Example 5: Inheritance in Data Analytics
```python
class DataAnalyzer:
    """Base class for data analysis"""
    
    def __init__(self, data):
        self.data = data
    
    def clean_data(self):
        """Remove None values"""
        return [x for x in self.data if x is not None]

class StatisticalAnalyzer(DataAnalyzer):
    """Extended analyzer with statistical methods"""
    
    def mean(self):
        cleaned = self.clean_data()
        return sum(cleaned) / len(cleaned) if cleaned else 0
    
    def median(self):
        cleaned = sorted(self.clean_data())
        n = len(cleaned)
        if n == 0:
            return 0
        mid = n // 2
        if n % 2 == 0:
            return (cleaned[mid - 1] + cleaned[mid]) / 2
        return cleaned[mid]
    
    def std_deviation(self):
        cleaned = self.clean_data()
        if not cleaned:
            return 0
        mean_val = self.mean()
        variance = sum((x - mean_val) ** 2 for x in cleaned) / len(cleaned)
        return variance ** 0.5

# Usage
data = [10, 20, None, 30, 40, 50]
analyzer = StatisticalAnalyzer(data)

print(f"Mean: {analyzer.mean()}")              # Output: Mean: 30.0
print(f"Median: {analyzer.median()}")          # Output: Median: 30.0
print(f"Std Dev: {analyzer.std_deviation():.2f}") # Output: Std Dev: 14.14
```

---

## Practice Exercises

### Exercise 1: List Comprehensions
Create a list comprehension that extracts all email domains from a list of email addresses.
```python
emails = ["john@gmail.com", "jane@yahoo.com", "bob@gmail.com"]
# Expected output: ['gmail.com', 'yahoo.com', 'gmail.com']
```

### Exercise 2: Dictionary Comprehensions
Create a dictionary that maps each unique value in a list to its frequency count.
```python
data = ["A", "B", "A", "C", "B", "A", "D"]
# Expected output: {'A': 3, 'B': 2, 'C': 1, 'D': 1}
```

### Exercise 3: Functions
Write a function that calculates the compound annual growth rate (CAGR) given starting value, ending value, and number of years.
```python
# Formula: CAGR = (Ending Value / Beginning Value)^(1/years) - 1
```

### Exercise 4: Classes
Create a `Portfolio` class that tracks multiple stocks with methods to add stocks, calculate total value, and get the best performing stock.

---

## Best Practices for Data Analytics

1. **Use comprehensions** for simple transformations and filtering operations
2. **Write functions** for reusable analysis steps and complex calculations
3. **Create classes** when you need to bundle related data and methods together
4. **Add docstrings** to document your code for future reference
5. **Handle errors** gracefully when processing real-world data
6. **Use meaningful variable names** that describe the data they contain
7. **Break complex operations** into smaller, testable functions

---

## Additional Resources

- [Python Official Documentation](https://docs.python.org/3/)
- [Real Python Tutorials](https://realpython.com/)
- [Pandas Documentation](https://pandas.pydata.org/) (Next step for data analytics)
- [NumPy Documentation](https://numpy.org/) (Numerical computing in Python)

---

## Contributing

Feel free to contribute additional examples or improvements to this guide. Create a pull request with your changes!

## License

This guide is provided for educational purposes. Feel free to use and modify as needed.
