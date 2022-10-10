class: dark middle

# Enterprise Web Development C&#35;
> Chapter 5 - David's and Goliath's Architecture

---
### David's and Goliath's Architecture
# Table of contents
- [Modern Web Applications](#modern-web-applications)
- [Hosting Models](#hosting-models)
- [Common design principles](#common-design-principles)
- [Common Architectures](#architecture)

---
class: dark middle
name:modern-web-applications
# Architecture
> Modern Web Applications

---
### Modern Web Applications
# Characteristics
- Higher user expectations and greater demands than ever before.
- Available 24/7 from anywhere in the world
- Usable from virtually any device or screen size
- Secure, flexible, and scalable to meet spikes
- Rich user experiences

> Microsoft's answer to cope with these characteristics: [ASP.NET](http://asp.net/)

---
### Modern Web Applications
# [ASP.NET](https://asp.net)
- Builts on top of  [.NET](https://dot.net)
- A framework for building web apps and services with [.NET](https://dot.net) and [C#](https://docs.microsoft.com/en-us/dotnet/csharp/).
- Optimized for the cloud
    - low-memory and high-throughput
- Cross platform for development and deployment
- Modular and loosely coupled
    - Composed of many libraries through [NuGet](https://www.nuget.org/) distribution
    - Supports **D**ependency **I**njection
        - Swap out 1 implementation for another through `interface`s
- Easily tested with automated tests
- Traditional and SPA behaviors are supported
- Developed by the community and Microsoft

---
### Modern Web Applications
# Traditional vs. Modern
- Traditional
    - Full page reloads
    - "Thin" clients
        - Server takes care of (almost) every interaction.
        - All Code stays on the server
    - Simple User Experience
- Modern (**S**ingle **P**age **A**pplications)
    - Initialized within a static HTML file
    - "Fat" client: 
        - Client takes care of (almost) every interaction
        - Client code is downloaded to the browser
    - Richer user experience

> Read more [here](https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/modern-web-applications-characteristics#traditional-and-spa-behaviors-supported)
---
### Modern Web Applications
# What should you choose?
Use traditional web applications when:
- Client-side requirements are simple or even read-only.
- Application needs to function in browsers without JavaScript support.
- Team is unfamiliar with JavaScript or Blazor development techniques.

Use a SPA when:
- Application must expose a rich user interface with many features.
- Team is familiar with JavaScript, TypeScript, or Blazor development.
- Your application must already expose an API for other clients.

However:
- SPA frameworks require greater architectural and security expertise.

> Read more [here](https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/choose-between-traditional-web-and-single-page-apps) or [here](https://docs.microsoft.com/en-us/aspnet/core/tutorials/choose-web-ui?view=aspnetcore-6.0)

---
name:hosting-models
### Modern Web Applications
# Support in ASP.NET
Following templates are available in ASP.NET:

<img src="images/project-templates.svg" width="100%">

> Can be generated through `dotnew new [templatename]`

---
class: dark middle
name:razor-pages
# Hosting Models
> Razor Pages

---
### Razor Pages
# Schemantic
<img src="images/client-server.svg" width="75%" class="center">
1. Client sends a HTTP Request for a specific page `/[page]`
2. Server processes the request
    - `[page]` is found in the `pages` folder.
    - Uses the `[Page.cshtml.cs]` code-behind to handle the request.
    - `[Page.cshtml]` which consists of C# + HTML is rendered (server).
       - Rendered by the [Razor View Engine](https://www.c-sharpcorner.com/article/learn-about-razor-view-engine/)
    - HTTP Response with the content of the HTML page is returned.
3. Client can interact with the `[page]`

---
### Razor Pages
# > dotnet new razor
Complete the following tutorial series:
1. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/?view=aspnetcore-6.0">Create a Razor Pages web app</a>
2. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/model?view=aspnetcore-6.0">Add a model to a Razor Pages app</a>
3. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/page?view=aspnetcore-6.0">Scaffold (generate) Razor pages</a>
4. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/sql?view=aspnetcore-6.0">Work with a database</a>
5. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/da1?view=aspnetcore-6.0">Update Razor Pages </a>
6. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/search?view=aspnetcore-6.0">Add Search</a>
7. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/new-field?view=aspnetcore-6.0">Add a new field</a>
8. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/validation?view=aspnetcore-6.0">Add validation</a>

---
class: dark middle
name:mvc
# Hosting Models
> Model View Controller (MVC)

---
### Model View Controller (MVC)
# Schemantic
<img src="images/client-server.svg" width="75%" class="center">
1. Client sends a HTTP Request for a specific page `/[controller/action]`
2. Server processes the request
    - `[controller]` is found in the `controller` folder.
    - Uses the method of the `[controller]` to handle the request.
    - `[controller]` looks for a `View` in the `Views/[controller]` folder.
    - `[View.cshtml]` which consists of C# + HTML is rendered (server).
    - HTTP Response with the content of the HTML page is returned.
3. Client can interact with the `page`

---
### Model View Controller (MVC)
# > dotnet new webapp
Complete the following tutorial series:
1. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-6.0">Get started with ASP.NET</a>
2. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-controller?view=aspnetcore-6.0">Add a controller</a>
3. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-view?view=aspnetcore-6.0">Add a view</a>
4. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-model?view=aspnetcore-6.0">Add a model</a>
5. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/working-with-sql?view=aspnetcore-6.0">Work with a database</a>
6. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/controller-methods-views?view=aspnetcore-6.0">Controller actions and views</a>
7. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/search?view=aspnetcore-6.0">Add search</a>
8. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/new-field?view=aspnetcore-6.0">Add a new field</a>
9. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/validation?view=aspnetcore-6.0">Add validation</a>
10. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/details?view=aspnetcore-6.0">Examine Details and Delete</a>


---
class: dark middle
name:web-api
# Hosting Models
> Web API

---
### Web API
# Schemantic
<img src="images/client-server.svg" width="75%" class="center">
1. Client sends a HTTP Request to a specific route `api/[controller/action]`
2. Server processes the request
    - `[controller]` is found in the `controller` folder.
    - Uses the method of the `[controller]` to handle the request.
    - `[controller]` does not render a `View` but returns `JSON|XML|... `
    - HTTP Response with the `JSON|XML|...` data is returned.
3. Client can view the response in cURL|Postman|Swagger

---
### Web API
# > dotnet new webapi
More in Chapter 7 - Ain't no REST for the wicked

However:
- The template is almost the same as the MVC template. 
- If you like to take a peek at the template, run:
```
dotnet new webapi
```

---
class: dark middle
name:blazor-wasm
# Hosting Models
> Blazor **W**eb **As**se**m**bly


---
### Blazor **W**eb **As**se**m**bly
# Schemantic
<img src="images/client-server.svg" width="75%" class="center">
- Blazor WASM is different than the other project templates.
- Blazor only **takes care of the client side of things**. 
- In fact Blazor can be hosted as a **static html page**.
- Once the DLL's and .NET runtime are downloaded to the browser, Blazor runs in the **browser's sandbox**.
- Combined with a Web API, the client can fetch data from the server. 

---
### Blazor **W**eb **As**se**m**bly
# > dotnet new blazorwasm
Complete the following tutorial:
1. <a target="_blank" href="https://dotnet.microsoft.com/learn/aspnet/blazor-tutorial/intro">Build your first Blazor app. (10 mins.)</a>
> The tutorial is meant to give you a sneak peek at 
>
> Chapter 6 - Suit up wear a Blazor.

---
class: dark middle
name:blazor-server
# Hosting Models
> Blazor Server

---
### Blazor Server
# Schemantic
<img src="images/client-server.svg" width="75%" class="center">
- Blazor Server is different than the other project templates (Hybrid).
- Blazor Server **does not download any code to the browser**.
- Uses a Web Socket connection through SignalR.
- Cannot run without an active internet connection.
- Interactions are send to the server and a HTML diff is send back to the client.

> More information can be found [here](https://docs.microsoft.com/en-us/aspnet/core/blazor/hosting-models?view=aspnetcore-6.0)
>
> We won't be creating a Blazor Server application in this course, we'll use the WASM version.
---
class: dark middle
name:common-design-principles
# Architecture
> Architectural principles

---
### Architectural principles
# Common design principles
The principles outlined in this section can help guide you toward architectural decisions that will result in **clean**, **maintainable** applications.
- [Separation of concerns](#separation-of-concerns)
- [Encapsulation](#encapsulation)
- [Dependency inversion](#dependency-inversion)
- [Explicit dependencies](#explicit-dependencies)
- [Single responsibility](#single-responsibility)
- [**D**on't **R**epeat **Y**ourself](#dry)
- [Persistence ignorance](#persistence-ignorance)
- [**K**eep **I**t **S**imple, **S**tupid](#kiss)
- [**Y**ou **A**in't **G**onna **N**eed **I**t ](#yagni)
- [**D**omain **D**riven **D**esign](#ddd)

---
name:separation-of-concerns
### Common design principles
# Separation of concerns
Software should be **separated** based on the kinds of work it performs.

Separate core business behavior from infrastructure and user-interface logic.

Business rules and logic should reside in a **separate project**, which should not depend on other projects in the application.

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/architectural-principles#separation-of-concerns">here.</a>

---
name:encapsulation
### Common design principles
# Encapsulation
Different parts of an application should use encapsulation to **insulate** them from other parts of the application. 

Application components and layers should be able to adjust their internal implementation **without breaking their collaborators** as long as external contracts are not violated.

Achieves **loose coupling and modularity** since objects and packages can be replaced with alternative implementations so long as the same interface is maintained.

In classes, encapsulation is achieved by limiting outside access to the class's internal state.

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/architectural-principles#encapsulation">here.</a>

---
name:dependency-inversion
### Common design principles
# Dependency inversion
- The direction of dependency within the application should be in the direction of **abstraction**, **not implementation** details.
- Introduction of interfaces means that **different implementations** of these **interfaces** can easily be plugged in
<img src="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image4-2.png" width="80%" class="center"/>

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/architectural-principles#dependency-inversion">here.</a>

---
name:explicit-dependencies
### Common design principles
# Explicit dependencies
Methods and classes should **explicitly** require any collaborating objects they need in order to function correctly.

Class constructors provide an opportunity for classes to identify the things they need in order to be in a valid state and to function properly.

If you define classes that can be constructed and called, but that will only function properly if certain global or infrastructure components are in place, these classes are being **dishonest** with their clients/callers.

Construct objects that are honest and valid from the **point of creation**.

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/architectural-principles#explicit-dependencies">here.</a>


---
name:single-responsibility
### Common design principles
# Single responsibility
Objects should have only **one responsibility** and that they should have **only one reason to change**.

Helps to produce more **loosely coupled and modular** systems

Adding new classes is always **safer** than changing existing classes, since no code yet depends on the new classes

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/architectural-principles#single-responsibility">here.</a>

---
name:dry
### Common design principles
# **D**on't **R**epeat **Y**ourself
Rather than duplicating logic, encapsulate it in a programming construct. Make this construct the single authority over this behavior, and have any other part of the application that requires this behavior use the new construct.

Avoid binding together behavior that is only coincidentally repetitive. For example, just because two different constants both have the same value, that doesn't mean you should have only one constant, if conceptually they're referring to different things.

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/architectural-principles#dont-repeat-yourself-dry">here.</a>

---
name:persistence-ignorance
### Common design principles
# Persistence ignorance
- Allows the same business model to be persisted in multiple ways.
- Persistence choices might change over time.
- Some violations (in theory):
    - A required base class.
    - A required interface implementation.
    - Required parameterless constructor.
    - Properties requiring virtual keyword.
    - Persistence-specific required attributes.

We will be violating this principle in this course, since it's the lesser evil.

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/architectural-principles#persistence-ignorance">here.</a>

---
name:kiss
### Common design principles
# **K**eep **I**t **S**imple, **S**tupid
- Don't overengineer.
- Is certain complexity worthwhile?
- Complexity/flexibility comes at a cost.

> More information can be found <a target="_blank" href="https://deviq.com/principles/keep-it-simple">here.</a>

---
name:kiss
### Common design principles
# **Y**ou **A**in't **G**onna **N**eed **I**t
- Always implement things when you actually need them, never when you just foresee that you may need them.
- Features that aren't actually necessary are a huge source of waste.
- Don't write code that **might be needed**.

> More information can be found <a target="_blank" href="https://deviq.com/principles/yagni">here.</a>

---
name:ddd
### Common design principles
# **D**omain **D**riven **D**esign
- Agile approach to building software that emphasizes focusing on the business domain
- Designed to address large, complex business problems.
- Encapsulate complex behavior within the model
- When the domain model lacks behavior and merely represents the state of the system, it is said to be an anemic model, which is undesirable in DDD.

However:

DDD involves investments in modeling, architecture, and communication that may not be warranted for smaller applications or applications that are essentially just CRUD.

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/develop-asp-net-core-mvc-apps#domain-driven-design--should-you-apply-it">here.</a>


---
class: dark middle
name:common-architectures
# Architecture
> Common web application architectures

---
### Architecture
# Common architectures
- [Monolithic](#monolithic)
- [N-Layer](#n-layer)
- [Clean Architecture](#clean-architecture)

---
name:monolithic
### Common web application architectures
# Monolithic
- Entirely self-contained
- Entire logic of the application is contained in a single project
    - Presentation
    - Business
    - Data access
- Compiled to a single assembly
- Deployed as a single unit
- Pretty simple and for a lot of projects simple enough.
- When the project grows, it can get messy.

> The default when you run the following command
```
dotnet new mvc --auth Individual
```

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures#what-is-a-monolithic-application">here.</a>

---
### Monolithic
# Project Structure
<img src="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-1.png" width="100%" class="center">

<a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-1.png">Full screen</a>

---
name:n-layer
### Common web application architectures
# N-Layer
As applications grow in complexity, one way to manage that complexity is to break up the application according to its responsibilities. 

<img src="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-2.png" width="50%" class="center">


Logical layering is a common technique for improving the organization of code in enterprise software applications, and there are several ways in which code can be organized into layers.

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures#traditional-n-layer-architecture-applications">here.</a>

---
### N-Layer
# Project Structure
<img src="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-3.png" width="100%" class="center">

<a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-3.png">Full screen</a>

---
name:clean-architecture
### Common web application architectures
# Clean | Onion Architecture
- Puts the **business logic** and application model at the **center** of the application
- Instead of having business logic depend on data access or other infrastructure concerns, this **dependency is inverted**
- Achieved by **defining abstractions, or interfaces**, in the Application Core, which are then implemented by types defined in the Infrastructure layer

---
### Clean | Onion Architecture
<img src="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-7.png" width="100%" class="center">
- Dependencies flow toward the innermost circle
- Application Core has no dependencies

<a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-7.png">Full screen</a>

---
### Clean | Onion Architecture
<img src="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-9.png" width="100%" class="center">

<a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/media/image5-9.png">Full screen</a>

---
### Clean | Onion Architecture
# Organisation
Each project has clear responsibilities:
- **Application Core**
   - Business Model (Domain)
   - Business services (Managers)
   - Interfaces
- **Infrastructure**
    - Data access implementations (Repositories)
    - External Services (Mailing, SMS Sender)
- **Presentation**
    - Controllers | Views |ViewModels
    - Startup : Responsible for wiring up the implementation types to the interfaces (Dependency Injection)

> More information can be found <a target="_blank" href="https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures#clean-architecture">here.</a>

---
### Architecture
# Side note
> *"Not every problem is a nail and not every solution is a hammer."*

- Every project is different.
- You can easily over-/underengineer a project.
- Are you really going to switch | replace your data store?
- How many client applications do you have and do you maintain them yourself?
- If you make a architectural decision, prepare for the pro's and con's.
- Compromise, it can save your project.

> [Clean Architecture: The Bad Parts](https://www.jamesmichaelhickey.com/clean-architecture/) 
>
> [Should you abstract away your database?](https://enterprisecraftsmanship.com/posts/should-you-abstract-database/) 