## 🟥 Abstract Class
An abstract class is a class that cannot be instantiated directly. It can contain both abstract (unimplemented) methods and concrete (implemented) methods. Abstract classes are useful when you want to share code between several related classes, but still enforce that certain methods are implemented by the subclasses.
### Characteristics of Abstract Class:
1. Can have both abstract and concrete methods:
    -   An abstract method is a method without implementation, while a concrete method can have an implementation.
    #### 🧩 Example
    ```csharp
    public abstract class Animal
    {
    public abstract void MakeSound(); // Abstract method (no implementation)
    public void Eat() // Concrete method (implementation provided)
    {
    Console.WriteLine("Eating...");
    }
    }
    ```
2.  Can have **fields, constructors, and static** members:
    -   Abstract classes can contain **fields, constructors, and static members**, which cannot be declared in an interface.
3.  Can inherit from another class:
    -   An abstract class can inherit from another class and can implement interfaces.
4.  Access modifiers:
    -   Abstract classes can have different access modifiers for methods, properties, and fields (e.g., public, protected).
5.  Can have state:
    -   Abstract classes can maintain state in fields (instance variables).
### Use Case for Abstract Class:
-   When you want to inherit some common implementation across derived classes and share code.
-   When you want to provide default behavior for some methods but leave others to be implemented by derived classes.
-   When you want to define a common base class for a family of related objects, especially if you plan to share some implementation across all subclasses.
<br>

#### Can an abstract class have constructor?
**Answer:**
Yes ✅ an abstract class can have a constructor in C#.
Here’s the explanation:
-   You **cannot directly instantiate** an abstract class.
-   But an abstract class **can define a constructor**, and that constructor is called when **a derived (concrete) class** is instantiated.
-   This is useful if you want to initialize **common fields or logic** for all derived classes.</br>
#### 🧩 Example
```csharp
abstract class Animal
{
    protected string Name;

    // Constructor in abstract class
    public Animal(string name)
    {
        Name = name;
        Console.WriteLine("Abstract class constructor called");
    }
}
class Dog : Animal
{
    public Dog(string name) : base(name)
    {
        Console.WriteLine($"Dog created with name: {name}");
    }
}
class Program
{
    static void Main()
    {
        Dog d = new Dog("Tommy");
    }
}
```
Output
```csharp
Abstract class constructor called
Dog created with name: Tommy
```
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
## 🟥 Interfaces
An interface defines a contract, meaning it only defines method signatures and properties but no implementation. Any class that implements an interface must provide an implementation for all of its methods.
<br>An interface in C# is a contract that defines a set of methods, properties, events, or indexers without providing implementations. A class or struct that implements the interface must provide the implementation for its members.
#### 🧩 Example

Syntax

```csharp
public interface IMyInterface
{
 // Methods
 void Method1();
 int Method2(string param);
 // Properties
 string Property1 { get; set; }
 // Events
 event EventHandler MyEvent;
 // Indexers
 string this[int index] { get; set; }
}
```
### Characteristics of Interface:
1.  Contains only method signatures (no implementation):
    -   Interfaces cannot provide method implementations, only method declarations.
#### 🧩 Example
```csharp
public interface IAnimal
{
 void MakeSound(); // Method declaration, no implementation
}
```
2.  Cannot contain fields or constructors:
    -   Interfaces cannot have fields, constructors, or static members.
3.  A class can implement multiple interfaces:
    -   In C#, a class can implement multiple interfaces, which is not possible with abstract classes (a class can inherit only one abstract class).
4.  Implicitly public members:
    -   All members of an interface are implicitly public, and they cannot have any access modifiers.
5.  No state:
    -   Interfaces cannot maintain any state (i.e., no instance fields).
#### 🧩 Steps to implement Interface:

1.  Defining the Interface:

```csharp
public interface IVehicle
{
    void StartEngine();
    void StopEngine();
    int GetNumberOfWheels();
}
```
#### 🧩 Example

2. Implementing an Interface in a Class:

```csharp
public class Car : IVehicle
{
    public void StartEngine()
    {
        Console.WriteLine("Car engine started.");
    }
    public void StopEngine()
    {
        Console.WriteLine("Car engine stopped.");
    }
    public int GetNumberOfWheels()
    {
        return 4;
    }
}
```
#### 🧩 Example

