## Exception Handling
In .NET, exceptions are handled using try-catch blocks. It’s essential to catch specific exceptions (e.g., `SqlException`, `IOException`) rather than a general Exception to handle different error scenarios properly. You should also use the finally block to clean up resources. It's good practice to log exceptions and, when necessary, rethrow them for higher-level handlers.
### 1. try Block:
-   The `try` block is where you write the code that might throw an exception.
-   If an exception occurs within the try block, the control is transferred to the corresponding catch block, if it exists.
### 2. catch Block:
-   The `catch` block catches the exception thrown by the try block. It allows you to handle the exception in a controlled manner.
-   Multiple catch blocks can be used to catch different types of exceptions.
### 3. finally Block:
-    The `finally` block is always executed, regardless of whether an exception is thrown or not.
-   It is typically used for cleanup operations, such as releasing resources, closing file streams, or database connections.
### Exception Handling in C# – Key Points:
-   **try**: Used to wrap the code that may cause exceptions.
-   **catch**: Catches and handles the exception. It can be used to handle specific exceptions or general ones.
-   **finally**: Executes regardless of whether an exception was thrown, useful for cleanup (e.g., closing files or releasing resources).
#### Dependency Injection and Exception Handling in .NET Core:
-   .NET Core uses dependency injection by default, and exception handling can be extended or customized using middleware in ASP.NET Core applications.
-   For instance, in ASP.NET Core, you can use custom middleware to handle exceptions globally and return a standardized response to the client.
#### Exception Handling with when Clause (Exception Filter):
.NET Core introduced the **exception filter** feature, which allows you to handle exceptions based on certain conditions using the `when` keyword. This feature is not available in .NET Framework.
#### 🧩 Example
The catch block with the when clause only catches IndexOutOfRangeException if the exception message contains the word "bounds."
```csharp
try
{
    int[] numbers = { 1, 2, 3 };
    Console.WriteLine(numbers[5]); // Throws IndexOutOfRangeException
}
catch (IndexOutOfRangeException ex) when (ex.Message.Contains("bounds"))
{
    Console.WriteLine("Caught an index out of bounds exception.");
}
catch (Exception ex)
{
    Console.WriteLine($"General error: {ex.Message}");
}
```
### Global Exception Handling in ASP.NET Core:
In ASP.NET Core, exception handling can be managed globally through **middleware**. This allows for centralized exception handling, which is particularly useful for logging, custom error responses, and ensuring that the application doesn't crash due to unhandled exceptions.
#### Creating Custom Middleware for Global Exception Handling:
You can create custom middleware to handle exceptions globally. This is especially useful in ASP.NET Core applications to catch all exceptions and return custom error messages or log them.
#### 🧩 Example
-   The ErrorHandlingMiddleware catches all exceptions thrown during the HTTP request pipeline.
-   The catch block returns a 500 HTTP status code and a JSON error response with the exception message.
-   You would then register this middleware in your `Configure` method in `Startup.cs`.
```csharp
public class ErrorHandlingMiddleware
{
    private readonly RequestDelegate _next;
    public ErrorHandlingMiddleware(RequestDelegate next)
    {
        _next = next;
    }
    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            // Log the exception or do any custom processing
            context.Response.StatusCode = 500;
            context.Response.ContentType = "application/json";
            var result = JsonConvert.SerializeObject(new { error = ex.Message });
            await context.Response.WriteAsync(result);
        }
    }
}
// In Startup.cs
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseMiddleware<ErrorHandlingMiddleware>();
    app.UseMvc();
}
```
#### Using Built-In Exception Handling Middleware:
ASP.NET Core provides built-in exception handling middleware (`UseExceptionHandler`) for handling errors globally. This is more common in production environments to ensure a standardized error response.
#### Example
-   `UseDeveloperExceptionPage` provides detailed exception information during development.
-   `UseExceptionHandler` provides a more user-friendly error page or redirection in productio
```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage(); // Shows detailed exception page in dev mode
    }
    else
    {
        app.UseExceptionHandler("/Home/Error"); // Redirects to error page in prod mode
        app.UseHsts();
    }
    app.UseHttpsRedirection();
    app.UseMvc();
}
```
##  throw vs throw ex
### throw ex:
When you use throw ex in a catch block, you are explicitly r**ethrowing the exception object (ex)** that was caught. However, doing this will **reset the stack trace** of the exception, which can lead to losing valuable debugging information.
-   Issue with `throw ex`: When you rethrow the exception using throw ex, the original stack trace of the exception is lost, and it appears as if the exception was thrown from the point where you used throw ex. This can make debugging difficult, as it doesn’t provide the actual place where the exception originated.
### throw (without ex):
Using just `throw` without specifying the exception object rethrows the original exception without resetting its stack trace. This is the preferred approach for rethrowing exceptions because it preserves the original exception's stack trace, making it easier to trace the root cause.
-   Benefit of throw: When you rethrow the exception using throw alone, the original stack trace is preserved, which helps maintain accurate information about where the exception was thrown and provides better debugging and logging capabilities.

| 🔹 **Feature** | **throw ex** | **throw** |
|----------------|----------------|----------------|
| Stack Trace | Resets the stack trace, so the exception appears to be thrown from the point of `throw ex`. | Preserves the original stack trace, showing where the exception was first thrown. |
| Usage | Typically used when you need to modify the exception or add additional logic before rethrowing it. | Used when you want to preserve the exception as is and pass it along the call stack. |
| Best Practice | Not recommended because it loses valuable stack trace information. | Recommended because it maintains the original stack trace and helps with debugging. |
### When to Use Each:
-   Use `throw` when you need to rethrow the exception without altering its stack trace. This is the most common and preferred way to rethrow exceptions because it retains the original context.
-   Use `throw ex` only if you need to modify the exception (for example, adding extra information) or want to handle it in a different way. But be mindful that it will reset the stack trace, which can lead to less meaningful error logs.
### Error Handling in ASP.NET Core
Options:
-   **DeveloperExceptionPage** → Shows detailed errors (for dev).
-   **UseExceptionHandler** → Centralized error page in production.
-   **UseStatusCodePages** → For handling HTTP status codes (404, 500).
-   **Try-catch in Middleware** → Custom handling/logging.
-   **Filters (for MVC)** → `ExceptionFilterAttribute` for controller errors.
#### 🧩 Example
```csharp
app.UseExceptionHandler("/Home/Error"); // Global handle
```
