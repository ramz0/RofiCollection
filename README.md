# Rofi

<div align="center">
  <p>Colección de scripts Rofi para launcher, menús y applets</p>
  
  <a href="preview/rofi.webm">
    <img src="preview/launcher.png" alt="Ver video" width="400">
  </a>
  <br><small>Click para ver video</small>
  
  <a href="https://github.com/ramz0/rofi/stargazers">
    <img src="https://img.shields.io/github/stars/ramz0/rofi?colorA=363a4f&colorB=b7bdf8&style=for-the-badge">
  </a>
  <a href="https://github.com/ramz0/rofi/issues">
    <img src="https://img.shields.io/github/issues/ramz0/rofi?colorA=363a4f&colorB=f5a97f&style=for-the-badge">
  </a>
</div>

---

## Showcase

<details>
<summary><b>Launcher</b></summary>

![Launcher](preview/launcher.png)
</details>

<details>
<summary><b>Runner</b></summary>

![Runner](preview/runner.png)
</details>

<details>
<summary><b>Powermenu</b></summary>

![Powermenu](preview/powermenu.png)
</details>

<details>
<summary><b>Screenshot</b></summary>

![Screenshot](preview/screenshot.png)
</details>

<details>
<summary><b>Wifi</b></summary>

![Wifi](preview/wifi.png)
</details>

<details>
<summary><b>Calendar</b></summary>

![Calendar](preview/calendar.png)
</details>

---

## Requisitos

### Dependencias

```sh
# Arch / Arch-based
sudo pacman -S rofi playerctl brightnessctl maim xclip xdotool networkmanager nmcli pamixer dunst

# Debian / Ubuntu
sudo apt install rofi playerctl brightnessctl maim xclip xdotool network-manager pamixer dunst

# Fedora
sudo dnf install rofi playerctl brightnessctl maim xclip xdotool NetworkManager pamixer dunst
```

### Fuentes

- **Nerd Fonts** (obligatorio para iconos)
  
  ```sh
  # Arch
  sudo pacman -S nerd-fonts-jetbrains-mono

  # Debian/Ubuntu
  sudo apt install fonts-jetbrains-mono fonts-firacode

  # Manual: https://www.nerdfonts.com/font-downloads
  ```

---

## Instalación

```sh
git clone https://github.com/ramz0/rofi.git ~/.config/rofi
```

---

## Estructura

```
rofi/
├── bin/
│   ├── launcher           # Lanzador de apps
│   ├── runner             # Ejecutar comandos
│   ├── powermenu          # Apagar/reiniciar/bloquear
│   ├── screenshot         # Capturas
│   ├── calendar           # Calendario
│   ├── wifi               # Wifi
│   ├── volume             # Volumen
│   └── volume-bar         # Popup volumen
├── config/                 # Archivos .rasi
├── icons/                  # Iconos
├── themes/                 # Temas
└── preview/               # Capturas
```

---

## Uso

| Script | Descripción |
|--------|-------------|
| [`bin/launcher`](bin/launcher) | Launcher de aplicaciones |
| [`bin/runner`](bin/runner) | Ejecutar comandos |
| [`bin/powermenu`](bin/powermenu) | Apagar/reiniciar/suspender/lock |
| [`bin/screenshot`](bin/screenshot) | Capturas de pantalla |
| [`bin/wifi`](bin/wifi) | Gestión WiFi |
| [`bin/calendar`](bin/calendar) | Calendario con tareas |

Ejecutar directamente:
```sh
~/.config/rofi/bin/launcher
~/.config/rofi/bin/powermenu
# etc...
```

---

## Atajos de teclado (Qtile)

Los scripts pueden ejecutarse desde Qtile. Más detalles en [`~/.config/qtile/shortcuts/`](https://github.com/ramz0/dotfiles/tree/main/qtile/shortcuts).

---

## Notas

- Iconos: Nerd Fonts (codepoint `\uf...`)
- Wifi: requiere `nmcli`
- Volumen: usa `pamixer`
- Calendario: lee `~/.local/share/rofi-calendar-tasks`

---

<div align="center">
  <p>Basado en el trabajo de <a href="https://github.com/mdfk15/Rofi">mdfk15/Rofi</a></p>
</div>