class: dark middle

# Enterprise Web Development C&#35;
> Suit up, wear a Blazor

---
### Suit up, wear a Blazor
# Table of contents

- [Blazor Workshop](#introduction)

---
name:introduction
### Suit up, wear a Blazor
# Introduction
- [Single Page Application Framework](https://en.wikipedia.org/wiki/Single-page_application)
- Combination of the words Browser and Razor (.NET HTML View Engine)
- Capable of rendering views on the client.
- Utilises [WebAssembly (WASM)](https://blazor-university.com/overview/what-is-webassembly/)
 - Intermediate Binary like the Common Intermediate Language(CIL)
 - C# is thus compiled to WASM
 - Does not need plugins
 - Can run in all [modern browsers](https://caniuse.com/?search=wasm)
- [Open Source on GitHub](https://github.com/dotnet/aspnetcore/tree/main/src/Components)

---
name:hosting-models
### Suit up, wear a Blazor
# Hosting Models
- Server side
- Client side (WASM)

---
### Hosting Models
# Client Side (WASM)
- Pro's
    - Runs on the client, inside the browser, so it can be deployed as **static files**.
    - Blazor Wasm **can work off-line**.
    - Can easily run as a [Progressive Web App](https://web.dev/progressive-web-apps/).
    - Server load is reduced, since it runs on the Client's machine.
- Con's
    - Is slower since .NET DLL assemblies have to be downloaded (the first time)
    - The Mono Framework interprets .NET Intermediate Language so is slower than running server-side Blazor.
    - Only works on modern browsers
    - Single threaded
    - **Not SEO friendly** by default (server-side pre-rendering)
---
name:blazor-workshop
### Suit up, wear a Blazor
# Blazor Workshop

Follow the following tutorial:
- <a href="https://github.com/dotnet-presentations/blazor-workshop" target="_blank">Blazor Workshop</a>
---
