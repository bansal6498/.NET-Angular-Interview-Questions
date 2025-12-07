🟥 **High Priority**
<br>
## SOLID Principles
**SOLID** is an acronym for five design principles that help create more maintainable and scalable software:
-   **S: Single Responsibility Principle (SRP)** – A class should have only one reason to change, meaning it should only have one job.
-   **O: Open/Closed Principle (OCP)** – Software entities (classes, modules, functions) should be open for extension but closed for modification.
-   **L: Liskov Substitution Principle (LSP)** – Subtypes must be substitutable for their base types without altering the correctness of the program.
-   **I: Interface Segregation Principle (ISP)** – A client should not be forced to depend on interfaces it does not use.
-   **D: Dependency Inversion Principle (DIP)** – High-level modules should not depend on lowlevel modules; both should depend on abstractions.
#### 🧩 Example

Correct implementation LSP

```csharp
public abstract class Bird
{
    public abstract void Fly();
}
public class Sparrow : Bird
{
    public override void Fly()
    {
        Console.WriteLine("Sparrow is flying");
    }
}
```
Violation of LSP
```csharp
public abstract class Bird
{
    public abstract void Fly();
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotImplementedException("Penguins can't fly!");
    }
}
```
-   Problem: A Penguin is a Bird, but it cannot fly.
If code expects all birds to fly, replacing Bird with Penguin breaks functionality.
❌ This violates LSP.

**🔑 Interview-Ready Answer**

“The **Liskov Substitution Principle** states that a derived class should be substitutable for its base class without breaking functionality. In other words, if class B inherits from class A, then B should be usable anywhere A is expected. A common violation example is having a Bird base class with a Fly method, and then creating a Penguin subclass that throws an exception because penguins cannot fly. This breaks LSP. The correct approach is to restructure the hierarchy, for example, by splitting Bird into FlyingBird and NonFlyingBird. This ensures subclasses honor the behavior expected by the base class.”