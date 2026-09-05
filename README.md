# Lua Tools Activity

A Millennium plugin for Windows that publishes the name of a game added by [Lua Tools](https://lua.tools/app) as Steam activity.

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
- Millennium
- Lua Tools
- .NET 8 Runtime

## Installation

Install **Lua Tools Activity** from the Millennium plugin store and restart Steam. Enable the plugin in Millennium settings if it is not enabled automatically.

Start a Lua Tools game normally from the Steam library. The plugin intercepts only the launch notification: Lua Tools remains responsible for starting the game, while the hidden helper publishes and monitors its Steam activity.

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
