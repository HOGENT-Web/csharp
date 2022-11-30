class: dark middle

# Enterprise Web Development C&#35;
> Chapter 9 - Data, the new raw material

---
### Data, the new raw material

# Table of contents

- [Introduction](#intro)
- [Dapper](#dapper)
- [Entity Framework Core](#ef-core)
- [Tutorial EF Core](#tutorial-ef-core)
- [EF Core Explained](#ef-core-explained)
- [Switch to SQL Server](#sql-server)
- [Configurations](#configurations)
- [Queries](#queries)
- [Saving Data](#saving-data)
- [Summary](#summary)

---
name: intro
class: dark middle

# Data, the new raw material
> Introduction

---
### Data, the new raw material
# Introduction

Fetching in data in .NET can be done in different ways:

* [ADO.NET](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/ado-net-overview)
* [Dapper](https://dapper-tutorial.net/)
* [Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/)
* ...

Each has its own (dis)advantages: simplicity, need to known SQL, ...

> We'll cover Dapper and EF Core in this course.

---
name: dapper
class: dark middle

# Data, the new raw material
> Dapper

---
### Data, the new raw material
# Dapper

First read through the [Dapper Introduction documentation](https://dapper-tutorial.net/dapper).

Then move on to the [Dapper notebook](../notebooks/dapper.ipynb) and learn what it's capable of.

At last solve the [exercises](.../../../notebooks/exercises.ipynb), there is an example
[solution](../notebooks/solutions.ipynb) provided.

> **Note**: This is not the only solution, your queries might differ a little.

<img src="./images/dapper.png" alt="Dapper Logo" width="20%" style="display: block; margin: 0 auto;" />

---
name: ef-core
class: dark middle

# Data, the new raw material
> Entity Framework Core

---
### Entity Framework Core
# What is it?

* **O**bject **R**elational **M**apper (ORM) framework
* open-source and cross platform
* works with relational and not relational data stores
    * use the right provider to give EF Core access to your data store
    * <a href="https://docs.microsoft.com/en-us/ef/core/providers/?tabs=dotnet-core-cli" target="_blank">List of available providers</a>
* access data through the model classes
    * instead of writing SQL yourself

---
### Entity Framework Core
# How does it work?

* It **generates a persistence layer**: infrastructure to fetch/write objects from/to the database
    * converts classes into tables and properties into columns in a table
    * converts objects to table rows
    * converts associations to foreign keys (and thus relations)
    * supports inheritance
* It **provides an API** named <a href="https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities" target="_blank">Linq to Entities</a> to fetch and manipulate the objects
    * actions will be converted to queries
    * no need to write them yourself!
    * independent of database query language

---
### Entity Framework Core
# Creating your model

You have two options for creating the database and model

1. **Code-First**: build the model and generate the database, two possible workflows
    - Drop-create database (not so great in production 😏)
    - <a href="https://www.learnentityframeworkcore.com/migrations" target="_blank">Migrations</a>: build/update a database step by step
2. **Database-first**: generate the model starting from an existing database
    - Use command `dotnet ef dbcontext scaffold`
    - More info in the <a href="https://docs.microsoft.com/en-us/ef/core/cli/dotnet" target="_blank">documentation</a>

> We choose the first approach, but feel free to change depending on your project

---
### Creating your model
# Code-first workflow
Different packages are needed for the different providers, choose one.
```
dotnet add package Microsoft.EntityFrameworkCore.`SqlServer`
dotnet add package Microsoft.EntityFrameworkCore.`Sqlite`
dotnet add package Microsoft.EntityFrameworkCore.`InMemory`
```

After installing EF Core, a typical workflow for the **code-first** approach is as follows

1. Create a persistence layer and configure the database provider
2. Create or adapt the domain model
3. Drop and create the database (or migrate)
4. Customize mapping where necessary
5. Repeat from step 2 until database is correct

---
name: tutorial-ef-core
class: dark middle

# Data, the new raw material
> Tutorial Entity Framework Core

---
### Entity Framework Core
# Tutorial

Complete the following tutorial
[Persist and retrieve relational data with Entity Framework Core](https://docs.microsoft.com/en-us/learn/modules/persist-data-ef-core/)

> Note that the tutorial is **mandatory** to go forward.


---
name: ef-core-explained
class: dark middle

# Data, the new raw material
> Entity Framework Core explained

---
### Entity Framework Core
# Explained
On the following slides, we'll explain the code which was already implemented in chapter 8. We just copy-pasted the solution branch. The code is not perfect, but it's a good starting point to learn how to map.

clone <a href="https://github.com/HOGENT-Web/csharp-ch-9-example-1" target="_blank"> this repository</a> to get started.

- DbContext
    - Entity Types
    - Entity Base class
    - OnConfiguring
    - OnModelCreating
    - Lifetime
- Persistence.csproj
    - Configurations
    - Triggers

> We advise to read through the links provided in the next slides to get a better understanding of EF Core.

---
### Entity Framework Core
# DbContext


```cs
public class BogusDbContext : DbContext
{
    public DbSet<Product> Products => Set<Product>();

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {

    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {

    }
}
```
The `DbContext` class is an integral part of Entity Framework. An instance of `DbContext` represents a session with the database which can be used to query and save instances of your entities to a database. `DbContext` is a combination of the Unit Of Work and Repository patterns.

> More information can be found <a href="https://www.entityframeworktutorial.net/efcore/entity-framework-core-dbcontext.aspx#:~:text=The%20DbContext%20class%20is%20an,Of%20Work%20and%20Repository%20patterns" target="_blank">here</a> 


---
### DbContext
# Entity Types

```cs
public class BogusDbContext `: DbContext`
{
*   public DbSet<Product> Products => Set<Product>();
}
```

- DbSet<T> is a collection of entities of type `T`, `Product` in this case.
- Each DbSet<T> represents a table in the database.
- The `Set<T>` method is used to access the DbSet<T> collection.

> More information can be found <a href="https://learn.microsoft.com/en-gb/ef/core/modeling/entity-types?tabs=fluent-api" target="_blank">here</a> 

---
### DbContext
# Entity Base class

```cs
public abstract class Entity
{
    public int Id { get; protected set; }
    public DateTime CreatedAt { get; set; }
    public DateTime UpdatedAt { get; set; }
    // other stuff
}
```

- Each Entity in our domain model should inherit from this class.
- This class contains the `Id` property, which is the primary key of the table.
- The `CreatedAt` and `UpdatedAt` properties are used to track when an entity was created and updated.

```cs
public class Product `: Entity`
{
    // other stuff and properties
}
```
> More information can be found <a href="https://enterprisecraftsmanship.com/posts/entity-base-class/" target="_blank">here</a> 

---
### DbContext
# Constructors for entities
Declare private constructors for classes that are stored in the database, so EF Core will always use this constructor.

```cs
public class Product : Entity
{
*   private Product() { }
    // other stuff and properties
}
```

If you don't do this, EF Core will use the default constructor, if there is one or the one with the most parameters. If you're using setter validation in your entities, this can cause problems. Since EF Core will use that constructor and set the properties, the validation will be triggered.

> More information can be found <a href="https://learn.microsoft.com/en-us/ef/core/modeling/constructors" target="_blank">here</a>

---
### DbContext
# OnConfiguring

```cs
public class BogusDbContext : DbContext
{
   public DbSet<Product> Products => Set<Product>();
   
   protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        base.OnConfiguring(optionsBuilder);
        optionsBuilder.EnableDetailedErrors();
        optionsBuilder.EnableSensitiveDataLogging();
*       optionsBuilder.UseInMemoryDatabase(databaseName: "BogusDb");
    }
}
```
This method is called for each instance of the context that is created.

> Later we will change this to use a real database

---
### DbContext
# OnModelCreating
Entity Framework Core uses a set of conventions to build a model based on the shape of your entity classes. You can specify additional configuration to supplement and/or override what was discovered by convention.

You can override the `OnModelCreating` method in your derived context and use the ModelBuilder API to configure your model. This is the most powerful method of configuration and allows configuration to be specified without modifying your entity classes. Fluent API configuration has the highest precedence and will override conventions and data annotations.

```cs
public class BogusDbContext : DbContext
{
  public DbSet<Product> Products => Set<Product>();
    // Other stuff
  protected override void OnModelCreating(ModelBuilder modelBuilder)
  {
      modelBuilder.Entity<Product>()
          .Property(x => x.Name)
          .HasMaxLength(50)
          .IsRequired();
  }
}
```

> More information can be found <a href="https://learn.microsoft.com/en-us/ef/core/modeling/" target="_blank">here</a> 


---
### DbContext
# Grouping configuration
To reduce the size of the `OnModelCreating` method all configuration for an entity type can be extracted to a separate class implementing `IEntityTypeConfiguration<TEntity>.`

```cs
class ProductConfiguration : IEntityTypeConfiguration<Product>
{
    public void Configure(EntityTypeBuilder<Product> builder)
    {
        builder.Property(x => x.Name)
               .HasMaxLength(50);
               .IsRequired();
    }
}
```
> More information can be found <a href="https://learn.microsoft.com/en-gb/ef/core/dbcontext-configuration/" target="_blank">here</a> 
>
> Do not forget to apply the configuration in the `OnModelCreating` method of the `DbContext` (see next slide).


---
### DbContext
# Applying all configurations

```cs
public class BogusDbContext : DbContext
{
    public DbSet<Product> Products => Set<Product>();
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);
        modelBuilder.ApplyConfigurationsFromAssembly(typeof(BogusDbContext).Assembly);
    }
}
```

---
### DbContext
# Conventions
Most of the time Entity Framework Core will map the models based on conventions so you don't need to configure everything yourself. Knowing these conventions can help you to understand what is going on and why something is (not) working. On the following links, you can find a list of all conventions that are used by EF Core.
- <a href="https://www.entityframeworktutorial.net/efcore/conventions-in-ef-core.aspx"> Basic Conventions</a>
- <a href="https://learn.microsoft.com/en-us/ef/core/modeling/relationships?tabs=fluent-api%2Cfluent-api-simple-key%2Csimple-key"> Relationship Conventions</a>

---
### DbContext
# Lifetime
The lifetime of a `DbContext` begins when the instance is created and ends when the instance is disposed. A `DbContext` instance is designed to be used for a single unit-of-work. This means that the **lifetime** of a `DbContext` instance is usually **very short**.

In many web applications, each HTTP request corresponds to a single unit-of-work. This makes tying the context lifetime to that of the request a good default for web applications, which is `scoped`.

**Server/Program.cs**
```cs
builder.Services.AddDbContext<BogusDbContext>();
```

> More information can be found <a href="https://learn.microsoft.com/en-gb/ef/core/dbcontext-configuration/" target="_blank">here</a> 

---
### Persistence.csproj
# Configurations
We used the grouping configuration and provide 1 file per entity type. As can be seen in the `ProductConfiguration.cs` file.

```cs
class ProductConfiguration : IEntityTypeConfiguration<Product>
{
    public void Configure(EntityTypeBuilder<Product> builder)
    {
        builder.OwnsOne(x => x.Price).Property(x => x.Value);
    }
}
```

---
### Persistence.csproj
# Triggers
A Trigger is something that is executed before or after an action is performed on the database. In this case we will use triggers to set the `CreatedAt` and `UpdatedAt` properties of the entities. Notice that this is database agnostic and will work for any database provider.

```cs
public class EntityBeforeSaveTrigger : IBeforeSaveTrigger<Entity>
{
    public Task BeforeSave(ITriggerContext<Entity> context, 
                           CancellationToken cancellationToken)
    {
        if (context.ChangeType == ChangeType.Added)
        {
            context.Entity.CreatedAt = DateTime.UtcNow;
            context.Entity.UpdatedAt = DateTime.UtcNow;
        }
        if (context.ChangeType == ChangeType.Modified)
        {
            context.Entity.UpdatedAt = DateTime.UtcNow;
        }
        return Task.CompletedTask;
    }
}
```

> This is not built-in so we've used the `EntityFrameworkCore.Triggered` package.


---
name: sql-server
class: dark middle

# Data, the new raw material
> Switch to Microsoft SQL Server

---
### Switch to Microsoft SQL Server
**Persistence.csproj**
```bash
dotnet `add` package Microsoft.EntityFrameworkCore.`SqlServer`
dotnet `remove` package Microsoft.EntityFrameworkCore.`InMemory`
```

**Server/Program.cs**
```cs
builder.Services.AddDbContext<BogusDbContext>(`options =>`
*{
*    options.UseSqlServer
*    (
*        builder.Configuration.GetConnectionString("SqlServer")
*    );
});
```
> Note that the connectionstring is fetched from the `AppSettings.json` file.

---
### Switch to Microsoft SQL Server
**Server/AppSettings.json**

Windows
```json
{
  "ConnectionStrings": {
    "Storage": "YOUR_BLOB_STORAGE_CONNECTION_STRING_HERE",
    "SqlServer": "Server=(localdb)\\mssqllocaldb;Database=BogusDb;Trusted_Connection=True;"
  }
}
```
macOS/Linux
```json
{
  "ConnectionStrings": {
    "Storage": "YOUR_BLOB_STORAGE_CONNECTION_STRING_HERE",
    "SqlServer": "Server=localhost,1433;Database=Csharp.BogusDb;User=sa;Password=p@ssw0rd"
  }
}
```
> You will need Docker if you're on Linux / macOS.

---
### DbContext
# MS SQL Server 
**BogusDbContext.cs**
```cs
public class BogusDbContext : DbContext
{
   public DbSet<Product> Products => Set<Product>();

*  public BogusDbContext(DbContextOptions<BogusDbContext> options)
*  : base(options) {}

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        base.OnConfiguring(optionsBuilder);
        optionsBuilder.EnableDetailedErrors();
        optionsBuilder.EnableSensitiveDataLogging();
*       // Remove the InMemoryDatabase
        optionsBuilder.UseTriggers(options =>
        {
            options.AddTrigger<EntityBeforeSaveTrigger>();
        });
    }
}
```

---
### Switch to Microsoft SQL Server
**FakeSeeder.cs**

```cs
public void Seed()
{
    // Not a good idea in production.
*   dbContext.Database.EnsureDeleted();
*   dbContext.Database.EnsureCreated();

    SeedProducts();
    SeedTags();
    SeedCustomers();
}
```
For now we'll use a drop/create strategy to make sure we have a clean database. In production you would use migrations.

> Learn how to use migrations <a href="https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/?tabs=dotnet-core-cli" target="_blank">here</a>

---
class: dark middle

# Data, the new raw material
> 📝 Commit: Switch to Sql Server
>
> Show the database schema using SSMS or Azure Data Studio

---
name:configurations
### Overriding the default conventions
**BogusDbContext.cs**

```cs
// Other methods omitted
protected override void ConfigureConventions(ModelConfigurationBuilder configurationBuilder)
{
    // All decimals should have 2 digits after the comma
    configurationBuilder.Properties<decimal>().HavePrecision(18, 2);
    // Max Length of a NVARCHAR that can be indexed
    configurationBuilder.Properties<string>().HaveMaxLength(4_000);
}
```
> Global configuration for all entities and `decimal` / `string` properties.

---
class: dark middle

# Data, the new raw material
> 📝 Commit: Global Conventions

---
### Overriding the logging
**Server/AppSettings.json**

```json
{
  "ConnectionStrings": {
    "Storage": "YOUR_CONNECTION_STRING_HERE",
    "SqlServer": "YOUR_CONNECTION_STRING_HERE"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning",
*     "EntityFrameworkCore.Triggered" : "Warning"
    }
  },
  "AllowedHosts": "*"
}
```
> Making the Triggered package shut-up a bit more.

---
class: dark middle

# Data, the new raw material
> 📝 Commit: Less Logging From Triggered

---
### Default values for `Entities`
**Persistence/Configurations/EntityConfiguration.cs**

```cs
class EntityConfiguration<T> : IEntityTypeConfiguration<T> where T : Entity
{
    public virtual void Configure(EntityTypeBuilder<T> builder)
    {
        // All tables are singlular named and have the name of the Entity
        builder.ToTable(typeof(T).Name); 
        // All entities can be soft deleted but are not by default
        builder.Property(x => x.IsEnabled).IsRequired().HasDefaultValue(true).ValueGeneratedNever();
        // Default SQL constraint for CreatedAt and UpdatedAt
        builder.Property(x => x.CreatedAt).HasDefaultValueSql("GETUTCDATE()");
        builder.Property(x => x.UpdatedAt).HasDefaultValueSql("GETUTCDATE()").IsConcurrencyToken();
    }
}
```
> Default configuration for all entities.
>
> Continued on the next slide.

---
### Default values for `Entities`
**Persistence/Configurations/EntityConfiguration.cs**

Before
```cs
internal class ProductConfiguration `:  IEntityTypeConfiguration<Product>`
{
    public void Configure(EntityTypeBuilder<Product> builder)
    {
        builder.OwnsOne(x => x.Price).Property(x => x.Value);
    }
}
```

After
```cs
internal class ProductConfiguration `: EntityConfiguration<Product>`
{
    public `override` void Configure(EntityTypeBuilder<Product> builder)
    {
        `base.Configure(builder);`
        builder.OwnsOne(x => x.Price).Property(x => x.Value);
    }
}
```
> Do this for all your `EntityConfiguration` classes, so `CustomerConfiguration` etc.


---
class: dark middle

# Data, the new raw material
> 📝 Commit: Introduce EntityConfiguration&lt;T&gt;

---
### Rename Price_Value column to Price
**Persistence/Configurations/ProductConfiguration.cs**
```cs

internal class ProductConfiguration : EntityConfiguration<Product>
{
    public override void Configure(EntityTypeBuilder<Product> builder)
    {
        base.Configure(builder);

        builder`.OwnsOne(x => x.Price)`
               `.Property(x => x.Value)`
               `.HasColumnName(nameof(Product.Price))`;
    }
}
```
> Read through the <a href="https://learn.microsoft.com/en-us/ef/core/modeling/owned-entities" target="_blank">documentation</a> to learn more about `ValueObjects` and how to map them to the database.
> 
> `OwnsOne` / `OwnsMany` is **not** the same as `HasOne` / `HasMany`. Only use `OwnsOne` / `OwnsMany` for `ValueObjects` to store the object with the Entity that owns it.

---
class: dark middle

# Data, the new raw material
> 📝 Commit: Rename Price_Value column to Price

---
### OrderLine is not mapped at all.
**Persistence/Configurations/OrderLineConfiguration.cs**
```cs
internal class OrderLineConfiguration : EntityConfiguration<OrderLine>
{
    public override void Configure(EntityTypeBuilder<OrderLine> builder)
    {
        base.Configure(builder);

        // Was not mapped due to {get;}
        builder.Property(x => x.Quantity);
        builder.Property(x => x.Description);
        
        // Value Object Mapping and rename of column
        builder.OwnsOne(x => x.Price)
               .Property(x => x.Value)// Was not mapped due to {get;}
               .HasColumnName(nameof(OrderLine.Price));
        // 1 to Many relationship with a cascade restrict behavior
        builder.HasOne(x => x.Product)
               .WithMany()
               .OnDelete(DeleteBehavior.Restrict);
    }
}
```
> Note that `{get;}` properties are not mapped by default so we need the `.Property(x => x.Value)` to map the `Value` property or use `{get; private set;}` but that's lying to the Domain. More information about `one-to-many` relationships <a href="https://docs.microsoft.com/en-us/ef/core/modeling/relationships" target="_blank">here</a>.

---
class: dark middle

# Data, the new raw material
> 📝 Commit: OrderLine Configuration

---
class: dark middle

# Data, the new raw material
> Exercise

---
### Data, the new raw material
# Exercise
Use the <a href="https://learn.microsoft.com/en-us/ef/core/" target="_blank">documentation</a> of EF Core and configurations to:

Tags
- Set the max length of a `Tag` to 50 characters

Products
- Add a unique index to the `Name` column

Customers
- Rename the `Email_Value` column to `Email`
- Add a unique index for the `Email` column
- Rename the `Address_Street` column to `Street`, do this for all the `Address` properties

---
class: dark middle

# Data, the new raw material
> 📝 Commit: Additional Mappings

---
class: dark middle

# Data, the new raw material
> 📝 Commit: Additional Mappings

---
### ProductTag as Entity (if you want to)
**Persistence/Configurations/TagConfiguration.cs**
```cs
internal class TagConfiguration : EntityConfiguration<Tag>
{
    public override void Configure(EntityTypeBuilder<Tag> builder)
    {
        base.Configure(builder);

        builder.Property(x => x.Name).HasMaxLength(50);
*       builder.HasMany(x => x.Products)
*              .WithMany(x => x.Tags)
*              .UsingEntity<ProductTag>
*              (
*                  x => x.HasOne(x => x.Product).WithMany(),
*                  x => x.HasOne(x => x.Tag).WithMany().OnDelete(DeleteBehavior.Restrict),
*                  x => x.ToTable($"{nameof(Product)}_{nameof(Tag)}")
*              );
*   }
}
```
```cs
*public class ProductTag : Entity // In the Domain
*{
*    public Product Product { get; set; } = default!;
*    public Tag Tag { get; set; } = default!;
*    private ProductTag() { }
*}
```

---
name: queries
class: dark middle

# Data, the new raw material
> Queries

---
### Queries
# LINQ

EF Core uses Language-Integrated Query to query data from the database. LINQ allows you to use C# to write strongly typed queries. Database providers in turn translate it to database-specific query language.
```cs
using (var context = new BloggingContext())
{
    var blogs = context.Blogs.ToList();
}
```

```cs
using (var context = new BloggingContext())
{
    var blog = context.Blogs
        .Single(b => b.BlogId == 1);
}
```

```cs
using (var context = new BloggingContext())
{
    var blogs = context.Blogs
        .Where(b => b.Url.Contains("dotnet"))
        .ToList();
}
```

> Read more about it <a href="https://docs.microsoft.com/en-us/ef/core/querying/" target="_blank">here</a>, and see Chapter 4.

---
### Queries
# Client vs Server evaluation
EF Core attempts to evaluate a query on the database server as much as possible. However, there are some limitations. 

In the following example, a helper method is used to standardize URLs for blogs, which are returned from a SQL Server database. Since the SQL Server provider has no insight into how this method is implemented, it isn't possible to translate it into SQL. 
```cs
var blogs = context.Blogs
    .Select(blog => new { 
                Id = blog.BlogId,
                Url = `StandardizeUrl(blog.Url)` 
            })
    .ToList();
```
```cs
public static string StandardizeUrl(string url)
{
    url = url.ToLower();
    if (!url.StartsWith("http://"))
        url = string.Concat("http://", url);
    return url;
}
```

> Read more about it <a href="https://learn.microsoft.com/en-us/ef/core/querying/client-eval" target="_blank">here</a>.

---
### Queries
# Tracking vs. No-Tracking
Tracking behavior controls if EF Core will keep information about an entity instance in its change tracker. If an entity is tracked, any changes detected in the entity will be persisted to the database during `SaveChanges()`. EF Core will also fix up navigation properties between the entities in a tracking query result and the entities that are in the change tracker.

**Tracking** (default)
```cs
var blog = context.Blogs.SingleOrDefault(b => b.BlogId == 1);
blog.Rating = 5;
context.SaveChanges();
```

**Non-tracking**

Are useful when the results are used in a **read-only scenario**. They're quicker to execute because there's no need to set up the change tracking information. If you don't need to update the entities retrieved from the database, then a no-tracking query should be used.
```cs
var blogs = context.Blogs.`AsNoTracking()`.ToList();
```

> Read more about it <a href="https://learn.microsoft.com/en-us/ef/core/querying/tracking" target="_blank">here</a>.

---
### Queries
# Loading Related Data
- <a href="https://learn.microsoft.com/en-us/ef/core/querying/related-data/eager" target="_blank">Eager loading</a> 
     - means that the related data is loaded from the database as part of the initial query.
     - We'll use this approach, which is also the most standard.
- <a href="https://learn.microsoft.com/en-us/ef/core/querying/related-data/explicit" target="_blank">Explicit loading</a> 
    - means that the related data is explicitly loaded from the database at a later time.
    - Rarely used.
    - We won't go into detail for this approach.
- <a href="https://learn.microsoft.com/en-us/ef/core/querying/related-data/lazy" target="_blank">Lazy loading</a> 
    - means that the related data is transparently loaded from the database when the navigation property is accessed.
    - Can cause unneeded extra database roundtrips to occur (the so-called N+1 problem), and care should be taken to avoid this. We don't recommend this approach.
    - We won't go into detail for this approach.


---
### Loading Related Data
# Eager loading
You can use the `Include` method to specify related data to be included in query results. In the following example, the blogs that are returned in the results will have their Posts property populated with the related posts. Think about it as a `JOIN` in SQL.

```cs
using (var context = new BloggingContext())
{
    var blogs = context.Blogs
        `.Include(blog => blog.Posts)`
        .ToList();
}
```

```cs
using (var context = new BloggingContext())
{
    var blogs = context.Blogs
        `.Include(blog => blog.Posts)`
        `.Include(blog => blog.Owner)`
        .ToList();
}
```

> Read more about it <a href="https://learn.microsoft.com/en-us/ef/core/querying/related-data/eager" target="_blank">here</a>.

---
### Loading Related Data
# Eager loading
Eager loading a collection navigation in a single query may cause performance issues. Therefore you can use a Filtered Include to specify a filter condition for the related data to be included in the query results. 

```cs
using (var context = new BloggingContext())
{
    var filteredBlogs = context.Blogs
        .Include(blog => `blog.Posts.Where(post => post.Rating >= 5`)
        .ToList();
}
```
Including multi-level
```cs
using (var context = new BloggingContext())
{
    var blogs = context.Blogs
        `.Include(blog => blog.Posts)`
            `.ThenInclude(post => post.Author)`
                `.ThenInclude(author => author.Photo)`
        .ToList();
}
```

> Read more about it <a href="https://learn.microsoft.com/en-us/ef/core/querying/related-data/eager" target="_blank">here</a>.

---
name: saving-data
class: dark middle

# Data, the new raw material
> Saving Data

---
### Saving Data
# ChangeTracker
Each context instance has a `ChangeTracker` that is responsible for keeping track of changes that need to be written to the database. As you make changes to instances of your entity classes, these changes are recorded in the ChangeTracker and then written to the database when you call SaveChanges. The database provider is responsible for translating the changes into database-specific operations (for example, `INSERT`, `UPDATE`, and `DELETE` commands for a relational database).

> Read more about it <a href="https://learn.microsoft.com/en-us/ef/core/saving/" target="_blank">here</a>.

---
### Saving Data
# Basic Save
Use the `DbSet.Add` method to add new instances of your entity classes. The data will be inserted in the database when you call `SaveChanges`.

Adding
```cs
using (var context = new BloggingContext())
{
    var blog = new Blog { Url = "http://example.com" };
    `context.Blogs.Add(blog);`
    `context.SaveChanges();`
}
```

Updating
```cs
using (var context = new BloggingContext())
{
    var blog = context.Blogs.First();
    blog.Url = "http://example.com/blog";
    context.SaveChanges();
}
```

> Read more about it <a href="https://learn.microsoft.com/en-us/ef/core/saving/basic" target="_blank">here</a>.

---
### Saving Data
# Basic Save
Deleting
```cs
using (var context = new BloggingContext())
{
    var blog = context.Blogs.First();
    `context.Blogs.Remove(blog);`
    `context.SaveChanges();`
}
```

Multiple operations
```cs
using (var context = new BloggingContext())
{
    // add
    context.Blogs.Add(new Blog { Url = "http://example.com/blog_one" });
    context.Blogs.Add(new Blog { Url = "http://example.com/blog_two" });
    var firstBlog = context.Blogs.First();
    firstBlog.Url = ""; // update
    var lastBlog = context.Blogs.OrderBy(e => e.BlogId).Last();
    context.Blogs.Remove(lastBlog); //delete
    context.SaveChanges();
}
```

---
### Saving Data
# Relational
Deleting
```cs
using (var context = new BloggingContext())
{
    var blog = context.Blogs.First();
    `context.Blogs.Remove(blog);`
    `context.SaveChanges();`
}
```

Multiple operations
```cs
using (var context = new BloggingContext())
{
    // add
    context.Blogs.Add(new Blog { Url = "http://example.com/blog_one" });
    context.Blogs.Add(new Blog { Url = "http://example.com/blog_two" });
    var firstBlog = context.Blogs.First();
    firstBlog.Url = ""; // update
    var lastBlog = context.Blogs.OrderBy(e => e.BlogId).Last();
    context.Blogs.Remove(lastBlog); //delete
    context.SaveChanges();
}
```

---
name: summary
class: dark middle

# Data, the new raw material
> Summary

---
### Data, the new raw material
# Summary

* There are many options for data access in .NET
* **Choose the most appropriate**
* **Dapper**:
    * write your own queries
    * maps data to models for free
    * good for small projects
* **Entity Framework Core**:
    * writes queries itself
    * maps data to models for free
    * good for big projects with lots of tables
