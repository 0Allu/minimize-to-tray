# minimize-to-tray
![Users](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fmods.windhawk.net%2Fcatalog.json&query=%24.mods%5B'minimize-to-tray'%5D.details.users&label=users&style=for-the-badge)

[Official Windhawk mod repository](https://github.com/ramensoftware/windhawk-mods/tree/main/mods/minimize-to-tray.wh.cpp)

[Official Windhawk mod website](https://windhawk.net/mods/minimize-to-tray)

Right-click a window's minimize button to hide the window in the system tray.

![Minimize to tray demo](https://raw.githubusercontent.com/0Allu/minimize-to-tray/main/assets/minimize-to-tray-demo.gif)

## Usage

- Right-click a window's minimize button to send it to the tray.
- Left-click its tray icon to restore it.
- Right-click its tray icon to restore or close the window.

The application continues running while its window is hidden.

## Custom title bars

Standard Windows minimize buttons work automatically. For applications which
draw their own title bar, the mod also uses an approximate Windows-style caption
button layout. This compatibility detection is enabled by default and can be
disabled in the mod settings if it conflicts with a particular application.

Custom rules can override the generic geometry for applications with unusual
title bars, such as Steam. A custom rule uses this format:

`executable|window class|height|min right|max right`

The three numeric values are in DPI-independent pixels. `height` is the maximum
distance below the top of the window, and `min right` / `max right` define the
button's distance from the right edge.

## Excluded processes

Add executable names (for example `notepad.exe`) to the exclusion list in the
mod settings to leave their minimize button alone. Right-clicking it then
should do nothing. Matching is case-insensitive and uses
the executable file name only.

## Compatibility

Windows 10 version 1703 or later is required.

Applications running with administrator privileges are not supported when the
mod is running at normal user privileges. This is due to Windows User Interface
Privilege Isolation (UIPI).

Custom title bar compatibility detection applies only to unowned top-level
application windows. Tool windows, non-activating windows, child windows,
dialogs and owned popups are ignored.

## Safety

A tray icon is created before a window is hidden. If the tray icon cannot be
created, the window is left visible. If the mod is disabled or unloaded
normally, restore requests are posted for all windows hidden by the mod. Hidden
windows are also recovered if the dedicated mod process restarts.

If the dedicated tool process is forcibly terminated and the mod is then
disabled before it can restart, recovery code cannot run. In that unusual case,
the affected application may need to be restarted manually.
