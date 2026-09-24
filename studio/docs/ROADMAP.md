# PromptTest Studio — Product Roadmap & Task Tracker

> **Document Version:** 1.2.0  
> **Status:** All Core & Active UX Tasks Completed  
> **Scope:** PromptTest Studio Desktop App & Integrated Sidecar Engine

---

## 1. Executive Status Overview

| Capability / Milestone | Status | Verified Evidence |
| :--- | :--- | :--- |
| **Core Architecture & Desktop IDE** | ✅ Complete | Tauri v2 + Rust + React 18 frontend |
| **Codebase Refactoring & Modularity** | ✅ Complete | `App.tsx` extracted into dedicated hooks and components |
| **Engine & ADB Sidecar Packaging** | ✅ Complete | Standalone `prompttest-win-x64.exe` + portable `platform-tools` |
| **Desktop Production Packaging** | ✅ Complete | NSIS installer + portable `.exe` + release manifests |
| **Physical Hardware Verification** | ✅ Complete | Xiaomi Redmi Note 11S (Android 13) smoke tested |
| **Device Classification & Badges** | ✅ Complete | Canonical `connectionType` ('usb' \| 'wifi' \| 'emulator') + visual icons |
| **Dynamic Package Detection** | ✅ Complete | Live refresh on tab change + copy-on-click package badge |
| **Autopilot Spec Export Modal** | ✅ Complete | `ExportSpecModal` with timestamped unique naming |
| **Visual Baselines Toggle** | ✅ Complete | Inline `[📷 Baselines ON/OFF]` in recording toolbar |
| **CI Export Modernization** | ✅ Complete | Node 24 workflows + artifact retention for GitHub & GitLab |
| **Clean Windows VM Smoke Test** | ✅ Complete | Verified on clean Windows environment without developer tools |
| **Git Synchronization** | ✅ Complete | `dev` & `main` branches synchronized across repositories |

---

## 2. Completed Feature & UX Enhancements

### 2.1 Wi-Fi Experience Enhancements
- [x] **Dedicated Wi-Fi API:** Extracted Wi-Fi endpoints from `doctorApi.ts` into a clean, dedicated `src/api/wifiApi.ts`.
- [x] **Android 11+ Pairing UI:** Dedicated **Pairing Tab** in `WifiModal` (IP, pairing port, 6-digit code) supporting the pair-then-connect workflow.
- [x] **Custom Port & Endpoint Memory:** Provided custom port input (default 5555) and persistent last-used Wi-Fi address in `localStorage`.
- [x] **Canonical Device Classification:** Added `connectionType: 'usb' | 'wifi' | 'emulator'` to `AndroidDevice` model, with `classifyDevice()` and `formatDeviceLabel()` rendering icons in the device dropdown (`🔌 [USB]`, `📶 [Wi-Fi]`, `💻 [Emulator]`).

### 2.2 Live Dynamic Package Detection
- [x] **Dynamic Package Refresh:** Screen state and foreground package automatically refresh on tab switch (`studio`, `explorer`, `memory`) and Doctor modal opening.
- [x] **Copy-on-Click Badge:** Phone-mirror "Foreground: `<pkg>`" badge is clickable to copy the package name to clipboard with "Copied!" feedback toast.
- [x] **Cross-Module Sync:** Target package in Auto-Pilot and Memory automatically defaults to the live foreground package when idle.

### 2.3 Studio Module Refinements
- [x] **Data Table Parameterization:** Wired `dataFile` and `dataFileContent` parameters from `DataTableModal` to `specsApi.runSuite` for variable substitution.
- [x] **AI Macro Endpoint Alignment:** Registered `EXPAND: '/api/expand'` in `src/constants/endpoints.ts`.
- [x] **Cold Boot / Resume:** Forwarded `freshEnabled` state into `handleResumeFromStep` so cold boot options are honored when resuming.
- [x] **CI Export Modernization:** Updated CI workflow template to Node 24 with artifact preservation (`actions/upload-artifact@v4`) and self-hosted runner guidance.
- [x] **AI Heal Indicator:** Added visual `healed` badge and tooltip on `AuditStep` entries in `ExecutionFeed`.

### 2.4 Confirmed UX Enhancements
- [x] **Profiling 3-State Button UX:** Implemented 3-state model: `IDLE` ➔ `STARTING` (disabled + spinner) ➔ `PROFILING` in `MemoryView`.
- [x] **Profiling Report Generation:** Added HTML performance report and raw CSV metrics export upon stopping profiling.
- [x] **Autopilot Spec Export Modal:** Created `ExportSpecModal` with exploration telemetry and unique timestamped naming: `autopilot_<pkg>_<YYYYMMDD_HHMM>.txt`.
- [x] **Visual Baselines Toggle:** Added persistent `[📷 Baselines ON/OFF]` toggle in the recording toolbar to auto-approve golden master baselines during recording.

---

## 3. Operational & Infrastructure Backlog (Deferred External Items)

- [x] **Clean Windows VM Smoke Test:** Test running the NSIS installer on an isolated Windows VM with zero developer tools (no Node.js, Python, or Rust) to verify first-run experience.
- [ ] **Authenticode Code Signing:** Configure CI signing secrets (`PROMPTTEST_SIGNING_CERT_BASE64`, `PROMPTTEST_SIGNING_CERT_PASSWORD`) when a commercial digital certificate is purchased (currently operating under `unsigned internal/staging` policy).
- [ ] **Toolchain Linter:** Integrate ESLint into CI once ecosystem flat-config peer dependency issues (`@eslint/js@10` vs `typescript-eslint`) are resolved.

---

## 4. Completed Historical Milestones

### Phase 1: Engine & Desktop Build Baseline
- [x] Embedded engine sidecar (`prompttest-win-x64.exe`) and portable ADB platform-tools.
- [x] Fail-safe resource synchronization script (`npm run sync:engine`).
- [x] Automated release manifest (`npm run release:manifest`) and SHA-256 preflight checks (`npm run release:preflight`).
- [x] Zero-vulnerability dependency remediation (Vite 8.3.0, Vitest 5.0.1, esbuild 0.28.2).

### Phase 2: Codebase Refactoring & Modularity
- [x] Refactored monolithic `App.tsx` into dedicated domain components (`PhoneCanvas`, `SpecEditor`, `ElementInspector`, `ExecutionFeed`, `StudioView`).
- [x] Extracted custom hooks for device state, session recording, test specs, and real-time streaming (`useDeviceState`, `useSessionRecorder`, `useSpecEditor`, `useEngineConnection`, `useExplorer`, `useReports`, `useBaselines`).
- [x] Maintained 100% build passing and clean test suites across all component tests.

### Phase 3: Desktop Packaging & Public Distribution
- [x] Multi-format packaging: NSIS installer (`PromptTest Studio-1.0.0-setup.exe`) and portable binary (`PromptTest Studio-1.0.0-portable.exe`).
- [x] Embedded WebView2 bootstrapper (`webviewInstallMode: embedBootstrapper`).
- [x] Configured public site distribution pipeline (`shriramsingh/prompttest-studio-site`).

### Phase 4: Physical Hardware Smoke Verification
- [x] Attached Xiaomi Redmi Note 11S (Android 13 / MIUI) recognized via `adb` and `prompttest devices`.
- [x] Extracted live UI hierarchy and generated auto-scaffolded test specs (`SC-01`).
- [x] Executed live tests on physical hardware with touch event dispatching to real screen coordinates.
- [x] Verified failure triage bundle creation and HTML report generation.
