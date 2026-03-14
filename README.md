# RustyIsland

A Dynamic Island-inspired desktop widget for Windows, built with Tauri v2 and React. It floats at the top of your screen showing real-time system stats — and lets you kill runaway processes without ever opening Task Manager.

![Tauri](https://img.shields.io/badge/Tauri-v2-blue) ![React](https://img.shields.io/badge/React-18-61dafb) ![Rust](https://img.shields.io/badge/Rust-stable-orange)

## Features

### Process Killer

Kill any process directly from the widget. The expanded view shows the top CPU-consuming processes, each with a kill button. Click it, and the process is terminated immediately via the Rust backend using the `sysinfo` crate. The UI refreshes automatically after a kill.

### Transparency Slider

Customize how transparent the widget is. A range slider in the expanded view lets you set opacity from 10% to 100%. Your preference is saved to `localStorage` and persists across restarts.

### System Monitoring

- Real-time CPU and memory usage with animated progress bars
- Top active processes ranked by CPU consumption
- Live clock display

### Dynamic Interface

- **Compact mode** — minimal pill showing time, CPU, and memory at a glance
- **Expanded mode** — full stats, process list with kill buttons, and opacity slider
- Glass morphism design with backdrop blur
- Drag the widget anywhere on screen

### Desktop Integration

- Always-on-top, borderless, and transparent
- Positioned at top-center on launch (like iPhone's Dynamic Island)
- Skips the taskbar — stays out of the way
- Click to expand/collapse

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Rust + Tauri v2 |
| Frontend | React 18 + TypeScript |
| Styling | CSS with glass morphism and backdrop-filter |
| System Info | `sysinfo` crate |
| Build | Vite + npm |

## Getting Started

### Prerequisites

- Rust (stable)
- Node.js 18+
- Windows 10/11

### Install and Run

```bash
git clone https://github.com/iamdhakrey/rustyisland.git
cd rustyisland
npm install
npm run tauri dev
```

### Build for Production

```bash
npm run tauri build
```

Installers (`.msi` and `.exe`) are output to `src-tauri/target/release/bundle/`.

## Project Structure

```
rustyisland/
├── src/                    # React frontend
│   ├── DynamicIsland.tsx   # Main widget (process killer, opacity slider, stats)
│   ├── DynamicIsland.css   # Widget styling
│   ├── App.tsx             # Root component
│   └── App.css             # Global styles
├── src-tauri/              # Rust backend
│   ├── src/lib.rs          # Tauri commands (get_system_info, kill_process, etc.)
│   ├── Cargo.toml          # Rust dependencies
│   └── tauri.conf.json     # Tauri configuration
├── .github/workflows/      # CI/CD pipelines
│   ├── ci.yml              # Lint + type check on every push/PR
│   └── release.yml         # Auto-version bump + build + GitHub Release
└── package.json
```

## CI/CD

Automated via GitHub Actions:

- **CI** (`ci.yml`) — runs TypeScript and Rust checks on every push and PR to `main`
- **Release** (`release.yml`) — auto-bumps the patch version, builds Windows installers, and publishes a GitHub Release on every push to `main`

## License

MIT

## Acknowledgments

- Inspired by Apple's Dynamic Island
- Built with [Tauri](https://tauri.app)
- System monitoring powered by the [sysinfo](https://crates.io/crates/sysinfo) crate
