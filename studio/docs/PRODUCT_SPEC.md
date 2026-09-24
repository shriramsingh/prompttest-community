# PromptTest Studio — Product Specification & Requirements (PRD)

> **Document Version:** 1.1.0  
> **Status:** Approved  
> **Target Release:** PromptTest Studio Desktop v1.0.0+  
> **Confidentiality:** Proprietary & Commercial — Closed Source  
> **License:** Commercial EULA (End User License Agreement)

---

## 1. Product Vision & Commercial Strategy

**PromptTest Studio** is a commercial, closed-source visual desktop IDE for autonomous mobile QA testing on Android. It empowers non-technical users (QA engineers, manual testers, product managers, designers) and automation leads to inspect native mobile apps, author tests using plain English, and execute automated suites with zero setup.

### Business Goals:
1. **Commercial Monetization:** PromptTest Studio is the primary paid revenue engine of the PromptTest ecosystem.
2. **Freemium Funnel via BSL 1.1 CLI:** The open-core `prompttest` CLI (licensed under Business Source License 1.1) serves as the developer acquisition channel, funneling teams and enterprises into PromptTest Studio.
3. **Zero-Friction Adoption:** End users must install **nothing** manually. No Node.js, Python, Git, Android SDK, or manual ADB setup required.

---

## 2. Target User Personas

* **Primary Persona: Non-Technical Manual QA Testers & Product Managers**
  * *Characteristics:* Comfortable with graphical interfaces, lacks deep terminal or scripting experience.
  * *Expectation:* Downloads an `.exe` installer, connects an Android phone via USB or Wi-Fi, and immediately sees an interactive mirror with element boundaries and click-to-prompt test creation.
* **Secondary Persona: Software Engineers & QA Automation Leads**
  * *Characteristics:* Wants rapid test authoring, visual element inspection, CI/CD export, and visual regression baselines.

---

## 3. Comprehensive Feature Matrix (CLI to Studio UI)

| CLI Capability | Studio Desktop Module | Purpose & User Benefit |
| :--- | :--- | :--- |
| **`prompttest record`** | **Visual Session Recorder ("Record Flow")** | Click, type, and swipe on the live mirror; Studio synthesizes plain-English test steps in real time. |
| **`prompttest run <spec.txt>`** | **Spec Hub & Execution Cockpit** | Load, edit, organize, and execute `.txt` specs with live pass/fail diagnostics and failure triage. |
| **`prompttest repl`** | **Live Action Console / Command Bar** | Single-line natural language prompt to dispatch immediate one-off actions on the phone. |
| **`prompttest explore`** | **Autonomous AI Explorer ("Auto-Pilot")** | Autonomous app crawler with safety modes (`strict`, `moderate`, `disabled`) and live telemetry. |
| **`prompttest baseline`** | **Visual Regression & Baseline Hub** | Side-by-side golden master comparison, `pixelmatch` diff overlay, and baseline management. |
| **`prompttest report`** | **Visual Audit Logs & History** | Test run history, step-by-step screenshot timeline, error triage bundles, and HTML/PDF export. |
| **`prompttest wifi`** | **Wireless ADB Manager** | 1-click USB to Wi-Fi switching, IP detection, and Android 11+ wireless pairing dialog. |
| **`prompttest doctor`** | **Mobile System Doctor** | Health check modal for ADB status, battery %, temperature, Android API level, and screen DPI. |
| **`prompttest memory`** | **Real-Time Performance Dashboard** | Real-time frame times, PSS memory, native heap monitoring, and jank detection. |
| **`prompttest init-ci`** | **CI/CD Workflow Exporter** | Export generated specs into GitHub Actions / GitLab CI YAML pipelines. |

---

## 4. Core Functional Modules & Specifications

### 4.1 Zero-Setup Desktop Distribution (`FR-01`)
- Distributed as a standalone Windows installer (`PromptTest-Studio-Setup.exe`) and portable binary.
- Bundles embedded WebView2 runtime support, portable platform-tools (`adb.exe`, DLLs), and prebuilt engine SEA (`prompttest-win-x64.exe`).

