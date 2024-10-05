class: dark middle

# Enterprise Web Development C&#35;
> Chapter 10 - Try "Password123"

> Updated to .NET 8

---
### Try "Password123"
# Table of contents
- [Introduction](#introduction)
- [Auth0](#auth0)
- Extra:
    - [Azure AAD](#azure-aad)
    - [Azure AD B2C](#azure-ad-b2c)
    - [Identity Server](#identity-server)

---
name:overview
### Try "Password123"
# Overview

This is not a security course, we're not even going to pretend it is. Learning all the aspects of security is a course all by itself.

However in this module we'll show how to setup Authentication and Authorization using Blazor WASM in combination with Auth0. 

There are multiple ways and identity providers you can use
- [Auth0](#auth0)
- [Azure AAD](#azure-aad)
- [Azure AD B2C](#azure-ad-b2c)
- [Identity Server](#identity-server)
- ... 

The problem is, these things change every year...

---
name:introduction
### Try "Password123"
# Introduction
If you're unfamiliar with JWT's, Cookies, Access Tokens, Id Tokens, RBAC, ... We highly recommend you to watch the following webinar.

<video controls width="90%">
  <source src="https://videos.ctfassets.net/2ntc334xpx65/58EF02DMi7g7MmfdW86pae/e24609566a25921060eaa9146e4360f6/Modern_Authentication_Demystified.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

&nbsp;

---
### Try "Password123"
# Webinar

You cannot google Identity without finding learning resources of Vittorio Bertocci. He is a Principal Architect for Auth0. Before Auth0, he had a lengthy career with Microsoft, where Vittorio worked with Fortune 100 and Global 100 companies, including working on Microsoft’s Azure Active Directory team as principal program manager focusing on the developer experience. In his series Learn Identity he explains Authentication and Authorization. It's really a go-to resource of you want to know more about Identity in general.

<img src="https://images.ctfassets.net/cdy7uua7fh8z/3cCv1v1rVUKWg4z9IH5kal/4826403f616a8a4e65a0b81e63341484/learn-identity-intro.jpg" width="70%" class="center"/>

<a target="_blank" href="https://auth0.com/docs/videos/learn-identity-series">Learn Identity By Vittorio Bertocci</a>

---
### Try "Password123"
# No Cookies for you

The engineering design of Blazor WebAssembly is settled on OAuth and OIDC as the best option for authentication in Blazor WebAssembly apps.
Token-based authentication based on JSON Web Tokens (JWTs) was chosen over cookie-based authentication for functional and security reasons.

However Blazor Server still uses cookies, which makes sense since everything is rendered on the Server.

> Read more about <a target="_blank" href="https://learn.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/?view=aspnetcore-8.0">Securing Blazor Apps</a>.
---
name:auth0
### Try "Password123"
# Auth0

Auth0 is a identity provider which helps us to authenticate and authorize users in our apps. More information about Auth0 can be read on <a href="https://auth0.com/" target="_blank">their website</a>. 

---
### Auth0
# Tutorial

Follow the following articles (in the correct sequence)
1. <a target="_blank" href="https://benjaminvertonghen.medium.com/role-based-acces-control-with-blazor-and-auth0-i-ffd9656e6f01">Blazor Authentication with Auth0</a>
2. <a target="_blank" href="https://benjaminvertonghen.medium.com/blazor-authorization-with-auth0-rbac-d65cd14acab2">Blazor Authorization with Auth0</a>
3. <a target="_blank" href="https://benjaminvertonghen.medium.com/blazor-with-auth0-using-the-management-api-23eda404dfef">Blazor with Auth0, using the management API</a>
4. <a target="_blank" href="https://benjaminvertonghen.medium.com/blazor-with-auth0-using-swagger-openapi-58fb1db8ba17">Blazor with Auth0, using Swagger / OpenAPI</a>

---
class: dark middle
# Chapter 10 - Try "Password123"
> Additional providers

---
name:azure-aad
### Try "Password123"
# Azure AAD
To integrate with Azure AAD you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-azure-active-directory?view=aspnetcore-8.0">here</a>.


---
name:azure-ad-b2c
### Try "Password123"
# Azure AD B2C
To integrate with Azure AD B2C you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-azure-active-directory-b2c?view=aspnetcore-8.0">here</a>.

---
name:identity-server
### Try "Password123"
# Identity Server
To integrate with Identity Server you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-identity-server?view=aspnetcore-8.0&tabs=visual-studio">here</a>.

However you might want to read-up on the license changes of Identity Server and why it might or might not be suitable for your project, read it <a href="https://devblogs.microsoft.com/aspnet/asp-net-core-6-and-authentication-servers/">here</a>...

**However:**
Since the community complained about these changes, it was reverted to a pre-duende era in ASP.NET 8. Read more about it in <a href="https://devblogs.microsoft.com/dotnet/improvements-auth-identity-aspnetcore-8/">this post</a>
