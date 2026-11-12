# Zoth Reality Shader & Theme Forge

Interactive WebGL/Canvas shader synthesizer and ZothOS desktop theme compiler (`v3.4.0`). Customizes five color palettes ("Zoth Realities") and compiles deterministic KDE Plasma `.colors` schemes, Alacritty `.toml` terminal configs, CSS `:root` design tokens, and `zothos/reality/v3` JSON descriptors. Zero external Python runtime dependencies.

- **Version**: `3.4.0`
- **Default Loopback Endpoint**: `http://127.0.0.1:8134`
- **Zoth Studio v2 Dossier**: [https://zoth.nullai.tech/tools/reality-shader-forge](https://zoth.nullai.tech/tools/reality-shader-forge)
- **Author**: 1nc0gn30 (`@1nc0gn30` · [https://1nc0gn30.si](https://1nc0gn30.si)) & NullAI ([https://nullai.tech](https://nullai.tech))
- **License**: MIT (100% free and open-source)

## Overview

Zoth Reality Shader & Theme Forge (`reality-shader-forge`) provides both an interactive browser workstation (`public/index.html`) and a zero-dependency Python HTTP/CLI compiler (`server.py`, `bin/reality-shader-forge`):

- **Five Zoth Realities**: `gold` (`Aurum Gold`), `emerald` (`Sovereign Emerald`), `cyan` (`Cyber Cyan`), `crimson` (`Ghost Crimson`), and `purple` (`Void Obsidian`).
- **Deterministic Output Formats**:
  - `kde` — KDE Plasma 6 `[General]`, `[Colors:Window]`, `[Colors:Selection]`, and `[Colors:Button]` RGB `.colors` scheme (`ZothOS-<reality>`).
  - `alacritty` — Alacritty TOML `[colors.primary]`, `[colors.cursor]`, `[colors.selection]`, and `[colors.normal]` configuration.
  - `css` — CSS `:root` custom properties (`--zoth-reality-primary`, `--zoth-reality-secondary`, `--zoth-reality-void`, `--zoth-reality-surface`, `--zoth-reality-text`, `--zoth-border-accent`, `--zoth-shadow-glow`).
  - `frag` — GLSL fragment shader (`.frag`) for procedural kinetic particle / reality waves.
  - `vert` — GLSL standard screen quad vertex shader (`.vert`).
  - `json` — Structured `zothos/reality/v3` palette descriptor.
- **Unicode Braille TUI (`bin/reality-shader-forge-tui`)**: Terminal sparkline (`U+2800`) telemetry and benchmark harness.

## Architecture

```text
reality-shader-forge/
├── bin/
│   ├── reality-shader-forge                # Theme compiler & status CLI
│   └── reality-shader-forge-tui            # Unicode U+2800 Braille TUI & benchmark
├── electron/main.cjs                       # Optional desktop shell wrapper (:8134)
├── public/index.html                       # Interactive shader & theme preview workstation
├── server.py                               # ThreadingTCPServer REST API & static host (:8134)
└── tests/test_reality_shader_forge.py      # Pytest compiler, CLI, & HTTP API suite
```

## Quickstart

Clone the repository and start the local server on `127.0.0.1:8134`:

```bash
git clone https://github.com/1nc0gn30/reality-shader-forge.git
cd reality-shader-forge
python3 server.py --port 8134
```

Verify service health:

```bash
curl -s http://127.0.0.1:8134/health
```

## CLI & API Usage

### CLI (`bin/reality-shader-forge`)

```bash
# Help, version, and JSON status
./bin/reality-shader-forge --help
./bin/reality-shader-forge --version
./bin/reality-shader-forge --status --json

# List all five Zoth Realities
./bin/reality-shader-forge --list
./bin/reality-shader-forge --list --json

# Compile a reality into KDE Plasma, Alacritty, CSS, or JSON
./bin/reality-shader-forge --reality emerald --format kde > ~/.local/share/color-schemes/ZothOS-emerald.colors
./bin/reality-shader-forge --reality gold --format alacritty > alacritty-gold.toml
./bin/reality-shader-forge --reality cyan --format css > reality-cyan.css
./bin/reality-shader-forge --reality crimson --format json

# Launch the HTTP workstation on port 8134
./bin/reality-shader-forge --serve 8134

# Run the Unicode Braille TUI benchmark
./bin/reality-shader-forge-tui --json
```

### ZothOS v3.4.0 Integration

On ZothOS v3.4.0 workstations, `reality-shader-forge` and `reality-shader-forge-tui` are installed on the system `PATH` and connect to the Zoth Studio v2 dossier (`https://zoth.nullai.tech/tools/reality-shader-forge`) over loopback port `127.0.0.1:8134`.

### REST API Endpoints (`127.0.0.1:8134`)

| Method | Path | Description |
| :--- | :--- | :--- |
| `GET` | `/health`, `/api/health` | Service status, version (`3.4.0`), bound port, and reality IDs |
| `GET` | `/api/status` | Online status, supported formats (`kde`, `alacritty`, `css`, `json`), and reality names |
| `GET` | `/api/realities` | Full hex palette definitions for all five Zoth Realities |
| `GET` | `/api/compile` | Compile a theme (`?reality=gold\|emerald\|cyan\|crimson\|purple&format=kde\|alacritty\|css\|json`) |

## Testing & Verification

Install `pytest` if needed and run the test suite and secret scan:

```bash
python3 -m pytest -q
./bin/reality-shader-forge --status --json
gitleaks detect --source . --no-banner --redact
```

## Support

Zoth Reality Shader & Theme Forge is 100% free and open-source with zero paywalls. Optional community support: [Buy Us a Coffee via Stripe](https://buy.stripe.com/3cIfZg27PdKo2D64Ocfw40X).

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 1nc0gn30 & NullAI ([https://nullai.tech](https://nullai.tech)).
