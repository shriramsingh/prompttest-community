# ⚡ PromptTest Community Hub & Issue Tracker

> **Ultra-fast, zero-code autonomous mobile testing & visual QA brain for Android.**  
> The official public community tracker, Q&A forum, and feedback portal for PromptTest.

[![npm version](https://img.shields.io/npm/v/prompttest.svg?color=cb3837)](https://www.npmjs.com/package/prompttest)
[![npm downloads](https://img.shields.io/npm/dm/prompttest.svg?color=blue)](https://www.npmjs.com/package/prompttest)
[![License: BSL 1.1](https://img.shields.io/badge/License-BSL%201.1-blue.svg)](https://www.npmjs.com/package/prompttest)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-green.svg)](https://nodejs.org/)
[![Android ADB](https://img.shields.io/badge/Android-ADB%20Native-orange.svg)](https://developer.android.com/tools/adb)

---

## 📌 About This Repository

This is the **public community hub** for PromptTest. While the core test engine and state-graph algorithms are proprietary and maintained in a private repository, this repository provides:

- 🐛 **Public Bug Tracker**: File bugs, crashes, or ADB compatibility issues.
- 💡 **Feature Requests**: Propose new plain-English commands, CLI flags, or integrations.
- 💬 **GitHub Discussions**: Ask questions, share tips, and discuss plain-English testing workflows.
- 📢 **Release Announcements**: Track public updates, changelogs, and fixes.

---

## 🖥️ PromptTest Studio (Visual Desktop IDE)

**[PromptTest Studio](https://shriramsingh.github.io/prompttest-studio-site/)** is the official visual desktop IDE and interactive mobile QA studio for PromptTest:
- 📱 **Real-Time Device Mirroring**: Low-latency screen streaming with instant click, drag, and hardware navigation.
- 🎯 **Visual Element Inspector**: Point and click to inspect native views with instant auto-generated plain-English assertions.
- 📸 **Visual Regression & Exclude Masks**: Pixel-level baseline comparisons with draggable exclude masks for dynamic areas (clocks, battery, banners).
- 🚀 **100% Local-First & Air-Gapped**: Runs entirely on your machine over local ADB with zero cloud dependencies.

👉 **[Download PromptTest Studio for Windows (v0.1.0)](https://shriramsingh.github.io/prompttest-studio-site/downloads.html)**  
📖 **[Read the Studio Documentation & Guides](https://shriramsingh.github.io/prompttest-studio-site/studio.html)**  
📄 **[Studio Technical Overview](studio/README.md)**

---

## 🚀 Quick Start with PromptTest

Install PromptTest into your React Native, Expo, Flutter, or Native Android project:

```bash
# Run instantly with npx:
npx prompttest doctor

# Or install as a dev dependency:
npm install --save-dev prompttest
```

### 3 Core Workflows

1. **Environment Diagnostic Check:**
   ```bash
   npx prompttest doctor
   ```
2. **Zero-Code Autonomous App Exploration (AI Crawl):**
   ```bash
   npx prompttest explore com.yourcompany.app
   ```
3. **Run Plain-English Test Specification:**
   ```bash
   npx prompttest run specs/login.txt com.yourcompany.app --heal
   ```

---

## 📱 Platform Support & Current Scope

To set clear expectations, here is PromptTest's current platform status:

| Platform / Framework | Current Status | Notes |
| :--- | :---: | :--- |
| **Android (Physical & Emulators)** | **✅ Production Ready** | Battle-tested on React Native, Expo, Flutter, and Native Android. |
| **iOS / iPhone & iPad** | **🚧 In Active Development** | iOS execution engine is in development; not supported in v1.3.x. |
| **Websites / Desktop Browsers** | **❌ Not Supported** | PromptTest is dedicated strictly to mobile apps. For web, use Playwright or Cypress. |
| **Standard UI Hierarchy** | **✅ Full Support** | Reads all accessibility trees (`text`, `content-desc`, `resource-id`). |
| **Custom Canvas / OpenGL Games** | **⚠️ Not Supported** | Games drawn directly on custom canvas/OpenGL lack native accessibility nodes. |

---

## ⚠️ Common Pitfalls & How to Solve Them

### 1. Hardware Back Button Minimizing the App
* **What happens**: Running `Press back` while on the app's root dashboard or home tab tells the Android OS to minimize or exit the app.
* **How to solve it**:
  - In specs, tap the in-app back icon/button (e.g. `Tap 'Back'` or `Tap '<'`) instead of the hardware key on top-level screens.
  - In autonomous exploration (`explore`), PromptTest's built-in **Package Jail Guard** automatically detects if the app was backgrounded and restores it.
  - Add the `--fresh` flag when running specs to cold-start your app cleanly before tests.

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
