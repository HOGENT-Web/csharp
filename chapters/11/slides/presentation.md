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
- [You are naming your tests wrong](#naming)
- [Exercises](#exercises)
- [Solutions](#solutions)
- Extra:
    - [Literature](#literature)


---
name:overview
### Headless testing
# Overview
In this module we'll show how to start using integration tests, explain the differences compared to Unit Tests and show some pitfalls.

We'll use <a target="_blank" href="https://playwright.dev">Playwright</a>, a new cross-platform tool to create end-to-end integration tests.


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

<img src="https://i0.wp.com/www.e4-services.com/wp-content/uploads/2017/08/Testing.png?w=900&ssl=1" class="center" width="75%"/>

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

These bugs cannot be found or tested using a In Memmory Database, since there are no JOINS. So the bug cannot be replicated...

While writing integration tests, you want to replicate a production environnment. Changing database providers in your integration test suite is *most of the time*... **lying to yourself**.

---
name:levels-of-testing
### Headless testing
# Levels of testing
How far are you willing to go? What part of the application are you going to test keeping in mind that integration tests take longer to run, which can be "Ok" for a handfull of tests but knowing that test suites of 1k - 10k tests are not uncommon in larger projects.

1. Domain Layer 
    - Can easily be united tested
2. Service Layer
    - Can be unit- and integration tested
    - Does not test the request-response pipeline
3. Persistence Layer
    - Meh, you don't own Entity Framework
4. Server Layer
    - Can be unit- and integration tested
    - You can test the endpoints in your controllers and in fact the service layer and the domain layer in one go.
5. Client Layer
    - Can be unit- and integration tested
    - Unit testing components can be done with <a target="_blank" href="https://bunit.dev">bUnit</a>
6. Client - Server - Service - Persistence - Domain Layer
    - Test the entire thing.
    - It takes longer to run the tests
    - Gives most confidence but can be brittle

> We're going with 6. Testing the entire thing, however combinations can be used too and other approaches are not uncommon.

---
class: dark middle
name:playwright
# Chapter 11 - Headless testing
> Introducing Playwright

---
### Playwright
# Overview
<a target="_blank" href="https://playwright.dev">Playwright</a> is a framework for Web Testing and Automation. If you're familiar with Cypress it's not that different.

Some key features:
- Any browser
    - Supports all modern rendering engines, including Chromium, WebKit and Firefox.
- Any platform
    - Test on Windows, Linux and macOS, locally or on CI.
- One API
    - Use the Playwright API in TypeScript, JavaScript, Python, .NET, Java.

---
### Playwright
# Introduction
Watch the short but descriptive video, using <a target="_blank" href="https://playwright.dev">Playwright</a>

<iframe width="100%" height="75%" src="https://www.youtube.com/embed/jUnSNPxaOo0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---
### Playwright
# Example
Create a new folder called `csharp-ch-11-example`
```
mkdir csharp-ch-11-example
```
Create a new `solution`
```
mkdir dotnet new sln
```
Create a new `source` folder
```
mkdir src
```
Create a new `tests` folder
```
mkdir tests
```
Add a `gitignore`
```
dotnet new gitignore
```

---
name:naming
### Headless testing
# You are naming your tests wrong.

Your tests **should** describe your system’s behavior in a way that’s understandable not only to programmers, but to **non-technical people too**.  Test against obersable behavior and not implementation detials.

Using the name of the function or method, is not very descriptive. Also think about renaming the function, the test name will not be renamed automatically...

```
[MethodUnderTest]_[Scenario]_[ExpectedResult]
```

```
[Fact]
public void IsDeliveryValid_InvalidDate_ReturnsFalse()
```

You simply can’t fit a high-level description of a complex behavior into a narrow box of such a policy. You must allow freedom of expression.

```
[Fact]
public void Delivery_with_a_past_date_is_invalid()
```

The latter version is clearly better. It reads like plain English and describes the use case under test using business terms. It conveys the system’s observable behavior.


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





