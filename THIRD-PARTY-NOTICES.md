# Third-party notices

This file lists the third-party material that ships inside Tengwar.

## MoonSharp

The optional DCS World aircraft importer (the `dcs` folder) includes `MoonSharp.Interpreter.dll`,
MoonSharp 2.0.0, a Lua interpreter for .NET: https://github.com/xanathar/moonsharp.

- Licence: BSD 3-Clause, full text in [licenses/BSD-3-Clause-MoonSharp.txt](licenses/BSD-3-Clause-MoonSharp.txt).
- Copyright (c) 2014-2016, Marco Mastropaolo. Parts of the string library are based on KopiLua,
  Copyright (c) 2012 LoDC.
- Unmodified.

## Microsoft WebView2 SDK

`Tengwar.exe` includes the Microsoft WebView2 SDK 1.0.4258.31 (`Microsoft.Web.WebView2`), which shows
Tengwar's window. The WebView2 Runtime itself is part of Windows and is not shipped with Tengwar.

- Licence: BSD 3-Clause, full text in [licenses/BSD-3-Clause-WebView2.txt](licenses/BSD-3-Clause-WebView2.txt).
- Copyright (C) Microsoft Corporation.
- Unmodified.

## Game data

The action lists Tengwar ships (the names and ids of game commands, such as Elite Dangerous's binding
names, X4: Foundations' input ids, War Thunder's control names and the DCS World commands in each
aircraft's input files) are facts about those games, used so Tengwar can write the files the games
read. They belong to their owners: Frontier Developments, Egosoft, Gaijin Entertainment, Eagle
Dynamics and the makers of each DCS module. **Add a DCS aircraft** reads such lists from modules
installed on your own PC and does not change them.

Tengwar is not affiliated with or endorsed by any of these companies.

## Packages

NuGet and npm packages used only to build and test Tengwar keep their licences in their own packages
and are not part of what Tengwar ships.
