<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="DEI Tech | Printer Supply Tracker" height="70" />
</a>

<br /><br />

[繁體中文](../../README.md) · **English** · [简体中文](README_zh-CN.md)

# Printer Supply Tracker (PST / PQT)

### Automated Network Printer Toner & Counter Monitoring Utility with Google Sheets Sync for Windows
Say goodbye to manual meter reading! Automatically poll CMYK toner levels and total page counts via SNMP, scheduled background upload to Google Sheets, with unattended startup recovery.

[![Platform](https://img.shields.io/badge/Platform-Windows%207%20%7C%208%20%7C%2010%20%7C%2011%20%7C%20WinPE-blue?style=flat-square&logo=windows)](https://github.com/robert820/printer-supply-tracker)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](../../LICENSE)
[![Type](https://img.shields.io/badge/Type-Freeware%20%7C%20Portable-success?style=flat-square)](#-download--usage)
[![Download](https://img.shields.io/badge/Download-GitHub%20Releases-blue?style=flat-square&logo=github)](https://github.com/robert820/printer-supply-tracker/releases)

**Eliminate Windows Task Scheduler unreliability with a lightweight, system-tray daemon built for 100% unattended automation!**

[Overview](#-overview) · [Key Features](#-key-features) · [Screenshots](#-screenshots) · [Download & Usage](#-download--usage) · [System Requirements](#-system-requirements) · [FAQ](#-frequently-asked-questions-faq) · [Support](#-support--feedback)

</div>

---

## 📖 Overview

In modern office environments, enterprise IT departments and general administration personnel often struggle with monthly copier and printer management:
1. **Time-consuming manual meter checks**: Walking to every single multifunction printer (MFP) to record monochrome and color page counts from hardware menus.
2. **Unpredictable toner depletion**: Running out of Cyan, Magenta, Yellow, or Black (CMYK) toner unexpectedly during critical print jobs.
3. **Flaky Windows Task Scheduler**: Traditional PowerShell scripts scheduled in Windows Task Scheduler often fail silently due to PC sleep states, changed user passwords, credential mismatches, or holiday power-downs.

**Printer Supply Tracker (PST / PQT)** is a native, portable Windows desktop utility designed to solve these exact headaches. It periodically queries network copiers and printers via the standard SNMP protocol to fetch live page counts and remaining toner percentages, then seamlessly streams the structured data directly into a **Google Spreadsheet** via a lightweight Web API.

With a built-in, independent **smart scheduling and startup recovery engine**, it automatically adapts to weekends and national holidays, and automatically triggers missed tasks when the host computer powers back on—guaranteeing your reports are never incomplete.

---

## ✨ Key Features

### 1. ⚡ Multi-Brand Printer SNMP Auto-Polling
- Automatically scans network printers over standard SNMP (v1/v2c).
- Reads device model, serial number, physical location, total B&W pages, total color pages, and remaining CMYK toner percentages.
- **Specific Supported Models & OID Profiles**:
  - **Ricoh**:
    - Color MFPs: Full line of commercial color multifunction printers (Dual B&W / Color counters, CMYK 4-color toner levels)
    - Monochrome models: MP 3554, MP 3555, IM 3500, MP 6054, MP 6055, MP 6502, MP 6503, MP 7502, MP 7503
  - **Fuji Xerox / FUJIFILM**:
    - Color MFPs: ApeosPort series, DocuCentre series color printers
    - Monochrome models: ApeosPort 3060, ApeosPort 3560, DocuCentre 3060
  - **SHARP**:
    - Color MFPs: MX color series, BP color series MFPs
    - Monochrome models: MX-M series (including MX-M365N), BP-M series
- Non-blocking error handling: Unreachable or offline devices are marked clearly without freezing or interrupting the overall batch polling routine.

### 2. 📊 Automatic Google Sheets Sync
- Formats queried device metrics and automatically uploads them with timestamps to your designated Google Sheet.
- Integrates via Google Apps Script Web App URLs without requiring bulky local Python or Node.js runtime environments.
- Built-in sanity checks: Validates Web App endpoints and worksheet tab permissions, reporting clear actionable error messages upon failure.

### 3. ⏰ Smart Scheduling & Missed-Task Recovery Engine
- **Self-Contained Scheduling**: Completely eliminates reliance on unstable Windows Task Scheduler configurations.
- **Multi-Day Monthly Execution**: Select specific days of the month (e.g., 1st, 15th, 25th) for automated runs.
- **Weekend Adjustment**: Automatically shifts runs before or after weekends to match real working days.
- **Taiwan Public Holiday Handling**: Automatically checks holiday calendars to bypass non-working dates.
- **Startup Catch-Up Mechanism**: If the computer was off during a scheduled run, the application automatically detects the omission upon boot and performs an immediate make-up sync.

### 4. 🛡️ System Tray Daemon with 3-Color Status LED
- Minimizes directly into the Windows system tray without occupying desktop space.
- Real-time status LED indicators:
  - 🔵 **Blue**: Actively executing SNMP polling or Google Sheets upload
  - 🟢 **Green**: All target devices connected normally and schedule is active
  - 🔴 **Red**: One or more devices failed connection, or IP list is unconfigured
- Double-click to restore the settings window; right-click context menu provides instant manual execution and clean exit options.

### 5. 🧪 Manual Diagnostics & Instant Execution
- **Test SNMP Connection**: Instantly verifies IP connectivity and MIB response without writing data to the cloud.
- **Run Immediately & Upload**: Manually triggers a complete query and sync cycle anytime without waiting for the timer.

### 6. 📝 Complete Local Audit Logging
Every query result, upload response, timestamp, and network error code is written to `PST_Unattended.log` for troubleshooting and IT compliance.

---

## 📸 Screenshots

<div align="center">
  <img src="../../images/應用程式執行畫面.png" alt="Printer Supply Tracker UI" width="720" />
  <p>▲ Printer Supply Tracker: Real-time multi-brand printer dashboard, CMYK toner gauges, and scheduling settings</p>
</div>

---

## 📦 Download & Usage

### 📥 Download
1. Head over to the project's [Releases Page](https://github.com/robert820/printer-supply-tracker/releases) to download the latest binary.
2. The application is distributed as a **single standalone portable executable**. No installation, runtime libraries, or administrative setup required.

### 🚀 Quick Start Guide

1. **Configure Target Printers**: Go to the **Target Devices & SNMP** tab, paste your printer IP addresses (one per line), and specify the SNMP Community string (`public` by default).
2. **Set Up Google Sheets**: Under **General Settings**, paste your Google Apps Script Web App URL (`https://.../exec`) and specify your target Sheet name.
3. **Verify Connectivity**: Click **Test SNMP Connection** to ensure all network printers respond properly.
4. **Schedule Execution**: In the **Execution Schedule** tab, select target monthly dates/times and enable **Weekend Shift**, **Holiday Shift**, and **Startup Catch-up**.
5. **Enable Auto-Start**: Under **System Settings**, toggle **Launch on Windows Startup** to allow the program to run silently in the system tray.

---

## 🖥️ System Requirements

- **Operating System**: Windows 11 / 10 / 8.1 / 8 / 7 (SP1) & Windows Server 2012+
- **Architecture**: Universal support for both 64-bit (x64) and 32-bit (x86)
- **Network**: Local area network (LAN) access to target printer IPs, and outbound HTTPS access to Google APIs
- **Dependencies**: Native pure Rust binary; zero external runtimes (.NET, VC++ Redistributable, Python) needed

---

## ❓ Frequently Asked Questions (FAQ)

<details>
<summary><b>Q1: Is this tool completely free for business use?</b></summary>
A: Yes. It is released under a proprietary freeware license for personal, educational, and commercial business use. You may use it freely within your office or client maintenance environments. Commercial resale or redistribution for a standalone fee is strictly prohibited.
</details>

<details>
<summary><b>Q2: Which printer brands and models are natively supported?</b></summary>
A: The application includes native OID mapping rules optimized specifically for three major enterprise office equipment manufacturers:
- **Ricoh**:
  - Color MFPs: All commercial color multifunction printer series (monochrome and color page counts, CMYK 4-color toner levels)
  - Monochrome models: MP 3554, MP 3555, IM 3500, MP 6054, MP 6055, MP 6502, MP 6503, MP 7502, MP 7503
- **Fuji Xerox / FUJIFILM**:
  - Color MFPs: ApeosPort series, DocuCentre series color models
  - Monochrome models: ApeosPort 3060, ApeosPort 3560, DocuCentre 3060
- **SHARP**:
  - Color MFPs: MX color series, BP color series MFPs
  - Monochrome models: MX-M series (including MX-M365N), BP-M series
As long as the target device has SNMP service enabled, the application will automatically identify the hardware model and query the matching metrics.
</details>

<details>
<summary><b>Q3: Why avoid Windows Task Scheduler?</b></summary>
A: Task Scheduler frequently misses tasks during power save/sleep states and lacks built-in "missed run recovery on boot". This tool's dedicated lightweight tray daemon ensures 100% reliable execution.
</details>

---

## 💬 Support & Feedback

- 🐛 **Issues & Suggestions**: Feel free to submit via [GitHub Issues](https://github.com/robert820/printer-supply-tracker/issues).
- 🌐 **DEI Tech Official Website**: [https://blog.dei3c.com](https://blog.dei3c.com)

---

## 📄 License

This software is distributed as Proprietary Freeware. For full terms, conditions, and disclaimers, please refer to the [LICENSE](../../LICENSE) file.
