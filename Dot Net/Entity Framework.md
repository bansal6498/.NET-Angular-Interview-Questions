## Entity Framework
Entity Framework (EF) is an Object-Relational Mapper (ORM) that allows developers to interact with a database using C# objects instead of writing raw SQL queries. It abstracts the database interactions and provides methods to query, insert, update, and delete data. EF supports both code-first and database-first approaches. EF Core is the lightweight, cross-platform version of EF, typically used with .NET Core.
#### Have you worked with ORM? Which ORM did you use, and how?
**Answer:**
-   Yes, Entity Framework Core.
-   Used for database mapping → LINQ queries to interact with SQL Server.
-   Applied migrations for schema changes.
-   Optimized with AsNoTracking, compiled queries.
### Pagination with EF Core
```csharp
var pageSize = 10;
var data = db.Users
             .Skip((page-1)*pageSize)
             .Take(pageSize)
             .ToList();
```
#### How to fetch only Active records from all 100 tables in EF without adding WHERE Active = 1 everywhere?
**Answer:**
Use global query filters (EF Core) plus a shared interface/base type.
#### 🧩 Example
```csharp
public interface IHasIsActive { bool IsActive { get; set; } }

public class Employee : IHasIsActive
{
    public int Id { get; set; }
    public string Name { get; set; }
    public bool IsActive { get; set; } = true;
}

protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    // Apply to all entities implementing IHasIsActive
    foreach (var entityType in modelBuilder.Model.GetEntityTypes()
             .Where(t => typeof(IHasIsActive).IsAssignableFrom(t.ClrType)))
    {
        var method = typeof(MyDbContext).GetMethod(nameof(ApplyIsActiveFilter),
                      BindingFlags.NonPublic | BindingFlags.Static)
                      .MakeGenericMethod(entityType.ClrType);
        method.Invoke(null, new object[] { modelBuilder });
    }
}

private static void ApplyIsActiveFilter<TEntity>(ModelBuilder builder) where TEntity : class, IHasIsActive
{
    builder.Entity<TEntity>().HasQueryFilter(e => EF.Property<bool>(e, nameof(IHasIsActive.IsActive)) == true);
}
```
