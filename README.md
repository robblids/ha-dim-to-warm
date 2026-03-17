# 💡 Dim to Warm – Home Assistant Blueprint

Automatically links brightness to color temperature – the lower the brightness, the warmer the light.

Emulates the behavior of halogen and incandescent bulbs where dimming produces a warmer glow, using any smart light with adjustable color temperature (Kelvin).

## Features

- **Multi-light support** – select any number of lights in a single automation
- **Per-light updates** – only the light whose brightness changed gets updated (no unnecessary commands)
- **Configurable Kelvin range** – set your preferred min (warmest) and max (coolest) temperatures
- **Brightness zones** – define flat zones at the bottom and top of the brightness range where Kelvin stays constant, with linear interpolation in between
- **Loop prevention** – built-in 25K deadband and 150ms stabilization delay
- **Transition control** – configurable transition time for smooth color shifts
- **Turn-on support** – optionally apply dim-to-warm when a light is first turned on
- **Future-proof** – uses `color_temp_kelvin` (not deprecated mireds)

## How it works

```
Brightness %    Color Temperature
    0% ─┐
       │  Lower zone → Min Kelvin (constant, warm)
   10% ─┘
       │
       │  Transition zone → Linear interpolation
       │
   90% ─┐
       │  Upper zone → Max Kelvin (constant, cool)
  100% ─┘
```

With defaults (min=2500K, max=4000K, lower=10%, upper=90%):
- **0–10%** brightness → 2500 K (warm, constant)
- **10–90%** brightness → 2500–4000 K (linear transition)
- **90–100%** brightness → 4000 K (cool, constant)

## Installation

### Import via Home Assistant UI

[![Open your Home Assistant instance and show the blueprint import dialog with this blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Frobblids%2Fha-dim-to-warm%2Fblob%2Fmain%2Fdim_to_warm.yaml)

### Manual installation

1. Copy `dim_to_warm.yaml` to your `config/blueprints/automation/robblids/` directory
2. Reload automations or restart Home Assistant
3. Go to **Settings → Automations & Scenes → Blueprints** and create a new automation

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| Lights | *(required)* | One or more lights to apply dim-to-warm to |
| Min Kelvin | 2500 | Warmest color temperature (used at low brightness) |
| Max Kelvin | 4000 | Coolest color temperature (used at high brightness) |
| Lower zone | 10% | Below this brightness, min Kelvin is always used |
| Upper zone | 90% | Above this brightness, max Kelvin is always used |
| Transition time | 0.5s | Duration of the color temperature change |
| Apply on turn on | Yes | Also apply when the light is first turned on |

## Requirements

- Home Assistant **2024.6.0** or later
- Lights with adjustable color temperature (Kelvin)

## License

MIT

## Author

Robin / [robblids](https://github.com/robblids)
