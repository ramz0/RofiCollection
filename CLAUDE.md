# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Rofi launcher configuration based on the Catppuccin (Deathemonic) theme. It provides themed menus for app launching, running commands, power management, screenshots, and a calendar with task display.

## Structure

- `config.rasi` — Top-level rofi config: sets modi (drun/run/window), icon theme (Oranchelo), terminal (wezterm), and loads `themes/catppuccin-mocha.rasi`
- `config/` — Per-menu `.rasi` layout files (one per script). Also contains `colors.rasi` (Catppuccin Latte palette variables) and `font.rasi` (Iosevka 10)
- `themes/` — Standalone theme files; `catppuccin-mocha.rasi` is the active theme loaded by `config.rasi`
- `bin/` — Shell scripts that invoke `rofi`; each script references its own layout from `config/`
- `Rofi/` — Upstream reference repo (git submodule/clone); not actively used but contains original rasi layouts and icons

## Keybinds (configured externally, e.g. sxhkd)

| Key | Script |
|-----|--------|
| Meta+D | `bin/launcher` — app launcher (drun) |
| Meta+R | `bin/runner` — run commands |
| Meta+P | `bin/powermenu` — shutdown/reboot/lock/suspend/logout |
| Meta+S | `bin/screenshot` — select/window/screen/delay via maim+xclip |
| *(none)* | `bin/calendar` — month view + tasks from `~/.local/share/rofi-calendar-tasks` |

## How to apply/test changes

Rofi reads config files at runtime — no build step needed. To test a layout change:

```sh
# Test a specific config
rofi -show drun -config ~/.config/rofi/config/launcher.rasi

# Test a theme directly
rofi -show drun -theme ~/.config/rofi/themes/catppuccin-mocha.rasi

# Run a bin script directly
~/.config/rofi/bin/launcher
```

## Theme/color conventions

- `config/colors.rasi` defines palette variables (`BG`, `FG`, `SEL`, `ON`, `OFF`, etc.) used by the per-menu configs
- `themes/catppuccin-mocha.rasi` defines a different variable set (`bg-col`, `blue`, `fg-col`, etc.) used by the top-level launcher
- Icons use Font Awesome classic codepoints (`\uf0xx`) via Nerd Fonts — ensure a Nerd Font is installed
- Font for per-menu configs: Iosevka 10 (`config/font.rasi`); font for the main theme: JetBrainsMono Nerd Font 14

## External dependencies

`bin/powermenu`: `systemctl`, `bspc` (bspwm), `~/.local/bin/lock` (custom lock script), `mpc`, `amixer`  
`bin/screenshot`: `maim`, `xclip`, `xdotool`, `notify-send`  
`bin/calendar`: tasks file at `~/.local/share/rofi-calendar-tasks` (plain text, newline-separated)
