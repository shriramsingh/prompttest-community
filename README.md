# ⚡ PromptTest Mobile — Community Hub & Issue Tracker

> **Ultra-fast, zero-code autonomous mobile testing & visual QA brain for Android & iOS.**  
> The official public community tracker, Q&A forum, and feedback portal for PromptTest Mobile.

[![npm version](https://img.shields.io/npm/v/prompttest-mobile.svg?color=cb3837)](https://www.npmjs.com/package/prompttest-mobile)
[![npm downloads](https://img.shields.io/npm/dm/prompttest-mobile.svg?color=blue)](https://www.npmjs.com/package/prompttest-mobile)
[![License: BSL 1.1](https://img.shields.io/badge/License-BSL%201.1-blue.svg)](https://www.npmjs.com/package/prompttest-mobile)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-green.svg)](https://nodejs.org/)
[![Android ADB](https://img.shields.io/badge/Android-ADB%20Native-orange.svg)](https://developer.android.com/tools/adb)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7-blue.svg)](https://www.typescriptlang.org/)
[![GitHub Release](https://img.shields.io/github/v/release/shriramsingh/prompttest-community?color=blue&label=release)](https://github.com/shriramsingh/prompttest-community/releases)

---

### 📦 Official Distribution & Releases

| Channel                             | Platform / Target                             | Download / Install Link                                                                                   |
| :---------------------------------- | :-------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| **NPM (Mobile Flagship)**           | Cross-Platform (Node 18+)                     | `npm install -g prompttest-mobile` or `npx prompttest-mobile`                                             |
| **NPM (Core Engine)**               | Cross-Platform (Node 18+)                     | `npm install -g prompttest` or `npx prompttest`                                                           |
| **Windows Turnkey Bundle & .exe**   | Windows x64 (Includes tested ADB, zero setup) | 👉 **[Get Latest Windows Release](https://github.com/shriramsingh/prompttest-community/releases/latest)** |
| **macOS Turnkey Bundle & Binary**   | macOS Apple Silicon (Includes tested ADB)     | 👉 **[Get Latest macOS Release](https://github.com/shriramsingh/prompttest-community/releases/latest)**   |
| **Linux Turnkey Bundle & Binary**   | Linux x64 (Includes tested ADB)               | 👉 **[Get Latest Linux Release](https://github.com/shriramsingh/prompttest-community/releases/latest)**   |
| **GitHub Releases Hub**             | All Platforms + SHA256 Checksums               | 👉 **[Browse All Releases](https://github.com/shriramsingh/prompttest-community/releases)**               |
| **PromptTest Studio (Desktop IDE)** | Windows Desktop GUI (macOS soon)              | 👉 **[Download Studio Installer](https://shriramsingh.github.io/prompttest-studio-site/downloads.html)**  |

---

## 📌 About This Repository

This is the **public community hub** for PromptTest Mobile. While the core test engine and state-graph algorithms are proprietary and maintained in a private repository, this repository provides:

- 🐛 **Public Bug Tracker**: File bugs, crashes, or ADB compatibility issues.
- 💡 **Feature Requests**: Propose new plain-English commands, CLI flags, or integrations.
- 💬 **GitHub Discussions**: Ask questions, share tips, and discuss plain-English testing workflows.
- 📢 **Release Announcements**: Track public updates, changelogs, and fixes.

---

## 🖥️ PromptTest Studio (Visual Desktop IDE)

**[PromptTest Studio](https://shriramsingh.github.io/prompttest-studio-site/)** is the official visual desktop IDE and interactive mobile QA studio for PromptTest Mobile:
- 📱 **Real-Time Device Mirroring**: Low-latency screen streaming with instant click, drag, and hardware navigation.
- 🎯 **Visual Element Inspector**: Point and click to inspect native views with instant auto-generated plain-English assertions.
- 📸 **Visual Regression & Exclude Masks**: Pixel-level baseline comparisons with draggable exclude masks for dynamic areas (clocks, battery, banners).
- 🚀 **100% Local-First & Air-Gapped**: Runs entirely on your machine over local ADB with zero cloud dependencies.

👉 **[Download PromptTest Studio for Windows (v0.1.0)](https://shriramsingh.github.io/prompttest-studio-site/downloads.html)**  
📖 **[Read the Studio Documentation & Guides](https://shriramsingh.github.io/prompttest-studio-site/studio.html)**  
📄 **[Studio Technical Overview](studio/README.md)**

---

## 🚀 Quick Start with PromptTest Mobile

Install PromptTest Mobile into your React Native, Expo, Flutter, or Native Android project:

```bash
# Run instantly with npx (recommended):
npx prompttest-mobile doctor

# Or install as a dev dependency:
npm install --save-dev prompttest-mobile

# (Legacy package alias also supported):
# npx prompttest doctor
```

### Core Workflows

1. **Environment Diagnostic Check:**
   ```bash
   npx prompttest-mobile doctor
   ```
2. **Interactive Spec Scaffolding Wizard:**
   ```bash
   npx prompttest-mobile wizard
   ```
3. **Zero-Code Autonomous App Exploration (State-Graph Crawl):**
   ```bash
   npx prompttest-mobile explore com.yourcompany.app --video
   ```
4. **Run Plain-English Test Specification (Android or iOS):**
   ```bash
   # Android:
   npx prompttest-mobile run specs/login.txt com.yourcompany.app --fresh --heal

   # iOS Simulator (macOS):
   npx prompttest-mobile run specs/login.txt --serial=<SIMULATOR-UDID> --ios-app=build/MyApp.app --fresh
   ```

---

## ⚡ PromptTest Mobile vs. Appium & Detox

| Capability | Appium | Detox | ⚡ PromptTest Mobile |
| :--- | :--- | :--- | :--- |
| **Initial Setup Time** | 1–2 hours (Java, drivers, server) | 45 mins (Build config, pods) | **0 seconds (instant via npx)** |
| **App Instrumentation** | Server daemon required | Test runner compiled into app | **Zero instrumentation (pure native)** |
| **Test Script Language** | Java / Python / TS (XPath) | JavaScript (Matchers) | **Plain English natural language** |
| **Dynamic Locators** | Fragile XPaths | Test IDs required | **Self-healing AI heuristics** |
| **Visual Regression** | Third-party plugin | None built-in | **Built-in pixel diff + exclude masks** |
| **Autonomous Crawling** | None (manual scripts only) | None | **Autonomous state-graph AI crawler** |
| **Execution Architecture**| Heavy background server | Test binary embedded in app | **Direct ADB streams (ultra-fast)** |

---

## 📱 Platform Support & Verification Matrix

To set clear expectations, here is PromptTest's platform verification matrix:

| Platform | Target Type | Current Status | Notes & Capabilities |
| :--- | :--- | :---: | :--- |
| **Android** | Physical Devices (USB) | **✅ Production Ready** | Battle-tested on React Native, Expo, Flutter, and Native Android. |
| **Android** | Wi-Fi Wireless ADB | **✅ Production Ready** | Zero-typing camera QR pairing (Android 11+), auto mDNS discovery, manual IP. |
| **Android** | Android Emulators | **✅ Production Ready** | All features, headless CI execution, cold-starts. |
| **Apple iOS** | **iOS Simulators** | **✅ Verified & Stable** | Supported via native `xcrun simctl` + local WebDriverAgent on macOS with Xcode 15+. Auto-installs `.app` bundles, captures unified logs, and retina screenshots. |
| **Apple iOS** | **Physical iOS Hardware** | ⚠️ **Experimental** | Community-driven: requires manual Apple Developer code signing for WebDriverAgentRunner. Session recording is Android-only due to iOS sandboxing. |
| **Websites** | Desktop Browsers | **❌ Not Supported** | PromptTest is dedicated strictly to mobile apps. For web, use Playwright or Cypress. |
| **Accessibility Tree** | Standard UI Hierarchy | **✅ Full Support** | Reads all accessibility trees (`text`, `content-desc`, `resource-id`). |
| **Canvas / Games** | Custom OpenGL / Canvas | **⚠️ Not Supported** | Games drawn directly on custom canvas/OpenGL lack native accessibility nodes. |

---

### 🚨 Top 5 Mobile QA Blockers & Instant Fixes

Before diagnosing automation issues, check these 5 most frequent mobile QA hurdles:

| # | Common Blocker | Root Cause | Instant Fix |
|---|---|---|---|
| **1** | **Xiaomi / MIUI / HyperOS ignores touch inputs** | Xiaomi restricts simulated input via ADB by default. | Open **Developer options** → Toggle ON **"USB debugging (Security settings)"** (Requires an active SIM card). |
| **2** | **Target button not clickable because keyboard covers it** | Virtual IME keyboard obscures elements in lower half of screen. | PromptTest automatically dismisses soft keyboards during step taps. You can also explicitly add step: `Hide keyboard` or `Press back`. |
| **3** | **Physical iOS device fails or cannot record touches** | iOS lacks ADB-style `getevent` raw touch capture; physical devices require Apple Code Signing. | **Use iOS Simulators for test execution** (fully verified). Touch recording is Android-only; write specs manually or scaffold via wizard on iOS. |
| **4** | **`adb devices` shows device as `unauthorized` or `offline`** | RSA workstation key was not accepted on phone screen or USB cable is loose. | Re-plug USB cable. Unlock device and check **"Always allow from this computer"** on prompt. Run `prompttest doctor` to verify. |
| **5** | **`EADDRINUSE: address already in use :::4040`** | Previous PromptTest live server or background process is still active. | Pass a custom port using `--serve 4041`, or run `prompttest doctor` / terminate zombie node instances on port 4040. |

---

## ⚠️ Common Pitfalls & How to Solve Them

### 1. Hardware Back Button Minimizing the App
* **What happens**: Running `Press back` while on the app's root dashboard or home tab tells the Android OS to minimize or exit the app.
* **How PromptTest solves it**:
  - **Root Anchor Safe Harbor**: Starting in v1.5.3, PromptTest automatically indexes your app's root navigation hubs (bottom tabs, home screens). When a back action would cause the app to exit, PromptTest intercepts and suppresses the escape.
  - **Package Jail Guard**: In autonomous exploration (`explore`), the built-in jail guard automatically detects if an app was backgrounded and restores foreground focus immediately.
  - In your own specs, you can also use `Tap 'Back'` or add `--fresh` to guarantee a clean cold-start.

### 2. Android OS Permission Dialogs ("Allow Notifications / Location")
* **What happens**: System dialogs belong to Android OS (`com.android.permissioncontroller`), not your app, and can appear unexpectedly on new installs.
* **How to solve it**:
  - Use conditional handling in your spec:
    ```text
    Tap 'While using the app' (if present)
    Tap 'Allow' (if present)
    ```
  - Or auto-grant permissions via ADB before running tests:
    ```bash
    adb shell pm grant com.yourcompany.app android.permission.POST_NOTIFICATIONS
    ```

### 3. Off-Screen Items in Long Lists (FlatList / RecyclerView)
* **What happens**: Mobile frameworks only render visible items on screen to save memory. Elements located further down the page are not in the hierarchy yet.
* **How to solve it**:
  - Scroll before tapping:
    ```text
    Scroll down
    Verify 'Save Changes' is visible
    Tap 'Save Changes'
    ```

### 4. Layout Animations & Shimmer Settling
* **What happens**: Tapping an element during a layout animation or skeleton fade-in can cause touch coordinates to miss while elements shift.
* **How to solve it**:
  - Add a brief settling pause: `Wait 500ms` or assert an anchor element first: `Verify 'Dashboard' is visible`.
  - Disable animations on test devices to run tests 2x faster:
    ```bash
    adb shell settings put global window_animation_scale 0
    adb shell settings put global transition_animation_scale 0
    adb shell settings put global animator_duration_scale 0
    ```

### 5. WebViews & In-App Browsers (OAuth & Payment Gateways)
* **What happens**: In-app web pages (like Google Sign-In or Stripe) expose rendered text to ADB, but not internal HTML DOM tags or CSS selectors.
* **How to solve it**:
  - Use plain text matching (`Tap 'Sign in with Google'`). Deep DOM selector manipulation inside WebViews is not supported.

### 6. Multiple Devices Connected
* **What happens**: If a physical phone and an emulator are both plugged in, ADB doesn't know which one to target.
* **How to solve it**:
  - Target a specific device serial using `--serial`:
    ```bash
    npx prompttest run specs/login.txt com.app --serial=emulator-5554
    ```

---

## 💡 Pro-Tips & Best Practices

### 1. The "Record & Refine" Workflow
* `prompttest record` captures your natural physical device interactions and generates plain-English test steps in real time—scaffolding 90% of your test boilerplate in seconds.
* **QA Best Practice**: After recording, do a quick 30-second review of the generated `.txt` spec to fine-tune timings or add custom `Verify` assertions.
* Preview without touching your device:
  ```bash
  npx prompttest run specs/flow.txt --dry-run
  ```

### 2. Deterministic Clean States (`--fresh`)
* Prevent "already-logged-in" test pollution by adding `--fresh` to cold-start the target app before execution:
  ```bash
  npx prompttest run specs/login.txt com.yourcompany.app --fresh
  ```

### 3. Zero-Maintenance Dynamic Badges (`--heal`)
* When notification badges or counts change dynamically (e.g. `'Cart (1)'` vs `'Cart (3)'`), pass `--heal` to allow PromptTest's heuristic engine to self-heal the locator without failing.

### 4. Device & Screen Resolution Agnostic Portability
* PromptTest binds interactions to semantic accessibility labels and proportional gestures—not fragile hardware pixel coordinates. Specs recorded on a phone seamlessly run on foldables and tablets.

### 5. 🛡️ Enterprise Safety Guardrails & Custom Blacklists
Autonomous exploration is safe by default, but enterprise applications often have company-specific sensitive keywords (e.g. *"Deactivate"*, *"Transfer Funds"*, *"Revoke Access"*).

* **Default Protection**: PromptTest automatically detects and blocks destructive actions like `"Delete"`, `"Wipe"`, `"Remove"`, and `"Discard Changes"`.
* **Add Your Own Sensitive Keywords**: You can supply your own custom blocked keywords to run **alongside** the defaults:
  ```bash
  # Via CLI flag:
  npx prompttest explore com.yourcompany.app --safety-blacklist="Transfer,Deactivate,Revoke,Unsubscribe"
  ```
* **Or configure once in `.prompttestrc.json`**:
  ```json
  {
    "safety": {
      "mode": "strict",
      "customBlacklist": ["Transfer", "Deactivate", "Revoke", "Unsubscribe"]
    }
  }
  ```

---

## 🤝 How to Report Issues & Contribute Feedback

We want PromptTest to be the fastest, most reliable mobile testing engine in your toolchain. If you encounter any unexpected behavior, please report it!

| Purpose | Link | Description |
| :--- | :--- | :--- |
| **Bug Reports** | [Open a Bug Report](https://github.com/shriramsingh/prompttest-community/issues/new?template=1_bug_report.yml) | Report crashes, element detection failures, or ADB connection errors. |
| **Feature Requests** | [Suggest an Idea](https://github.com/shriramsingh/prompttest-community/issues/new?template=2_feature_request.yml) | Propose new natural-language syntax, CLI flags, or reporting options. |
| **Q&A / General Help** | [GitHub Discussions](https://github.com/shriramsingh/prompttest-community/discussions) | Ask questions about test patterns, CI/CD setups, or device pools. |

---

## 📋 Tips for Filing Great Bug Reports

To help us diagnose and fix issues quickly:

1. Run `npx prompttest doctor` and include the output.
2. Provide your **device details** (e.g. Pixel 7, Samsung Galaxy S23, or Android Emulator) and **Android OS version**.
3. Specify your **mobile framework** (React Native, Expo, Flutter, Jetpack Compose, etc.).
4. Include the exact **plain-English step** or command that caused the issue.
5. If possible, run with `--dry-run` or provide the terminal output log.

---

## 🛡️ Security Vulnerabilities

If you discover a security vulnerability, please do **not** open a public issue. Instead, report it directly via email to:

📧 **`uic.17mca1009@gmail.com`**

We will respond promptly and coordinate a patch release.

---

## 📄 License & Community Usage

PromptTest is distributed under the **Business Source License 1.1 (BSL 1.1)**:
- **Free for Community Use**: 100% free for individual developers, educational use, open-source projects, and organizations under \$100,000 in annual revenue.
- **Commercial Inquiries**: For commercial licensing, enterprise self-hosting, or custom integrations, contact: `uic.17mca1009@gmail.com`.
