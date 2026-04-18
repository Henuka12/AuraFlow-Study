# AuraFlow

> **A high-fidelity desktop productivity application with a Liquid Glass UI**

[![Version](https://img.shields.io/badge/Version-1.0.0-blueviolet)](https://github.com/Henuka12/Study.app/releases)
[![React](https://img.shields.io/badge/React-19.2.4-61DAFB?logo=react)](https://react.dev/)
[![Tauri](https://img.shields.io/badge/Tauri-2.10.3-FFC131?logo=tauri)](https://tauri.app/)
[![Platform](https://img.shields.io/badge/Platform-Windows-0078D4?logo=windows)](https://github.com/Henuka12/Study.app)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

AuraFlow is a Windows desktop productivity suite built with **React + Tauri**. It brings together task management, a Pomodoro focus timer, native screen-time tracking, an ambient music dock, and collaborative comments — all wrapped in a **Liquid Glass** aesthetic with glassmorphism, parallax depth, and spring-physics animations.

---

## Features

### Liquid Glass UI & Dynamic Backgrounds

- Proprietary **Liquid Glass** design system — glassmorphism layers, Gaussian blur, spatial depth, and hardware-accelerated parallax driven by cursor movement.
- **Graphics quality toggle** — Standard or High fidelity, adjustable on the fly.
- **Dynamic backgrounds** — built-in animated presets (gradient mesh, particles, bubbles, enchanted forest, daylight) plus support for **remote MP4 streams** and **custom uploaded videos** (stored locally in IndexedDB; upload, rename, and delete without leaving the app).
- Hover-activated **navigation dock** — contextual settings panels with squishy spring animations.
- Custom **frameless window** with a drag-region title bar and smooth close / minimize / maximize actions.

### Intelligent Task Management

- Create tasks with **subtasks**, **priority levels** (High / Medium / Low), **due dates**, and **recurrence patterns**.
- **Reminder notifications** — set a reminder time per task; the app delivers a desktop notification even when minimized.
- **Voice input** — dictate a new task by voice directly in the task field.
- **Task templates** — save and reuse task structures with one click.
- **Smart search and filters** — real-time filtering by status, priority, and keyword.
- Drag-to-**reorder** tasks when in the default view.
- Focus credits — every completed Pomodoro session records minutes directly against the locked task.

### Pomodoro Focus Timer

- Classic **focus / short break / long break** cycle with configurable durations and presets.
- **Extend +5 min** without breaking concentration or resetting the cycle.
- **Task lock** — anchor the timer to a specific task; focus time is credited automatically.
- Auditory feedback (tones) and optional **desktop notifications** at session end.
- **Focus mode** — hides the timer UI to reduce distraction; toggled with the `F` key.
- Session counter and daily session history.

### Ambient Music Dock

- Curated library of **8 lofi / ambient tracks** with individual cover art.
- **Playlist picker** — browse and jump to any track.
- **Autoplay** toggle — when on, the next track plays automatically when the current one ends; when off, playback stops (preference saved across restarts).
- **Favorites** — star any track; preference persisted in localStorage.
- Full **scrubber**, elapsed / remaining time, and per-track cover artwork with a decorative landscape illustration.
- Smooth **volume slider** with persistent level.
- Reduced-motion aware — all animations respect the OS accessibility setting.

### ScreenTime Dashboard

- **Real-time foreground-window tracking** via Windows APIs (WinAPI, Rust) — monitors which application is active and for how long.
- **Heuristic categorisation** — apps are automatically grouped (Browsing, Development, Productivity, Communication, etc.).
- **App icon extraction** — renders each tracked app's native icon in the dashboard.
- Views: **Overview**, **per-App breakdown**, and **Trends** charts (hourly activity, peak hours, category splits).
- **Focus daily goal** and weekly history.
- **Pause / resume** tracking, and option to clear all data.
- **Silent startup** — launching at login runs the app hidden (system tray only) via `--hidden`; the tray icon reveals the window on demand.
- **Minimize to tray** — closing the window hides it rather than quitting.

### Collaborative Comments

- **Real-time comment panel** backed by **Firebase Firestore** — attach notes or share thoughts that sync live across instances.

### Customization

- **Accent themes** — multiple curated color schemes, switchable with live preview.
- **Light / Dark mode** — full theme support across all panels.
- **Multi-language support** — English and Sinhala (`si`) interfaces, switchable at runtime.
- **Launch on startup** — toggle autostart via `tauri-plugin-autostart`; app starts hidden in the tray.

---

## Technology Stack

| Layer | Technology |
|-------|-----------|
| UI Framework | React 19.2.4 + Vite 8 |
| Desktop Runtime | Tauri 2.10.3 (Rust) |
| Animation | Framer Motion 12 |
| Charts | Recharts 3 |
| Icons | Lucide React |
| WebGL utilities | OGL 1.0 |
| Calendar widget | React Calendar 6 |
| State & persistence | React Hooks + localStorage + IndexedDB |
| Real-time backend | Firebase Firestore (comments only) |
| Native system APIs | WinAPI via Rust — process tracking, window focus, tray, icon extraction |
| Autostart | tauri-plugin-autostart 2 |
| Single-instance lock | tauri-plugin-single-instance 2 |
| Logging | tauri-plugin-log 2 (debug builds) |
| Build tooling | Tauri CLI 2.10.1 + Vite 8 + ESLint 9 |

---

## System Requirements

### End Users

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| OS | Windows 10 64-bit | Windows 11 64-bit |
| RAM | 4 GB | 8 GB+ |
| Storage | 250 MB free | 500 MB+ free |
| Display | 800 × 600 px | 1280 × 860 px or higher |
| GPU | DirectX 11 compatible | Dedicated GPU (for blur and parallax) |
| Internet | Required | Required (Firebase comments sync) |

> AuraFlow uses Windows-native APIs (WinAPI) for screen-time tracking, system tray integration, and app icon extraction. macOS and Linux are not currently supported.

### Developers (Building from Source)

| Tool | Required Version |
|------|----------------|
| Node.js | 18.0.0 or higher |
| npm | Bundled with Node.js |
| Rust | 1.77.2 or higher (install via [rustup](https://rustup.rs/)) |
| Tauri CLI | 2.10.1 or higher |
| Git | Latest stable |

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Henuka12/Study.app.git
cd Study.app
```

### 2. Install Node.js dependencies

```bash
npm install
```

### 3. Configure environment variables

```bash
cp .env.example .env.local
```

Open `.env.local` and fill in your Firebase project credentials:

```
VITE_FIREBASE_API_KEY=...
VITE_FIREBASE_AUTH_DOMAIN=...
VITE_FIREBASE_PROJECT_ID=...
VITE_FIREBASE_STORAGE_BUCKET=...
VITE_FIREBASE_MESSAGING_SENDER_ID=...
VITE_FIREBASE_APP_ID=...
```

> The app runs without Firebase (comments panel will be inactive), but you will see console warnings without valid credentials.

### 4. Run in development mode

```bash
npm run tauri:dev
```

Starts the Vite dev server and launches the Tauri window with hot reload.

### 5. Build a production installer

```bash
npm run tauri:build
```

Produces installers under `src-tauri/target/release/bundle/`:

```
bundle/
├── msi/    AuraFlow Study_1.0.0_x64_en-US.msi
└── nsis/   AuraFlow Study_1.0.0_x64-setup.exe
```

---

## Project Structure

```
Study.app/
├── public/
│   └── Music/              # Ambient music tracks and cover art (SVG)
├── src/
│   ├── components/         # All UI components
│   │   ├── AmbientMusicDock.jsx
│   │   ├── BackgroundManager.jsx
│   │   ├── CommentsPanel.jsx
│   │   ├── PomodoroTimer.jsx
│   │   ├── ScreenTimePanel.jsx
│   │   ├── TaskInput.jsx
│   │   ├── TaskItem.jsx
│   │   ├── TitleBar.jsx
│   │   └── ...
│   ├── data/
│   │   └── musicPlaylist.js    # Ambient track definitions
│   ├── hooks/
│   │   ├── useTaskManager.js
│   │   ├── useTaskTemplates.js
│   │   └── useKeyboardShortcuts.js
│   ├── App.jsx             # Root component and main layout
│   ├── firebase.js         # Firebase initialisation
│   ├── index.css           # Global styles and Liquid Glass design tokens
│   ├── soundUtils.js       # Pomodoro audio feedback
│   ├── notificationUtils.js
│   └── translations.js     # i18n strings (English + Sinhala)
├── src-tauri/
│   ├── src/
│   │   ├── lib.rs          # All Tauri commands and screen-time engine
│   │   └── main.rs         # Tauri app entry point
│   ├── capabilities/       # IPC capability declarations
│   ├── icons/              # App icons (PNG, ICO, ICNS)
│   ├── tauri.conf.json     # Tauri configuration
│   └── Cargo.toml          # Rust dependencies
├── index.html
├── vite.config.js
└── package.json
```

---

## Security & Architecture

### Security

- **Tauri capability model** — all IPC commands are declared in `src-tauri/capabilities/`; the renderer cannot call arbitrary system APIs.
- **Content Security Policy** — strict CSP on the WebView restricts scripts, styles, and network requests to known safe origins.
- **Firebase credentials** — stored in `.env.local` (never committed); loaded at build time as `VITE_*` env vars.
- **Single-instance lock** — `tauri-plugin-single-instance` focuses the existing window if the app is launched again, preventing data races.

### Architecture

- **Single-page shell** — no client-side router; all panels are conditionally rendered overlays and flyouts within one React tree.
- **Local-first persistence** — tasks, Pomodoro state, music preferences, and themes are stored in **localStorage**; custom videos in **IndexedDB**; screen-time data in a Rust-managed JSON file in the OS app-data directory.
- **Firestore for comments only** — the app functions fully offline except for the comments panel.
- **Rust screen-time engine** — a background thread polls the foreground window every ~1 second, accumulates sessions, rolls up daily summaries, and persists them to disk; all data is exposed to the frontend via typed Tauri commands.
- **Hidden-start flow** — on autostart (`--hidden`), the Tauri window is created with `visible: false` and only shown when the user clicks the tray icon or the app is opened manually.

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `N` | Focus the new-task input |
| `S` | Focus the search bar |
| `F` | Toggle focus mode |
| `Escape` | Close the active modal or panel |

---

## Version History

| Version | Highlights |
|---------|-----------|
| **1.0.0** | Initial release — Liquid Glass UI, Pomodoro timer, task management, ambient music dock with autoplay, ScreenTime dashboard, Firebase comments, silent startup and tray |

---

## Contributing

Contributions are welcome. To get started:

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request and describe what you changed and why.

### Development standards

- Follow existing code style and Framer Motion patterns.
- Add proper cleanup in `useEffect` hooks (timeouts, listeners, object URLs).
- Keep i18n keys in sync across `en` and `si` blocks in `src/translations.js`.
- Never commit `.env.local` or any file containing Firebase credentials.

---

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

## Contact

Project: [https://github.com/Henuka12/Study.app](https://github.com/Henuka12/Study.app)

---

## Acknowledgements

- [React](https://react.dev/) — UI framework
- [Tauri](https://tauri.app/) — lightweight, secure desktop runtime
- [Framer Motion](https://www.framer.com/motion/) — advanced animation library
- [Firebase](https://firebase.google.com/) — real-time Firestore backend
- [Lucide](https://lucide.dev/) — open-source icon set
- [Recharts](https://recharts.org/) — composable chart library

---

*Built with care for focus, flow, and simplicity.*

