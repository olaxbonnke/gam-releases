# Gas Accounting Manager (GAM) — Releases & Distribution CDN

[![Platform](https://img.shields.io/badge/platform-Windows%20x64-0078D6?style=flat-square&logo=windows)](https://www.microsoft.com/)
[![Runtime](https://img.shields.io/badge/runtime-Electron%2033-47848F?style=flat-square&logo=electron)](https://www.electronjs.org/)
[![Frontend](https://img.shields.io/badge/frontend-React%2019%20%7C%20TypeScript-61DAFB?style=flat-square&logo=react)](https://react.dev/)
[![Database](https://img.shields.io/badge/database-Embedded%20SQLite%20(WAL)-003B57?style=flat-square&logo=sqlite)](https://www.sqlite.org/)
[![Distribution](https://img.shields.io/badge/distribution-GitHub%20Releases%20CDN-181717?style=flat-square&logo=github)](https://github.com/olaxbonnke/gam-releases/releases)
[![License](https://img.shields.io/badge/license-Proprietary%20EULA-blue?style=flat-square)](LICENSE)
[![Privacy](https://img.shields.io/badge/privacy-Offline%20Local--First-green?style=flat-square)](PRIVACY.md)

Welcome to the official public release distribution repository for **GAM (Gas Accounting Manager)**. 

This repository serves as the high-availability binary Content Delivery Network (CDN) for verified Windows installation packages (`GAM-Setup-<version>.exe`), release manifests (`latest.yml`), and differential auto-update patches (`.blockmap`).

---

## 📖 About Gas Accounting Manager (GAM)

**GAM** is an offline-first desktop Point of Sale (POS) and plant operations management platform built specifically for Liquefied Petroleum Gas (LPG) refill plants, bulk depots, and cylinder retail businesses.

It bridges the gap between fast-paced retail checkout and complex industrial bulk gas math, delivering sub-second thermal hardware printing, live central tank pool tracking, and tamper-resistant local financial auditing.

---

## 💡 Why GAM? The Real-World Problem

Most retail POS software is designed for supermarkets selling pre-packaged goods with static barcodes. **LPG gas plants operate completely differently:**

1. **Continuous Decimal Kilogram Math**: Gas is sold by weight in flexible decimal quantities (e.g., `6.25 kg`, `12.5 kg`, or custom Naira amounts like `₦3,500`). Conventional supermarket software cannot handle continuous fractional unit pricing.
2. **Physical Bulk Tank Depletion**: Every sale physically drains a massive bulk LPG tank. Without live central pool tracking, plant owners cannot detect pump calibration drift, leaks, or unaccounted inventory loss.
3. **Cashier Shift Accountability**: Stations run continuous multi-shift rotations. Handover audits must instantly compare expected cash against counted physical cash, POS card slips, electronic bank transfers, and station operating expenses.
4. **Harsh & Offline Environments**: Internet connectivity at gas plants is frequently unstable or completely unavailable. A cloud-dependent system will freeze operations during connectivity drops. GAM operates 100% offline with zero cloud latency.

---

## 🔄 How It Works at a Glance

```
  [ 1. Fast Pump Ticket ]      ───▶   [ 2. Sub-Second Thermal Print ]
   Cashier types kg or ₦               Receipt prints in < 100ms
   bundles gas + accessories           via raw USB ESC/POS streaming
             │                                   │
             ▼                                   ▼
  [ 3. Live Tank Deduction ]   ───▶   [ 4. Shift Handover Audit ]
   Central gas pool drops by           System reconciles physical cash
   exact weight sold in real time      vs expected revenue at close
```

---

## ✨ Key Features (What the App Does)

### 1. High-Velocity Pump Sales (POS)
- **Instant Dual Calculations**: Type the desired weight in kilograms (e.g., `12.5`) to get the exact total, or enter an amount in Naira (e.g., `₦5,000`) to compute the exact fractional gas volume to dispense.
- **Unified Checkout Basket**: Sell bulk gas refills and retail hardware (burners, regulators, hose clips, new cylinders) on a single combined customer ticket.
- **Split Payment Channels**: Seamlessly log payments across Cash, POS card terminals, and direct Bank Transfers.
- **Typed-Only Numerical Input**: Universal suppression of browser stepper arrows (`▲/▼`) to prevent accidental number jumping on touchscreens or physical numpads.

### 2. Live Bulk Gas Tank Pool & Stock Control
- **Real-Time Storage Readout**: High-visibility pool indicator reflects available LPG in the plant storage tank at all times.
- **Safety Level Alerts**: Prominent status badges notify operators whenever reserves dip below safety thresholds.
- **Dual Stock Intake Modules**: Side-by-side modules to log incoming LPG tanker deliveries and bulk accessory shipments with cost-per-kg records.
- **Inter-Branch Dispatches**: Create and track transfer manifests when moving bulk gas or hardware to other depot branches, complete with driver credentials, vehicle numbers, and printed waybills.

### 3. Shift Handover & Financial Balancing
- **Session-Locked Shifts**: Cashiers open individual shifts. No transactions can occur without an active, accountable operator on duty.
- **Automated Arithmetic Balancing**: At shift close, GAM calculates the exact expected cash by summing cash sales, subtracting recorded station expenses, and isolating electronic transfers.
- **Instant Thermal Close Slips**: Prints an itemized shift manifest showing ticket sequences, sales totals, payment method distributions, and start/end tank levels for handover sign-off.

### 4. Zero-Friction Backup & 1-Click Migration
- **100% Offline Autonomy**: All transaction records, price matrices, and user accounts live locally on the computer. No cloud lag, no monthly server outages.
- **Automatic USB Flash Drive Mirroring**: Inserting an authorized USB flash drive triggers background database mirroring. If the primary station PC ever suffers hardware failure, business records remain safe.
- **Instant New PC Setup**: When replacing a station computer, restore the entire station database with one click during setup—no manual file copying or database server configurations required.

### 5. Seamless Background Auto-Updates
- **Silent Differential Downloads**: New versions download quietly in the background via differential `.blockmap` binary patches without interrupting cashiers.
- **Subtle Notification Pill**: When an update is ready, a calm indicator appears in the header. Cashiers choose when to restart the application at their convenience.
- **Offline Silence**: If the station has no internet, GAM suppresses all network prompts and operates uninterrupted.

---

## 🏛 Technical Architecture

For developers and technical evaluators, GAM is structured as a resilient local multi-process desktop application:

```
┌─────────────────────────────────────────────────────────────┐
│                       Renderer Layer                        │
│   React 19 SPA · TypeScript · Custom Token-Driven Theme     │
│       Stateful Forms · Real-time Analytics · Fast POS       │
└──────────────────────────────┬──────────────────────────────┘
                               │ IPC Bridge (Context Isolation)
┌──────────────────────────────▼──────────────────────────────┐
│                    Electron Main Process                    │
│   Window Lifecycle · Native Hardware USB · Background Sync  │
│             Transaction Handlers · Event Security           │
└──────────────┬──────────────────────────────┬───────────────┘
               │                              │
┌──────────────▼──────────────┐┌──────────────▼───────────────┐
│   Embedded Data Layer       ││       Hardware Engine        │
│  better-sqlite3 (WAL Mode)  ││   Raw ESC/POS Thermal Driver │
│   ACID Financial Durability ││   USB Stream Printing (80mm) │
└─────────────────────────────┘└──────────────────────────────┘
```

### Technical Highlights:
1. **Isolated Multi-Process Security**: The React frontend runs in a sandboxed renderer without direct Node.js system access (`contextIsolation: true`, `nodeIntegration: false`). Communication flows through a strictly-typed IPC bridge (`GamAPI`).
2. **ACID Financial Storage**: Utilizes `better-sqlite3` operating in **WAL (Write-Ahead Logging)** mode with `synchronous = NORMAL`. Readers never block writers, preventing UI freezing while large shift reports compile.
3. **Hardware Thermal Driver**: Generates raw binary ESC/POS buffers directly in the main process, streaming data directly to 80mm receipt printers in under 100 milliseconds without triggering slow operating system print dialogues.
4. **Clean Design Token System**: Custom CSS token architecture supporting light and dark modes with high-contrast surfaces, solid non-gradient colors, and resting visual tints so clickable elements stand out naturally.

---

## 💻 Tech Stack Summary

| Area | Technology | Purpose |
| :--- | :--- | :--- |
| **Desktop Shell** | Electron 33 | Native Windows desktop environment and hardware device access |
| **User Interface** | React 19 + TypeScript | High-speed reactive user interface with compile-time type safety |
| **Local Database** | better-sqlite3 | Ultra-fast embedded SQL storage running in Write-Ahead Log (WAL) mode |
| **Receipt Engine** | Custom ESC/POS Driver | Direct binary stream generation for 80mm thermal receipt printers |
| **Asset Pipeline** | Vite & Electron-Vite | Optimized modern bundling and sub-second Hot Module Replacement |
| **Design System** | Custom CSS Tokens | Lightweight zero-runtime styling engine with full dark/light theme support |

---

## 📦 Releases & Downloads

All official release builds are compiled, hashed, and published to GitHub Releases:

👉 **[Browse Latest Official Releases & Installers](https://github.com/olaxbonnke/gam-releases/releases)**

- **Latest Setup Package**: `GAM-Setup-<version>.exe` (Self-extracting NSIS installer for 64-bit Windows 10/11)
- **Auto-Update Metadata**: `latest.yml` & `GAM-Setup-<version>.exe.blockmap` (Enables automated differential patching)

---

## 🔑 Acquiring an Operating License

GAM is licensed per station terminal with on-site hardware receipt printer configuration, staff role training, and real-time database disaster recovery setup.

To purchase an operating license, schedule a station deployment, or request a live plant demonstration:

- **WhatsApp Official Support**: [https://wa.me/message/BFSG3COETP6IP1](https://wa.me/message/BFSG3COETP6IP1)
- **Direct Developer Inquiry**: [@olaxbonnke](https://github.com/olaxbonnke)
- **Source Code Repository**: [olaxbonnke/gam](https://github.com/olaxbonnke/gam) *(Private)*

---

## 🛡️ License, Privacy & Compliance

All software binaries, blockmaps, and release tags distributed through this CDN are the proprietary commercial property of OLAITAN. Any unauthorized distribution, re-hosting, cracking, or unauthorized commercial use is a violation of intellectual property laws.

- 📄 **Commercial End-User License Agreement (EULA)**: Review our full terms at [LICENSE](LICENSE).
- 🔒 **Offline-First Data Privacy Policy**: Review our zero-telemetry commitments at [PRIVACY.md](PRIVACY.md).
- 🏢 **100% Station Data Sovereignty**: All sales, financial figures, customer logs, and inventory data remain 100% owned by the station operator and stored exclusively on local workstation storage.
