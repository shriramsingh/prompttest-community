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
