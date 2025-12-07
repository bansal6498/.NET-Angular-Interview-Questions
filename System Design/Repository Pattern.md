## Repository Pattern
The Repository Pattern is a design pattern that provides a way to separate the logic of data access from the business logic of an application. It acts as a mediator between the data access  layer (e.g., database operations) and the business logic layer, encapsulating the logic required to interact with data sources (e.g., databases, APIs, etc.).
### Purpose of the Repository Pattern
1. **Encapsulation:** It abstracts data access, allowing the business layer to focus on business logic.
2.  **Separation of Concerns:** Keeps data access logic separate from the application's core logic.
3.  **Testability:** Makes it easier to write unit tests by mocking repositories instead of the database.
4.  **Maintainability:** Simplifies code maintenance and refactoring by centralizing data access logic.
### How It Works
1.  Repository: Handles the data access logic (e.g., CRUD operations).
2.  Business Logic: Calls the repository to retrieve or modify data.
3.  Database or External Data Source: Serves as the actual data storage.
### When to Use the Repository Pattern?
-   When your application interacts with complex data sources (databases, APIs, etc.).
-   When you want to write unit tests for your business logic without depending on the database.
-   When you aim to adhere to the Single Responsibility Principle in the SOLID principles.
### Problems Solved by Repository Pattern
1.  **Decoupling:** The business layer is decoupled from the data access layer.
2.  **Code Reusability:** Centralizes data access logic, making it reusable across the application.
3.  **Testability:** Abstracts data access, allowing the use of mock objects for testing.
4.  **Flexibility:** Supports switching between different data sources (e.g., SQL, NoSQL) with minimal changes to the business layer.
5.  **Readability and Maintainability:** Provides a clean API for accessing data.</br>

**🔑 Interview-Ready Answer**

“The repository pattern abstracts the data access layer and provides a clean separation between business logic and data access logic. Its benefits include better separation of concerns, reusability of data access code, easier unit testing by mocking repositories, flexibility to switch databases, improved maintainability, and consistency in data access. For example, instead of directly using EF Core in controllers, I would inject an IEmployeeRepository that provides methods like GetEmployees() or AddEmployee(). This makes the application more testable, flexible, and maintainable.”
### Implementation of Repository Pattern in .NET
#### Step 1: Define the Model
```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```
#### Step 2: Define the Repository Interface
```csharp
public interface IProductRepository
{
    IEnumerable<Product> GetAllProducts();
    Product GetProductById(int id);
    void AddProduct(Product product);
    void UpdateProduct(Product product);
    void DeleteProduct(int id);
}
```
#### Step 3: Implement the Repository
```csharp
using System.Collections.Generic;
using System.Linq;
public class ProductRepository : IProductRepository
{
    private readonly List<Product> _products = new List<Product>();
    public IEnumerable<Product> GetAllProducts()
    {
        return _products;
    }
    public Product GetProductById(int id)
    {
        return _products.FirstOrDefault(p => p.Id == id);
    }
    public void AddProduct(Product product)
    {
        _products.Add(product);
    }
    public void UpdateProduct(Product product)
    {
        var existingProduct = GetProductById(product.Id);
        if (existingProduct != null)
        {
            existingProduct.Name = product.Name;
            existingProduct.Price = product.Price;
        }
    }
    public void DeleteProduct(int id)
    {
        var product = GetProductById(id);
        if (product != null)
        {
            _products.Remove(product);
        }
    }
}
```
#### Step 4: Use the Repository in the Business Logic
```csharp
public class ProductService
{
    private readonly IProductRepository _productRepository;
    public ProductService(IProductRepository productRepository)
    {
        _productRepository = productRepository;
    }
    public void AddNewProduct(string name, decimal price)
    {
        var product = new Product { Name = name, Price = price };
        _productRepository.AddProduct(product);
    }
    public IEnumerable<Product> GetAllProducts()
    {
        return _productRepository.GetAllProducts();
    }
}
```
 ### Advantages of Repository Pattern
-   Decouples business logic from database logic.
-   Supports multiple data storage mechanisms.
-   Promotes code reuse and separation of concerns.
-   Improves unit testing by mocking repositories instead of databases.
-   Centralizes data access code for easier refactoring and maintenance.
### Disadvantages of Repository Pattern
-   **Overhead**: For simple applications, the pattern may add unnecessary complexity.
-   **Redundancy**: May duplicate ORM functionalities (e.g., Entity Framework’s DbSet).
