class: dark middle

# Enterprise Web Development C&#35;
> Come as you are

---
### Template
# Table of contents

- [Overview](#overview)
- [Auth0](#auth0)
- [Azure AAD](#azure-aad)
- [Azure AD B2C](#azure-ad-b2c)
- [Identity Server](#identity-server)

---
name:overview
### Come as you are
# Overview
The engineering design of Blazor WebAssembly is settled on OAuth and OIDC as the best option for authentication in Blazor WebAssembly apps.
Token-based authentication based on JSON Web Tokens (JWTs) was chosen over cookie-based authentication for functional and security reasons:

Follow the docs, since they change every year... <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/?view=aspnetcore-5.0">here</a> and <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/?view=aspnetcore-5.0">here</a>.

---
name:auth0
### Come as you are
# Auth0
To integrate with Auth0 you can follow the tutorial <a href="https://auth0.com/blog/securing-blazor-webassembly-apps/">here</a>.

---
name:azure-aad
### Come as you are
# Azure AAD
To integrate with Azure AAD you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-azure-active-directory?view=aspnetcore-5.0">here</a>.


---
name:azure-ad-b2c
### Come as you are
# Azure AD B2C
To integrate with Azure AD B2C you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-azure-active-directory-b2c?view=aspnetcore-5.0">here</a>.

---
name:identity-server
### Come as you are
# Identity Server
To integrate with Identity Server you can follow the tutorial <a href="https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-identity-server?view=aspnetcore-5.0&tabs=visual-studio">here</a>.

However you might want to read-up on the license changes of Identity Server and why it might or might not be suitable for your project, read it <a href="https://devblogs.microsoft.com/aspnet/asp-net-core-6-and-authentication-servers/">here</a>..





