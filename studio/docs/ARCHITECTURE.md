# PromptTest Studio — Architecture & Technical Design

> **Document Version:** 1.1.0  
> **Confidentiality:** Proprietary — All Rights Reserved  
> **Target Framework:** Tauri v2 + Rust + React 18 + Bundled Sidecars

---

## 1. High-Level Architecture Overview

PromptTest Studio is architected as a compiled native desktop application leveraging **Tauri v2** with a **Rust** host process and a **React + Tailwind** presentation layer. 

The architecture guarantees:
1. **Zero External Dependencies:** Users install nothing; all engines and ADB tools are bundled as native sidecars.
2. **IP Protection:** No exposed HTTP ports for UI serving; rendered inside the OS WebView2 runtime with developer inspection disabled.
3. **High Performance:** Native memory footprint under 60MB RAM with instant cold-start time (< 200ms).

```
+-------------------------------------------------------------------------+
|                  PromptTest Studio Desktop (.exe)                       |
|                                                                         |
|  +-------------------------------------------------------------------+  |
|  |             Frontend Layer (React 18 + Tailwind CSS)             |  |
|  |  - Phone Mirror Canvas      - Visual Element Inspector            |  |
|  |  - Live Step Stream         - Plain-English Prompt Editor         |  |
|  +----------------------------------^--------------------------------+  |
|                                     | Tauri IPC Events                  |
|  +----------------------------------v--------------------------------+  |
|  |               Rust Native Controller (Tauri Core)                |  |
|  |  - Lifecycle Management     - Security & Anti-DevTools Shield     |  |
|  |  - Offline License Auth     - Sidecar Process Supervisor          |  |
|  +------------------+------------------------------+-----------------+  |
|                     |                              |                    |
|        spawns & supervises            spawns & directs                  |
|                     |                              |                    |
|  +------------------v--------------+  +------------v-----------------+  |
|  |   Engine Sidecar (Node SEA)     |  |     ADB Sidecar (Portable)   |  |
|  |   - UIAutomator XML Parser      |  |     - adb.exe                |  |
|  |   - Plain-English AST Runner    |  |     - AdbWinApi.dll          |  |
|  |   - Local Unix/Named Pipe       |  |     - AdbWinUsbApi.dll       |  |
|  +------------------+--------------+  +------------+-----------------+  |
+---------------------|------------------------------|--------------------+
                      |                              |
                      +--------------> USB / Wi-Fi --+
                                            |
                                 +----------v---------+
                                 |   Android Device   |
                                 +--------------------+
```

---

## 2. Component Specifications

### 2.1 Presentation Layer (React + Tailwind CSS)
- Located in `src/`.
- Built as static assets via `vite build` into `dist/`.
- Embedded into the Tauri binary at compile time via `tauri.conf.json`.
- Communicates with the engine sidecar via `fetch('http://127.0.0.1:4040/api/...')` + SSE `/events` stream.
- Protected by typed component boundaries (`PhoneCanvas`, `SpecEditor`, `ElementInspector`, `ExecutionFeed`) and custom hooks (`useDeviceState`, `useEngineConnection`).

### 2.2 Host Layer (Rust / Tauri v2)
- Located in `src-tauri/`.
- Responsibilities:
  - **Window Management:** Frameless/custom titled native desktop window.
  - **Process Supervision:** Automatically starts, monitors, and gracefully kills sidecar processes on window close.
  - **Security Shield:** Disables browser context menus, disables F12 / DevTools in production builds.
  - **License Verification:** Validates encrypted Ed25519 license keys locally without mandatory internet access.

### 2.3 Engine Sidecar (`prompttest-win-x64.exe`)
- The standalone executable of the PromptTest core engine.
- Packaged using Node.js Single Executable Application (SEA).
- Eliminates any user requirement for Node.js, Python, or npm.
- Exposes local HTTP endpoints and real-time Server-Sent Events on `127.0.0.1:4040`.

### 2.4 ADB Driver Sidecar
- Standalone portable platform-tools bundled in `src-tauri/resources/bin/platform-tools/`:
  - `adb.exe`
  - `AdbWinApi.dll`
  - `AdbWinUsbApi.dll`
- Managed directly by the engine sidecar without mutating user `PATH` or system environment variables.

---

## 3. Coordinate System & Canvas Math Architecture

To eliminate coordinate misalignment between the phone screen and desktop canvas:

```
[Screen Coordinates (Device: W_dev x H_dev)]
                      ^
                      |  Scale & Offset Transform
                      v
[Rendered Image Bitmap (DOM: W_rendered x H_rendered)]
                      ^
                      |  Padding & Aspect Fit (object-contain)
                      v
[Viewport Container (DOM: W_container x H_container)]
```

### Transformation Formula:
1. `aspectDevice = naturalWidth / naturalHeight`
2. `aspectContainer = containerWidth / containerHeight`
3. If `aspectContainer > aspectDevice`:
   - `renderedHeight = containerHeight`
   - `renderedWidth = containerHeight * aspectDevice`
   - `offsetX = (containerWidth - renderedWidth) / 2`
   - `offsetY = 0`
4. Else:
   - `renderedWidth = containerWidth`
   - `renderedHeight = containerWidth / aspectDevice`
   - `offsetX = 0`
   - `offsetY = (containerHeight - renderedHeight) / 2`
5. Click mapping:
   - `deviceX = Math.round((clickX - offsetX) * (naturalWidth / renderedWidth))`
   - `deviceY = Math.round((clickY - offsetY) * (naturalHeight / renderedHeight))`

---

## 4. Packaging & Distribution Pipeline

- **Tool:** `tauri build` configured with NSIS target.
- **Output:** `PromptTest-Studio-Setup-<version>.exe`
- **Signing:** Windows Authenticode certificate integration via GitHub Actions.
- **Auto-Update:** Secure differential updates via Tauri Updater with signed minisign signatures.

---

## 5. Strategic & Architectural Decision Log

### Decision: Standalone Commercial Desktop Form Factor
- **Context:** The end-user target audience includes non-technical QA testers, manual testers, and product managers who cannot be expected to install Node.js, Git, or Android SDKs manually.
- **Decision:** PromptTest Studio is distributed as a standalone, zero-setup desktop application (`.exe`). The user downloads and runs a single installer with no prerequisites.
- **Outcome:** The installer bundles all runtime dependencies, including a standalone engine sidecar and portable ADB.

### Decision: Framework Selection — Tauri v2 + Rust
- **Context:** Evaluated Tauri v2 vs. Electron. Electron provides built-in Node.js execution, but suffers from heavy bundle sizes (~150MB), high RAM consumption, and exposed Chromium inspection surfaces.
- **Decision:** Selected **Tauri v2 + Rust**:
  1. **Maximum IP Protection:** Compiles to native binary machine code; disables browser DevTools and context menus to prevent inspection of proprietary studio logic.
  2. **Minimal Footprint:** Sub-20MB installer and < 60MB RAM footprint.
  3. **Zero-Setup Sidecar Pattern:** The Node.js engine is packaged as a standalone Single Executable Application (SEA) sidecar managed by the Rust host.

### Decision: Commercial Closed-Source Model & BSL Funnel
- **Context:** Relationship between the open `prompttest` CLI and `prompttest-studio`.
- **Decision:**
  - `prompttest` CLI is licensed under **Business Source License 1.1 (BSL 1.1)** to foster community adoption, automated CI runs, and developer goodwill.
  - `prompttest-studio` is **100% Closed Source & Commercial** (Proprietary EULA).
  - The CLI acts as the free acquisition funnel promoting the Studio desktop app to QA leads and testing teams.
