## Encapsulation
Encapsulation is the concept of bundling the data (variables) and methods (functions) that operate on the data into a single unit, or class, and restricting direct access to some of the object's components. This is usually done by making  the fields private and providing public getter and setter methods to access or modify them.
### Key Points
-   Encapsulation helps protect an object's internal state and ensures that it can only be modified through well-defined methods.
-   This allows for better control over the data and helps enforce business rules or validation.
#### 🧩 Example
the name field is private, but it is accessed and modified through the Name property with validation logic.
```csharp
public class Person
{
    private string name; // private field
    // Public property for accessing and modifying the private field
    public string Name
    {
        get { return name; }
        set
        {
            if (!string.IsNullOrEmpty(value)) // Validation
            name = value;
            else
            Console.WriteLine("Name cannot be empty.");
        }
    }
}
class Program
{
    static void Main()
    {
        Person person = new Person();
        person.Name = "John"; // Setter sets the name
        Console.WriteLine(person.Name); // Getter retrieves the name
    }
}
```
#### What is the difference between a property and a field in C#?
**Answer:**
A field is a variable defined directly within a class or struct. A property is a member that provides a way to access the value of a field, but it can include logic for validation or transformation of the value. Properties are accessed like fields but can encapsulate logic via getters and setters.
#### Difference between Abstraction vs Encapsulation
**Answer:**
-   **Abstraction**: Hides implementation details.
-   **Encapsulation**: Hides data using access modifiers (private, public, etc.).
#### Can you explain the different Access Specifiers in .NET and why they matter?
**Answer:**
Access specifiers (modifiers) define the scope/visibility of classes, methods, and members.
-   **public** → Accessible anywhere.
-   **private** → Accessible only inside the class.
-   **protected** → Accessible in the class + derived classes.
-   **internal** → Accessible only within the same assembly.
-   **protected internal** → Accessible in the same assembly + derived classes (even in other assemblies).
-   **private protected** → Accessible only in the same assembly AND only in derived classes.</br>

**✅ Why they matter** → They enforce **encapsulation**, protect sensitive code, and define API boundaries.
