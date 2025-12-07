## Basic
#### What experience do you have with C# and .NET? Can you describe a project where you used them?
**Answer:**
"I have worked extensively with C# and .NET, including .NET Core, in developing various enterprise-level applications. In one project, I developed a web application using ASP.NET Core MVC, where I implemented complex business logic using C# and integrated it with an Oracledatabase. I also created APIs using Web API, ensuring they followed best practices for performance and security."
#### How do you implement security in .NET Core applications?
**Answer:**
Security can be implemented in .NET Core applications by using: • Authentication: Verify the identity of users via JWT tokens, cookie-based authentication, or third-party providers like OAuth. • Authorization: Use role-based or policy-based authorization to control access to application.
#### What is your experience with APIs, and how do you test them?
**Answer:**
"I have developed RESTful APIs using ASP.NET Core Web API, and I ensure they are welldocumented using tools like Swagger. I test APIs using Postman, where I write test cases to check for expected responses, status codes, and error handling. I also use unit tests to ensure API controllers function as expected."
#### Describe your experience with Agile methodologies and working in an onshore/offshore model.
**Answer:**
"I have worked in Agile environments, where we use Scrum or Kanban to manage sprints and tasks. In the onshore/offshore model, I have collaborated with both onshore teams and offshore developers. We used tools like JIRA for tracking progress, and I was involved in daily standups, sprint planning, and code reviews to ensure alignment between teams."
#### Hard Binding vs Loose Binding
-   **Hard Binding**: This refers to a strong coupling between components. One component explicitly depends on the other, and changes to one will likely require changes to the other. It’s common in traditional development where dependencies are tightly coupled.<br>
Example: A method directly calls another method within the same class.
-   **Loose Binding**: This refers to a weak coupling between components. One component can function without knowing about the other’s internal details. It allows for more flexible, maintainable, and scalable systems.<br>
Example: Using interfaces or dependency injection to decouple classes.
#### Explain ENUM.
**Answer:**
**Enums** (short for **Enumerations**) are a special data type in C# that allows you to define a set of named constants. They are used to represent a collection of related values in a more readable and maintainable way.
#### 🧩 Example
SYNTAX- Here, Day is an enumeration, and its values (Sunday, Monday, etc.) are constants starting from 0 by default. You can explicitly assign values if needed.
```csharp
enum Day
{
    Sunday,
    Monday,
    Tuesday,
}
```
-   Key Points:
1.  Enums improve code readability and reduce the risk of invalid values.
2.  They can be cast to integers and vice versa.
3.  Enums can have different underlying types (e.g., byte, short, int).
#### Printing vs Logging
**Printing** typically refers to sending output to a console or display, often for debugging or temporary visibility.
#### 🧩 Example

Print is used for displaying messages to the user or developers during runtime for debugging purposes.

```csharp
Console.WriteLine("Hello, World!");
```
**Logging** is the process of recording runtime information (such as errors, warnings, or information) into a log file or a logging system.
#### 🧩 Example

Logging is a more formalized and persistent method of tracking application activity. It supports various log levels (e.g., Info, Error, Warning) and can write logs to files or external systems.

```csharp
ILogger logger = LoggerFactory.Create(builder => builder.AddConsole()).CreateLogger<Program>();
logger.LogInformation("Application started");
```
-   Difference
Printing is more of a temporary or debugging feature, whereas logging is a structured and persistent record of events or activities in an application.
#### Value Types vs Reference Types
**Value Types** These types hold data directly and are stored on the stack. Examples include `int, double, char, struct.`
-   When a value type is assigned to another variable, a copy of the data is made.</br>

