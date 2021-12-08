class: dark middle

# Enterprise Web Development C&#35;
> Chapter 10 - Try "Password123"

---
### Try "Password123"
# Table of contents
- [Introduction](#introduction)
- [Auth0](#auth0)
- [Exercises](#exercises)
- [Solutions](#solutions)
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

The problem is, these things change every year...

---
name:introduction
### Try "Password123"
# Introduction
If you're unfamiliar with JWT's, Cookies, Access Tokens, Id Tokens, RBAC, ... We highly recommend you to watch the following webinar.

<video controls="" src="//videos.ctfassets.net/2ntc334xpx65/58EF02DMi7g7MmfdW86pae/e24609566a25921060eaa9146e4360f6/Modern_Authentication_Demystified.mp4" width="100%" height="100%" class="sc-1t7m45w-0 ktSVqQ"></video>

&nbsp;

---
### Try "Password123"
# Webinar

You cannot google Identity without finding learning resources of Vittorio Bertocci. He is a Principal Architect for Auth0. Before Auth0, he had a lengthy career with Microsoft, where Vittorio worked with Fortune 100 and Global 100 companies, including working on Microsoft’s Azure Active Directory team as principal program manager focusing on the developer experience. In his series Learn Identity he explains Authentication and Authorization. It's really a go-to resource of you want to know more about Identity in general.

<a target="_blank" href="https://auth0.com/docs/videos/learn-identity-series">Learn Identity By Vittorio Bertocci</a>

---
### Try "Password123"
# No Cookies for you

The engineering design of Blazor WebAssembly is settled on OAuth and OIDC as the best option for authentication in Blazor WebAssembly apps.
Token-based authentication based on JSON Web Tokens (JWTs) was chosen over cookie-based authentication for functional and security reasons.

However Blazor Server still uses cookies, which makes sense since everything is rendered on the Server.

> Read more about <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/?view=aspnetcore-5.0">Securing Blazor Apps</a>.
---
name:auth0
### Try "Password123"
# Auth0

Auth0 is a identity provider which helps us to authenticate and authorize users in our apps. More information about Auth0 can be read on <a href="https://auth0.com/" target="_blank">their website</a>. 

---
### Auth0
# Tutorial

Follow the following articles (in the correct sequence)
1. <a target="_blank" href="https://benjaminvertonghen.medium.com/role-based-acces-control-with-blazor-and-auth0-i-ffd9656e6f01?sk=b8c9e562c78f620d6856e737c62927aa">Blazor Authentication with Auth0</a>
2. <a target="_blank" href="https://benjaminvertonghen.medium.com/blazor-authorization-with-auth0-rbac-d65cd14acab2?sk=1c7d500ef3c2c5e224f5040a0b03f54a">Blazor Authorization with Auth0</a>
3. <a target="_blank" href="https://benjaminvertonghen.medium.com/blazor-with-auth0-using-the-management-api-23eda404dfef?sk=93888fb900875e01e7053ba53958445d">Blazor with Auth0, using the management API</a>


---
name:exercises
class: dark middle
# Chapter 10 - Try "Password123"
> Exercises

---
### Chapter 10 - Try "Password123"
# Exercises
1. <a href="https://github.com/HOGENT-Web/csharp-ch-10-exercise-1" target="_blank">SportStore with Auth0</a>

---
name: solutions
class: dark middle

# Chapter 10 - Try "Password123"
> Solutions

---
### Chapter 10 - Try "Password123"
# Solutions

1. <a href="https://github.com/HOGENT-Web/csharp-ch-10-exercise-1/tree/solution" target="_blank">SportStore with Auth0</a>

---
class: dark middle
# Chapter 10 - Try "Password123"
> Additional providers


---
name:azure-aad
### Try "Password123"
# Azure AAD
To integrate with Azure AAD you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-azure-active-directory?view=aspnetcore-5.0">here</a>.


---
name:azure-ad-b2c
### Try "Password123"
# Azure AD B2C
To integrate with Azure AD B2C you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-azure-active-directory-b2c?view=aspnetcore-5.0">here</a>.

---
name:identity-server
### Try "Password123"
# Identity Server
To integrate with Identity Server you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-identity-server?view=aspnetcore-5.0&tabs=visual-studio">here</a>.

However you might want to read-up on the license changes of Identity Server and why it might or might not be suitable for your project, read it <a href="https://devblogs.microsoft.com/aspnet/asp-net-core-6-and-authentication-servers/">here</a>..
