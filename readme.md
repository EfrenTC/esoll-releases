# 🎮 ESOLL

> Your all-in-one desktop companion for The Elder Scrolls Online — open source, cross-platform, and designed to be as simple as possible.

![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Tauri](https://img.shields.io/badge/Tauri-v2-blue)
![Svelte](https://img.shields.io/badge/Svelte-5-orange)
![Status](https://img.shields.io/badge/status-v0.7.0-yellow)

---

## What is ESOLL?

ESOLL is a native desktop application that brings together all the tools an ESO player needs into a single modern interface. Manage your addons, track achievements, manage screenshots, monitor system performance, install ReShade, read official news, launch the game and back up your configuration — all without needing an account, without touching game memory, and with zero risk of violating the Terms of Service.

The app works by reading and writing local game files and consuming public APIs (ESOUI, UESP, elderscrollsonline.com). It includes full **internationalization** support in **Spanish** (default) and **English**, with ~828 translation keys per language.

---

## Features

### 🔌 Addon Manager
A modern replacement for Minion. Connects to the public ESOUI API to search, install, update and uninstall addons with **automatic dependency resolution**. The manager is organized into four tabs:

**Addons tab:**
- Subtabs: Installed / Popular / All
- Sorting by downloads, name, date, author
- Pagination and real-time search
- Automatic update detection and "Update All" button (with auto-backup before updating)
- Library visibility toggle
- Ignore list to exclude addons from updates
- Custom addons path support
- Detail modal with changelog, full description and images
- Disk usage overview per installed addon

**Collections tab:**
- Named addon collections with color coding (blue, green, purple, amber, red) and descriptions
- Take snapshots of currently installed addons into a collection
- Apply a collection (installs/uninstalls addons to match the saved set)
- Import and export collections as JSON
- Duplicate and edit existing collections

**Backups tab:**
- Named snapshots of the entire `SavedVariables` folder
- Pin, rename and annotate snapshots with notes
- Diff view to compare two snapshots (which addons changed)
- Restore with a single click, export to a chosen directory
- Automatic backup before bulk addon updates

**Settings tab:**
- Custom addons path override with folder picker and auto-detect
- ESO installation status and detected paths

### 💾 SavedVariables Backup & Restore
The dedicated backup route (`/addon-backups`) offers the full feature set standalone:
- All snapshots from the Backups tab, with the same CRUD, diff and restore capabilities
- Snapshot name and notes fields for lightweight annotation
- Configuration subtab: SavedVariables path override, auto-backup toggle, max snapshot retention, scheduled backups

### 🎯 Achievement Tracker
A complete tracking system for ESO's 3000+ achievements:

- **Rich import**: ESOLL includes its own addon (`ESOLLAchievements` v1.2.0, API 101044-101048) that exports rich data per achievement: name, description, points, completed criteria, category, subcategory and icon. Can be installed/uninstalled from the Settings tab
- **Legacy import**: Compatible with `AccountAchievements.lua` as fallback (IDs only)
- **UESP Catalog**: Scrapes the UESP wiki to obtain title, description, category, icon and URL per achievement — with batch processing of 15 articles at a time. Catalog updates run asynchronously (non-blocking) with a progress bar in the Settings tab
- **Enrichment by ID**: Individual lookup of up to 200 achievements with rate-limiting
- **UESP Guide links**: Resolves and caches guide URLs per achievement with in-app HTML rendering (sanitized via `ammonia`)
- **ESO Icons**: Downloads textures from `esoicons.uesp.net` with local cache at `~/.cache/esoll/eso-icons/`
- Filtering by category, DLC, difficulty and status (all/completed/incomplete/new)
- Progress summary bar
- **First-install guidance**: Empty state shows step-by-step instructions to install the addon, export data and sync; progress counters show 0 until real data is loaded
- **In-app confirm dialogs**: Catalog refresh and destructive actions use an internal modal instead of native OS dialogs
- localStorage persistence
- Multi-account support with account selector

### 📸 Media Gallery
A full screenshot manager for ESO:

- **Automatic detection**: Finds the ESO screenshots folder on each platform; custom path override supported
- **Steam Cloud sync**: Fetches screenshots from the Steam Web API (requires Steam API key + SteamID64) alongside local files
- **Tags**: Per-screenshot tagging with 8 categories — Combat, Nature, Roleplay, Housing, Group, PvP, Outfits, Other
- **Metadata**: Character name, zone, display name, notes, favorites per screenshot
- **Albums**: Named groupings; photos can belong to multiple albums; album tiles show cover image
- **Filters**: By tag, character, zone, album, favorites or free-text search
- **Views**: Grid (masonry) and list view; sortable by date, name or size
- **Compare view**: Side-by-side A/B comparison of two screenshots
- **Lightbox**: Full-screen viewer with navigation
- **Exports**: Copy selected screenshots to a chosen directory
- **Settings**: Custom screenshots path, Steam API credentials

### 📊 Performance Metrics
Real-time system monitor focused on ESO performance:

- **Live gauges**: CPU usage (%), RAM (used / total), GPU utilization and temperature — polled at 1 Hz
- **Sparkline charts**: 60-second rolling history for CPU, RAM and GPU
- **ESO process tracking**: CPU and RAM usage attributed specifically to the running game process
- **Addon impact analysis**: Lists all installed addons by disk size with Low / Medium / High impact labels; search and toggle individual addons on/off without uninstalling
- **ReShade toggle**: Enable/disable the ReShade DLL directly from the Metrics panel
- **Performance tips**: Contextual suggestions based on ReShade status and high-impact addon count
- Hardware info summary (CPU model, RAM type/speed, VRAM)

### 🎨 ReShade Manager
Full ReShade management for ESO:

**Installation and detection:**
- Automatic detection of ReShade DLLs, version from `ReShade.ini`, active preset
- Automatic installation from reshade.me — headless on Windows, 7z extraction on Linux (auto-installs p7zip via pkexec, fallback to Wine/Proton)
- Shader pack installation and uninstallation
- vkBasalt detection (Vulkan layer on Linux)
- Clean uninstallation with backup restoration

**Community presets:**
- Gallery with 5 curated built-in presets: Neat Perfection, SweetFX HEROIC, Plushenko, ESO Real Life Graphics, Daybreak
- NexusMods metadata (endorsements, downloads, screenshots)
- One-click download, installation and activation
- Image proxy with SHA-256 disk cache

**Local presets:**
- Full CRUD: create, rename, delete, import, export
- **In-app preset editor** to edit `.ini`/`.txt` files directly
- Modification detection from original
- Origin tracking (which community preset it came from)
- Restore to built-in original

**Configuration:**
- ReShade settings editor: hotkey, performance mode, FPS overlay, clock, shader search paths

### 📰 News Reader
Official Elder Scrolls Online news aggregator:
- Scrapes `elderscrollsonline.com/es/news` with automatic age gate handling
- Up to 50 news items: tier-1 editorial + tier-2 listing + up to 4 AJAX pages
- 6-hour cache at `~/.local/share/esoll/esoll-news-cache.json`
- Text search and category filtering
- Responsive 3-column card grid
- Full article modal with rendered HTML body and image galleries
- Force refresh button and last update timestamp

### 🚀 Game Launcher
A full-featured launcher with multiple tabs:

**Launch:**
- Automatic executable detection (Live, PTS, Launcher) on all platforms
- Launch via Steam protocol on Linux, `open -a` on macOS, direct exe on Windows
- **Auto-play**: Automatic game start bypassing the login screen using xdotool (Linux), PowerShell (Windows) or AppleScript (macOS)
- **Auto-close launcher**: Closes the official Bethesda/Zenimax launcher after startup to free memory
- Active session timer
- Server maintenance warning

**Launch profiles:**
- Profiles with custom arguments
- Create, edit, delete and duplicate profiles

**Status:**
- Game and launcher process status with PID
- Process detection via `/proc` (Linux), `tasklist` (Windows), `ps` (macOS)
- Window focus with wmctrl/xdotool/PowerShell/osascript

**Statistics:**
- Session history (date, duration, client)
- Launch counter and total playtime
- Tracking toggle and stats clearing

**Server status:**
- Real-time status of 6 servers: PC EU/NA, PS EU/NA, Xbox EU/NA
- Status badges (up/down/unknown)

**Scheduled launch:**
- Schedule future launches with date/time picker and labels

**Maintenance:**
- Game file integrity verification (missing, empty, corrupt files, spot-check SHA-256)
- Repair via Steam (`steam://validate/306130`)
- Contextual guidance for Steam installs where certain managed files appear missing

### ⚙️ General Settings
- **Language**: Spanish / English with instant switching
- **Theme**: Light / Dark
- **Font size**: Small / Medium / Large
- **Font family**: Inter (default), Cinzel (Gold Road), IM Fell English SC (Necrom)
- **Modules**: Toggle individual app features on/off; minimum one module must remain active
- **Autostart**: Auto-start with the operating system (via `tauri-plugin-autostart`)
- **Updates**: In-app update check with download progress and install (via `tauri-plugin-updater`)
- Full localStorage persistence

---

## Tech Stack

| Layer | Technology |
|---|---|
| Native backend | **Tauri v2** (Rust) |
| Frontend | **SvelteKit** + **Svelte 5** (runes) + **TypeScript** |
| Styling | **Tailwind CSS** + custom `frame-*` design system |
| IPC | `@tauri-apps/api` v2 |
| HTTP (Rust) | `reqwest` 0.12 (blocking, rustls-tls, cookies, gzip) |
| Serialization | `serde` + `serde_json` |
| ZIP | `zip` 2 (deflate) for addon extraction |
| Hashing | `sha2` 0.10 (file verification, image caching) |
| Encoding | `base64` 0.22 (icons and screenshots as data URIs) |
| Dates | `chrono` 0.4 |
| System info | `sysinfo` 0.33 (CPU, RAM, GPU, process metrics) |
| HTML sanitization | `ammonia` 4 (UESP guide HTML) |
| URL parsing | `url` 2 |
| System directories | `dirs-next` 2.0 |
| Native dialogs | `tauri-plugin-dialog` |
| Open URLs | `tauri-plugin-opener` |
| Autostart | `tauri-plugin-autostart` |
| In-app updates | `tauri-plugin-updater` |
| Addon data | ESOUI public API (`api.mmoui.com`) |
| Achievement data | UESP wiki scraping + custom addon |
| ESO icons | `esoicons.uesp.net` with local cache |
| News | `elderscrollsonline.com` scraping |
| Screenshots (cloud) | Steam Web API |
| Builds | Community-contributed static JSON in repository |

Tauri was chosen over Electron because it produces native binaries for all three platforms at a fraction of the size (~10MB vs ~150MB), with full local filesystem access.

---

## Architecture

```
esoll/
├── src/                          # SvelteKit frontend
│   ├── app.css                   # Global styles + frame-* design system
│   ├── app.html                  # HTML shell
│   ├── lib/
│   │   ├── index.ts              # Central barrel export
│   │   ├── app/config/           # navigation.ts (feature registry)
│   │   ├── features/             # 9 feature modules
│   │   │   ├── achievements/     # types/ + services/ + stores/ + components/
│   │   │   ├── addon-backups/
│   │   │   ├── addons/
│   │   │   ├── build-planner/    # disabled, files preserved
│   │   │   ├── launcher/
│   │   │   ├── media/            # screenshot gallery
│   │   │   ├── news/
│   │   │   ├── reshade/
│   │   │   └── updater/          # in-app update flow
│   │   └── shared/
│   │       ├── components/layout/ # AppShell, custom title bar
│   │       ├── components/        # ConfirmModal, Select (shared UI primitives)
│   │       ├── i18n/             # es + en (~828 keys each)
│   │       ├── stores/           # theme, fontSize, settings, metrics, game-update
│   │       ├── types/
│   │       └── utils/
│   └── routes/
│       ├── +layout.svelte        # Layout with AppShell
│       ├── +page.svelte          # Dashboard
│       ├── achievements/
│       ├── addon-backups/        # Standalone backups route
│       ├── addons/               # Addon manager (Addons / Collections / Backups / Settings)
│       ├── build-planner/        # Disabled
│       ├── launcher/
│       ├── media/                # Screenshot gallery
│       ├── news/
│       ├── reshade/
│       ├── settings/
│       └── api/                  # Proxy endpoints (ESOUI, UESP, icons)
├── src-tauri/                    # Rust backend
│   ├── src/
│   │   ├── main.rs
│   │   ├── lib.rs                # Command and plugin registration
│   │   └── commands/
│   │       ├── mod.rs
│   │       ├── addons.rs         # Catalog, install, uninstall, fingerprint
│   │       ├── achievements.rs   # Import, catalog, enrichment, icons, guides
│   │       ├── backups.rs        # Snapshot CRUD, diff, export
│   │       ├── builds.rs         # CP writing to SavedVariables
│   │       ├── launcher.rs       # Launch, status, verify, repair
│   │       ├── media.rs          # Screenshot scan, metadata, Steam cloud
│   │       ├── news.rs           # Scraping + cache
│   │       ├── reshade.rs        # Installation, presets, shaders, config
│   │       ├── system.rs         # Metrics (CPU/RAM/GPU), addon status, ReShade toggle
│   │       └── updater.rs        # tauri-plugin-updater wrapper
│   ├── capabilities/default.json
│   └── tauri.conf.json           # Frameless window
├── static/
│   ├── addons/ESOLLAchievements/ # Custom achievement addon (.lua + .txt)
│   ├── addons/ESOLLcp/           # CP addon (.lua + .txt)
│   └── builds/community-builds.json
└── scripts/
    ├── tauri-native.mjs          # Dev wrapper for VS Code Snap (Linux)
    └── build-achievement-translations.mjs
```

Each feature module follows a consistent pattern: `types/` → `services/` → `stores/` → `components/`, with reactive Svelte 5 rune-based stores, localStorage persistence and Tauri IPC calls.

---

## Cross-Platform Support

| Feature | Linux | Windows | macOS |
|---|---|---|---|
| ESO detection | Steam, Proton, Lutris, Flatpak, external drives | Standard paths + Registry | `~/Documents/Elder Scrolls Online` |
| Launch | `steam://run/306130` | Direct exe | `open -a` |
| Auto-play | `xdotool` | `PowerShell` | `AppleScript` |
| Process detection | `/proc` | `tasklist` | `ps aux` |
| Window focus | `wmctrl`/`xdotool` | `PowerShell` | `osascript` |
| ReShade install | 7z + Wine/Proton | Headless setup | — |
| Shader installation | `p7zip` (auto-install) | Built-in | — |
| vkBasalt | Vulkan layer detection | — | — |
| RAM type detection | `/sys/bus` | `winreg` | — |

---

## Design & UX

- **Custom title bar**: Draggable with window controls (minimize, maximize, close) using the Tauri Window API — no native decorations
- **Navigable sidebar**: SVG icons per feature, settings link at the bottom; optional per-module enable/disable from Settings
- **`frame-*` design system**: `frame-tab`, `frame-tab-active`, `frame-nav-link`, `frame-nav-link-active`, `frame-input`, `frame-sidebar`, `frame-titlebar`, `frame-divider`
- **Accent palette**: Green, Red, Blue, Yellow, Orange, Purple, Cyan — all as CSS custom properties
- **Static sidebar**: Active and inactive nav links share identical padding and margin — no layout shift when navigating between modules
- **Module system**: Features can be individually toggled on/off from Settings → Modules; the sidebar only shows active modules
- **Game update detection**: On startup, `eso64.exe` is fingerprinted — if it changed since last session, caches are invalidated and data is refreshed automatically
- **In-app updater**: Checks for new app versions, shows download progress and restarts after install
- **Dashboard**: Overview with addon status, active ReShade preset thumbnail, server status, achievement progress and latest news

---

## ToS Compliance

ESOLL only reads and writes local game files — the same thing ESO addons do. It never modifies game memory, intercepts network traffic, or touches server-side data. All functionality is within the boundaries explicitly permitted by ZeniMax's Terms of Service.

---

## Getting Started (Development)

```bash
# Prerequisites: Rust, Node.js

# Install Tauri CLI
cargo install tauri-cli

# Clone and install dependencies
git clone https://github.com/your-username/esoll
cd esoll
npm install

# Run as native desktop app (recommended)
npm run tauri dev

# Optional: web-only UI preview (without native APIs)
npm run dev
```

> For desktop features (filesystem access, native commands, local ESO detection), always test with `npm run tauri dev`.

> **Linux (VS Code Snap) note:** The `scripts/tauri-native.mjs` script automatically restores environment variables sanitized by the Snap sandbox, fixing library resolution issues during development.

---

## Contributing

Contributions are welcome in any form — bug reports, feature suggestions, new builds for the community gallery, or code. You can contribute community builds by directly editing `static/builds/community-builds.json` and opening a pull request.

This project is licensed under the **MIT License**.

---

## Community

- Reddit: [r/elderscrollsonline](https://www.reddit.com/r/elderscrollsonline)
- ESOUI Forums: [esoui.com](https://www.esoui.com)

---

*ESOLL is a community project and is not affiliated with or endorsed by ZeniMax Media or Bethesda Softworks.*