3.  Using the Interface:
```csharp
public class Program
{
    public static void Main()
    {
        IVehicle myCar = new Car();
        myCar.StartEngine();
        Console.WriteLine($"Number of wheels: {myCar.GetNumberOfWheels()}");
        myCar.StopEngine();
    }
}
```
#### 🧩 Example

Example with Multiple Interfaces:

```csharp
public interface IFlyable
{
    void Fly();
}
public interface ISwimmable
{
    void Swim();
}
public class Duck : IFlyable, ISwimmable
{
    public void Fly()
    {
        Console.WriteLine("Duck is flying.");
    }
    public void Swim()
    {
        Console.WriteLine("Duck is swimming.");
    }
}
```
### Use case for Interface:
-   When you want to define a contract that multiple unrelated classes can implement.
-   When you want to define functionality that can be shared across different classes without enforcing a particular class hierarchy.
-   When you want to allow a class to implement multiple sets of behaviors, as a class can implement multiple interfaces.
### Abstract Class vs Interface
An interface defines a contract that classes can implement. It can contain method declarations, properties, events, and indexers but no implementation. A class can implement multiple interfaces, promoting loose coupling and flexibility.
An abstract class can have both defined methods and abstract methods (without implementation), and a class can inherit only one abstract class due to C#’s single inheritance model.
-   A class can implement multiple interfaces, but it can inherit only one abstract class.
-   Abstract classes can have fields and constructors, while interfaces cannot.
-   Abstract classes can provide implementation, while interfaces cannot (in versions prior to C# 8.0, where default implementations were introduced).<br>

In C#, both abstract classes and interfaces are used to define methods or properties that must
be implemented by derived classes. However, they serve different purposes and have different
characteristics.

|Feature | Abstract Class | Interface|
|---------|---------------|-----------|
|**Implementation**| Can have both abstract and concrete methods. | Can only have method signatures, no implementation. |
|**State**| Can have fields and instance variables. | Cannot have fields or state.|
|**Constructors**| Can have constructors. | Cannot have constructors. |
|**Inhertance**| Can inherit from only one class (abstract or not). | A class can implement multiple interfaces. |
|**Access Modifiers**| Can have access modifiers (e.g., `public, private`).| All members are implicitly public and cannot have access modifiers. |
|**Multiple Inhertance**| A class can inherit only one abstract class. | A class can implement multiple interfaces. |
|**Default Implementations**| Can provide default implementation for some methods. | Cannot provide any implementation (before C# 8.0) |

### When to use which?
1.  Use an Abstract Class when:
    -   You have common functionality (shared code) that you want to provide in the base class.
    -   You want to inherit from a base class with some default implementation.
    -   You want to maintain state (instance variables).
    -   You want to limit inheritance (a class can inherit only one abstract class).
2.  Use an Interface when:
    -   You want to define a contract that multiple classes can implement, regardless of their class hierarchy.
    -   You need to implement multiple behaviors (as a class can implement multiple interfaces).
    -   You don’t need any common implementation, only method signatures and property declarations.
    -   You want to ensure flexibility by decoupling the implementation from the interface.
### Example of Abstract Class vs Interface:
#### 🧩 Example

Abstract Class Example:

```csharp
public abstract class Shape
{
    public abstract void Draw(); // Abstract method
    public void Move() // Concrete method
    {
        Console.WriteLine("Moving shape");
    }
}
public class Circle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing Circle");
    }
}
```
#### 🧩 Example

Interface Example

```csharp
public interface IDrawable
{
    void Draw(); // Method signature
}
public class Circle : IDrawable
{
    public void Draw()
    {
        Console.WriteLine("Drawing Circle");
    }
}
```
### Conclusion
-   Use an Abstract Class when you need to provide a default implementation for shared functionality across related classes and manage common state.
-   Use an Interface when you want to define a contract for classes that may not share a common hierarchy but need to implement the same behavior. It’s also helpful when you need multiple types of behavior that a class can implement.
### Abstract vs Static Class
| Feature       | Abstract Class                              | Static Class             |
| ------------- | ------------------------------------------- | ------------------------ |
| Instantiation | ❌ Cannot be instantiated directly           | ❌ Cannot be instantiated |
| Inheritance   | ✅ Can be inherited                          | ❌ Cannot be inherited    |
| Members       | Abstract + non-abstract (instance + static) | Only static              |
| Polymorphism  | ✅ Supports (via overriding/virtual)         | ❌ Not supported          |
| Use Case      | Base class to enforce contracts             | Utility/helper functions |
