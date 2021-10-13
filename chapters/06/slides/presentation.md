class: dark middle

# Enterprise Web Development C&#35;
> Suit up, wear a Blazor

---
### Suit up, wear a Blazor
# Table of contents

- [Hosting Models](#hosting-models)
- [Snake Eyes](#snake-eyes)
- [Unboxing Blazor](#unboxing-blazor)
- [Deployment](#deployment)
- [Workshop](#workshop)

---
name:introduction
### Suit up, wear a Blazor
# Introduction
Blazor:
- [Single Page Application Framework](https://en.wikipedia.org/wiki/Single-page_application)
- Combination of the words Browser and Razor (.NET HTML View Engine)
- Capable of rendering views on the server and client.
- Utilises [WebAssembly (WASM)](https://blazor-university.com/overview/what-is-webassembly/) for client side rendering
 - Intermediate Binary like the Common Intermediate Language(CIL)
 - C# is compiled to WASM
 - Does not need plugins
 - Can run in all [modern browsers](https://caniuse.com/?search=wasm)
- [Open Source on GitHub](https://github.com/dotnet/aspnetcore/tree/main/src/Components)

---
name:hosting-models
### Suit up, wear a Blazor
# Hosting Models
Blazor is a web framework designed to run server-side in ASP.NET (Blazor Server) or client-side in the browser on a WebAssembly-based .NET runtime (Blazor WebAssembly). Regardless of the hosting model, **the app and component models are the same**.
- Server side
- Client side (WASM)

> In this course we'll use Web Assembly (WASM).

> Read more about hosting models <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/hosting-models?view=aspnetcore-5.0">here</a>.

---
### Hosting Models
# Client Side (WASM)
- Pro's
    - Runs on the client, inside the browser, so it can be deployed as **static files**.
    - Blazor Wasm **can work off-line**.
    - Can easily run as a [Progressive Web App(PWA)](https://web.dev/progressive-web-apps/).
    - Server load is reduced, since it runs on the client's machine.
- Con's
    - Is slower since .NET DLL assemblies have to be downloaded (the first time), cached the second time.
    - The Mono Framework interprets .NET Intermediate Language so is slower than running server-side Blazor.
    - Only works on modern browsers
    - Single threaded
    - **Not SEO friendly** by default (server-side pre-rendering)

---
### Hosting Models
# Server Side
- Pro's
    - Pre-renders HTML content before it is sent to the browser
        - **SEO friendly** by default (server-side pre-rendering)
        - Faster start-up time
    - No requirement for Web Assembly
        - Works on **older browsers** (IE 11) 
        - .NET code can be debugged in Visual Studio (code)
- Con's
    - Server sets up a in-memory session for **every client**
        - Memory and CPU are consumed by the server and not the client
        - Cannot work **without** a internet connection ([SignalR](https://docs.microsoft.com/en-us/aspnet/core/signalr/introduction?view=aspnetcore-5.0))
    - **Latency** can be an issue with events that fire frequently

> Read more about hosting models <a target="_blank" href="https://blazor-university.com/overview/blazor-hosting-models">here</a>.

---
name:snake-eyes
### Suit up, wear a Blazor
# SnakeEyes
- We'll develop a game to learn basic concepts of Blazor WASM
- Concepts of the Game:
    - 2 dices are rolled on the click of a button.
    - If the dices both show `1`, you lose.
    - If the dices are not both equal to 1 you sum up the amount
    - Play as long as you don't get Snake Eyes 🎲-🎲.

> A live version can be found <a href="https://hogent-web.github.io/csharp-ch-6-example-1/" target="_blank">here</a>

---
### SnakeEyes
# Creating the Solution
Create a new folder called `SnakeEyes`

```
mkdir SnakeEyes
cd SnakeEyes
```

Initialize the GIT Repository with a `.gitignore`

```
git init
dotnet new gitignore
```

Create a Visual Studio Solution (`.sln`)
```
dotnet new sln
```

---
### SnakeEyes
# Creating the Projects
Create a `src` folder which will contain our projects.
```
mkdir src
cd src
```

Create a Blazor Web Assembly Project called `Client`
```
dotnet new blazorwasm -o Client
```

Create a Class Library called `Domain`
```
dotnet new classlib -o Domain
```

Reference the Domain Class Library in the Client
```
dotnet add Client/Client.csproj reference Domain/Domain.csproj
```

---
### Linking the Solution
Open the Solution in Visual Studio and follow along

<img src="images/snake-eyes-project-setup.gif" width="100%" class="center">

> <a href="images/snake-eyes-project-setup.gif" target="_blank">Fullscreen</a>

---
class: dark middle

# Suit up, wear a Blazor
> 📝 Commit: Add Project Files

---
### SnakeEyes
# Run the app
You should see the following:

<img src="images/run-wasm.gif" width="100%" class="center">

> <a href="images/run-wasm.gif" target="_blank">Fullscreen</a>



---
### SnakeEyes
# Why a domain project?
Imagine, you want to re-use this super kewl game in a 
- MVC Application
- Razor Application
- Console Application
- ...

Then we can re-use the `Domain.csproj` with all it's fluffy goodness and just implement the presentation layer.

> TBH: You would probably never do this for this small app, but for bigger apps it might be a good idea.

---
### SnakeEyes
# Domain
Let's implement the following Domain
<img src="images/snake-eyes-domain.png" width="75%" class="center">

> For now all the methods can `throw new ImplementedException()`

---
### SnakeEyes - Domain
# Dice
Implement the following:
- `Constructor`
    - Set's the default value of `Dots` which is `6`.
- `Roll()`
    - Uses the `_randomizer` to set the `Dots` to a value between `1` and `6`
    > Google is your friend for this one...
- `Eye1 | Eye2`
    - Return the `Dots` (which should be private) of `_dice1` and `_dice2`.

---
### SnakeEyes - Domain
# Game
Implement the following:
- `Constructor`
    - Uses the `Initialize()` method
- `Restart()`
    - Uses the `Initialize()` method
- `Initialize()`
    - Initializes the 2 `Dice`s
- `Play()`
    - Rolls the 2 `dice`s
    - Checks if the game is finished (HasSnakeEyes)
    - If so :Adds the `Total` to the `_highscores` and resets the `Total`.
    - If not: Adds the sum of the 2 Eyes / Dices to the `Total`.


---
class: dark middle

# Suit up, wear a Blazor
> 📝 Commit: Implement Domain

---
name:unboxing-blazor
### SnakeEyes - Client
# Unboxing the Client
```
Dependencies
Properties
|- launchSettings.json 
wwwroot
|- css
|- sample-data
   |- weather.json
|- favicon.ico
|- index.html
Pages
|- Counter.razor
|- FetchData.razor
|- Index.razor
Shared
|- MainLayout.razor
|- NavMenu.razor
|- SurveyPrompt.razor
_Imports.razor
App.razor
Program.cs
```
> Read more about the structure <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/project-structure?view=aspnetcore-5.0#blazor-webassembly-1">here</a>

---
### Unboxing the Client
# launchSettings.json

<img src="images/launchsettings.png" width="75%" class="center">
- Is only used on the local development machine.
- Contains profile settings.

> Read more about profils <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/environments?view=aspnetcore-5.0#development-and-launchsettingsjson-1">here</a>

---
### Unboxing the Client
# wwwroot
- **Static assets** which are available on the Web Server.
- Can be downloaded by the client.
```
css
|- bootstrap
       |- bootstrap.min.css  // Default template is bootstrap.
|- open-iconic           // Some Fonts to use in App.css
       |- font
|- app.css               // Main CSS file 
sample-data              
|- weather.json          // Mock JSON data for the FetchData.razor page
favicon.ico              // Icon in the browser tab
index.html               // Entry point of the client.
```

---
### Unboxing the Client
# index.html
```html
<!DOCTYPE html>
<html>
<head>
    <title>Client</title>
    <base href="/" />
    <link href="css/bootstrap/bootstrap.min.css" rel="stylesheet" />
    <link href="css/app.css" rel="stylesheet" /> // Main CSS File
    <link href="Client.styles.css" rel="stylesheet" /> 
    <!-- Compiled Scoped CSS File -->
</head>
<body>
    <!-- Looks for the <App/> component and loads it here. -->
    <div id="app">Loading...</div> 
    <div id="blazor-error-ui">
        An unhandled error has occurred.
        <a href="" class="reload">Reload</a>
        <a class="dismiss">🗙</a>
    </div>
    <!-- Starts | Bootstraps the Blazor Application -->
    <script src="_framework/blazor.webassembly.js"></script> 
</body>
</html>
```

---
### Unboxing the Client
# Index.razor
```
*@page "/"

<h1>Hello, world!</h1>

Welcome to your new app.

*<SurveyPrompt Title="How is Blazor working for you?" />
```
- Is a page, specified by the `@page` directive
- Navigate to **`/`** and you'll see this page.
- Uses HTML + C# (Razor)
- Renders a component called `SurveyPrompt`

---
### Unboxing the Client
# SurveyPrompt.razor
```
<div class="alert alert-secondary mt-4" role="alert">
    <span class="oi oi-pencil mr-2" aria-hidden="true"></span>
    <strong>`@Title`</strong>
    <span class="text-nowrap">
        Please take our
        <a target="_blank" class="font-weight-bold" href="google.com">
            brief survey
        </a>
    </span>
    and tell us what you think.
</div>

*@code {
*    [Parameter] public string Title { get; set; }
*}
```
- Is not a page but a component, since there is no `@page` directive
- Has a `[Parameter]` called `Title` that can be passed by the `Parent`

> Read more about components <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-5.0"> here</a>

---
### Unboxing the Client
# Counter.razor
```
@page "/counter" 

<h1>Counter</h1>
<p>Current count: `@currentCount`</p>
<button class="btn btn-primary" `@onclick="IncrementCount"`>Click</button>
@code {
*   private int currentCount = 0;

*   private void IncrementCount()
*   {
*       currentCount++;
*   }
}
```
- The `code` block can use all the C# goodness you're used to.
- The event handler `@onclick` takes in a delegate.
    - Called the same as HTML ones but don't forget `@`

> Read more about event handling <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/components/event-handling?view=aspnetcore-5.0"> here</a>

---
### Unboxing the Client
# Counter.razor.cs
```
@page "/counter"  // Counter.razor
<h1>Counter</h1>
<p>Current count: `@currentCount`</p>
<button class="btn btn-primary" `@onclick="IncrementCount"`>Click</button>
```

```
*namespace Client.Pages // Counter.razor.cs
{
    public `partial` class Counter
    {
        private int currentCount = 0;
        void IncrementCount()
        {
            currentCount++;
        }
    }
}
```
- Code behind can be separated into it's own file (recommended)

> Read more about code-behind and partial class support <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-5.0#partial-class-support-1"> here</a>



---
### Unboxing the Client
# MainLayout.razor
```
*@inherits LayoutComponentBase
<div class="page">
    <div class="sidebar">
        `<NavMenu />`
    </div>
    <div class="main">
        <div class="top-row px-4">
            <a href="/" target="_blank" class="ml-md-auto">About</a>
        </div>
        <div class="content px-4">
            `@Body`
        </div>
    </div>
</div>
```
- MainLayout page for the Application, but can be changed / nested.
- `NavMenu` is a component with navigation links (left side)
- Renders pages inside the `@Body` 

> Read more about layouts <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/components/layouts?view=aspnetcore-5.0"> here</a>

---
### Unboxing the Client
# NavMenu.razor
```
<ul class="nav flex-column">
    <li class="nav-item px-3">
*     <NavLink class="nav-link" href="" Match="NavLinkMatch.All">
*         <span class="oi oi-home" aria-hidden="true"></span> Home
*     </NavLink>
    </li>
    <li class="nav-item px-3">
      <NavLink class="nav-link" href="counter">
          <span class="oi oi-plus" aria-hidden="true"></span> Counter
      </NavLink>
    </li>
    <li class="nav-item px-3">
      <NavLink class="nav-link" href="fetchdata">
          <span class="oi oi-list-rich" aria-hidden="true"></span> Fetch
      </NavLink>
    </li>
</ul>
```
- Take a look at the source code for <a target="_blank" href="https://github.com/dotnet/aspnetcore/blob/8b30d862de6c9146f466061d51aa3f1414ee2337/src/Components/Web/src/Routing/NavLink.cs">NavLink</a>

> Read more <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/fundamentals/routing?view=aspnetcore-5.0#navlink-and-navmenu-components-1"> here</a>

---
### Unboxing the Client
# NavMenu.razor.css
```css
h1 { 
    color: brown;
    font-family: Tahoma, Geneva, Verdana, sans-serif;
}
```
- CSS Isolation is used to not leak styles to other components.
- Any `h1` CSS declarations defined elsewhere in the app don't conflict with the `NavMenu` component's styles.
- Convention in file naming: 
  - Component.**razor**
  - Component.**razor.css**
- Used in `index.html`
  - `<link href="Client.styles.css" rel="stylesheet" />`
- Shared CSS can be put inside `wwwroot/css/app.css`


> Read more about CSS Isolation <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/components/css-isolation?view=aspnetcore-5.0"> here</a>

---
### Unboxing the Client
# App.razor
```html
<Router AppAssembly="@typeof(Program).Assembly" 
        PreferExactMatches="@true">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" 
                   DefaultLayout="@typeof(MainLayout)" />
    </Found>
    <NotFound>
        <LayoutView Layout="@typeof(MainLayout)">
            <p>Sorry, there is nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>
```
- Loaded in the index.**html**, bootstraps the App
- Layouts are defined
- 404 page is available, due to the `<Router>` component

> Read more about routing <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/fundamentals/routing?view=aspnetcore-5.0"> here</a>

---
### Unboxing the Client
# Program.cs
```
namespace Client
{
    public class Program
    {
        public static async Task Main(string[] args)
        {
            var builder = WebAssemblyHostBuilder.CreateDefault(args);
            //Link to index.html and App.razor
            builder.RootComponents.Add<App>("#app"); 
            // Possibility to add Dependency Injection
            // HttpClient in this case, refers to it's own wwwroot folder
            builder.Services.AddScoped(sp => new HttpClient 
            { 
               BaseAddress = new Uri(builder.HostEnvironment.BaseAddress) 
            });

            await builder.Build().RunAsync();
        }
    }
}
```
> Read more about Dependency Injection <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/fundamentals/dependency-injection?view=aspnetcore-5.0&pivots=webassembly"> here</a>

---
### Unboxing the Client
# FetchData.razor (1)
```
@code {
    private WeatherForecast[] forecasts;
*   protected override async Task OnInitializedAsync()
    {
*       forecasts = await Http.GetFromJsonAsync<WeatherForecast[]>
*       (
*           "sample-data/weather.json" // JSON file in wwwroot
*                                      // Can also be any (JSON) Web API
*       );
    }
    public class WeatherForecast // Data Transfer Object (DTO) Class.
    {
        public DateTime Date { get; set; }
        public int TemperatureC { get; set; }
        public string Summary { get; set; }
        public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
    }
}
```

> Read more about `OnInitializedAsync` and component lifecycles <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/fundamentals/dependency-injection?view=aspnetcore-5.0&pivots=webassembly"> here</a>

---
### FetchData.razor (2)
```razor
*@if (forecasts == null) { <p><em>Loading...</em></p> }
else
{
    <table class="table">
        <thead><tr>
            <th>Date</th>
            <th>Temp. (C)</th>
            <th>Temp. (F)</th>
        </tr></thead>
        <tbody>
*           @foreach (var forecast in forecasts)
            `{`
                <tr>
                    <td>`@forecast.Date.ToShortDateString()`</td>
                    <td>`@forecast.TemperatureC`</td>
                    <td>`@forecast.TemperatureF`</td>
                </tr>
            `}`
        </tbody>
    </table>
}
```
> Rendering Razor which is a combination of C# and HTML.

---
### Unboxing the Client
# _Imports.razor
```
@code {
@using System.Net.Http
@using System.Net.Http.Json
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.AspNetCore.Components.Web.Virtualization
@using Microsoft.AspNetCore.Components.WebAssembly.Http
@using Microsoft.JSInterop
@using Client
@using Client.Shared
```
Every folder of an app can optionally contain a template file named `_Imports.razor`. The compiler includes the directives specified in the imports file in all of the Razor templates in the same folder and recursively in all of its subfolders.

> Read more about `_Imports.razor` <a target="_blank" href="https://docs.microsoft.com/en-us/aspnet/core/blazor/components/layouts?view=aspnetcore-5.0#apply-a-layout-to-a-folder-of-components-1"> here</a>

---
### SnakeEyes - Client
# Clean-up - Unused files
Let's remove everything we don't need, remove the following files:

```
wwwroot
|- sample-data (entire folder)
   |- weather.json

Pages
|- Counter.razor
|- FetchData.razor

Shared
|- SurveyPrompt.razor
```

---
### SnakeEyes - Client
# Clean-up - Index**.razor**
Replace the contents of the `Index.razor` with following:

```
@page "/"

<h1>Snake Eyes</h1>
```

---
### SnakeEyes - Client
# Clean-up - NavMenu.razor
Remove the unused `NavLink` elements and their parent `<li>` elements, keep the rest of the file.
```
<li class="nav-item px-3">
   <NavLink class="nav-link" href="`counter`">
      <span class="oi oi-plus" aria-hidden="true"></span> Counter
   </NavLink>
</li>
<li class="nav-item px-3">
   <NavLink class="nav-link" href="`fetchdata`">
      <span class="oi oi-list-rich" aria-hidden="true"></span> Fetch data
   </NavLink>
</li>
```

---
class: dark middle

# Suit up, wear a Blazor
> 📝 Commit: Clean-up boilerplate

---
### SnakeEyes - Client
# Components
<img src="images/snake-eyes-game.gif" width="50%" class="center">

We'd like to show:
- 2 `Dice`s 🎲
- A button to play, when possible else it's disabled
- A label that shows the current score or 0 by default
- A list of highscores ordered by descending
- An `Alert` when you lose the game.
- A restart button only visible when you lost.

---
### SnakeEyes - Client
# Dice
- Create a new solution folder
- Add a Razor Component called `Dice`
<img src="images/dice.gif" width="100%" class="center">

> <a href="images/dice.gif" target="_blank">Fullscreen</a>

---
### SnakeEyes - Client
# Dice.razor
A dice is a simple `span` element which renders a `Parameter` of type `int` called `pips`.
Implement the component as follows:
```razor
<span>`@Pips`</span>
@code 
{
    [Parameter] public int Pips { get; set; }
}
```

> Since it's such a basic component, we're not using code-behind.

---
### SnakeEyes - Client
# Dice.razor.css
However we still need to style the component in it's scoped .css file
```css
span{
    border: 2px solid black;
    font-size: 2em;
    font-weight: bold;
    padding: 5px;
}
```
- The css will not be leaked to any other components. Therefore we can simply use the `span` selector.
- On compilation the `<link href="Client.styles.css" rel="stylesheet" />` file will contain the css

> See next slide to add a scoped .css file

---
### SnakeEyes - Client
# Dice.razor.css
<img src="images/dice-file-nesting.gif" width="100%" class="center">

> <a href="images/dice-file-nesting.gif" target="_blank">Fullscreen</a>

---
### SnakeEyes - Client
# Index.razor
Let's use our `Dice` component in the `Index.razor` file and pass constant values `4` en `6` as `Parameter`.

```
@page "/"
@using Client.Components // namespace of the Dice component

<h1>Snake Eyes</h1>
<div>
   `<Dice Pips="4" />`
   `<Dice Pips="6" />`
</div>
```

- The using statement can be removed if you add it to the `_Imports.razor` file.
- Remove the `@using Client.Components` and add it to `_Imports.razor`

---
### SnakeEyes - Client
# _Imports.razor
```
@using System.Net.Http
@using System.Net.Http.Json
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.AspNetCore.Components.Web.Virtualization
@using Microsoft.AspNetCore.Components.WebAssembly.Http
@using Microsoft.JSInterop
@using Client
@using Client.Shared
*@using Client.Components
```

---
### SnakeEyes - Client
# Dice
You should see the following when you run the app
<img src="images/snake-eyes-dice.png" width="100%" class="center">

> <a href="images/snake-eyes-dice.png" target="_blank">Fullscreen</a>

---
class: dark middle

# Suit up, wear a Blazor
> 📝 Commit: Implement Dice Component

---
### SnakeEyes - Client
# Game
- Let's introduce the `Game` domain object and initialize it.

```
@page "/"
*@using Domain // can also be added in Imports.razor
<h1>Snake Eyes</h1>
<div>
    <Dice Pips="4" />
    <Dice Pips="6" />
</div>
*@code{
*    private Game _game = new Game();
*}
```

> 📝 Commit: Introduce Game

---
### SnakeEyes - Client
# Game
- Show the label with the total score of the current game

```
@page "/"
@using Domain 
<h1>Snake Eyes</h1>
<div>
    <Dice Pips="4" />
    <Dice Pips="6" />
</div>
*<p>Score: @_game.Total</p>
@code{
    private Game _game = new Game();
}
```

> 📝 Commit: Show Score Label

---
### SnakeEyes - Client
# Game
- Pass the actual game parameters to the `Dice` components

```
@page "/"
@using Domain 
<h1>Snake Eyes</h1>
<div>
    <Dice Pips="`@_game.Eye1`" />
    <Dice Pips="`@_game.Eye2`" />
</div>
<p>Score: @_game.Total</p>
@code{
    private Game _game = new Game();
}
```

> 📝 Commit: Pass Parameters to Dice
---
### SnakeEyes - Client
# Game
- Add a Playbutton and hook the `@onclick` handler onto it.

```
@page "/"
@using Domain 
<h1>Snake Eyes</h1>
<div>
    <Dice Pips="@_game.Eye1" />
    <Dice Pips="@_game.Eye2" />
</div>
<p>Score: @_game.Total</p>
*<button @onclick="_game.Play">Play</button>

@code{
    private Game _game = new Game();
}
```

> 📝 Commit: Introduce Play Button

---
### SnakeEyes - Client
# Game - Exercise
- Show the highscores using 
    - 1 `<ul>` element
    - a `foreach`
    - `<li>` element(s)

It should look something like this:
<img src="images/snake-eyes-highscore.png" width="45%" class="center">

---
### SnakeEyes - Client
# Game - Solution
```
@page "/"
@using Domain 
<h1>Snake Eyes</h1>
<div>
    <Dice Pips="@_game.Eye1" />
    <Dice Pips="@_game.Eye2" />
</div>
<p>Score: @_game.Total</p>
<button @onclick="_game.Play">Play</button>
*<h3>Highscores</h3>
*<ul>
*  @foreach(int score in _game.HighScores.OrderByDescending(x => x))
*  {
*    <li>@score</li>
*  }
*</ul>
@code{
    private Game _game = new Game();
}
```

> 📝 Commit: Show Highscores

---
### SnakeEyes - Client
# Alert - Exercise 
- Show an alert when you lose the game use the following:
    - `HasSnakeEyes`
    - <a target="_blank" href="https://getbootstrap.com/docs/4.0/components/alerts/"> Bootstrap alert</a>
    - an `if` statement
    - a `button` with a click handler to `Restart()` the `Game`

---
### SnakeEyes - Client
# Alert - Solution 

```
@if (_game.HasSnakeEyes)
{
    <div class="alert alert-danger">Oeps you did it again!</div>
    <button @onclick="_game.Restart">Restart</button>
}
```

If you like you can create a component for this

```
@if (Game.HasSnakeEyes) // Alert.razor
{
    <div class="alert alert-danger">Oeps you did it again!</div>
    <button @onclick="Game.Restart">Restart</button>
}
@code{
    [Parameter] public Game Game { get; set; }
}
```

> 📝 Commit: Show Alert

---
### SnakeEyes - Client
# Disable Play - Exercise 
- Disable the play button when the game is lost, use
    - `HasSnakeEyes`
    - <a target="_blank" href="https://www.w3schools.com/tags/att_disabled.asp">The disabled attribute</a>

---
### SnakeEyes - Client
# Disable Play - Solution 
```
<button @onclick="_game.Play" `disabled="@_game.HasSnakeEyes"`>Play</button>
```

> 📝 Commit: Disable Play when lost

---
class: dark middle

# Suit up, wear a Blazor
> Deployment

---
name:deployment
### Suit up, wear a Blazor
# Deployment
Deployments can be tricky, there are multiple ways to host your awesome game online. Since Blazor WASM is actually a static website (just like HTML + JavaScript) it can be hosted on multiple platforms.
- <a target="_blank" href="https://docs.microsoft.com/en-us/azure/static-web-apps/deploy-blazor">Azure Static Web App</a> 
- <a target="_blank" href="https://swimburger.net/blog/dotnet/how-to-deploy-blazor-webassembly-to-heroku">Heroku</a> 
- <a target="_blank" href="https://swimburger.net/blog/dotnet/how-to-deploy-blazor-webassembly-to-firebase-hosting">Firebase</a> 
- GitHub Pages

> In this course we'll deploy to GitHub Pages for now.


---
name:github-pages
### Deployment
# GitHub Pages
- Publish your repository to GitHub using any tool you'd like.
- Create a workflow file, copy the contents of <a target="_blank" href="https://raw.githubusercontent.com/HOGENT-Web/csharp-ch-6-example-1/main/.github/workflows/deployment.yml">this file</a>
- Replace "csharp-ch-6-example-1" with your repository name

<img src="images/deployment-1.gif" width="80%" class="center">

> <a href="images/deployment-1.gif" target="_blank">Fullscreen</a>

---
### Deployment
# GitHub Pages
- Set the deployment branch to gh-pages once the action ran successfully
<img src="images/deployment-2.gif" width="80%" class="center">

> <a href="images/deployment-2.gif" target="_blank">Fullscreen</a>

---
<br/>
<br/>
<br/>
<img src="https://c.tenor.com/-iop9obK0IwAAAAC/i-want-to-play-a-game-play-time.gif" width="100%" class="center">

---
name:exercises
class: dark middle

# Suit up, wear a Blazor
> Exercises

---
### Suit up, wear a Blazor
# Exercises
Complete the following exercise:
1. <a href="https://github.com/HOGENT-Web/csharp-ch-6-exercise-1" target="_blank">Blackjack</a>

---
name:solutions
### Suit up, wear a Blazor
# Solution
On the following links you can find the solutions for the exercises.
1. <a href="https://github.com/HOGENT-Web/csharp-ch-6-exercise-1/tree/solution/src/Client" target="_blank">Blackjack</a>

---
name:workshop
### Suit up, wear a Blazor
# Blazor Workshop

Follow the following tutorial:
- <a href="https://github.com/dotnet-presentations/blazor-workshop" target="_blank">Blazor Workshop</a>

Note that
- The tutorial uses `dotnet new blazorwasm --hosted` which contains a Web API which also serves the Client (WASM)