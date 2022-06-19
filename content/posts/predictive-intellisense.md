---
title: "Predictive Intellisense"
date: 2022-06-19T16:28:46+02:00
draft: false
toc: true
images:
tags:
  - powershell
  - pwsh
  - module
  - intellisense
---
## Introduction
If you are using PowerShell (pwsh) on a daily basis like me, you should take a look at enabling Predictive IntelliSense in your pwsh prompt. It was announced in [late 2020](https://devblogs.microsoft.com/powershell/announcing-psreadline-2-1-with-predictive-intellisense/) but I dont think that many people are aware and have it enabled in their pwsh profile. You can think of Predictive IntelliSense like taking tab completion to the next level.
## How to
1. Check that you have (PSReadLine) minimum version 2.1.0 installed.
```powershell
Get-Module -ListAvailable -Name PSReadLine
```
2. If not install/update it from PowerShell Gallery.
```powershell
Find-Module PSReadLine -Repository PSGallery
```
3. Import the module to your pwsh session.
```powershell
Import-Module PSReadLine
```
4. Set PSReadLine option (add it to your $profile so it will load on each new session).
```powershell
Set-PSReadLineOption -PredictionSource History -PredictionViewStyle ListView
```
## Screenshots
Find the module on PoserShell Gallery.
[![PSReadLine](/img/posts/psreadline.png)](/img/posts/psreadline.png)

Using Predictive IntelliSense from your prompt.
[![PSReadLine](/img/posts/psreadline2.png)](/img/posts/psreadline2.png)