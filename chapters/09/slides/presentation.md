class: dark middle

# Enterprise Web Development C&#35;
> Chapter 9 - Data, the new raw material

---
### Data, the new raw material

# Table of contents

- [Introduction](#intro)
- [Dapper](#dapper)
- [Entity Framework Core](#ef-core)
- [Working with EF Core](#tutorial-ef-core)
- [Overriding conventions](#overriding-conventions)
- [Exercises](#exercises)
- [Solutions](#solutions)
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
    * use right provider to give EF Core access to your data store
    * <a href="https://docs.microsoft.com/en-us/ef/core/providers/?tabs=dotnet-core-cli" target="_blank">List of available providers</a>
* access data through the model classes
    * instead of writing SQL yourself
    * like with Dapper

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

First, install Entity Framework Core

**Windows:**
```
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

**macOS/Linux**

You can also opt for SQL Server and run it in Docker (see Dapper notebook) or choose MySQL for example:

```
dotnet add package MySql.Data.EntityFramework
```

> More information about MySQL in Entity Framework can be found <a href="https://dev.mysql.com/doc/connector-net/en/connector-net-entityframework60.html" target="_blank">here</a>

---
### Creating your model
# Code-first workflow

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
> Working with EF Core

---
### Entity Framework Core
# Working with EF Core

Complete the following tutorial
[Persist and retrieve relational data with Entity Framework Core](https://docs.microsoft.com/en-us/learn/modules/persist-data-ef-core/)

> Note that the tutorial is **mandatory** to go forward.

<br />

> Choose **Fluent** as **data access** syntax starting from Unit 5

---
name: overriding-conventions
class: dark middle

# Data, the new raw material
> Overriding conventions

---
### Entity Framework Core
# Overriding conventions

If you don't obey the conventions of EF Core, like for example the `Id` or `<Entity name>Id`
convention, you need the <a href="https://www.learnentityframeworkcore.com/configuration/data-annotation-attributes" target="_blank">data annotations</a> or <a href="https://www.learnentityframeworkcore.com/configuration/fluent-api" target="_blank">EF Core Fluent API</a> to map you model to the database.

Sometimes the Fluent API is easier to use and easier to maintain than the data annotations. Also **not everything is possible with data annotations**, you sometimes really need the Fluent API.

<img src="./images/know-the-rules.jpg" alt="You know the rules and so do I" class="center"  style="max-width: 50%;" />

---
### Entity Framework Core
# Overriding conventions

Read through the following documentation sections:

- <a href="https://www.learnentityframeworkcore.com/configuration" target="_blank">Configuration in Entity Framework Core</a>
- <a href="https://www.learnentityframeworkcore.com/configuration/data-annotation-attributes" target="_blank">Data Annotation Attributes</a> (only this page)
- <a href="https://www.learnentityframeworkcore.com/configuration/fluent-api" target="_blank">Fluent Api</a> (only this page)
- <a href="https://docs.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/implement-value-objects#persist-value-objects-as-owned-entity-types-in-ef-core-20-and-later" target="_blank">Persist value objects as owned entity types</a>

<img src="./images/follow-the-rules.jpeg" alt="Follow the rules, ain't nobody got time for that" class="center" style="max-width: 50%;" />

---
name: exercises
class: dark middle

# Data, the new raw material
> Exercises

---
### Data, the new raw material
# Exercises

1. [Dapper](.../../../notebooks/exercises.ipynb)
2. <a href="https://github.com/HOGENT-Web/csharp-ch-9-exercise-1" target="_blank">SportStore with EF</a>

---
name: solutions
class: dark middle

# Data, the new raw material
> Solutions

---
### Data, the new raw material
# Solutions

1. [Dapper](.../../../notebooks/solutions.ipynb)
2. <a href="https://github.com/HOGENT-Web/csharp-ch-9-exercise-1/tree/solution" target="_blank">SportStore with EF</a>

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
