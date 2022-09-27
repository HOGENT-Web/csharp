class: dark middle

# Enterprise Web Development C&#35;
> Installation Guide

---
### Installation Guide
# Table of contents

Code Editors (IDE)
- [Visual Studio 2022](#visual-studio)<sup> **Kinda Cross-platform**</sup>
- [Visual Studio Code](#visual-studio-code)<sup> **Cross-platform**</sup>
  - With various extensions

Data Management
- [Microsoft SQL Server Management Studio (SSMS)](#ssms)
- [Azure Data Studio](#azure-data-studio)<sup> **Cross-platform**</sup>

GIT
- [Git](#git)<sup> **Cross-platform**</sup>
- [Gitkraken](#gitkraken)<sup> **Cross-platform**</sup>
---
class: dark middle

# Installation Guide
> Code Editors

---
name:visual-studio
### Installation Guide
# Visual Studio 2022 Community 
A fullblown source code editor to manipulate code **with a local database**

1. Download Visual Studio 2022
  - <a href="https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&channel=Release&version=VS2022&source=VSLandingPage&cid=2030&passive=false" target="_blank">Download for Windows</a>
  - <a href="https://visualstudio.microsoft.com/thank-you-downloading-visual-studio-mac/?sku=communitymac&rel=17" target="_blank">Download for Apple</a>
  - Linux: Visual Studio Code + dotnet CLI is sufficient

2. Install* (for Windows)
  - Double click the installer
  - Select `ASP.NET and web development` workload
  - Select the tab `Individual components`
  - Search for `Class Designer`
  - Select `Class Designer`
  - Click `Install`

> *GIF provided in the next slide.

---
### Visual Studio 2022 Community - Installation workflow
<video controls width="100%">
  <source src="images/visual-studio-install.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

---
name:visual-studio-code
### Installation Guide
# Visual Studio Code
A lightweight source code editor to manipulate code.

1. Download Visual Studio Code
  - [Download for Windows](https://code.visualstudio.com/sha/download?build=stable&os=win32-x64-user)
  - [Download for Apple](https://code.visualstudio.com/sha/download?build=stable&os=darwin-universal)
  - [Dowload for Linux](https://code.visualstudio.com/download)

2. Install* (for Windows)
  - Double click the installer
  - Install as you normally should **but**:
      - **Select Add Open with code action... file context menu**
      - **Select Add Open with code action... directory context menu**
      - **Select Register Code as an editor for supported file types**
  - Click `Install`

> *GIF provided in the next slide.

---
### Visual Studio Code - Installation workflow
<video controls width="85%" class="center">
  <source src="images/visual-studio-code-install.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
> Your version could be a little bit different.

---
### Installation Guide
# Visual Studio Code Extensions
Some extra extensions to make our lives easier.

1. Click on the name of the extension.
2. Click `Install` on the page.

Mandatory
- <a href="https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp" target="_blank">C#</a>
- <a href="https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode" target="_blank">.NET Interactive Notebooks</a>

Optional
- <a href="https://marketplace.visualstudio.com/items?itemName=patcx.vscode-nuget-gallery" target="_blank">NuGet Gallery</a>
- <a href="https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps" target="_blank">Azure Static Web Apps</a>
- <a href="https://marketplace.visualstudio.com/items?itemName=adrianwilczynski.asp-net-core-switcher" target="_blank">ASP.NET Core Switcher</a>

---
class: dark middle

# Installation Guide
> Data Management

---
name:ssms
### Installation Guide
# SQL Server Management Studio
A fullblown data editor.

1. Download SQL Server Management Studio (SSMS)
  - [Download for Windows](https://aka.ms/ssmsfullsetup)
  - [Alternative for macOS & Linux](https://tableplus.com/)
      - You should use [Docker to run SQL Server](https://hub.docker.com/_/microsoft-mssql-server)

2. Install*
  - Double click the installer
  - Click `Install`

> *GIF not provided in the next slide, since well yeah...

---
name:azure-data-studio
### Installation Guide
# Azure Data Studio
A lightweight data editor to manipulate the database.

1. Download Azure Data Studio
  - [Download for Windows](https://go.microsoft.com/fwlink/?linkid=2170400)
  - [Download for Apple](https://go.microsoft.com/fwlink/?linkid=2169955)
  - [Download for Linux](https://docs.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio?view=sql-server-ver15#download-azure-data-studio)

2. Install* (for Windows)
  - Double click the installer
  - Install as you normally should **but**:
      - **Select Register Studio as an editor for supported file types**
  - Click `Install`

> *GIF provided in the next slide.

---
### Azure Data Studio - Installation workflow
<video controls width="85%" class="center">
  <source src="images/azure-data-studio-install.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
> Your version could be a little bit different.

---
class: dark middle

# Installation Guide
> GIT: *unpleasant person* in British English slang

---
name:git
### Installation Guide
# GIT
Source control for your code.

1. Download Git
- <a href="https://git-scm.com/download/win" target="_blank">Download for Windows</a>
- <a href="https://git-scm.com/download/mac" target="_blank">Download for Apple</a>
- <a href="https://git-scm.com/download/linux" target="_blank">Download for Linux</a>

2. Install* (for Windows)
  - Double click the installer
  - Follow the GIF on the next slide
  > Else you're gonna have a bad time...
  - Restart your PC.

> *GIF provided in the next slide.

---
### GIT - Installation workflow
<video controls width="85%" class="center">
  <source src="images/git-install.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
> Your version could be a little bit different.

---
name:gitkraken
### Installation Guide
# Gitkraken
A lightweight **G**raphical **U**ser **I**nterface for GIT

1. Download GitKraken
- <a href="https://www.gitkraken.com/download/windows64" target="_blank">Download for Windows</a>
- <a href="https://www.gitkraken.com/download/mac" target="_blank">Download for Apple</a>
- <a href="https://www.gitkraken.com/download" target="_blank">Download for Linux</a>

2. Install* (for Windows)
  - Double click the installer
  - Sign-in with your GitHub account.

> *GIF not provided in the next slide, since well yeah...

---
### Installation Guide
# Success!
You're now ready to follow the classes in this course! #yay

<img src="https://media.giphy.com/media/a0h7sAqON67nO/giphy.gif" width="90%" class="center">


