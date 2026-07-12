# Template BepInEx Plugin

A small BepInEx plugin template for Unity modding Casualties Unknown (or any other unity game).

## Overview

- Project: `ScavTemplate`
- Target framework: `net48`
- Purpose: Simplification
- Includes `CUCoreLib` references/usings, Harmony, Newtonsoft.Json, and Unity assembly references
- Includes a `ContentReloadManager.EnableHotReload(...)` starter pattern
- Automatically embeds `.png`, `.jpg`, and `.jpeg` files placed under `images/` or `assets/`
- Auto-detects common Steam install paths on Windows and Linux, while still allowing manual overrides in `vars.targets`

## Build

1. Open the project in Visual Studio or JetBrains Rider.
2. Build `ScavTemplate/Template.csproj`.
3. If auto-detection misses your setup, open the linked `vars.targets` file from the project and override `BaseGamePath` and/or `CUCoreLibDllPath`.

## Usage

1. Update `Plugin.cs` with your plugin GUID, name, version.
2. Update the namespace in `Plugin.cs` and `Patches.cs`.
3. Put startup-only work before `ContentReloadManager.EnableHotReload(ModGUID)`.
4. Put reloadable item/recipe/content registration inside `RegisterReloadable()` / `DoStuff()`.
5. Place embedded art in `ScavTemplate/images/` or `ScavTemplate/assets/`, then load it with `AssetLoader.LoadEmbeddedSprite(...)`.
6. Run the game with BepInEx and `CUCoreLib` installed.

## Hot Reload Notes

- `ContentReloadManager.EnableHotReload(ModGUID)` must be called from the owning plugin `Awake()`.
- Use `reloadcontent <modGuid>` in the in-game console to replay supported registrations.
- Use `autohotreload <modGuid> true` to enable watch mode.
- If Windows locks the deployed plugin DLL, set `[Hot Reload] -> <modGuid>.overridePath` in `CUCoreLib.cfg` to your rebuilt `bin\Debug` DLL.