### 4.2 Interactive Live Phone Mirror & Canvas (`FR-02`)
- Sub-second screen mirror of connected USB or Wi-Fi Android devices.
- Visual bounding boxes outlining interactive elements (buttons, inputs, labels).
- Interactive canvas taps: Clicking the phone mirror dispatches hardware touch events to the exact device coordinates.
- Virtual navigation bar: Physical Back (key 4), Home (key 3), and Recents (key 187) buttons.

### 4.3 Visual Element Inspector & Click-to-Prompt Step Generator (`FR-03`)
- Hovering or clicking on any element highlights its bounding box and displays:
  - Display text, content description, resource ID (`id/login_button`), class name (`android.widget.Button`), and clickable/scrollable states.
- Click-to-Prompt action shortcuts:
  - `Tap "<element>"`
  - `Type "<text>" into "<element>"`
  - `Assert "<element>" is visible`

### 4.4 Test Suite Editor & In-App Execution Engine (`FR-04`, `FR-05`)
- Built-in editor to create, edit, and organize plain-English test scripts.
- Single-click **"Run Prompt Suite"** execution directly within the desktop app.
- Execution controls: Cold Start (`--fresh`), Continue on Failure (`--continue`), Performance Profiling (`--profile`), and Data Table injection (`--data`).
- Real-time step execution stream displaying live pass/fail status, execution duration, and error diagnostics.

### 4.5 Visual Session Recorder ("Record Flow") (`FR-06`)
- Real-time synthesis of finger touches, scrolls, swipes, and keypresses on both physical device and screen mirror into plain-English test steps.
- Appends synthesized steps into active spec editor with live step counter and session duration timer.

### 4.6 Visual Regression Baselines & Pixel Diffing (`FR-07`)
- 3-column visual baseline dashboard: Golden Master Baseline, Current Run Frame, and Pixel Diff (`pixelmatch`).
- Ignore mask regions to exclude volatile screen areas (clock, battery, dynamic counters).
- Automatic regression comparison during test suite execution.

### 4.7 Autonomous Auto-Pilot & App Exploration (`FR-08`)
- Autonomous app crawler interface with policy controls: Strict (read-only), Moderate (synthetic form filling), and Disabled (stress testing).
- Exploration budgets: Maximum Depth (1–10) and Step Budget (10–200).
- Live telemetry: Unique screens visited, UI elements mapped, and crash/ANR signals intercepted.
- Export discovered navigation path directly as an executable `.txt` test specification.

### 4.8 Advanced Engine Features (`FR-09`)
- **Semantic Intent Expansion:** Preview and expand high-level macro statements into concrete steps using semantic AI.
- **Self-Healing Locators:** Toggleable self-healing mode (`--heal`) to auto-recover from renamed or relocated UI elements across app versions.
- **Wireless Device Connectivity:** 1-click Wi-Fi connection wizard and Android 11+ PIN pairing interface (`prompttest wifi`).
- **System Doctor & Telemetry:** Diagnostic modal displaying battery %, temperature, Android API level, display DPI, and ADB health.
- **Data-Driven Parameterization:** Parameterize test specs with CSV and JSON data tables (`--data`, `--iterations`).
- **CI/CD Exporter:** 1-click generation of GitHub Actions and GitLab CI automated test workflows.

---

## 5. Non-Functional & Security Requirements (NFR)

* **NFR-01: Source Code & IP Protection (Closed-Source Shield)**
  * 100% proprietary code.
  * Native binary compilation via Tauri + Rust; DevTools (F12, Right-Click Inspect) disabled in production builds.
* **NFR-02: Performance & Footprint**
  * Sub-25MB installer download footprint; native memory footprint under 60MB RAM.
  * 60 FPS smooth canvas mouseover and bounding box rendering without frame drops.
* **NFR-03: Offline Operation & Air-Gapped Compatibility**
  * Core phone mirroring, element inspection, and test execution function completely offline without internet connectivity.
  * Cryptographic offline license verification (signed Ed25519 license key).

---

## 6. Commercial Licensing Tiers

| Tier | Price | Features Included |
| :--- | :--- | :--- |
| **Free Trial** | Free (14 Days) | 1 connected device, up to 25 steps per suite, community support. |
| **Pro License** | $39 / mo ($390 / yr) | Unlimited devices, unlimited steps, click-to-prompt generator, visual baselines, CI export. |
| **Enterprise** | Custom / $99 / seat | Multi-device orchestration, priority support, custom integrations, enterprise SLA. |
