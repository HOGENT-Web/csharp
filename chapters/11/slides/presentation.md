class: dark middle

# Enterprise Web Development C&#35;
> Chapter 11 - Headless testing

---
### Headless testing
# Table of contents
- [Introduction](#introduction)
- [Concepts](#concepts)
- [Managed vs Unmanaged dependencies](#managed-vs-unmanaged-dependencies)
- [Levels of testing](#levels-of-testing)
- [Playwright](#playwright)
- [Exercises](#exercises)
- [Solutions](#solutions)
- Extra:
    - [Literature](#literature)


---
name:overview
### Headless testing
# Overview
In this module we'll show how to start using integration tests, explain the differences compared to Unit Tests and show some pitfalls.

We'll use <a target="_blank" href="https://playwright.dev">Playwright</a>, a cross-platform tool to create end-to-end integration tests.


---
name:concepts
### Headless testing
# Concepts

Integration tests evaluate an app's components on a broader level than unit tests. Unit tests are used to test isolated software components, such as individual class methods. 

Integration tests confirm that two or more app components work together to produce an expected result, possibly including every component required to fully process a request.

These broader tests are used to test the app's infrastructure and the whole framework, often including the following components:
- Database
- File system
- Network appliances
- Request-response pipeline

---
### Headless testing
# Confidence

When testing, it's all about confidence and the time you spent on writing tests. If you write tests, it takes time to write these tests, which in essence is an extra cost to the client. 

The test suite you write needs a descent architecture, when tests are too hard to write, nobody will write any, when they're brittle (a.k.a. flaky tests) it takes a lot of time to fix the suite when introducing new features.

<img src="https://i0.wp.com/www.e4-services.com/wp-content/uploads/2017/08/Testing.png?w=900&ssl=1" class="center" width="55%"/>

---
### Headless testing
# Integration- vs Unit tests

Don't write integration tests for every possible permutation of data and file access with databases and file systems. Regardless of how many places across an app interact with databases and file systems, a focused set of read, write, update, and delete integration tests are usually capable of adequately testing database and file system components. 

Use unit tests for routine tests of method logic that interact with these components. In unit tests, the use of infrastructure fakes/mocks result in faster test execution.

**Tip:**

> When creating a test project for an app, separate the unit tests from the integration tests into different projects. This helps ensure that infrastructure testing components aren't accidentally included in the unit tests. Separation of unit and integration tests also allows control over which set of tests are run.

---
name:managed-vs-unmanaged-dependencies
### Headless testing
# Managed vs unmanaged dependencies

**Managed dependencies**

Are out-of-process dependencies that are only accessible through your application; interactions with them aren’t visible to the external world. A typical example is the application database. You own this codebase and you are responsible for it.

**Unmanaged dependencies**

Are out-of-process dependencies that are observable externally. Examples include an SMTP server and storing images in Azure BLOB Storage.
You do not own this codebase, you are just using it.

When it comes to out-of-process dependencies and mocking, the guideline is the following:

Use real instances of managed dependencies; replace unmanaged dependencies with mocks or fakes.

> You do not own Azure BLOB storage, so don't test their code.

---
### Headless testing
# Abstracting away the database
Some developers are fond of abstracting away the database, however one of the most common bugs (using Entity Framework) is forgetting an include statement. Which in essence is forgetting a `(LEFT) JOIN`.
```
.Include(x => x.NavigationProperty)
``` 

These bugs cannot be found or tested using an in-memory collection, since there are no JOINS. So the bug cannot be replicated...

While writing integration tests, you want to replicate a production environment. Changing database providers in your integration test suite is *most of the time*... **lying to yourself**.

---
name:levels-of-testing
### Headless testing
# Levels of testing
How far are you willing to go? What part of the application are you going to test keeping in mind that integration tests take longer to run, which can be "Ok" for a handfull of tests but knowing that test suites of 1k - 10k tests are not uncommon in larger projects.

- Domain Layer 
    - Can easily be unit tested
- Service Layer
    - Can be unit and integration tested
    - Does not test the request-response pipeline
- Persistence Layer
    - Meh, you don't own Entity Framework


---
### Headless testing
# Levels of testing

- Server Layer
    - Can be unit and integration tested
    - You can test the endpoints in your controllers and in fact the service layer and the domain layer in one go
- Client Layer
    - Can be unit and integration tested
    - Unit testing components can be done with <a target="_blank" href="https://bunit.dev">bUnit</a>
- Client - Server - Service - Persistence - Domain Layer
    - Test the entire thing
    - It takes longer to run the tests
    - Gives most confidence but can be brittle

> We're going with the last one. Testing the entire thing, however combinations can be used too and other approaches are not uncommon.

---
class: dark middle
name:playwright
# Chapter 11 - Headless testing
> Introducing Playwright

---
### Playwright
# Overview
<a target="_blank" href="https://playwright.dev">Playwright</a> is a framework for Web Testing and Automation. If you're familiar with <a target="_blank" href="https://www.cypress.io">Cypress</a> it's not that different.

Some key features:
- Any browser
    - Supports all modern rendering engines, including Chromium, WebKit and Firefox.
- Any platform
    - Test on Windows, Linux and macOS, locally or via the  CI/CD pipeline.
- One API
    - Use the Playwright API in TypeScript, JavaScript, Python, .NET, Java.

---
### Playwright
# Introduction
Watch the short but descriptive video, using <a target="_blank" href="https://playwright.dev">Playwright</a>

<iframe width="80%" height="60%" class="center" src="https://www.youtube.com/embed/jUnSNPxaOo0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---
### Playwright
# Example
Add the Playwright CLI as a .NET global tool (only once)
```
dotnet tool install --global Microsoft.Playwright.CLI
```
Create a new `blazor wasm hosted` project 
```
dotnet new blazorwasm --hosted -o Example
```
Create a new `nUnit` project (xUnit is barely supported)
```
cd Example
dotnet new nunit -o PlaywrightTests -n Example.PlaywrightTests
```
Add the nUnit Test project to the solution
```
dotnet sln add PlaywrightTests
```

> Continued on the next slide

---
### Playwright
# Example
Add package `Microsoft.Playwright.NUnit` to the test project 
```
cd PlaywrightTests
dotnet add package Microsoft.Playwright.NUnit --version 1.17.3
```
Build the test project and install browsers
``` 
dotnet build
playwright install
```

Open the solution `Example.sln`

---
### Playwright
# CounterTests
What we'll do is test that clicking on the Counter, actually increases the count.
Replace the contents of `UnitTest1.cs` with the following:
```
[Parallelizable(ParallelScope.Self)]
public class CounterTests : PageTest
{
    private const string ServerBaseUrl = "https://localhost:5001";
    
    [Test]
    public async Task Clicking_Counter_Updates_Count()
    {
        // Navigate to the counter page
        await Page.GotoAsync($"{ServerBaseUrl}/counter");
        // Wait until the counter page is really there.
        await Page.WaitForSelectorAsync("h1");
        // Click on counter
        await Page.ClickAsync("text=Click Me");
        // Assert
        var content = await Page.TextContentAsync("p");
        Assert.AreEqual("Current count: 1", content);
    }
}
```

---
### Playwright
# CounterTests
1. Run the server project (in the correct folder) or use VS
```
dotnet run
```
2. Run the tests (in the correct folder) or use VS
```
dotnet test
```

---
### Playwright
# Exercise
- Create a new file in the test project called `FetchDataTests`
- Create a new test based on the `CounterTests` that checks if there are 5 `li` items being rendered on the `fetchdata` page.

Tips:
- Use the documentation of <a target="_blank" href="https://playwright.dev/dotnet/docs/intro">Playwright.net</a>
- Don't forget to wait for the page to be loaded

---
### Playwright
# Flaky tests
Using selectors as the following brings some issues with it...
```
await Page.ClickAsync("text=Click Me");
```

What if you localize your app or rename the contents of the button? It's better to use test-data specific selectors and add them to the HTML/razor document, for example:
```
<button data-test-id="counter-button" class="btn btn-primary" 
        @onclick="IncrementCount">Click me</button>
```
Then you can use the following to test:
```
await Page.ClickAsync("data-test-id=counter-button");
```

---
### Playwright
# Documentation
Using the documentation you can get the hang of Playwright, some interesting ones:
- <a target="_blank" href="https://playwright.dev/dotnet/docs/codegen">Auto generate tests using the codegen</a>
- <a target="_blank" href="https://playwright.dev/dotnet/docs/debug">Debugging tools</a>
- <a target="_blank" href="https://playwright.dev/dotnet/docs/input">Using forms</a>


---
class: dark middle
name:exercises
# Chapter 11 - Headless testing
> Exercises

---
name:exercises
### Headless testing
# Exercises
Complete the following exercise:
1. <a target="_blank" href="https://github.com/HOGENT-Web/csharp-ch-11-exercise-1">Integration Tests for the SportStore</a>

---
name:solutions
### Headless testing
# Solutions
1. <a target="_blank" href="https://github.com/HOGENT-Web/csharp-ch-11-exercise-1/tree/solution">Integration Tests for the SportStore</a>

---
class: dark middle
name:literature
# Chapter 11 - Headless testing
> Extra : Literature

---
### Headless testing
# Literature

Creating a non-flaky, high confidence test suite can be hard. Here are some additional resources you can use and we highly recommend:
- Video's
    - <a target="_blank" href="https://www.pluralsight.com/courses/integration-testing-asp-dot-net-core-applications-best-practices?aid=7010a000002BWqGAAW&promo=&utm_source=non_branded&utm_medium=digital_paid_search_google&utm_campaign=EMEA_Dynamic&utm_content=&gclid=Cj0KCQiAweaNBhDEARIsAJ5hwbeqzns-7rhw1aLYRqFfW0RBonXiTyy_j5GhCUhOmIvLd2yFHnnj9FAaArbFEALw_wcB">Integration Testing ASP.NET Core Applications: Best Practices</a>
- Books
    - <a target="_blank" href="https://www.manning.com/books/unit-testing">Unit Testing Principles, Practices, and Patterns </a>
- Packages
    - <a target="_blank" href="https://bunit.dev">bUnit: a testing library for Blazor components</a>
    - <a target="_blank" href="https://nunit.org">nUnit: a testing library by Microsoft</a>
    - <a target="_blank" href="https://xunit.net">xUnit: a testing library by the community</a>
- Articles
    - <a target="_blank" href="https://enterprisecraftsmanship.com/posts/when-to-mock/">When to mock</a>
- Infographic
    - <a target="_blank" href="https://khorikov.org/files/infographic.pdf?__s=v4g93rxwb5klb8iv97jj">Infographic about testing</a>