**Reference Types** These types store a reference (or pointer) to the actual data, which is stored on the heap. Examples include `class`, `string`, `array`, `delegate`.
-   When a reference type is assigned to another variable, both variables point to the same memory location, so changes to one will affect the other.
#### Out vs Ref
In C#, both `out` and `ref` are used to pass arguments to methods by reference, allowing the method to modify the values of the arguments. However, there are key differences in how they work:
#### ref (reference Keyword)
**Definition**: The `ref` keyword is used to pass a parameter by reference, meaning that the method can modify the value of the argument. The parameter must be initialized before being passed to the method.<br>
**Usage**: The value of the argument is expected to be initialized before passing to the method.
#### 🧩 Example
```csharp
using System;
class Program
{
    static void ModifyValue(ref int number)
    {
        number = number + 5;
    }
    static void Main()
    {
        int num = 10;
        ModifyValue(ref num); // The value of num is passed by reference
        Console.WriteLine(num); // Output: 15
    }
}
```
**Key Points**
-   The variable must be initialized before calling the method.
-   The method can modify the value of the variable.
#### out (Output Keyword)
**Definition**: The out keyword is used to pass a parameter by reference, but it is specifically intended to return a value from the method. The argument does not need to be initialized before being passed, but it must be assigned a value before the method finishes execution.<br>
**Usage**: The parameter does not need to be initialized before passing it to the method.
#### 🧩 Example
```csharp
using System;
class Program
{
    static void GetNumber(out int number)
    {
        number = 42; // Assigning value inside the method
    }
    static void Main()
    {
        int num;
        GetNumber(out num); // The value of num is assigned inside the method
        Console.WriteLine(num); // Output: 42
    }
}
```
**Key Points**
-   The variable does not need to be initialized before calling the method.
-   The method must assign a value to the variable before returning.

| Feature                    | `ref`                    | `out`                     |
| -------------------------- | ------------------------ | ------------------------- |
| Initialization before call | Required                 | Not required              |
| Must assign inside method  | No                       | Yes                       |
| Can be used for input      | Yes                      | No (output only)          |
| Common use case            | Modifying existing value | Returning multiple values |

