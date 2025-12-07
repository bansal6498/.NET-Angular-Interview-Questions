## Question
#### 🟥 If a class have only private constructor then can we create object of it and can we inherit?
**Answer:**
1.  You cannot create an object of it outside the class because the constructor is not accessible.
    #### 🧩 Example
    ```csharp
    public class MyClass
    {
        private MyClass() { }

        public static void SayHello()
        {
            Console.WriteLine("Hello");
        }
    }
    // Outside
    // var obj = new MyClass(); // ❌ Compile error
    MyClass.SayHello(); // ✅ Works because static methods are accessible

    ```
    👉 Such classes are often used in Singleton pattern or static utility classes.
2.  Can it be inherited?
-   No, a class with only a private constructor cannot be inherited because:
    -   For inheritance, the derived class must call a constructor of the base class.
    -   But if the only constructor is private, it is not accessible to the derived class.
    #### 🧩 Example
    ```csharp
    public class BaseClass
    {
        private BaseClass() { }
    }

    public class Derived : BaseClass
    {
        // ❌ Error: BaseClass does not contain a constructor that is accessible
    }
    ```
    
#### Give me an simple code example to implement OOPS concept in C#
**Answer:**
```csharp
using System;

// 🔹 Abstraction (abstract class hides implementation details)
public abstract class Vehicle
{
    // 🔹 Encapsulation (private field with public property)
    private string _brand;

    public string Brand
    {
        get { return _brand; }
        set { _brand = value; }
    }

    // Abstract method (must be implemented by subclasses)
    public abstract void Start();

    // Virtual method (can be overridden)
    public virtual void DisplayInfo()
    {
        Console.WriteLine($"This is a vehicle of brand: {Brand}");
    }
}

// 🔹 Inheritance (Car inherits from Vehicle)
public class Car : Vehicle
{
    public int Wheels { get; set; }

    public Car(string brand, int wheels)
    {
        Brand = brand;
        Wheels = wheels;
    }

    // Implementation of abstract method
    public override void Start()
    {
        Console.WriteLine($"{Brand} car is starting with {Wheels} wheels!");
    }

    // 🔹 Polymorphism (method overriding)
    public override void DisplayInfo()
    {
        Console.WriteLine($"Car Brand: {Brand}, Wheels: {Wheels}");
    }
}

public class Program
{
    public static void Main()
    {
        // 🔹 Polymorphism (base reference, derived object)
        Vehicle myCar = new Car("Toyota", 4);

        myCar.Start();       // Calls overridden method in Car
        myCar.DisplayInfo(); // Calls overridden method in Car
    }
}

```
🔹 Explanation
-   Encapsulation → _brand is private, accessed via Brand property.
-   Inheritance → Car inherits from Vehicle.
-   Polymorphism → DisplayInfo() is overridden, and Vehicle myCar = new Car() uses base reference but executes child class method.
-   Abstraction → Vehicle is an abstract class, can’t be instantiated, only extended.
</br>

Output
```csharp
Toyota car is starting with 4 wheels!
Car Brand: Toyota, Wheels: 4
```