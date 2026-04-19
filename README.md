# Rofi - Catppuccin Theme

<div align="center">
  <img src="https://raw.githubusercontent.com/catppuccin/catppuccin/main/assets/logos/exports/1544x1544_circle.png" width="100" alt="Logo"/>
  <p>Rofi launcher, menus and applets with Catppuccin Mocha theme</p>
  
  <a href="https://github.com/ramz0/rofi/stargazers">
    <img src="https://img.shields.io/github/stars/ramz0/rofi?colorA=363a4f&colorB=b7bdf8&style=for-the-badge">
  </a>
  <a href="https://github.com/ramz0/rofi/issues">
    <img src="https://img.shields.io/github/issues/ramz0/rofi?colorA=363a4f&colorB=f5a97f&style=for-the-badge">
  </a>
</div>

---

## Showcase

| Launcher | Runner |
|----------|--------|
| ![Launcher](preview/launcher.png) | ![Runner](preview/runner.png) |

| Powermenu | Screenshot |
|-----------|------------|
| ![Powermenu](preview/powermenu.png) | ![Screenshot](preview/screenshot.png) |

| Wifi | Calendar |
|------|-----------|
| ![Wifi](preview/wifi.png) | ![Calendar](preview/calendar.png) |

---

## Requisitos

### Dependencias necesarias

```sh
# Arch / Arch-based
sudo pacman -S rofi playerctl brightnessctl maim xclip xdotool networkmanager nmcli

# Debian / Ubuntu
sudo apt install rofi playerctl brightnessctl maim xclip xdotool network-manager

# Fedora
sudo dnf install rofi playerctl brightnessctl maim xclip xdotool NetworkManager
```

### Fuentes requeridas

- **Nerd Fonts** (obligatorio para los iconos)
  
  ```sh
  # Arch
  sudo pacman -S nerd-fonts-jetbrains-mono

  # Debian/Ubuntu
  sudo apt install fonts-jetbrains-mono fonts-firacode

  # O descarga manualmente: https://www.nerdfonts.com/font-downloads
  ```

### Otros

- **bspwm** (para algunos atajos)
- **dunst** (para notificaciones)
- **amixer** / **pamixer** (para control de volumen)

---

## Instalación

```sh
# Clonar el repositorio
git clone https://github.com/ramz0/rofi.git ~/.config/rofi

# Asegurate de tener las dependencias instaladas
# Ver sección de requisitos
```

---

## Estructura

```
rofi/
├── bin/                    # Scripts ejecutables
│   ├── launcher           # Lanzador de aplicaciones
│   ├── runner             # Ejecutar comandos
│   ├── powermenu          # Apagar/reiniciar/bloquear
│   ├── screenshot         # Capturas de pantalla
│   ├── calendar           # Calendario con tareas
│   ├── wifi               # Gestión de WiFi
│   ├── volume             # Control de volumen
│   └── volume-bar         # Popup de volumen
├── config/                 # Archivos .rasi
├── icons/                  # Iconos
├── themes/                 # Temas
└── preview/               # Capturas de pantalla
```

---

## Atajos de teclado

| Atajo | Acción |
|-------|--------|
| `Super + D` | Launcher (lanzador) |
| `Super + R` | Runner (ejecutar comandos) |
| `Super + P` | Powermenu |
| `Super + S` | Screenshot |
| `Super + Shift + N` | Wifi |
| `Super + D` | Calendar |
| `Super + V` | Volume |

### En Qtile

Los atajos están configurados en `~/.config/qtile/shortcuts/keys_rofi.py` y `keys_media.py`.

---

## Uso

### Launcher (lanzador de apps)

```sh
rofi -show drun -theme ~/.config/rofi/config/launcher.rasi
# o
~/.config/rofi/bin/launcher
```

### Runner (ejecutar comandos)

```sh
rofi -show run -theme ~/.config/rofi/config/runner.rasi
# o
~/.config/rofi/bin/runner
```

### Powermenu

```sh
~/.config/rofi/bin/powermenu
```

### Screenshot

```sh
~/.config/rofi/bin/screenshot
```

### Wifi

```sh
~/.config/rofi/bin/wifi
```

### Calendar

```sh
~/.config/rofi/bin/calendar
```

### Volume

```sh
~/.config/rofi/bin/volume
```

---

## Temas disponibles

- `catppuccin-mocha` (defecto)
- `catppuccin-latte`

Para cambiar el tema, editá `config.rasi` y cambiá la línea que carga el tema.

---

## Personalización

### Cambiar tema de color

Editá el archivo `themes/catppuccin-mocha.rasi` para ajustar colores.

### Agregar más items al launcher

Rofi usa `drun` que automaticamente detecta tus aplicaciones instaladas.

---

## Notas

- Los iconos usan Nerd Fonts (codepoint Nerd Font). Asegurate de tener una instalada.
- Algunos scripts requieren `nmcli` para wifi y `amixer`/`pamixer` para volumen.
- El calendario busca tareas en `~/.local/share/rofi-calendar-tasks`.

---

## Inspiración

- [Deathemonic](https://github.com/Deathemonic)
- [adi1090x/rofi](https://github.com/adi1090x/rofi)
- [Catppuccin](https://github.com/catppuccin/catppuccin)

---

<div align="center">
  <p>Hecho con ❤️</p>
</div>