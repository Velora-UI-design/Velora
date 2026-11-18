# Aurix

Roblox UI library. One Lua file, no dependencies beyond a normal executor environment.

```lua
local Aurix = loadstring(game:HttpGet("https://raw.githubusercontent.com/Velora-UI-design/Velora/main/AurixSource"))()

local win = Aurix:CreateWindow({
    Name = "Aurix",
    LoadingTitle = "Aurix",
    LoadingSubtitle = "by Naru",
    ToggleUIKeybind = "N",
    Theme = "ice",
    AutoSave = true,
})

local tab = win:CreateTab("Combat", 4483362458)

tab:CreateToggle({ Name = "Silent Aim", Flag = "silentAim", Default = false, HUD = true })
tab:CreateSlider({ Name = "FOV", Range = { 0, 360 }, Increment = 1, Default = 120 })
tab:CreateColorPicker({ Name = "Highlight", Flag = "espColor", CurrentValue = Color3.fromRGB(155, 231, 255) })
```

## Loader

The previous raw URL keeps working. `VeloraSource` is now a shim that loads `AurixSource`.

```
https://raw.githubusercontent.com/Velora-UI-design/Velora/main/AurixSource
```

## Window

`CreateWindow` takes `Name`, `LoadingTitle`, `LoadingSubtitle`, `Logo`, `ToggleUIKeybind`, `Theme`, `UIscale`, `AutoSave`, `ConfigurationSaving`, `KeySystem`, `KeySettings`, `Position`, `StartHidden`.

```
CreateTab(name, iconId)
SetTheme(name)            ice | violet | ember | mono
GetTheme()  GetThemes()
CreateHUD(cfg)            returns control object: Add, Remove, Refresh, SetVisible, IsVisible, Destroy
SetCompact(on)            folds to the titlebar, tab names move into it
IsCompact()
SetUIScale(n)             clamped 0.7 to 1.4
GetFlag(flag)
Notify(title, content, color)
SaveConfiguration()  LoadConfiguration()
SaveConfigurationTo(name)  LoadConfigurationFrom(name)
IsConfigurationDirty()
GetChangedTabs()
GetNotificationHistory()
Destroy()
```

## Tabs

`CreateTab(name, iconId)` returns a tab object with:

`CreateSectionLabel(text)` (click to fold everything below), `CreateToggle`, `CreateButton`, `CreateSlider`, `CreateDropdown`, `CreateInput`, `CreateKeybind`, `CreateColorPicker`, `CreateConfigManager`, `CreateLabel`, `CreateParagraph`, `MarkChanged`, `ClearBadge`, `GetChangedCount`.

Common options worth knowing: `Flag` for saving, `Callback`, `Tooltip`, `Default` for tab badges, `HUD = true` plus `HUDValue` to appear in the active features panel.

- Loader progress is driven per frame, so the bar fills continuously rather than in stepped tweens.
- Themes retint instances already on screen, strokes and gradient keypoints included.
- The HUD is a small draggable panel listing enabled features; clicking a line turns it off.
- Config slots are JSON files under `AurixUI_Configs`, with a dirty dot when live flags drift from the saved file.
- Session state (window position, open tab, scale, theme, fold state) lives in `AurixUI_Configs/session.json` and restores on reinject.
- Tab badges mark a tab holding a flag away from its `Default`.
- Dropdowns past 8 options get a filter field; multi-select stays open while you tick.
- Sliders accept a typed value; keybinds warn when two rows claim the same key.
- Rich paragraphs support `{c:#9be7ff}`, `{b}`, `{i}` and `{code}` tokens.
- Particle field behind the rows, one loop, idles while the window is hidden.

## Preview

`aurix-preview.html` is a standalone HTML build of the interface: animated loader, draggable window, working toggles, sliders, dropdowns, colour picker, config slots, HUD, theme switch. Download it and open it in a browser.

`aurix-hud-demo.html` is only the active features panel, isolated.

## Files

| File | What it is |
| --- | --- |
| `AurixSource` | the library |
| `VeloraSource` | shim, points at `AurixSource` |
| `aurix-preview.html` | interactive preview |
| `aurix-hud-demo.html` | HUD-only demo |
| `pmo` | archived v2 source |
| `veasd` | archived obfuscated build |
