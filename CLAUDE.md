# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of rofi applets and themes for use on Arch Linux with Qtile. Each applet is a standalone shell script in `bin/` paired with a `.rasi` layout file in `config/`. The active global theme is set in `config.rasi` via `@theme "the-wall"`.

## Running scripts

Scripts are run directly — there is no build step:

```sh
~/.config/rofi/bin/launcher
~/.config/rofi/bin/powermenu
~/.config/rofi/bin/wifi
# etc.
```

`volume-bar` takes a positional argument: `up`, `down`, or `toggle`. It shows a transient popup and is meant to be called from keybinds rather than interactively.

To test a `.rasi` change without a keybind, invoke the script from a terminal while a display is available.

## Architecture

### Three script patterns

**Scripts using `bin/base.sh`** (`wifi`, `volume`): source the shared library and must define `options()` and `check_case()` before calling `main_menu`. `base.sh` provides `rofi_cmd`, `main_menu`, `menu_list`, and `status_options`.

**Self-contained scripts** (`powermenu`, `screenshot`, `launcher`, `runner`, `window`, `volume-bar`, `calendar`): call `rofi` directly with a hardcoded `-theme` path.

**Custom rofi modi** (`run-commands`): not launched directly — registered in `config.rasi`'s `modi:` list (as `cmds:.../bin/run-commands`) and invoked BY rofi, which calls the script with no args to list entries and with the chosen entry as `$1` to act on it. `run-commands` reads/appends its entries in the plain-text sibling file `bin/commands`, and shells out to a `confirm.rasi` dialog when adding a new command.

### Theme / color system

```
config/colors.rasi      ← raw palette (hex values + named aliases)
    ↑ imported by
config/color.rasi       ← maps palette to semantic vars (background, foreground, selected, …)
    ↑ imported by
config/*.rasi           ← per-applet layouts (iconmenu, listmenu, powermenu, …)

themes/the-wall.rasi    ← launcher/runner base theme; imports config/colors.rasi directly
    ↑ loaded by
config.rasi             ← global rofi config (@theme "the-wall")
```

To change the color scheme, edit `config/colors.rasi` (palette) or `config/color.rasi` (semantic mappings). Per-applet overrides live in their own `.rasi` files under `config/`.

To switch themes, change the `@theme` value in `config.rasi`. Available themes are in `themes/`: `the-wall`, `catppuccin-mocha`, `tokyo-night-storm`, `fullscreen`.

`config/font.rasi` sets a shared base font and is `@import`ed separately by individual layout files (`launcher.rasi`, `runner.rasi`, and the orphaned ones below) — it's not part of the colors.rasi/color.rasi chain.

### Per-applet layout files

| Script | Layout file | Notes |
|--------|-------------|-------|
| `bin/launcher` | `config/launcher.rasi` | |
| `bin/runner` | `config/runner.rasi` | |
| `bin/powermenu` | `config/powermenu.rasi` | Uses `bspc quit` for logout (BSPWM) |
| `bin/screenshot` | `config/screenshot.rasi` | Saves to `~/Pictures/Screenshots/` + clipboard |
| `bin/calendar` | `config/calendar.rasi` | |
| `bin/wifi` | `config/iconmenu.rasi` + `config/listmenu.rasi` | |
| `bin/volume` | `config/iconmenu.rasi` | |
| `bin/volume-bar` | inline `theme-str` | Transient popup, no standalone `.rasi` |
| `bin/window` | `config.rasi` (global) | Rofi built-in `window` mode |
| `bin/run-commands` | none (uses `config/confirm.rasi` for its add-command dialog) | Registered as the `cmds` modi in `config.rasi`; entries stored in `bin/commands` |

### Icons

All icons use Nerd Fonts codepoints (Unicode `\uf...`). **CaskaydiaCove Nerd Font** is used everywhere: the-wall theme, `font.rasi` (shared by launcher/runner), and iconmenu/listmenu. Icons are assigned with `printf '\ufXXX'` at the top of each script.

### Calendar tasks

`bin/calendar` reads plain-text tasks from `~/.local/share/rofi-calendar-tasks`. Create this file manually to add tasks.

### Orphaned config files

`config/` contains `.rasi` files with no matching `bin/` script: `bluetooth.rasi`, `mpd.rasi`, `network.rasi`, `networkmenu.rasi`, `askpass.rasi`, `listmenu-entry.rasi`. These are legacy or planned applets.

## Dependencies

```sh
# Runtime
rofi nmcli pamixer maim xclip xdotool dunst notify-send brightnessctl

# Optional (used by volume/calendar widgets)
playerctl mpc amixer
```

Lock screen actions in `bin/powermenu` call `~/.local/bin/lock` — this script must exist separately.
