## Middleware 
Middleware in .NET (specifically ASP.NET Core) refers to software components that are assembled into a pipeline to handle HTTP requests and responses. Each middleware component in the pipeline has the ability to perform operations on an incoming request or an outgoing response. They are typically used to add functionality like logging, authentication, authorization, request handling, error handling, and more to the web application.
### Key Concepts of Middleware:
1.  Request Handling: Middleware can process incoming HTTP requests before passing them on to the next middleware in the pipeline or handling the request by itself.
2.  Response Handling: Middleware can also modify the outgoing HTTP response before it is sent back to the client.
3.  Pipeline Sequence: The order in which middleware is configured in the application is crucial because it determines the order in which they are executed.
### How Middleware Works:
-   Middleware components are executed sequentially, based on their order in the Configure method in Startup.cs (or in the Program.cs for .NET 6 and later).
-   Each middleware has access to the request context (which contains request data) and response context (which holds the data to be sent back to the client).
### Middleware can choose to:
-   Pass control to the next middleware in the pipeline.
-   Handle the request or response and end the request processing.
-   Modify the request or response before passing it along.   
### 🧩 Example

Middleware Example (Syntax)

```csharp
using Microsoft.AspNetCore.Http;
using System.Threading.Tasks;
using System.Diagnostics;

public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;

    public RequestLoggingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        var stopwatch = Stopwatch.StartNew();

        // Log before request processing
        Console.WriteLine($"➡️ Incoming request: {context.Request.Method} {context.Request.Path}");

        // Call the next middleware in the pipeline
        await _next(context);

        stopwatch.Stop();

        // Log after response
        Console.WriteLine($"⬅️ Response status: {context.Response.StatusCode}, Time taken: {stopwatch.ElapsedMilliseconds} ms");
    }
}
```

To add this middleware to the pipeline, you would configure it in Startup.cs (or Program.cs for .NET 6 and later):

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

// 🔹 Register custom middleware
app.UseRequestLogging();

app.MapGet("/", () => "Hello Middleware!");
app.Run();
```
### Types of Common Middleware
1.  Authentication Middleware: Handles user authentication, verifying credentials, and creating user sessions.
2.  Authorization Middleware: Ensures that the authenticated user has permission to access the requested resource.
3.  Static Files Middleware: Serves static content (e.g., images, JavaScript files, CSS files) to the client.
4.  Routing Middleware: Determines which route to execute based on the incoming request.
5.  Exception Handling Middleware: Catches unhandled exceptions and returns error responses (e.g., 500 Internal Server Error).
6.  CORS Middleware: Manages Cross-Origin Resource Sharing (CORS) to control which domains can access the resources.
### Benefits of Middleware
-   Separation of Concerns: Each middleware handles a specific concern (e.g., authentication, logging, error handling), promoting cleaner and more maintainable code.
-   Customizability: You can write your own custom middleware for application-specific logic.
-   Flexibility: The middleware pipeline is highly configurable, allowing for conditional execution of middleware based on the request context.

#### For custom middleware the method name is always InvokeAsync as mentioned in earlier example also.
#### Explain Custom Middleware.
**Answer:**
```csharp
public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;
    public RequestLoggingMiddleware(RequestDelegate next) => _next = next;

    public async Task Invoke(HttpContext context)
    {
        Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");
        await _next(context); // pass to next middleware
    }
}

// Register in Program.cs
app.UseMiddleware<RequestLoggingMiddleware>();
```
#### What is short circuiting of middle ware ?
**Answer:**
**Short-circuiting** means a middleware decides **not to call the next middleware** and instead **ends the pipeline early** by directly generating a response.
👉 In other words, it **breaks the chain** and prevents execution of the rest of the middlewares.
#### 🧩 Example
-   If request has no Authorization header → pipeline short-circuits here.
-   If header exists → request flows to the next middleware.
```csharp
app.Use(async (context, next) =>
{
    if (!context.Request.Headers.ContainsKey("Authorization"))
    {
        context.Response.StatusCode = 401;
        await context.Response.WriteAsync("Unauthorized");
        return;  // short-circuit: next() is not called
    }

    await next(); // continue to next middleware if authorized
});
```
#### Common Use Cases of Short-Circuiting
1.  Authentication & Authorization
    -   Block unauthorized requests early before hitting controllers.
2.  CORS / Security Policies
    -   Stop invalid origins immediately.
3.  Rate Limiting / Throttling
    -   Deny requests if limits are exceeded.
4.  Static File Middleware
    -   If the requested file exists, return it and stop.
5.  Error handling / Custom responses
    -   Return a friendly error page without continuing the pipeline.</br>
**Short-circuiting of middleware** in .NET Core means a middleware **does not call `next()`**, thereby ending the request pipeline early and sending a response directly. It’s useful for **security checks, error handling, and performance optimizations**.
