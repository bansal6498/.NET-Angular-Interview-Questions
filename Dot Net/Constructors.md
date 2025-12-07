## Constructors
A class in C# can have multiple constructors. This is called **constructor overloading**. It allows you to define multiple constructors with different sets of parameters in the same class, enabling flexibility when creating objects of the class.
#### 🧩 Example
```csharp
using System;
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    // Default constructor
    public Person()
    {
        Name = "Unknown";
        Age = 0;
    }
    // Parameterized constructor
    public Person(string name)
    {
        Name = name;
        Age = 0;
    }
    // Parameterized constructor with multiple parameters
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Age: {Age}");
    }
}
class Program
{
    static void Main()
    {
        // Using default constructor
        Person person1 = new Person();
        person1.DisplayInfo();
        // Using constructor with one parameter
        Person person2 = new Person("Alice");
        person2.DisplayInfo();
        // Using constructor with two parameters
        Person person3 = new Person("Bob", 25);
        person3.DisplayInfo();
    }
}
```
#### 🧩 Output
```csharp
Name: Unknown, Age: 0
Name: Alice, Age: 0
Name: Bob, Age: 25
```
**Key Points**
1.  **Constructor Signature:** Each constructor must have a unique parameter list.
2.  **Constructor Chaining:** You can call one constructor from another using the : `this` keyword.
#### 🧩 Example
```csharp
public Person(string name) : this(name, 0) { }
```
3.  **Use Case:** Constructor overloading is useful when you want to provide multiple ways to initialize a class, with different levels of detail or default values.
#### 🟥 🟥 Suppose abstract class have constructor and base also have. Then what will be the sequence of constructor execution?
**Answer:**
In C#, the rule is:</br>
👉 Base class constructor runs first, then derived class constructor.
This applies even if the base is an abstract class.

✅ Sequence:
-   Top-most base class constructor
-   Abstract (intermediate) class constructor(s)
-   Derived (concrete) class constructor

This ensures all parent-level initialization is done before the child class starts.

🔑 Key Rules
-   Constructors are always called from top (base) to bottom (derived).
-   If you don’t explicitly call base(...), the compiler tries to call the base **default constructor**.
    -   If the base has **no default constructor**, you **must** call base(...).
-   Abstract class constructors participate in this chain just like normal base classes.

⚡ Quick Summary:
-   Sequence = Base → Abstract → Derived.
-   Parameterized constructors: You control what goes to base using : base(...).
-   If you forget and no default exists → compilation error.