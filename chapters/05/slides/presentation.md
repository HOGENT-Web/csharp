class: dark middle

# Enterprise Web Development C&#35;
> Chapter 5 - David's and Goliath's Architecture

---
### David's and Goliath's Architecture
# Table of contents
- [Modern Web Applications](#asp-net)
- [Hosting Models](#hosting-models)
    - [Model View Controller (MVC)](#mvc)
    - [Razor Pages](#razor-pages)
    - [Web API](#web-api)
    - [Blazor Web Assembly (WASM)](#blazor-wasm)
    - [Blazor Server](#blazor-server)
- [Architecture](#architecture)
    - [Onion Architecture](#onion)
    - [Microservices](#microservices)

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
- Builts on top of  
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
- Supported | developed by the community and Microsoft

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

> Read more [here](https://docs.microsoft.com/nl-be/dotnet/architecture/modern-web-apps-azure/choose-between-traditional-web-and-single-page-apps) or [here](https://docs.microsoft.com/en-us/aspnet/core/tutorials/choose-web-ui?view=aspnetcore-5.0)

---
### Modern Web Applications
# Support in ASP.NET
Following templates are available in ASP.NET:

<img src="images/project-templates.svg" width="100%">

> Can be generated through `dotnew new [templatename]`

---
class: dark middle
name:razor-pages
# Architecture
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
    - HTTP Response with the content of the HTML page is returned.
3. Client can interact with the `[page]`

---
### Razor Pages
# > dotnet new razor
Complete the following tutorial series:
1. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/?view=aspnetcore-5.0">Create a Razor Pages web app</a>
2. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/model?view=aspnetcore-5.0">Add a model to a Razor Pages app</a>
3. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/page?view=aspnetcore-5.0">Scaffold (generate) Razor pages</a>
4. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/sql?view=aspnetcore-5.0">Work with a database</a>
5. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/da1?view=aspnetcore-5.0">Update Razor Pages </a>
6. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/search?view=aspnetcore-5.0">Add Search</a>
7. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/new-field?view=aspnetcore-5.0">Add a new field</a>
8. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/validation?view=aspnetcore-5.0">Add validation</a>

---
class: dark middle
name:mvc
# Architecture
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
1. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-5.0">Get started with ASP.NET</a>
2. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-controller?view=aspnetcore-5.0">Add a controller</a>
3. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-view?view=aspnetcore-5.0">Add a view</a>
4. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-model?view=aspnetcore-5.0">Add a model</a>
5. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/working-with-sql?view=aspnetcore-5.0">Work with a database</a>
6. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/controller-methods-views?view=aspnetcore-5.0">Controller actions and views</a>
7. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/search?view=aspnetcore-5.0">Add search</a>
8. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/new-field?view=aspnetcore-5.0">Add a new field</a>
9. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/validation?view=aspnetcore-5.0">Add validation</a>
10. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/details?view=aspnetcore-5.0">Examine Details and Delete</a>


---
class: dark middle
name:web-api
# Architecture
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
Complete one of the following tutorials:
1. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-web-api?view=aspnetcore-5.0">Create a web API with an in-memory database.</a>
2. <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mongo-app?view=aspnetcore-5.0">Create a web API with a MongoDB.</a>
    - MongoDB experience is advised.

---
class: dark middle
name:blazor-wasm
# Architecture
> Blazor **W**eb **As**se**m**bly

---
### Blazor **W**eb **As**se**m**bly
# > dotnet new blazorwasm

---
class: dark middle
name:blazor-server
# Architecture
> Blazor Server

---
### Blazor Server
# > dotnet new blazorserver