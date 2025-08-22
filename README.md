# Csharp_Methods
A comprehensive guide to learning methods in c#
# C# Methods Comprehensive Learning Guide

## Table of Contents
- [Introduction](#introduction)
- [Method Basics](#method-basics)
- [Method Components](#method-components)
- [Method Types](#method-types)
- [Parameters and Arguments](#parameters-and-arguments)
- [Return Values](#return-values)
- [Method Overloading](#method-overloading)
- [Static vs Instance Methods](#static-vs-instance-methods)
- [Access Modifiers](#access-modifiers)
- [Advanced Concepts](#advanced-concepts)
- [Best Practices](#best-practices)
- [Common Patterns](#common-patterns)
- [Practice Exercises](#practice-exercises)
- [Resources](#resources)

## Introduction

Methods in C# are fundamental building blocks that allow you to organize code into reusable, modular units. A method is a block of code that performs a specific task and can be called from other parts of your program.

## Method Basics

### What is a Method?
A method is a code block containing a series of statements that can be executed by calling the method name. Methods enable code reusability, organization, and maintainability.

### Basic Method Syntax
```csharp
[access modifier] [modifiers] [return type] MethodName([parameters])
{
    // Method body
    [return statement]
}
```

### Simple Example
```csharp
public void SayHello()
{
    Console.WriteLine("Hello, World!");
}

public int Add(int a, int b)
{
    return a + b;
}
```

## Method Components

### 1. Access Modifiers
- **public**: Accessible from anywhere
- **private**: Accessible only within the same class
- **protected**: Accessible within the class and derived classes
- **internal**: Accessible within the same assembly
- **protected internal**: Accessible within the same assembly or derived classes

### 2. Method Modifiers
- **static**: Method belongs to the type itself, not to instances
- **virtual**: Method can be overridden in derived classes
- **abstract**: Method must be implemented in derived classes
- **override**: Method overrides a virtual method from base class
- **sealed**: Method cannot be overridden further
- **async**: Method is asynchronous

### 3. Return Type
- **void**: Method doesn't return a value
- **Value types**: int, double, bool, char, etc.
- **Reference types**: string, arrays, classes, etc.
- **Generic types**: T, List<T>, etc.

### 4. Method Name
- Must follow C# naming conventions (PascalCase)
- Should be descriptive and indicate what the method does
- Cannot be a C# keyword

### 5. Parameters
- Input values the method accepts
- Can have zero or more parameters
- Each parameter has a type and name

## Method Types

### 1. Void Methods
Methods that don't return a value:
```csharp
public void DisplayMessage(string message)
{
    Console.WriteLine(message);
}
```

### 2. Value-Returning Methods
Methods that return a value:
```csharp
public int Multiply(int x, int y)
{
    return x * y;
}

public string GetFullName(string firstName, string lastName)
{
    return firstName + " " + lastName;
}
```

### 3. Expression-Bodied Methods
Concise syntax for simple methods:
```csharp
public int Square(int x) => x * x;
public string GetGreeting(string name) => $"Hello, {name}!";
```

## Parameters and Arguments

### Parameter Types

#### 1. Value Parameters (Default)
```csharp
public void ModifyValue(int number)
{
    number = 100; // Only modifies the local copy
}
```

#### 2. Reference Parameters (ref)
```csharp
public void ModifyByReference(ref int number)
{
    number = 100; // Modifies the original variable
}

// Usage
int value = 50;
ModifyByReference(ref value); // value is now 100
```

#### 3. Output Parameters (out)
```csharp
public bool TryParseAge(string input, out int age)
{
    return int.TryParse(input, out age);
}

// Usage
if (TryParseAge("25", out int userAge))
{
    Console.WriteLine($"Age: {userAge}");
}
```

#### 4. Parameter Arrays (params)
```csharp
public int Sum(params int[] numbers)
{
    return numbers.Sum();
}

// Usage
int result1 = Sum(1, 2, 3, 4, 5);
int result2 = Sum(new int[] {1, 2, 3});
```

#### 5. Optional Parameters
```csharp
public void CreateAccount(string username, string email, bool isActive = true)
{
    // Method implementation
}

// Usage
CreateAccount("john", "john@email.com"); // isActive defaults to true
CreateAccount("jane", "jane@email.com", false);
```

#### 6. Named Parameters
```csharp
public void ProcessOrder(string productName, int quantity, decimal price)
{
    // Method implementation
}

// Usage with named parameters
ProcessOrder(price: 19.99m, productName: "Widget", quantity: 2);
```

## Return Values

### Single Return Value
```csharp
public double CalculateArea(double radius)
{
    return Math.PI * radius * radius;
}
```

### Multiple Return Values (Tuples)
```csharp
public (int min, int max) FindMinMax(int[] numbers)
{
    return (numbers.Min(), numbers.Max());
}

// Usage
var (minimum, maximum) = FindMinMax(new int[] {1, 5, 3, 9, 2});
```

### Early Returns
```csharp
public string ValidateEmail(string email)
{
    if (string.IsNullOrEmpty(email))
        return "Email cannot be empty";
    
    if (!email.Contains("@"))
        return "Invalid email format";
    
    return "Valid email";
}
```

## Method Overloading

Method overloading allows multiple methods with the same name but different parameter signatures:

```csharp
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }
    
    public double Add(double a, double b)
    {
        return a + b;
    }
    
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
    
    public string Add(string a, string b)
    {
        return a + b;
    }
}
```

### Overloading Rules
- Methods must have different parameter lists
- Return type alone cannot distinguish overloaded methods
- Parameter names don't matter, only types and count
- Optional parameters can complicate overload resolution

## Static vs Instance Methods

### Instance Methods
Belong to an instance of a class and can access instance members:
```csharp
public class Person
{
    private string name;
    
    public void SetName(string newName) // Instance method
    {
        name = newName;
    }
    
    public string GetName() // Instance method
    {
        return name;
    }
}

// Usage
Person person = new Person();
person.SetName("Alice");
```

### Static Methods
Belong to the class itself and cannot access instance members:
```csharp
public class MathUtils
{
    public static double ConvertToRadians(double degrees)
    {
        return degrees * Math.PI / 180;
    }
    
    public static bool IsEven(int number)
    {
        return number % 2 == 0;
    }
}

// Usage
double radians = MathUtils.ConvertToRadians(90);
bool even = MathUtils.IsEven(4);
```

## Access Modifiers

### Public Methods
```csharp
public class PublicExample
{
    public void PublicMethod() // Accessible from anywhere
    {
        Console.WriteLine("This is a public method");
    }
}
```

### Private Methods
```csharp
public class PrivateExample
{
    private void PrivateMethod() // Only accessible within this class
    {
        Console.WriteLine("This is a private method");
    }
    
    public void CallPrivateMethod()
    {
        PrivateMethod(); // OK - calling from within the same class
    }
}
```

### Protected Methods
```csharp
public class BaseClass
{
    protected void ProtectedMethod() // Accessible in derived classes
    {
        Console.WriteLine("Protected method");
    }
}

public class DerivedClass : BaseClass
{
    public void CallProtected()
    {
        ProtectedMethod(); // OK - accessible in derived class
    }
}
```

## Advanced Concepts

### 1. Method Chaining
```csharp
public class StringBuilder
{
    private string content = "";
    
    public StringBuilder Append(string text)
    {
        content += text;
        return this; // Return this for chaining
    }
    
    public StringBuilder AppendLine(string text)
    {
        content += text + Environment.NewLine;
        return this;
    }
    
    public override string ToString()
    {
        return content;
    }
}

// Usage
string result = new StringBuilder()
    .Append("Hello")
    .Append(" ")
    .AppendLine("World")
    .Append("How are you?")
    .ToString();
```

### 2. Extension Methods
```csharp
public static class StringExtensions
{
    public static bool IsValidEmail(this string email)
    {
        return !string.IsNullOrEmpty(email) && email.Contains("@");
    }
    
    public static string Truncate(this string value, int maxLength)
    {
        if (string.IsNullOrEmpty(value)) return value;
        return value.Length <= maxLength ? value : value.Substring(0, maxLength) + "...";
    }
}

// Usage
string email = "user@example.com";
bool isValid = email.IsValidEmail(); // Called as if it's a method of string

string longText = "This is a very long text";
string truncated = longText.Truncate(10);
```

### 3. Generic Methods
```csharp
public static class GenericUtils
{
    public static T GetDefault<T>()
    {
        return default(T);
    }
    
    public static void Swap<T>(ref T first, ref T second)
    {
        T temp = first;
        first = second;
        second = temp;
    }
    
    public static List<T> CreateList<T>(params T[] items)
    {
        return new List<T>(items);
    }
}

// Usage
int defaultInt = GenericUtils.GetDefault<int>(); // 0
string defaultString = GenericUtils.GetDefault<string>(); // null

int a = 5, b = 10;
GenericUtils.Swap(ref a, ref b); // a = 10, b = 5

List<string> names = GenericUtils.CreateList("Alice", "Bob", "Charlie");
```

### 4. Async Methods
```csharp
public async Task<string> DownloadContentAsync(string url)
{
    using (HttpClient client = new HttpClient())
    {
        return await client.GetStringAsync(url);
    }
}

public async Task ProcessDataAsync()
{
    string content = await DownloadContentAsync("https://api.example.com/data");
    // Process content
}
```

## Best Practices

### 1. Method Naming
```csharp
// Good
public bool IsValidUser(string username) { }
public void SaveToDatabase(User user) { }
public decimal CalculateTotalPrice(List<Item> items) { }

// Avoid
public bool check(string u) { }
public void Save(User user) { } // Too generic
public decimal calc(List<Item> items) { } // Abbreviations
```

### 2. Method Size
Keep methods small and focused on a single responsibility:
```csharp
// Good - Single responsibility
public bool IsValidPassword(string password)
{
    return password.Length >= 8 && 
           password.Any(char.IsUpper) && 
           password.Any(char.IsLower) && 
           password.Any(char.IsDigit);
}

// Better - Even more focused
public bool HasMinimumLength(string password) => password.Length >= 8;
public bool HasUpperCase(string password) => password.Any(char.IsUpper);
public bool HasLowerCase(string password) => password.Any(char.IsLower);
public bool HasDigit(string password) => password.Any(char.IsDigit);

public bool IsValidPassword(string password)
{
    return HasMinimumLength(password) &&
           HasUpperCase(password) &&
           HasLowerCase(password) &&
           HasDigit(password);
}
```

### 3. Parameter Validation
```csharp
public void ProcessOrder(Order order)
{
    if (order == null)
        throw new ArgumentNullException(nameof(order));
        
    if (order.Items == null || order.Items.Count == 0)
        throw new ArgumentException("Order must have at least one item", nameof(order));
        
    // Process the order
}
```

### 4. Consistent Return Types
```csharp
// Good - Consistent return types
public List<User> GetActiveUsers() => activeUsers ?? new List<User>();
public List<User> GetInactiveUsers() => inactiveUsers ?? new List<User>();

// Avoid - Inconsistent (one returns null, other returns empty list)
public List<User> GetActiveUsers() => activeUsers; // might return null
public List<User> GetInactiveUsers() => inactiveUsers ?? new List<User>();
```

## Common Patterns

### 1. Factory Methods
```csharp
public class User
{
    private User(string username, string email)
    {
        Username = username;
        Email = email;
    }
    
    public static User CreateStandardUser(string username, string email)
    {
        return new User(username, email);
    }
    
    public static User CreateAdminUser(string username, string email)
    {
        var user = new User(username, email);
        user.IsAdmin = true;
        return user;
    }
    
    public string Username { get; private set; }
    public string Email { get; private set; }
    public bool IsAdmin { get; private set; }
}
```

### 2. Fluent Interface
```csharp
public class QueryBuilder
{
    private string query = "";
    
    public QueryBuilder Select(string columns)
    {
        query += $"SELECT {columns} ";
        return this;
    }
    
    public QueryBuilder From(string table)
    {
        query += $"FROM {table} ";
        return this;
    }
    
    public QueryBuilder Where(string condition)
    {
        query += $"WHERE {condition} ";
        return this;
    }
    
    public string Build() => query.Trim();
}

// Usage
string sql = new QueryBuilder()
    .Select("*")
    .From("Users")
    .Where("IsActive = 1")
    .Build();
```

### 3. Template Method Pattern
```csharp
public abstract class DataProcessor
{
    public void ProcessData()
    {
        LoadData();
        ValidateData();
        TransformData();
        SaveData();
    }
    
    protected abstract void LoadData();
    protected abstract void ValidateData();
    protected abstract void TransformData();
    protected abstract void SaveData();
}

public class CSVProcessor : DataProcessor
{
    protected override void LoadData() { /* CSV loading logic */ }
    protected override void ValidateData() { /* CSV validation */ }
    protected override void TransformData() { /* CSV transformation */ }
    protected override void SaveData() { /* CSV saving logic */ }
}
```

## Practice Exercises

### Beginner Level

1. **Basic Calculator**: Create methods for Add, Subtract, Multiply, and Divide operations.

2. **String Utilities**: Create methods to:
   - Check if a string is palindrome
   - Count words in a sentence
   - Reverse a string
   - Convert string to title case

3. **Number Operations**: Create methods to:
   - Check if a number is prime
   - Find factorial of a number
   - Generate Fibonacci sequence

### Intermediate Level

4. **Array Operations**: Create methods to:
   - Find the second largest number in an array
   - Remove duplicates from an array
   - Sort an array using different algorithms

5. **Data Validation**: Create a validation class with methods for:
   - Email validation
   - Phone number validation
   - Password strength checking

6. **File Operations**: Create methods to:
   - Read and write text files
   - Count lines, words, and characters in a file
   - Find and replace text in files

### Advanced Level

7. **Generic Collections**: Create generic methods for:
   - Searching in collections
   - Filtering collections based on predicates
   - Transforming collections

8. **Async Operations**: Create async methods for:
   - Downloading files from URLs
   - Processing large datasets
   - Making API calls with retry logic

9. **Design Patterns**: Implement:
   - Builder pattern with fluent interface
   - Factory pattern for creating different types of objects
   - Observer pattern with event handling

## Resources

### Official Documentation
- [Microsoft C# Methods Documentation](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)
- [C# Programming Guide](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/)

### Books
- "C# in Depth" by Jon Skeet
- "Clean Code" by Robert C. Martin
- "Effective C#" by Bill Wagner

### Online Resources
- [C# Corner](https://www.c-sharpcorner.com/)
- [Stack Overflow C# Questions](https://stackoverflow.com/questions/tagged/c%23)
- [LeetCode C# Problems](https://leetcode.com/)

### Practice Platforms
- [HackerRank C# Challenges](https://www.hackerrank.com/domains/algorithms)
- [Codewars C# Kata](https://www.codewars.com/)
- [Exercism C# Track](https://exercism.io/tracks/csharp)

---

## Contributing
Feel free to contribute to this guide by submitting pull requests with improvements, additional examples, or corrections.

## License
This guide is provided under the MIT License. Feel free to use and modify as needed for educational purposes.