#### Const vs Var
In C#, const and var are used to declare variables, but they serve different purposes:
#### const (Constant):
**Definition:** The const keyword is used to define a constant value that cannot be changed during the program's execution. Once a value is assigned to a const variable, it is fixed and cannot be modified. <br>
**Usage:** You must assign a value at the time of declaration, and the value remains constant throughout the program.
#### 🧩 Example
```csharp
using System;
class Program
{
    const double Pi = 3.14; // Pi is a constant value
    static void Main()
    {
        Console.WriteLine(Pi); // Output: 3.14
    }
}
```
**Key Points**
-   The value assigned to a `const` is fixed at compile time.
-   `const` variables must be assigned a value at the time of declaration.
-   Constants are typically used for values that are not expected to change, such as mathematical constants.
#### var (Implicitly Typed Variable)
**Definition**: The var keyword is used to declare a variable without explicitly specifying its type. The compiler infers the type of the variable based on the assigned value.
**Usage**: You do not specify the type of the variable; the compiler automatically determines it based on the initializer.
#### 🧩 Example
```csharp
using System;
class Program
{
    static void Main()
    {
        var number = 10; // The compiler infers that 'number' is of type int
        var text = "Hello, world!"; // The compiler infers that 'text' is of type string
        Console.WriteLine(number); // Output: 10
        Console.WriteLine(text); // Output: Hello, world!
    }      
}
```
**Key Points**
-   The type of the variable is inferred by the compiler.
-   `var` can only be used when the variable is initialized at the time of declaration.
-   The type cannot change after the variable is initialized (it's strongly typed after initialization).
#### Const vs Readonly
`const`: A const is a constant value that is determined at compile time. It must be assigned a value at the time of declaration and cannot be modified later.
#### 🧩 Example
```csharp
public const int MaxLimit = 100; // Compile-time constant
```
`readonly`: A readonly field can only be assigned a value during its declaration or in a constructor. It can be modified at runtime, but once assigned, it cannot be changed again.
#### 🧩 Example
```csharp
public readonly int MaxLimit; // Run-time constant
public MyClass(int limit)
{
    MaxLimit = limit; // Can assign value in constructor
}
```
#### Summary of Differences
| 🔹 **Feature** | **out** | **ref** | **const** | **var** |
|----------------|----------------|----------------|-------------|-------------|
| **Initialization Before Use** | No, does not need to be initialized | Yes | Yes, must be initialized at declaration | No, the compiler infers the type based on the initializer |
| **Purpose** | To return a value from a method | To pass a value by reference | To define a constant value | To let the compiler infer the variable type |
| **Value Change**| Must be assigned in method | Can be modified in method | Cannot be changed once assigned | Can change the value but type is fixed | 
| **Typical Use Case** | Returning multiple values from a method | Passing large objects or modifying values | Defining constant values like Pi, or mathematical constants | When the type is obvious from the initializer |
#### Serialization and Deserialization
Serialization converts an object into a storable/transmittable format, while deserialization reverts it back into an object.
#### Array vs ArrayList
#### Arrays
-   Fixed-size collection of elements of the same type.
-   It cannot grow or shrink in size after initialization.
-   Best for storing a fixed set of elements.
#### 🧩 Example
```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
Console.WriteLine(numbers[0]); // Output: 1
```
#### ArrayList
-   A dynamic collection that can grow and shrink in size.
-   It can hold elements of any type (though it is commonly used with object type).
-   Introduced in the older versions of .NET but replaced by List<T> in newer versions.
#### 🧩 Example
```csharp
ArrayList arrayList = new ArrayList();
arrayList.Add(1);
arrayList.Add("Hello");
arrayList.Add(true);
Console.WriteLine(arrayList[0]); // Output: 1
Console.WriteLine(arrayList[1]); // Output: Hello
```
#### Boxing vs Unboxing
**Boxing** : Converting a value type to a reference type (object or interface). Stored in the heap.
```csharp
int x = 10;
object obj = x; // boxing
```
**Unboxing**: Extracting the value type from an object.
```csharp
int y = (int)obj; // unboxing
```
⚠️ Unboxing requires explicit cast and is costly in performance.
#### Equals() vs == 
**==**: Operator. Default for reference types compares **reference equality** (except for string, where it checks value).</br>
**Equals()** : Virtual method. Can be overridden for **value equality** (e.g., struct, string, custom classes).
### Generics
Provide **type safety** without boxing/unboxing.</br>
Common pitfalls:
-   Overuse leads to complexity.
-   Value type constraints → boxing if not handled properly.
-   Can’t use `null` with value type generics without `Nullable<T>`.
#### Records
Introduced in C# 9.</br>
**Immutable reference types** with value-based equality.
#### record vs class:
-   Class → reference equality by default.
-   Record → value equality (compares properties).</br>

Good for DTOs and immutable data models.
#### Task vs Thread vs ThreadPool
-   **Thread** → OS-level thread, heavy.
-   **ThreadPool** → Managed pool of reused threads.
-   **Task** → Higher-level abstraction on ThreadPool with cancellation, continuations, async support.
#### foreach vs Parallel.ForEach
-   **foreach** → Sequential iteration.
-   **Parallel.ForEach** → Splits work across threads, good for CPU-bound tasks. Avoid if tasks are I/O bound.
#### What is the Default Access Modifier of Class in C#?
**Answer:**</br>
Top-level class / abstract class → **internal** by default.</br>
Nested class → **private** by default.
1.  For a top-level class (including abstract class):
    -   The default access modifier is internal.
    -   Meaning: accessible only within the same assembly/project.
    #### 🧩 Example    
    ```csharp
    abstract class MyAbstractClass { }  // 👈 internal by default
    class MyClass { }                   // 👈 internal by default
    ```
    Equivalent to
    ```csharp
    internal abstract class MyAbstractClass { }
    internal class MyClass { }
    ```
2.  For a nested class (inside another class):
    -   The default access modifier is private.
    -   Meaning: only accessible inside the containing class.
    ```csharp
    class Outer
    {
        class Inner { }  // 👈 private by default
    }
    ```
    Equivalent to
    ```csharp
    class Outer
    {
        private class Inner { }
    }
    ```
#### How do you ensure clean, efficient, and maintainable code?
**Answer:**
"I follow coding best practices, such as writing clear and concise code, adhering to namingconventions, and keeping functions and classes small and focused on a single responsibility. I also perform code reviews and use static code analysis tools to detect potential issues. Proper documentation and writing unit tests also help in maintaining code quality."
#### What is your approach to mentoring junior developers?
**Answer:**
"I believe in providing guidance through code reviews, pair programming, and constructive feedback. I also help junior developers understand the bigger picture by explaining why certain decisions are made. I encourage them to ask questions and learn continuously by solving realworld problems and focusing on best practices."
#### How do you manage working with offshore teams, especially when collaborating with teams in different time zones?
**Answer:**
"I ensure effective communication by scheduling regular meetings that accommodate different time zones, such as daily standups or weekly reviews. I use collaboration tools like Slack and Microsoft Teams for asynchronous communication and track progress on JIRA. I focus on clear documentation to ensure everyone understands the project’s requirements, regardless of time zone differences."
#### Can you explain event-driven architecture and its benefits?
**Answer:**
"Event-driven architecture is a design pattern where components of a system communicate by emitting and handling events. This decouples the components, allowing them to operate independently. I have used this pattern in applications with asynchronous processing needs, such as updating databases or sending notifications when certain actions occur. It provides scalability and improves the responsiveness of applications."
#### What are the key features of the older versions of C#?
**Answer:**
-   C# 1.0 → Classes, structs, enums, events, delegates.
-   C# 2.0 → Generics, nullable types, iterators (yield).
-   C# 3.0 → LINQ, lambda expressions, anonymous types.
-   C# 4.0 → Dynamic binding (dynamic keyword), named/optional parameters.
-   C# 5.0 → async/await.
-   C# 6.0 → String interpolation, expression-bodied members.
#### What are the new features introduced in the latest version of C# (C# 12 as of 2023)?
**Answer:**
-   Primary constructors in classes.
-   Collection expressions ([1, 2, 3] syntax).
-   Alias any type (not just namespaces).
-   Interceptors for source generators.
-   Default values in lambda expressions.
#### How does the latest version of C# differ from older versions?
**Answer:**
-   Modern versions focus on developer productivity (less boilerplate).
-   More functional-style constructs (pattern matching, records).
-   Better performance and memory safety (Span, ref struct).
-   More interop with cloud, microservices, AI tools
#### What are the limitations of C# programs?
**Answer:**
-   Platform dependency reduced but still tied to .NET runtime.
-   Slower than low-level languages like C/C++.
-   Garbage collection overhead.
-   Not ideal for real-time systems.
-   Heavier runtime size for very small/embedded apps.
#### What are some of the new trends in C#? Why are newer versions considered better?
**Answer:**
-   **Trends**: Cloud-native apps, microservices, AI/ML integration, Blazor (web apps in C#), MAUI (cross-platform apps).
-   **Why better**: Cleaner syntax, higher performance, better tooling, async improvements.
#### What are the limitations or downsides of OOPs?
**Answer:**
-   Can lead to over-engineering.
-   Increased complexity with inheritance.
-   Performance overhead due to abstraction.
-   Not all problems fit into OOP (e.g., data processing pipelines → functional programming works better).
#### Does OOP solve all programming problems? Why or why not?
**Answer:**
-   No. Some problems are better solved with functional, procedural, or declarative approaches (SQL, ML pipelines).
-   Example: Recursive problems or mathematical computations → functional style is often simpler.
#### Which design patterns have you used in your projects, and how did you apply them?
**Answer:**
-   **Repository Pattern** → abstract DB calls in EF Core.
-   **Factory Pattern** → create objects without exposing creation logic.
-   **Singleton Pattern** → for shared services like logging, caching.
-   **Observer Pattern** → event-driven messaging (like Pub/Sub).
#### What is the difference between good code and bad code?
**Answer:**
-   **Good code:** Readable, maintainable, testable, follows SOLID, low coupling, high cohesion.
-   **Bad code:** Hard to read, tightly coupled, no tests, duplicate logic, poor naming.
#### What are extension methods in C# and how are they used?
**Answer:**
-   Extension methods are static methods that allow you to add new methods to existing types without modifying their source code.
-   They are defined as static methods in a static class and use the this keyword as the first parameter to specify the type they extend.
#### 🧩 Example
```csharp
public static class StringExtensions
{
    public static bool IsPalindrome(this string str)
    {
        int i = 0;
        int j = str.Length - 1;
        while (i < j)
        {
            if (str[i] != str[j]) return false;
            i++;
            j--;
        }
        return true;
    }
}
// Usage
string s = "radar";
bool result = s.IsPalindrome(); // true
```
#### Explain the concept of routing in ASP.NET Core.
**Answer:**
-   Routing is the process of mapping HTTP requests to corresponding controller actions. It is configured in the Startup class within the Configure method using `app.UseRouting()` and `app.UseEndpoints()`.

-   Routes can be defined using attributes on controllers/actions or through convention-based routing.</br>
#### Routing & Attribute Routes
-   Routing → Maps incoming requests to endpoints.</br>

**Two types:**
-   Convention-based (defined in MapControllerRoute).
-   Attribute routing (applied directly on controller/action).
#### 🧩 Example
```csharp
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    [HttpGet("{id}")]
    public IActionResult Get(int id) => Ok();
}
```
#### 🧩 Example
```csharp
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        // Code to return all products
    }

    [HttpGet("{id}")]
    public IActionResult GetById(int id)
    {
        // Code to return a product by id
    }
}
```
#### What is params?
**Answer:**
`params` allows you to pass a **variable number of arguments** to a method.
You don’t need to explicitly create an array.
It must be the **last parameter** in the method signature.
You can pass **zero, one, or many arguments**.
#### 🧩 Example 1: Without params
```csharp
void PrintNumbers(int[] numbers)
{
    foreach (var n in numbers)
        Console.WriteLine(n);
}
PrintNumbers(new int[] { 1, 2, 3 }); // Need to create array
```
#### 🧩 Example 2: With params
```csharp
void PrintNumbers(params int[] numbers)
{
    foreach (var n in numbers)
        Console.WriteLine(n);
}

PrintNumbers(1, 2, 3, 4, 5);  // Cleaner
PrintNumbers();               // Works, empty array
```
#### 🔑 Rules
-   Only one params parameter per method.
-   It must be the last parameter.
-   You can still pass an explicit array.
#### What is yield?
**Answer:**
-   The `yield` keyword is used in iterators to provide values to the caller one at a time, without creating and storing a full collection in memory.
-   Instead of returning all results at once (like an array or list), `yield` lets you `defer execution` and return values lazily when they’re needed.
-   It is used with:
    -   `yield return` → returns each element one by one.
    -   `yield break` → stops the iteration.
#### 🧩 Example: Simple Iterator with `yield return`
```csharp
IEnumerable<int> GetNumbers()
{
    yield return 1;
    yield return 2;
    yield return 3;
    // Automatically pauses after each return until next is requested
}

foreach (var num in GetNumbers())
{
    Console.WriteLine(num);
}
```
Output
```csharp
1
2
3
```
#### 🧩 Example: Using `yield break`
```csharp
IEnumerable<int> GetNumbers(int limit)
{
    for (int i = 1; i <= limit; i++)
    {
        if (i > 5)
            yield break; // stop iteration early

        yield return i;
    }
}

foreach (var n in GetNumbers(10))
{
    Console.WriteLine(n);
}
```
Output
```csharp
1
2
3
4
5
```
#### 🔑 Why use yield?

-   **Lazy evaluation** → Values are generated only when requested.
-   **Memory efficient** → No need to store entire collection in memory.
-   **Cleaner code** → No need to create temporary lists/arrays.
-   **Infinite sequences** → Can generate endless streams safely.

| Feature            | `==` Operator                                                | `Equals()` Method                     |
| ------------------ | ------------------------------------------------------------ | ------------------------------------- |
| Default behavior   | Value compare for value types, reference compare for objects | Reference compare (unless overridden) |
| Can be overridden? | Yes (operator overloading)                                   | Yes (override from `Object`)          |
| Works on           | Both value & reference types                                 | Both value & reference types          |
| Example            | `a == b`                                                     | `a.Equals(b)`                         |
#### What is unsafe?
**Answer:**
In C#, `unsafe` is a **keyword** that allows you to write code that bypasses the CLR’s (Common Language Runtime) safety checks.   
-   Normally, C# is a **safe language** → you don’t deal directly with memory addresses.    
-   With unsafe, you can use **pointers** like in C or C++.
-   It’s useful for **performance-critical code**, interop with unmanaged code, or working with memory directly.
#### Explain sql injection and how to save our application?
**Answer:**
SQL Injection (SQLi) is an attack where an attacker manipulates input to inject malicious SQL that the application then executes on the database. This can lead to data theft, data modification, privilege escalation, or full system compromise.
#### 🧩 Example of vulnerable code:
```csharp
// Vulnerable — DO NOT DO THIS
string sql = "SELECT * FROM Users WHERE Username = '" + username + "' AND Password = '" + password + "'";
var cmd = new SqlCommand(sql, conn);
```
If `username = admin' --` the attacker can bypass authentication or alter the query.</br>
#### Core Principle to Prevent SQLi
Never build SQL by concatenating untrusted input. Always use parameterized queries / prepared statements (or safe ORM abstractions) so input is treated as data — not executable SQL.
Prevent SQL injection first and foremost by using parameterized queries/prepared statements (or safe ORM LINQ), avoid concatenating SQL with user input, minimize DB privileges, validate inputs, and add monitoring/WAF for defense-in-depth.