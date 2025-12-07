🟧 **Medium Priority**

In ASP.NET Core, both ConfigureServices and Configure methods are part of the application's Startup class and play important roles in the application setup. They are used for different purposes, and understanding their distinction is crucial for correctly configuring your application.
## ConfigureServices
-   **Purpose:** This method is primarily used for service configuration. It is where you register application services (dependencies) that will be injected into the components (like controllers, middleware, etc.) via Dependency Injection (DI).
-   **What Happens:** In this method, you register the services that your application needs, such as database contexts, logging, authentication, authorization, and custom services.
These services are available for the entire lifecycle of the application.
-   **When It Runs:** It runs once at the start of the application's request processing pipeline.
-   **Common Usage:** Adding services like MVC, Entity Framework, logging, configuration, and other dependencies.
#### 🧩 Example

```csharp
public void ConfigureServices(IServiceCollection services)
{
 // Add MVC framework
 services.AddControllersWithViews();
 // Register a custom service
 services.AddScoped<IMyService, MyService>();
 // Add database context (Entity Framework example)
 services.AddDbContext<MyDbContext>(options =>
 options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
 // Add authentication
 services.AddAuthentication("Bearer")
 .AddJwtBearer(options =>
 {
 options.Authority = "https://example.com";
 options.Audience = "api";
 });
}
```
### Key Point
-   Dependency Injection (DI): This is the main purpose of ConfigureServices—to register services for DI.
-   It doesn't execute any application logic, it only prepares services and configurations.
-   Services added in this method are available across the application.
## ConfigureMethod
-   **Purpose:** The Configure method is used for application pipeline configuration. This is where you define how HTTP requests are processed (i.e., what middleware will be used and in what order).
-   **What Happens:** In this method, you configure middleware components that are responsible for handling requests and responses. For example, you set up things like routing, authentication, static files, CORS, and error handling middleware.
-   **When It Runs:** It runs after ConfigureServices and is invoked for every HTTP request made to the application.
-   **Common Usage:** Setting up middleware components such as routing, authentication, logging, static files, and exception handling.
#### 🧩 Example
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
 // Use exception handling middleware in development environment
 if (env.IsDevelopment())
 {
 app.UseDeveloperExceptionPage();
 }
 else
 {
 app.UseExceptionHandler("/Home/Error");
 app.UseHsts();
 }
 // Serve static files (e.g., images, JavaScript, CSS)
 app.UseStaticFiles();
 // Use routing middleware to map requests to endpoints
 app.UseRouting();
 // Use authentication middleware
 app.UseAuthentication();
 // Use authorization middleware
 app.UseAuthorization();
 // Define endpoint mapping for controllers
 app.UseEndpoints(endpoints =>
 {
 endpoints.MapControllers();
 });
}
```
### Key Points
-   Middleware: This is where you configure the HTTP request-response pipeline using middleware components.
-   It configures how the app should handle different types of requests and responses, such as static file handling, routing, error handling, security (authentication and authorization), etc.
-   Order matters: The order in which middleware is added in the Configure method is very important because each middleware has a chance to process the request before it gets passed to the next middleware in the pipeline.

| 🔹 **Aspect** | **ConfigureServices** | **ConfigureMethods** |
|----------------|----------------|----------------|
| Purpose | Register services required for the application (e.g., DI services). | Set up the HTTP requestresponse pipeline (e.g., middleware).|
| When it runs | Runs once during app startup (before the application starts processing requests). | Runs during every HTTP request (after services are configured). |
| Common Use cases |Add services for DI (e.g., MVC, Entity Framework, custom services). <br> Configure authentication, authorization, and logging. | Configure middleware (e.g., routing, static files, error handling, authentication).<br>Define the app's behavior for handling requests. |
| Example | `services.AddDbContext<MyDbContext>();`<br>`services.AddAuthentication();` | `app.UseRouting();`<br>`app.UseStaticFiles();` |
| Access | Access to the IServiceCollection to register services. | Access to the IApplicationBuiler to configure middleware. |
### Flow of Execution
1.  `ConfigureServices` is called during the startup process to register services with the DI container.
2.  After `ConfigureServices`, `Configure` is called to set up the application's middleware pipeline.
3.  The middleware defined in the `configure` processes incoming HTTP requests and outgoing `responses`.
#### How do you handle configuration in .NET Core applications?
**Answer:**
-   Configuration in .NET Core is managed using the `appsettings.json` file, environment variables, and other configuration sources.
-   The `IConfiguration` interface is used to access configuration settings.
#### 🧩 Example
```csharp
public class Startup
{
    public Startup(IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public IConfiguration Configuration { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        var mySetting = Configuration["MySetting"];
        // Use the configuration setting as needed
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        // Middleware configuration
    }
}
```
