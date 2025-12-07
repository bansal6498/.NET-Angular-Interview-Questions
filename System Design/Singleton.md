#### How do you implement Singleton in C# safely?
**Answer:**
```csharp
public sealed class Logger {
    private static readonly Logger _instance = new Logger();
    private Logger() { }
    public static Logger Instance => _instance;
}

```