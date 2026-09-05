# Non-Steam Activity for Lua Tools

**Non-Steam Activity** is a community-made Millennium plugin for Windows that publishes the name of a game added by **Lua Tools** as Steam activity.

It is an independent project and is not affiliated with, endorsed by, or distributed with Lua Tools.

## Features

- Detects Lua Tools games automatically; there is no hard-coded game list.
- Preserves the original Lua Tools launch process.
- Supports launches from the Steam library and Steam-created desktop shortcuts.
- Shows the running title as standard non-Steam game activity.
- Reuses one hidden helper shortcut instead of adding one shortcut per game.
- Applies the game's locally cached Steam artwork before launch.
- Clears the helper activity shortly after the real game closes.

## Requirements

- Windows 10 or newer (x64)
- [Millennium](https://docs.steambrew.app/users/getting-started/installation), installed in Steam and working
- Lua Tools, with at least one game added to the Steam library
- [.NET 8 Desktop Runtime (x64)](https://dotnet.microsoft.com/download/dotnet/8.0)
- Node.js 20 or newer, only when installing manually from this repository

## Installation

### Install from GitHub

1. Install Millennium first and open Steam once to confirm that Millennium's settings are available.
2. Install Lua Tools and the .NET 8 Desktop Runtime listed above.
3. On this GitHub page, select **Code → Download ZIP**, then extract the ZIP to a folder you can write to, such as your Desktop. You may also clone the repository with Git.
4. Open PowerShell in the extracted project folder and run:

   ```powershell
   npm install
   npm run build
   ```

   This creates `.millennium\Dist\index.js`, which Millennium needs for the plugin interface.
5. Exit Steam completely, including from the system tray.
6. Copy the **contents of the project folder once** to the Millennium plugins directory. In the standard Windows installation tested by this project, create this destination folder if it does not exist:

   ```text
   C:\Program Files (x86)\Steam\millennium\plugins\non-steam-activity
   ```

   Do **not** copy anything a second time. Just check that the first copy placed `plugin.json` at this exact path:

   ```text
   C:\Program Files (x86)\Steam\millennium\plugins\non-steam-activity\plugin.json
   ```

   Windows may ask for administrator permission because Steam is installed under `Program Files`.
7. Start Steam, open Millennium settings, enable **Non-Steam Activity**, and restart Steam once more if Millennium requests it.
8. Start a Lua Tools game normally from the Steam library or a Steam-created desktop shortcut. The profile should display the game as **In non-Steam game**.

The plugin does not replace or modify Lua Tools. Lua Tools remains responsible for launching the game; Non-Steam Activity only publishes and monitors the Steam presence.

## Building from source

```text
npm install
npm run build
dotnet publish launcher/LuaStatusMonitor.csproj -c Release
```

The frontend output is written to `.millennium/Dist/index.js`. The public package includes `launcher/LuaStatusMonitor.exe` through `plugin.json`.

## Limitations

- Steam labels this presence as **In non-Steam game**. The plugin does not impersonate official Rich Presence, ownership, achievements, cards, or official playtime.
- Games with unusual multi-process launchers may require future executable detection improvements.
- Artwork is sourced from Steam's local library cache and may be unavailable until Steam has downloaded it.
- Directly opening the game executable bypasses the Steam/Lua Tools launch hook.

## Privacy

The plugin does not collect telemetry or send personal data to third-party services. It reads local Steam and Lua Tools files required to identify the installed game and its artwork.

## Distribution and third-party components

- This repository contains the complete source for the Millennium frontend and Lua backend, as well as the C# source for `LuaStatusMonitor.exe`.
- The published executable is built from `launcher/Program.cs`. It requires the user-installed .NET 8 Runtime; no .NET runtime is redistributed with the plugin.
- Lua Tools is a user-installed prerequisite. This plugin neither bundles, modifies, nor redistributes Lua Tools or game files.
- The frontend uses Millennium's public `@steambrew` development packages. `@steambrew/client` is licensed under LGPL-2.1-only and `@steambrew/ttc` under MIT; their sources are available from the SteamClientHomebrew organization. The React type definitions used only during compilation are MIT-licensed.
- No external paid service, account, telemetry endpoint, or network API is required to use the plugin.

## License

MIT
