class: dark middle

# Enterprise Web Development C&#35;
> Optional: Logging

---
### Logging
# Table of contents
- [What to log](#what-to-log)
- [Default Logger](#default-logger)
- [Console.WriteLine](#console-writeline)
- [SeriLog](#serilog)
- [SeriLog ASP.NET](#serilog-aspnet)



---
name: what-to-log
class: dark middle

# Logging
> What to log

---
### Logging
# What to log

- One of the most important features in your application.
    - So is it really "optional"?
- Use logs to see what happend in production
    - Requests that failed
    - Time that a request took
    - Errors
    - ...
- Do **not** log:
    - Personal Data
    - Passwords
    - ...

---
name: console-writeline
class: dark middle

# Logging
> Console.WriteLine

---
### Logging
# Console.WriteLine

- Might be suffient for development but insufficient in production.
- Use a descent logger which can log to:
    - The console
    - Files
    - Rolling files
    - A logging server
    - Azure Diagnostics
    - ...

> You can use different packages to log to different sinks.

---
name: default-logger
class: dark middle

# Logging
> Default Logger

---
### Logging
# Default logger

- ASP.NET has a default logger `ILogger<T>`
- Since it's an interface, you can swap out and insert a logger of your choosing:
    - Default logger 
    - NLOG
    - Log4Net
    - Serilog
    - ...

Generally you should use the Microsoft `ILogger` abstractions to write log messages in your code. Using Serilog for the output lets you take advantage of the fact that Serilog and its sinks are much more powerful and flexible than the Microsoft logging providers.

> Read more about the default logger <a href="https://learn.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-6.0" target="_blank">here</a>

---
name: serilog
class: dark middle

# Logging
> Serilog

---
### Logging
# Serilog

Advantages:
- Structured Logging
- Wide Support of Sinks
- Configuration Options
- ASP.NET Integration
- ...

> Can be used in any layer of your application. Notice that `Serilog` and `Serilog.AspNetCore` are different packages that *can* work together. `Serilog` can be used anywhere you want, `Serilog.AspNetCore` only in the `Server` project.

---
### Serilog
# Structured Logging
Serilog is built with powerful structured event data in mind. Which (de)structures your objects automagically to JSON in your logs.

```cs
var pos = new { Latitude = 25, Longitude = 134 };
var ms = 34;

log.Information("Processed `{@Pos}` in `{Elapsed:000}` ms.", pos, ms);
```
Will log :
```log
09:14:22 [Information] Processed { Latitude: 25, Longitude: 134 } in 034 ms.
```
> Don't forget the **`@`** sign before `Pos`!

Basically the object is (de)serialized in JSON format. Without having to provide a `ToString()` method. 

> Read more about <a href="https://github.com/serilog/serilog/wiki/Structured-Data" target="_blank">Structured Data</a>

---
### Serilog
# Wide Support of Sinks
Multiple sinks (read: output) you can write to, for example:
- Files
- Blob Storage
- Console
- ...

> You can combine them, a console log and a file log for example.
>
> Read more about <a href="https://github.com/serilog/serilog/wiki/Provided-Sinks" target="_blank">Sinks and output</a>

---
### Serilog
# Configuration Options
- Use AppSettings.json for configuration
- Minimum Log Levels
    ```cs
    Log.Logger = new LoggerConfiguration()
        .MinimumLevel.`Debug`()
        .WriteTo.Console()
        .CreateLogger();
    ```
- **Verbose** is the noisiest level, rarely (if ever) enabled for a production app.
- **Debug** is used for internal system events that are not necessarily observable from the outside, but useful when determining how something happened.
- **Information** events describe things happening in the system that correspond to its responsibilities and functions. Generally these are the observable actions the system can perform.
- **Warning**, Wwen service is degraded, endangered, or may be behaving outside of its expected parameters, Warning level events are used.
- **Error**, when functionality is unavailable or expectations broken, an Error event is used.
- **Fatal**, the most critical level, Fatal events demand immediate attention.

> Read more about <a href="https://github.com/serilog/serilog/wiki/Writing-Log-Events" target="_blank">Log Levels</a>

---
### Serilog
# ASP.NET Integration

Create a new dotnet Web API or whatever ASP.NET Template.
```bash
dotnet new webapi -f net6.0 -o SerilogExample
```

Add Serilog Package (ASP.NET Integration)
```bash
cd SerilogExample
dotnet add package Serilog.AspNetCore
```

---
### ASP.NET Integration
Program.cs
```cs
using Serilog;
Log.Logger = new LoggerConfiguration()
    // Additional config here.
    .WriteTo.Console()
    .CreateLogger();
try
{
    Log.Information("Starting web application");
    var builder = WebApplication.CreateBuilder(args);
    builder.Host.UseSerilog(); // <-- Add this line
    // Other DI Stuff here
    var app = builder.Build();
    app.MapGet("/", () => "Hello World!");
    app.Run();
}
catch (Exception ex)
{
    Log.Fatal(ex, "Application terminated unexpectedly");
}
finally
{
    Log.CloseAndFlush();
}
```

---
### Serilog
# AppSettings

Note that `AppSettings` won't be used in the previous slide. So remove the entire "Logging" section in `AppSettings.json`

If you want to swap config on runtime without a rebuild, refer to the  <a href="https://github.com/serilog/serilog-aspnetcore/blob/dev/samples/Sample/Program.cs" target="_blank">the sample</a>.


---
### Logging
# Summary

- Logging is important.
- There are different packages, we've just taken 1 of the top ones
- Feel free to explore more about Serilog on the project website. <a href="https://serilog.net" target="_blank">Serilog.net</a>